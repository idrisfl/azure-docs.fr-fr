---
title: Ajouter du stockage à Azure HPC Cache
description: Comment définir des cibles de stockage pour qu’Azure HPC Cache puisse utiliser votre système NFS local ou des conteneurs d’objets blob Azure dans le but de stocker des fichiers à long terme
author: ekpgh
ms.service: hpc-cache
ms.topic: how-to
ms.date: 03/15/2021
ms.author: v-erkel
ms.openlocfilehash: 44b2534d7aeb12f4819a6c42cfb29d057ce26ddc
ms.sourcegitcommit: 20f8bf22d621a34df5374ddf0cd324d3a762d46d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/09/2021
ms.locfileid: "107259028"
---
# <a name="add-storage-targets"></a>Ajouter des cibles de stockage

Les *cibles de stockage* constituent un stockage back-end pour des fichiers accessibles via un Azure HPC Cache. Vous pouvez ajouter un stockage NFS (comme un système local), ou stocker des données dans un objet blob Azure.

Vous pouvez définir jusqu’à 20 cibles de stockage différentes pour un même cache. Le cache présente toutes les cibles de stockage d’un espace de noms agrégé.

Les chemins d’accès à l’espace de noms sont configurés séparément une fois que vous avez ajouté les cibles de stockage. En général, une cible de stockage NFS peut comporter jusqu’à dix chemins d’accès aux espaces de noms, ou plus pour certaines configurations volumineuses. Pour plus d’informations, consultez [chemins d’accès à l’espace de noms NFS](add-namespace-paths.md#nfs-namespace-paths) .

N’oubliez pas que les exportations de stockage doivent être accessibles à partir du réseau virtuel de votre cache. Pour le stockage matériel local, vous devrez peut-être configurer un serveur DNS capable de résoudre les noms d’hôtes pour l’accès au stockage NFS. Pour plus d’informations, lisez [Accès DNS](hpc-cache-prerequisites.md#dns-access).

Ajoutez des cibles de stockage après avoir créé votre cache. Procédez comme suit :

1. [Créer le cache](hpc-cache-create.md)
1. Définir une cible de stockage (informations disponibles dans cet article)
1. [Créer les chemins d’accès côté client](add-namespace-paths.md) (pour l’[espace de noms agrégé](hpc-cache-namespace.md))

La procédure d’ajout d’une cible de stockage est légèrement différente selon le type de stockage utilisé. Vous trouverez ci-dessous des informations détaillées pour chacune de ces options.

Cliquez sur l’image ci-dessous pour regarder une [vidéo de démonstration](https://azure.microsoft.com/resources/videos/set-up-hpc-cache/) montrant comment créer un cache et ajouter une cible de stockage à partir du portail Azure.

[![Miniature de vidéo : Azure HPC Cache : Configuration (cliquez pour visiter la page vidéo)](media/video-4-setup.png)](https://azure.microsoft.com/resources/videos/set-up-hpc-cache/)

## <a name="add-a-new-azure-blob-storage-target"></a>Ajouter une cible de stockage Blob Azure

Les nouvelles cibles de stockage Blob nécessitent un conteneur d’objets blob vide ou un conteneur comprenant des données au format du système de fichiers cloud Azure HPC Cache. Pour plus d’informations sur le préchargement d’un conteneur d’objets blob, consultez [Déplacer les données dans le stockage d’objets blob Azure](hpc-cache-ingest.md).

Sur le portail Azure, la page **Ajouter une cible de stockage** offre la possibilité de créer un conteneur d’objets blob juste avant de l’ajouter.

> [!NOTE]
> Pour le stockage Blob monté sur NFS, utilisez le type [Cible de stockage ADLS-NFS](#).

### <a name="portal"></a>[Portail](#tab/azure-portal)

À partir du portail Azure, ouvrez votre instance de cache, puis cliquez sur **Cibles de stockage** dans la barre latérale gauche.

![capture d’écran des paramètres > page de la cible de stockage, avec deux cibles de stockage existantes dans une table et une mise en surbrillance autour du bouton + ajouter une cible de stockage au-dessus du tableau](media/add-storage-target-button.png)

La page **Cibles de stockage** répertorie toutes les cibles existantes et fournit un lien permettant d’en ajouter une nouvelle.

Cliquez sur le bouton **Ajouter une cible de stockage**.

![capture d’écran de la page Ajouter une cible de stockage, où ont été renseignées les informations relatives à la nouvelle cible de stockage d’objets blob Azure](media/hpc-cache-add-blob.png)

Pour définir un conteneur d’objets blob Azure, entrez les informations ci-dessous.

* **Nom de la cible de stockage** - Définissez un nom permettant d’identifier cette cible de stockage dans Azure HPC Cache.
* **Type de cible** : choisissez **Objet blob**.
* **Compte de stockage** : sélectionnez le compte que vous souhaitez utiliser.

  Vous devez autoriser l’instance de cache à accéder au compte de stockage, en suivant la procédure décrite dans [Ajouter les rôles d’accès](#add-the-access-control-roles-to-your-account).

  Pour plus d’informations sur le type de compte de stockage que vous pouvez utiliser, lisez [Exigences relatives au stockage Blob](hpc-cache-prerequisites.md#blob-storage-requirements).

* **Conteneur de stockage** : sélectionnez le conteneur d’objets blob pour cette cible ou cliquez sur **Créer nouveau**.

  ![capture d’écran de la boîte de dialogue permettant de spécifier le nom et le niveau d’accès (privé) du nouveau conteneur](media/add-blob-new-container.png)

Lorsque vous avez terminé, cliquez sur **OK** pour ajouter la cible de stockage.

> [!NOTE]
> Si votre pare-feu de compte de stockage est défini de façon à limiter l’accès uniquement aux « réseaux sélectionnés », utilisez la solution de contournement temporaire décrite dans [Paramètres du pare-feu de compte de Stockage Blob](hpc-cache-blob-firewall-fix.md).

### <a name="add-the-access-control-roles-to-your-account"></a>Ajouter les rôles de contrôle d’accès à votre compte

Azure HPC Cache utilise le [contrôle d’accès en fonction du rôle (Azure RBAC)](../role-based-access-control/index.yml) pour autoriser le service de cache à accéder aux cibles de stockage Blob Azure de votre compte de stockage.

Le propriétaire du compte de stockage doit ajouter explicitement les rôles [Contributeur de comptes de stockage](../role-based-access-control/built-in-roles.md#storage-account-contributor) et [Contributeur aux données Blob du stockage](../role-based-access-control/built-in-roles.md#storage-blob-data-contributor) pour l’utilisateur « HPC Cache Resource Provider ».

Vous pouvez le faire à l’avance, ou en cliquant sur le lien de la page à partir de laquelle vous ajoutez une cible de stockage Blob. Rappelez-vous qu’il peut falloir jusqu’à cinq minutes pour que les paramètres de rôle se propagent dans l’environnement Azure. Par conséquent, après avoir ajouté les rôles, vous devez attendre quelques minutes avant de créer une cible de stockage.

Étapes nécessaires pour ajouter des rôles Azure :

1. Ouvrez la page **Contrôle d’accès (IAM)** du compte de stockage (le lien de la page **Ajouter une cible de stockage** ouvre automatiquement cette page pour le compte sélectionné).

1. Cliquez sur le **+** en haut de la page, puis choisissez **Ajouter une attribution de rôle**.

1. Sélectionnez le rôle « Contributeur de comptes de stockage » dans la liste.

1. Dans le champ **Attribuer l’accès à**, conservez la valeur par défaut (Utilisateur, groupe ou principal de service Azure AD).  

1. Dans le champ **Sélectionner**, recherchez « hpc ».  Cette chaîne doit correspondre au principal de service nommé « HPC Cache Resource Provider ». Cliquez sur ce principal pour le sélectionner.

   > [!NOTE]
   > Si la recherche de « hpc » ne retourne aucun résultat, essayez la chaîne « storagecache » à la place. Il se peut que les utilisateurs qui ont participé à la préversion (avant la mise à disposition générale) doivent utiliser l’ancien nom du principal de service.

1. Cliquez sur le bouton **Enregistrer** au bas de l’écran.

1. Répétez ce processus pour attribuer le rôle « Contributeur aux données Blob du stockage ».  

![capture d’écran de l’interface graphique utilisateur Ajouter une attribution de rôle](media/hpc-cache-add-role.png)

### <a name="azure-cli"></a>[Azure CLI](#tab/azure-cli)

### <a name="prerequisite-storage-account-access"></a>Condition préalable : Accès au compte de stockage

[Configurez Azure CLI pour Azure HPC Cache](./az-cli-prerequisites.md).

Avant d’ajouter une cible de stockage blob, vérifiez que le cache dispose des rôles appropriés pour accéder au compte de stockage et que les paramètres du pare-feu permettront la création de la cible de stockage.

Azure HPC Cache utilise le [contrôle d’accès en fonction du rôle (Azure RBAC)](../role-based-access-control/index.yml) pour autoriser le service de cache à accéder aux cibles de stockage Blob Azure de votre compte de stockage.

Le propriétaire du compte de stockage doit ajouter explicitement les rôles [Contributeur de comptes de stockage](../role-based-access-control/built-in-roles.md#storage-account-contributor) et [Contributeur aux données Blob du stockage](../role-based-access-control/built-in-roles.md#storage-blob-data-contributor) pour l’utilisateur « HPC Cache Resource Provider ».

La création de la cible de stockage échoue si le cache ne dispose pas de ces rôles.

Il peut s’écouler jusqu’à cinq minutes pour que les paramètres de rôle se propagent dans l’environnement Azure. Par conséquent, après avoir ajouté les rôles, vous devez attendre quelques minutes avant de pouvoir créer une cible de stockage.

Consultez [Ajouter ou supprimer des attributions de rôle Azure à l’aide d’Azure CLI](../role-based-access-control/role-assignments-cli.md) pour obtenir des instructions détaillées.

Vérifiez également les paramètres de pare-feu de votre compte de stockage. Si le pare-feu est configuré pour limiter l’accès uniquement aux « réseaux sélectionnés », la création de la cible de stockage peut échouer. Utilisez la solution de contournement décrite dans [Contourner les paramètres de pare-feu de compte de stockage Blob](hpc-cache-blob-firewall-fix.md).

### <a name="add-a-blob-storage-target-with-azure-cli"></a>Ajouter une cible de stockage d’objets blob avec Azure CLI

Utilisez l’interface [az hpc-cache blob-storage-target add](/cli/azure/ext/hpc-cache/hpc-cache/blob-storage-target#ext-hpc-cache-az-hpc-cache-blob-storage-target-add) pour définir une cible de stockage d’objets blob Azure.

> [!NOTE]
> Les commandes Azure CLI vous obligent à créer un chemin d’accès d’espace de noms lorsque vous ajoutez une cible de stockage. Cela diffère du processus utilisé avec l’interface du portail Azure.

Outre les paramètres standard du groupe de ressources et du nom de cache, vous devez fournir ces options pour la cible de stockage :

* ``--name`` - Définissez un nom permettant d’identifier cette cible de stockage dans Azure HPC Cache.

* ``--storage-account`` - L’identificateur du compte sous la forme : /subscriptions/ *<id_abonnement>* /resourceGroups/ *<groupe_ressources_stockage>* /providers/Microsoft.Storage/storageAccounts/ *<nom_compte>*

  Pour plus d’informations sur le type de compte de stockage que vous pouvez utiliser, lisez [Exigences relatives au stockage Blob](hpc-cache-prerequisites.md#blob-storage-requirements).

* ``--container-name`` -Spécifiez le nom du conteneur à utiliser pour cette cible de stockage.

* ``--virtual-namespace-path`` - Définissez le chemin côté client de cette cible de stockage. Placez les chemins d’accès entre guillemets. Pour plus d’informations sur la fonctionnalité Espace de noms virtuels, consultez [Planifier l’espace de noms agrégé](hpc-cache-namespace.md).

Exemple de commande :

```azurecli
az hpc-cache blob-storage-target add --resource-group "hpc-cache-group" \
    --cache-name "cache1" --name "blob-target1" \
    --storage-account "/subscriptions/<subscriptionID>/resourceGroups/myrgname/providers/Microsoft.Storage/storageAccounts/myaccountname" \
    --container-name "container1" --virtual-namespace-path "/blob1"
```

---

## <a name="add-a-new-nfs-storage-target"></a>Ajouter une cible de stockage NFS

Une cible de stockage NFS a des paramètres différents d’une cible de stockage d’objets blob. Le paramètre du modèle d’utilisation aide le cache à mettre en cache efficacement les données de ce système de stockage.

![Capture d’écran de la page Ajouter la cible de stockage avec le type de cible défini sur NFS](media/add-nfs-target.png)

> [!NOTE]
> Avant de créer une cible de stockage NFS, assurez-vous que votre système de stockage est accessible à partir de l’Azure HPC Cache et répond aux exigences d’autorisation. La création d’une cible de stockage échoue si le cache ne peut pas accéder au système de stockage. Pour plus d’informations, consultez [Conditions requises pour le stockage NFS](hpc-cache-prerequisites.md#nfs-storage-requirements) et [Résolution des problèmes de configuration NAS et des cibles de stockage NFS](troubleshoot-nas.md).

### <a name="choose-a-usage-model"></a>Choisir un modèle d’utilisation
<!-- referenced from GUI by aka.ms link -->

Lorsque vous créez une cible de stockage qui utilise NFS pour atteindre son système de stockage, vous devez choisir un modèle d’utilisation pour cette cible. Ce modèle détermine la façon dont vos données sont mises en cache.

Pour plus d’informations sur l’ensemble de ces paramètres, consultez [Comprendre les modèles d’utilisation](cache-usage-models.md).

Les modèles d’utilisation intégrés vous permettent de choisir la manière d’équilibrer la vitesse de réponse avec le risque d’obtenir des données obsolètes. Si vous souhaitez optimiser la vitesse de lecture des fichiers, vous pourriez ne pas vous préoccuper du fait que les fichiers dans le cache sont vérifiés par rapport aux fichiers sur le serveur principal. En revanche, si vous souhaitez vous assurer que vos fichiers sont toujours à jour avec le stockage étendu, choisissez un modèle qui effectue des vérifications fréquemment.

Ces trois options couvrent la plupart des situations :

* **Nombreuses lectures, écritures peu fréquentes** : accélère l’accès en lecture aux fichiers statiques ou rarement modifiés.

  Cette option met en cache les fichiers des lectures client, mais transmet immédiatement les écritures client au stockage principal. Les fichiers stockés dans le cache ne sont pas comparés automatiquement aux fichiers sur le volume de stockage NFS.

  N’utilisez pas cette option s’il existe un risque de modification directe d’un fichier sur le système de stockage sans l’avoir d’abord écrit dans le cache. Si cela se produit, la version mise en cache du fichier n’est pas synchronisée avec le fichier sur le serveur principal.

* **Opérations d’écriture supérieures à 15 %**  : cette option accélère les performances de lecture et d’écriture.

  Les lectures et écritures du client sont mises en cache. Les fichiers du cache sont supposés être plus récents que les fichiers sur le système de stockage principal. Les fichiers mis en cache ne sont automatiquement vérifiés par rapport aux fichiers du stockage principal que toutes les huit heures. Les fichiers modifiés dans le cache sont écrits dans le système de stockage principal une fois qu’ils se trouvent dans le cache pendant 20 minutes sans aucune modification supplémentaire.

  N’utilisez pas cette option si un client monte directement le volume de stockage principal, car il existe un risque que des fichiers soient obsolètes.

* **Les clients écrivent dans la cible NFS en ignorant le cache** : choisissez cette option si des clients dans votre workflow écrivent des données directement dans le système de stockage sans écrire au préalable dans le cache, ou si vous voulez optimiser la cohérence des données.

  Les fichiers demandés par les clients sont mis en cache, mais toute modification apportée à ces fichiers à partir du client est immédiatement retransmise au système de stockage backend. Les fichiers du cache sont fréquemment comparés aux versions backend pour y rechercher des mises à jour. Cette vérification assure la cohérence des données lorsque les fichiers sont modifiés directement sur le système de stockage plutôt que dans le cache.

Pour plus d’informations sur les autres options, consultez [Comprendre les modèles d’utilisation](cache-usage-models.md).

Ce tableau résume les différences entre les modèles d’utilisation :

[!INCLUDE [usage-models-table.md](includes/usage-models-table.md)]

> [!NOTE]
> La valeur **Vérification du serveur principal** s’affiche lorsque le cache compare automatiquement ses fichiers aux fichiers sources dans le stockage étendu. Toutefois, vous pouvez déclencher une comparaison en envoyant une requête client qui comprend une opération readdirplus sur le système de stockage principal. Readdirplus est une API NFS standard (également appelée lecture étendue) qui retourne des métadonnées d’annuaire, ce qui amène le cache à comparer et à mettre à jour les fichiers.

### <a name="create-an-nfs-storage-target"></a>Créer une cible de stockage NFS

### <a name="portal"></a>[Portail](#tab/azure-portal)

À partir du portail Azure, ouvrez votre instance de cache, puis cliquez sur **Cibles de stockage** dans la barre latérale gauche.

![capture d’écran des paramètres > page de la cible de stockage, avec deux cibles de stockage existantes dans une table et une mise en surbrillance autour du bouton + ajouter une cible de stockage au-dessus du tableau](media/add-storage-target-button.png)

La page **Cibles de stockage** répertorie toutes les cibles existantes et fournit un lien permettant d’en ajouter une nouvelle.

Cliquez sur le bouton **Ajouter une cible de stockage**.

![Capture d’écran de la page Ajouter la cible de stockage avec le type de cible défini sur NFS](media/add-nfs-target.png)

Fournissez les informations suivantes pour une cible de stockage NFS :

* **Nom de la cible de stockage** - Définissez un nom permettant d’identifier cette cible de stockage dans Azure HPC Cache.

* **Type de cible** - Choisissez **NFS**.

* **Nom d’hôte** - Entrez l’adresse IP ou le nom de domaine complet de votre système de stockage NFS (utilisez un nom de domaine uniquement si votre cache a accès à un serveur DNS capable de résoudre ce nom).

* **Modèle d’utilisation** : choisissez l’un des profils de mise en cache des données en fonction de votre workflow, comme décrit dans [Choisir un modèle d’utilisation](#choose-a-usage-model) précédemment.

Lorsque vous avez terminé, cliquez sur **OK** pour ajouter la cible de stockage.

### <a name="azure-cli"></a>[Azure CLI](#tab/azure-cli)

[Configurez Azure CLI pour Azure HPC Cache](./az-cli-prerequisites.md).

Utilisez la commande Azure CLI [az hpc-cache nfs-storage-target add](/cli/azure/ext/hpc-cache/hpc-cache/nfs-storage-target#ext-hpc-cache-az-hpc-cache-nfs-storage-target-add) pour créer la cible de stockage.

> [!NOTE]
> Les commandes Azure CLI vous obligent à créer un chemin d’accès d’espace de noms lorsque vous ajoutez une cible de stockage. Cela diffère du processus utilisé avec l’interface du portail Azure.

Fournissez ces valeurs en plus du nom du cache et du groupe de ressources du cache :

* ``--name`` - Définissez un nom permettant d’identifier cette cible de stockage dans Azure HPC Cache.
* ``--nfs3-target`` -L’adresse IP de votre système de stockage NFS. (Vous pouvez utiliser un nom de domaine complet ici si votre cache a accès à un serveur DNS capable de résoudre ce nom).
* ``--nfs3-usage-model`` -L’un des profils de mise en cache de données, décrit dans [Choisir un modèle d’utilisation](#choose-a-usage-model) précédemment.

  Vérifiez les noms des modèles d’utilisation à l’aide de la commande [az hpc-cache usage-model list](/cli/azure/ext/hpc-cache/hpc-cache/usage-model#ext-hpc-cache-az-hpc-cache-usage-model-list).

* ``--junction`` -Le paramètre junction lie le chemin d’accès du fichier virtuel orienté client à un chemin d’exportation sur le système de stockage.

  Une cible de stockage NFS peut avoir plusieurs chemins d’accès virtuels, à condition que chaque chemin d’accès représente une exportation ou un sous-répertoire différent sur le même système de stockage. Créez tous les chemins d’accès d’un système de stockage sur une cible de stockage.

  Vous pouvez [ajouter et modifier des chemins d’accès d’espace de noms](add-namespace-paths.md) sur une cible de stockage à tout moment.

  Le paramètre ``--junction`` utilise les valeurs suivantes :

  * ``namespace-path`` : chemin d’accès au fichier virtuel orienté client
  * ``nfs-export`` : exportation du système de stockage à associer au chemin d’accès orienté client
  * ``target-path`` (facultatif) : sous-répertoire de l’exportation, si nécessaire

  Exemple : ``--junction namespace-path="/nas-1" nfs-export="/datadisk1" target-path="/test"``

  Pour plus d’informations sur la fonctionnalité Espace de noms virtuels, consultez [Configurer un espace de noms agrégé](hpc-cache-namespace.md).

Exemple de commande :

```azurecli

az hpc-cache nfs-storage-target add --resource-group "hpc-cache-group" --cache-name "doc-cache0629" \
    --name nfsd1 --nfs3-target 10.0.0.4 --nfs3-usage-model WRITE_WORKLOAD_15 \
    --junction namespace-path="/nfs1/data1" nfs-export="/datadisk1" target-path=""
```

Sortie :
```azurecli

{- Finished ..
  "clfs": null,
  "id": "/subscriptions/<subscriptionID>/resourceGroups/hpc-cache-group/providers/Microsoft.StorageCache/caches/doc-cache0629/storageTargets/nfsd1",
  "junctions": [
    {
      "namespacePath": "/nfs1/data1",
      "nfsExport": "/datadisk1",
      "targetPath": ""
    }
  ],
  "location": "eastus",
  "name": "nfsd1",
  "nfs3": {
    "target": "10.0.0.4",
    "usageModel": "WRITE_WORKLOAD_15"
  },
  "provisioningState": "Succeeded",
  "resourceGroup": "hpc-cache-group",
  "targetType": "nfs3",
  "type": "Microsoft.StorageCache/caches/storageTargets",
  "unknown": null
}

```

---

## <a name="add-a-new-adls-nfs-storage-target-preview"></a>Ajouter une cible de stockage ADLS-NFS (PRÉVERSION)

Les cibles de stockage ADLS-NFS utilisent des conteneurs d’objets Blob Azure qui prennent en charge le protocole NFS 3.0.

> [!NOTE]
> La prise en charge du protocole NFS 3.0 dans Stockage Blob Azure est en préversion publique. La disponibilité est limitée et les fonctionnalités peuvent changer entre maintenant et le moment où la fonctionnalité sera proposée en disponibilité générale. N’utilisez pas la technologie en préversion dans des systèmes de production.
>
> Consultez [Prise en charge du protocole NFS 3.0](../storage/blobs/network-file-system-protocol-support.md) pour obtenir les dernières informations.

Les cibles de stockage ADLS-NFS ont des similarités avec les cibles de stockage d’objets Blob et avec les cibles de stockage NFS. Par exemple :

* Comme pour une cible de stockage d’objets Blob, vous devez accorder à Azure HPC Cache l’autorisation d’[accéder à votre compte de stockage](#add-the-access-control-roles-to-your-account).
* À l’instar d’une cible de stockage NFS, vous devez définir un [modèle d’utilisation](#choose-a-usage-model) du cache.
* Étant donné que les conteneurs d’objets Blob compatibles NFS possèdent une structure hiérarchique compatible NFS, vous n’avez pas besoin d’utiliser le cache pour ingérer les données, et les conteneurs sont lisibles par d’autres systèmes NFS. Vous pouvez précharger des données dans un conteneur ADLS-NFS, les ajouter à un cache HPC en tant que cible de stockage, puis accéder aux données ultérieurement à partir de l’extérieur d’un cache HPC. Lorsque vous utilisez un conteneur d’objets Blob standard en tant que cible de stockage du cache HPC, les données sont écrites dans un format propriétaire et sont accessibles uniquement à partir d’autres produits compatibles avec le Azure HPC Cache.

Avant de pouvoir créer une cible de stockage ADLS-NFS, vous devez créer un compte de stockage compatible NFS. Suivez les conseils dans [Conditions préalables pour Azure HPC Cache](hpc-cache-prerequisites.md#nfs-mounted-blob-adls-nfs-storage-requirements-preview) et les instructions dans [Monter le stockage Blob à l’aide de NFS](../storage/blobs/network-file-system-protocol-support-how-to.md). Une fois votre compte de stockage configuré, vous pouvez créer un conteneur lors de la création de la cible de stockage.

Pour en savoir plus sur cette configuration, consultez [Utiliser le stockage blob monté sur NFS avec Azure HPC Cache](nfs-blob-considerations.md).

Pour créer une cible de stockage ADLS-NFS, ouvrez la page **Ajouter une cible de stockage** dans le portail Azure. (Des méthodes supplémentaires sont en cours de développement.)

![Capture d’écran de la page Ajouter la cible de stockage avec le type de cible défini sur ADLS-NFS](media/add-adls-target.png)

Entrez les informations suivantes.

* **Nom de la cible de stockage** - Définissez un nom permettant d’identifier cette cible de stockage dans Azure HPC Cache.
* **Type de cible** - Choisissez **ADLS-NFS**.
* **Compte de stockage** : sélectionnez le compte que vous souhaitez utiliser. Si votre compte de stockage NFS ne figure pas dans la liste, vérifiez qu’il est conforme aux conditions préalables et que le cache peut y accéder.

  Vous devez autoriser l’instance de cache à accéder au compte de stockage, en suivant la procédure décrite dans [Ajouter les rôles d’accès](#add-the-access-control-roles-to-your-account).

* **Conteneur de stockage** : sélectionnez le conteneur d’objets blob compatible NFS pour cette cible ou cliquez sur **Créer nouveau**.

* **Modèle d’utilisation** : choisissez l’un des profils de mise en cache des données en fonction de votre workflow, comme décrit dans [Choisir un modèle d’utilisation](#choose-a-usage-model) précédemment.

Lorsque vous avez terminé, cliquez sur **OK** pour ajouter la cible de stockage.

## <a name="view-storage-targets"></a>Afficher les cibles de stockage

Vous pouvez utiliser le portail Azure ou l’interface de ligne de commande Azure pour afficher les cibles de stockage déjà définies pour votre cache.

### <a name="portal"></a>[Portail](#tab/azure-portal)

À partir du portail Azure, ouvrez votre instance de cache, puis cliquez sur **Cibles de stockage**, qi se trouve sous le titre Paramètres dans la barre latérale gauche. La page des cibles de stockage répertorie toutes les cibles existantes et les commandes permettant de les ajouter ou de les supprimer.

Cliquez sur le nom d’une cible de stockage pour ouvrir la page de détails correspondante.

Pour en savoir plus, consultez [Modifier les cibles de stockage](hpc-cache-edit-storage.md) .

### <a name="azure-cli"></a>[Azure CLI](#tab/azure-cli)

[Configurez Azure CLI pour Azure HPC Cache](./az-cli-prerequisites.md).

Utilisez l’option [az hpc-cache storage-target list](/cli/azure/ext/hpc-cache/hpc-cache/storage-target#ext-hpc-cache-az-hpc-cache-storage-target-list) pour afficher les cibles de stockage existantes pour un cache. Indiquez le nom du cache et le groupe de ressources (sauf si vous l’avez défini globalement).

```azurecli
az hpc-cache storage-target list --resource-group "scgroup" --cache-name "sc1"
```

Utilisez [az hpc-cache storage-target show](/cli/azure/ext/hpc-cache/hpc-cache/storage-target#ext-hpc-cache-az-hpc-cache-storage-target-list) pour afficher des détails sur une cible de stockage particulière. (Spécifiez la cible de stockage par nom.)

Exemple :

```azurecli
$ az hpc-cache storage-target show --cache-name doc-cache0629 --name nfsd1

{
  "clfs": null,
  "id": "/subscriptions/<subscription_ID>/resourceGroups/scgroup/providers/Microsoft.StorageCache/caches/doc-cache0629/storageTargets/nfsd1",
  "junctions": [
    {
      "namespacePath": "/nfs1/data1",
      "nfsExport": "/datadisk1",
      "targetPath": ""
    }
  ],
  "location": "eastus",
  "name": "nfsd1",
  "nfs3": {
    "target": "10.0.0.4",
    "usageModel": "WRITE_WORKLOAD_15"
  },
  "provisioningState": "Succeeded",
  "resourceGroup": "scgroup",
  "targetType": "nfs3",
  "type": "Microsoft.StorageCache/caches/storageTargets",
  "unknown": null
}
$
```

---

## <a name="next-steps"></a>Étapes suivantes

Après avoir créé des cibles de stockage, poursuivez avec ces tâches pour que votre cache soit opérationnel :

* [Configurer l’espace de noms agrégé](add-namespace-paths.md)
* [Monter le cache Azure HPC Cache](hpc-cache-mount.md)
* [Déplacer les données dans le stockage d’objets blob Azure](hpc-cache-ingest.md)

Si vous devez mettre à jour des paramètres, vous pouvez [modifier une cible de stockage](hpc-cache-edit-storage.md).
