---
title: Charger en parallèle de grandes quantités de données aléatoires dans le Stockage Azure
description: Découvrir comment utiliser la bibliothèque de client Stockage Azure pour charger en parallèle de grandes quantités de données aléatoires dans un compte de stockage Azure
author: roygara
ms.service: storage
ms.topic: tutorial
ms.date: 02/04/2021
ms.author: rogarana
ms.subservice: blobs
ms.openlocfilehash: ed7020a58f3f15403108934bcc3fab644bd1b627
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2021
ms.locfileid: "99584463"
---
# <a name="upload-large-amounts-of-random-data-in-parallel-to-azure-storage"></a>Charger en parallèle de grandes quantités de données aléatoires dans le stockage Azure

Ce tutoriel est le deuxième d’une série. Ce didacticiel décrit le déploiement d’une application qui charge une grande quantité de données aléatoires dans un compte de stockage Azure.

Dans ce deuxième volet, vous apprenez à :

> [!div class="checklist"]
> * Configurer la chaîne de connexion
> * Créer l’application
> * Exécution de l'application
> * Valider le nombre de connexions

Le Stockage Blob Microsoft Azure fournit un service évolutif pour stocker vos données. Pour que votre application soit aussi performante que possible, vous devez comprendre le fonctionnement du stockage blob. Vous devez connaître les limites des objets blob Azure. Pour en savoir plus sur ces limites, consultez : [Objectifs de performance et de scalabilité du Stockage Blob](../blobs/scalability-targets.md)

La [convention de nommage des partitions](../blobs/storage-performance-checklist.md#partitioning) est un autre facteur potentiellement important quand vous concevez une application hautes performances à l’aide d’objets blob. Pour les tailles de bloc supérieures ou égales à 4 Mio, des [objets blob de blocs à débit élevé](https://azure.microsoft.com/blog/high-throughput-with-azure-blob-storage/) sont utilisés, et le nommage des partitions n’affecte pas les performances. Pour les tailles de bloc inférieures à 4 Mio, le Stockage Azure utilise un schéma de partitionnement basé sur une plage pour mettre à l’échelle et équilibrer la charge. Cette configuration signifie que les fichiers qui ont des conventions de nommage ou des préfixes similaires sont dirigés dans la même partition. Cette logique inclut le nom du conteneur dans lequel les fichiers sont chargés. Dans ce didacticiel, vous utilisez des fichiers qui ont des GUID comme noms ainsi que du contenu généré aléatoirement. Ils sont ensuite chargés dans cinq conteneurs différents avec des noms aléatoires.

## <a name="prerequisites"></a>Prérequis

Pour suivre ce tutoriel, vous devez avoir terminé le tutoriel précédent sur le stockage : [Créer une machine virtuelle et un compte de stockage pour une application évolutive][previous-tutorial].

## <a name="remote-into-your-virtual-machine"></a>Ouvrir une session Bureau à distance sur votre machine virtuelle

Exécutez la commande suivante sur votre machine locale pour créer une session Bureau à distance avec la machine virtuelle. Remplacez l’adresse IP par l’adresse publicIPAddress de votre machine virtuelle. À l’invite, entrez les informations d’identification que vous avez utilisées pour créer la machine virtuelle.

```console
mstsc /v:<publicIpAddress>
```

## <a name="configure-the-connection-string"></a>Configurer la chaîne de connexion

Dans le portail Azure, accédez à votre compte de stockage. Sélectionnez **Clés d’accès** sous **Paramètres** dans votre compte de stockage. Copiez la **chaîne de connexion** de la clé primaire ou secondaire. Connectez-vous à la machine virtuelle créée dans le didacticiel précédent. Ouvrez une **invite de commandes** comme administrateur et exécutez la commande `setx` avec le commutateur `/m`, cette commande enregistre une variable d’environnement de paramètre de machine. La variable d’environnement n’est pas disponible tant que vous n’avez pas rechargé **l’invite de commandes**. Remplacez **\<storageConnectionString\>** dans l’exemple suivant :

```console
setx storageconnectionstring "<storageConnectionString>" /m
```

Une fois que vous avez terminé, ouvrez une autre **invite de commandes**, accédez à `D:\git\storage-dotnet-perf-scale-app` et tapez `dotnet build` pour créer l’application.

## <a name="run-the-application"></a>Exécution de l'application

Accédez à `D:\git\storage-dotnet-perf-scale-app`.

Saisissez `dotnet run` pour exécuter l’application. La première fois que vous exécutez `dotnet`, il remplit votre cache de package local pour améliorer la vitesse de restauration et activer l’accès hors connexion. L’exécution de cette commande prend jusqu’à une minute et ne se produit qu’une seule fois.

```console
dotnet run
```

L’application crée cinq conteneurs nommés de façon aléatoire et commence à charger les fichiers dans le répertoire de préproduction du compte de stockage.

La méthode `UploadFilesAsync` est présentée dans l’exemple suivant :

# <a name="net-v12"></a>[.NET v12](#tab/dotnet)

:::code language="csharp" source="~/azure-storage-snippets/blobs/howto/dotnet/dotnet-v12/Scalable.cs" id="Snippet_UploadFilesAsync":::

# <a name="net-v11"></a>[.NET v11](#tab/dotnet11)

Le nombre minimal de threads et le nombre maximal sont définis sur 100 afin de garantir qu’un grand nombre de connexions simultanées sont autorisées.

```csharp
private static async Task UploadFilesAsync()
{
    // Create five randomly named containers to store the uploaded files.
    CloudBlobContainer[] containers = await GetRandomContainersAsync();

    var currentdir = System.IO.Directory.GetCurrentDirectory();

    // Path to the directory to upload
    string uploadPath = currentdir + "\\upload";

    // Start a timer to measure how long it takes to upload all the files.
    Stopwatch time = Stopwatch.StartNew();

    try
    {
        Console.WriteLine("Iterating in directory: {0}", uploadPath);

        int count = 0;
        int max_outstanding = 100;
        int completed_count = 0;

        // Define the BlobRequestOptions on the upload.
        // This includes defining an exponential retry policy to ensure that failed connections
        // are retried with a back off policy. As multiple large files are being uploaded using
        // large block sizes, this can cause an issue if an exponential retry policy is not defined.
        // Additionally, parallel operations are enabled with a thread count of 8.
        // This should be a multiple of the number of processor cores in the machine.
        // Lastly, MD5 hash validation is disabled for this example, improving the upload speed.
        BlobRequestOptions options = new BlobRequestOptions
        {
            ParallelOperationThreadCount = 8,
            DisableContentMD5Validation = true,
            StoreBlobContentMD5 = false
        };

        // Create a new instance of the SemaphoreSlim class to 
        // define the number of threads to use in the application.
        SemaphoreSlim sem = new SemaphoreSlim(max_outstanding, max_outstanding);

        List<Task> tasks = new List<Task>();
        Console.WriteLine("Found {0} file(s)", Directory.GetFiles(uploadPath).Count());

        // Iterate through the files
        foreach (string path in Directory.GetFiles(uploadPath))
        {
            var container = containers[count % 5];
            string fileName = Path.GetFileName(path);
            Console.WriteLine("Uploading {0} to container {1}", path, container.Name);
            CloudBlockBlob blockBlob = container.GetBlockBlobReference(fileName);

            // Set the block size to 100MB.
            blockBlob.StreamWriteSizeInBytes = 100 * 1024 * 1024;

            await sem.WaitAsync();

            // Create a task for each file to upload. The tasks are
            // added to a collection and all run asynchronously.
            tasks.Add(blockBlob.UploadFromFileAsync(path, null, options, null).ContinueWith((t) =>
            {
                sem.Release();
                Interlocked.Increment(ref completed_count);
            }));

            count++;
        }

        // Run all the tasks asynchronously.
        await Task.WhenAll(tasks);

        time.Stop();

        Console.WriteLine("Upload has been completed in {0} seconds. Press any key to continue", time.Elapsed.TotalSeconds.ToString());

        Console.ReadLine();
    }
    catch (DirectoryNotFoundException ex)
    {
        Console.WriteLine("Error parsing files in the directory: {0}", ex.Message);
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
    }
}
```
En plus de définir les paramètres de limite de threads et de connexion, les valeurs [BlobRequestOptions](/dotnet/api/microsoft.azure.storage.blob.blobrequestoptions) pour la méthode [UploadFromStreamAsync](/dotnet/api/microsoft.azure.storage.blob.cloudblockblob.uploadfromstreamasync) sont configurées pour utiliser le parallélisme et désactiver la validation de hachage MD5. Les fichiers sont chargés dans des blocs de 100 Mo, cette configuration offre de meilleures performances, mais peut s’avérer coûteuse si vous utilisez un réseau peu performant, car, en cas d’échec, le bloc entier de 100 Mo est réessayé.

|Propriété|Valeur|Description|
|---|---|---|
|[ParallelOperationThreadCount](/dotnet/api/microsoft.azure.storage.blob.blobrequestoptions.paralleloperationthreadcount)| 8| Le paramètre divise l’objet blob en blocs pendant le chargement. Pour optimiser les performances, cette valeur doit être huit fois supérieure au nombre de cœurs. |
|[DisableContentMD5Validation](/dotnet/api/microsoft.azure.storage.blob.blobrequestoptions.disablecontentmd5validation)| true| Cette propriété désactive la vérification du hachage MD5 du contenu chargé. La désactivation de la validation MD5 entraîne un transfert plus rapide. Toutefois, elle ne confirme pas la validité ou l’intégrité des fichiers transférés.   |
|[StoreBlobContentMD5](/dotnet/api/microsoft.azure.storage.blob.blobrequestoptions.storeblobcontentmd5)| false| Cette propriété détermine si un hachage MD5 est calculé et stocké avec le fichier.   |
| [RetryPolicy](/dotnet/api/microsoft.azure.storage.blob.blobrequestoptions.retrypolicy)| Interruption de 2 secondes avec 10 nouvelles tentatives au maximum |Détermine la stratégie de nouvelle tentative des demandes. Les connexions qui ont échoué sont réessayées, dans cet exemple une stratégie [ExponentialRetry](/dotnet/api/microsoft.azure.batch.common.exponentialretry) est configurée avec une interruption de 2 secondes et 10 nouvelles tentatives au maximum. Ce paramètre est important quand votre application se rapproche des objectifs de scalabilité du Stockage Blob. Pour plus d’informations, consultez [Objectifs de performance et de scalabilité pour le Stockage Blob](../blobs/scalability-targets.md).  |

---

L’exemple suivant est une sortie d’application tronquée s’exécutant sur un système Windows.

```console
Created container 2dbb45f4-099e-49eb-880c-5b02ebac135e
Created container 0d784365-3bdf-4ef2-b2b2-c17b6480792b
Created container 42ac67f2-a316-49c9-8fdb-860fb32845d7
Created container f0357772-cb04-45c3-b6ad-ff9b7a5ee467
Created container 92480da9-f695-4a42-abe8-fb35e71eb887
Iterating in directory: C:\git\myapp\upload
Found 5 file(s)
Uploading 1d596d16-f6de-4c4c-8058-50ebd8141e4d.pdf to container 2dbb45f4-099e-49eb-880c-5b02ebac135e
Uploading 242ff392-78be-41fb-b9d4-aee8152a6279.pdf to container 0d784365-3bdf-4ef2-b2b2-c17b6480792b
Uploading 38d4d7e2-acb4-4efc-ba39-f9611d0d55ef.pdf to container 42ac67f2-a316-49c9-8fdb-860fb32845d7
Uploading 45930d63-b0d0-425f-a766-cda27ff00d32.pdf to container f0357772-cb04-45c3-b6ad-ff9b7a5ee467
Uploading 5129b385-5781-43be-8bac-e2fbb7d2bd82.pdf to container 92480da9-f695-4a42-abe8-fb35e71eb887
Uploaded 5 files in 16.9552163 seconds
```

### <a name="validate-the-connections"></a>Valider les connexions

Pendant le chargement des fichiers, vous pouvez vérifier le nombre de connexions simultanées sur votre compte de stockage. Ouvrez une fenêtre de console et tapez `netstat -a | find /c "blob:https"`. Cette commande affiche le nombre de connexions actuellement ouvertes. Comme vous pouvez le voir dans l’exemple suivant, 800 connexions étaient ouvertes pendant le chargement des fichiers aléatoires dans le compte de stockage. Cette valeur change à mesure de l’exécution du chargement. En chargeant des segments de bloc en parallèle, la quantité de temps nécessaire pour transférer le contenu est considérablement réduite.

```
C:\>netstat -a | find /c "blob:https"
800

C:\>
```

## <a name="next-steps"></a>Étapes suivantes

Dans la deuxième partie de la série, vous avez appris à charger de grandes quantités de données aléatoires dans un compte de stockage, notamment comment :

> [!div class="checklist"]
> * Configurer la chaîne de connexion
> * Créer l’application
> * Exécution de l'application
> * Valider le nombre de connexions

Passez à la troisième partie de la série pour télécharger de grandes quantités de données à partir d’un compte de stockage.

> [!div class="nextstepaction"]
> [Télécharger de grandes quantités de données aléatoires depuis le stockage Azure](storage-blob-scalable-app-download-files.md)

[previous-tutorial]: storage-blob-scalable-app-create-vm.md
