---
title: Ingérer des données dans Azure Data Lake Storage Gen2
description: Découvrez comment ingérer des données dans Azure Data Lake Storage Gen2 dans Azure Synapse Analytics
services: synapse-analytics
author: djpmsft
ms.service: synapse-analytics
ms.topic: conceptual
ms.subservice: ''
ms.date: 04/15/2020
ms.author: daperlov
ms.reviewer: jrasnick
ms.openlocfilehash: fbc4f11b450a645002daedc800d4fed74ed37a3d
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2021
ms.locfileid: "98219570"
---
# <a name="ingest-data-into-azure-data-lake-storage-gen2"></a>Ingérer des données dans Azure Data Lake Storage Gen2 

Cet article explique comment ingérer des données d’un emplacement dans un autre, dans un compte de stockage Azure Data Lake Gen 2 à l’aide d’Azure Synapse Analytics.

## <a name="prerequisites"></a>Prérequis

* **Abonnement Azure** : Si vous n’avez pas d’abonnement Azure, créez un [compte Azure gratuit](https://azure.microsoft.com/free/) avant de commencer.
* **Compte Stockage Azure** : Vous utilisez Azure Data Lake Gen 2 en tant que magasin de données *source*. Si vous ne possédez pas de compte de stockage, procédez de la manière décrite dans l’article [Créer un compte de stockage Azure](../../storage/common/storage-account-create.md?bc=%2fazure%2fsynapse-analytics%2fbreadcrumb%2ftoc.json&toc=%2fazure%2fsynapse-analytics%2ftoc.json) pour en créer un.

## <a name="create-linked-services"></a>Créez des services liés

Dans Azure Synapse Analytics, un service lié vous permet de définir vos informations de connexion à d’autres services. Dans cette section, vous allez ajouter Azure Synapse Analytics et Azure Data Lake Gen 2 en tant que services liés.

1. Ouvrez l’expérience utilisateur Azure Synapse Analytics et accédez à l’onglet **Gérer**.
1. Sous **Connexions externes**, sélectionnez **Services liés**.
1. Pour ajouter un service lié, sélectionnez **Nouveau**.
1. Sélectionnez la vignette Azure Data Lake Storage Gen2 dans la liste, puis sélectionnez **Continuer**.
1. Entrez vos informations d’identification d’authentification. Les types d’authentification actuellement pris en charge sont les suivants : clé de compte, principal de service et identité managée. Sélectionnez Tester la connexion pour vérifier que vos informations d’identification sont correctes. 
1. Lorsque vous avez terminé, sélectionnez **Créer**.

## <a name="create-pipeline"></a>Création d’un pipeline

Un pipeline contient le flux logique pour l’exécution d’un ensemble d’activités. Dans cette section, vous allez créer un pipeline contenant une activité de copie qui ingère des données d’Azure Data Lake Gen 2 dans un pool SQL dédié.

1. Accédez à l’onglet **Orchestrer**. Sélectionnez l’icône + en regard de l’en-tête Pipelines, puis sélectionnez **Pipeline**.
1. Dans le volet des activités, sous **Déplacer et transformer**, faites glisser **Copier les données** sur le canevas du pipeline.
1. Sélectionnez l’activité de copie, puis accédez à l’onglet **Source**. Sélectionnez **Nouveau** pour créer un jeu de données source.
1. Sélectionnez Azure Data Lake Storage Gen2 comme magasin de données, puis sélectionnez Continuer.
1. Sélectionnez DelimitedText comme format, puis sélectionnez Continuer.
1. Dans le volet Définir les propriétés, sélectionnez le service lié ADLS que vous avez créé. Spécifiez le chemin d’accès du fichier de vos données sources, puis spécifiez si la première ligne contient un en-tête. Vous pouvez importer le schéma à partir du magasin de fichiers ou d’un exemple de fichier. Sélectionnez OK lorsque vous avez terminé.
1. Accédez à l’onglet **Récepteur**. Sélectionnez **Nouveau** pour créer un jeu de données récepteur.
1. Sélectionnez Azure Data Lake Storage Gen2 comme magasin de données, puis sélectionnez Continuer.
1. Sélectionnez DelimitedText comme format, puis sélectionnez Continuer.
1. Dans le volet Définir les propriétés, sélectionnez le service lié ADLS que vous avez créé. Spécifiez le chemin d’accès du dossier dans lequel vous souhaitez écrire les données. Sélectionnez OK lorsque vous avez terminé.

## <a name="debug-and-publish-pipeline"></a>Déboguer et publier le pipeline

Une fois la configuration de votre pipeline terminée, avant de publier vos artefacts, vous pouvez exécuter un débogage pour vérifier que tout est correct.

1. Pour déboguer le pipeline, sélectionnez **Déboguer** dans la barre d’outils. L’état d’exécution du pipeline apparaît dans l’onglet **Sortie** au bas de la fenêtre. 
1. Une fois que le pipeline peut s’exécuter correctement, sélectionnez **Publier tout** dans la barre d’outils supérieure. Cette action publie les entités (jeux de données et pipelines) que vous avez créées dans le service Synapse Analytics.
1. Patientez jusqu’à voir le message **Publication réussie**. Pour voir les messages de notification, sélectionnez le bouton avec l’icône de cloche en haut à droite. 


## <a name="trigger-and-monitor-the-pipeline"></a>Déclencher et surveiller le pipeline

Au cours de cette étape, vous déclenchez manuellement le pipeline publié à l’étape précédente. 

1. Sélectionnez **Ajouter déclencheur** dans la barre d’outils, puis **Déclencher maintenant**. Dans la page **Exécution du pipeline**, sélectionnez **Terminer**.  
1. Accédez à l’onglet **Surveiller** dans la barre latérale gauche. Vous voyez un pipeline qui est déclenché par un déclencheur manuel. Vous pouvez utiliser les liens dans la colonne **Actions** pour afficher les détails de l’activité et réexécuter le pipeline.
1. Pour afficher les exécutions d’activités associées à l’exécution du pipeline, sélectionnez le lien **Afficher les exécutions d’activités** dans la colonne **Actions**. Dans cet exemple, il n’y a qu’une seule activité, vous ne voyez donc qu’une seule entrée dans la liste. Pour plus de détails sur l’opération de copie, sélectionnez le lien **Détails** (icône en forme de lunettes) dans la colonne **Actions**. Sélectionnez **Exécutions de pipeline** au sommet de la page pour revenir à la vue des exécutions du pipeline. Sélectionnez **Actualiser** pour actualiser l’affichage.
1. Vérifiez que vos données sont correctement écrites dans le pool SQL dédié.


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’intégration de données pour Azure Synapse Analytics, consultez l’article [Ingestion de données dans un pool SQL dédié](data-integration-sql-pool.md).