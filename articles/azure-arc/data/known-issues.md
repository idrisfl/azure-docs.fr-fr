---
title: Problèmes connus des services de données avec Azure Arc
description: Problèmes connus les plus récents
author: twright-msft
ms.author: twright
ms.reviewer: mikeray
services: azure-arc
ms.service: azure-arc
ms.subservice: azure-arc-data
ms.date: 03/02/2021
ms.topic: conceptual
ms.openlocfilehash: ee652047a33d73ece2d7648905fa590d90b1fb2f
ms.sourcegitcommit: d40ffda6ef9463bb75835754cabe84e3da24aab5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/07/2021
ms.locfileid: "107029503"
---
# <a name="known-issues---azure-arc-enabled-data-services-preview"></a>Problèmes connus – Services de données avec Azure Arc (préversion)

[!INCLUDE [azure-arc-data-preview](../../../includes/azure-arc-data-preview.md)]

## <a name="march-2021"></a>Mars 2021

### <a name="data-controller"></a>Contrôleur de données

- Vous pouvez créer un contrôleur de données en mode de connexion directe avec le portail Azure. Le déploiement avec d’autres outils de services de données avec Azure Arc n’est pas pris en charge. Plus précisément, vous ne pouvez pas déployer un contrôleur de données en mode de connexion directe avec l’un des outils suivants pendant cette version.
   - Azure Data Studio
   - Azure Data CLI (`azdata`)
   - Outils natifs Kubernetes

   L’article [Déployer le contrôleur de données Azure Arc | Mode de connexion directe](deploy-data-controller-direct-mode.md) explique comment créer le contrôleur de données dans le portail. 

### <a name="azure-arc-enabled-postgresql-hyperscale"></a>Azure Arc enabled PostgreSQL Hyperscale

- Le déploiement d’un groupe de serveurs Postgres Hyperscale avec Azure Arc dans un contrôleur de données Arc pour le mode de connexion directe n’est pas pris en charge.
- Le passage d’une valeur non valide au paramètre `--extensions` lors de la modification de la configuration d’un groupe de serveurs pour activer des extensions supplémentaires réinitialise de manière incorrecte la liste des extensions activées à ce qu’elle était au moment de la création du groupe de serveurs et empêche l’utilisateur de créer des extensions supplémentaires. La seule solution de contournement disponible dans ce cas est de supprimer le groupe de serveurs et de le redéployer.

## <a name="february-2021"></a>Février 2021

### <a name="data-controller"></a>Contrôleur de données

- Le mode de cluster de connexion directe est désactivé.

### <a name="azure-arc-enabled-postgresql-hyperscale"></a>Azure Arc enabled PostgreSQL Hyperscale

- La limite de restauration dans le temps n’est pas prise en charge pour l’instant sur le stockage NFS.
- Il n’est pas possible d’activer et de configurer l’extension pg_cron en même temps. Vous devez utiliser deux commandes pour cela. Une commande pour l’activer et une autre pour la configurer. 

   Par exemple :
   ```console
   § azdata arc postgres server edit -n myservergroup --extensions pg_cron 
   § azdata arc postgres server edit -n myservergroup --engine-settings cron.database_name='postgres'
   ```

   La première commande nécessite un redémarrage du groupe de serveurs. Ainsi, avant d’exécuter la deuxième commande, assurez-vous que l’état du groupe de serveurs est passé de Mise à jour à Prêt. Si vous exécutez la deuxième commande avant la fin du redémarrage, elle échouera. Si c’est le cas, attendez simplement quelques instants de plus et exécutez à nouveau la deuxième commande.

## <a name="introduced-prior-to-february-2021"></a>Introduit avant février 2021

### <a name="data-controller"></a>Contrôleur de données

- Sur Azure Kubernetes service (AKS), la version 1.19. x de Kubernetes n’est pas prise en charge.
- Sur Kubernetes 1.19, `containerd` n’est pas pris en charge.
- La ressource de contrôleur de données dans Azure est actuellement une ressource Azure. Toutes les mises à jour telles que les suppressions ne sont pas propagées vers le cluster kubernetes.
- Les noms d’instance ne peuvent pas dépasser 13 caractères
- Aucune mise à niveau sur place du contrôleur de données ou des instances de base de données Azure Arc.
- Les images conteneurs de services de données activés par Arc ne sont pas signées.  Il se peut que vous deviez configurer vos nœuds Kubernetes pour permettre l’extraction d’images de conteneur non signées.  Par exemple, si vous utilisez Docker en tant que runtime de conteneurs, vous pouvez définir la variable d’environnement DOCKER_CONTENT_TRUST=0 et redémarrer.  D’autres runtimes de conteneurs offrent des options similaires, par exemple dans [OpenShift](https://docs.openshift.com/container-platform/4.5/openshift_images/image-configuration.html#images-configuration-file_image-configuration).
- Impossible de créer des instances gérées SQL activées par Azure Arc, ou des groupes de serveurs PostgreSQL Hyperscale à partir du portail Azure.
- Pour le moment, si vous utilisez NFS, vous devez définir `allowRunAsRoot` sur `true` dans votre fichier de profil de déploiement avant de créer le contrôleur de données Azure Arc.
- Authentification de connexion SQL et PostgreSQL uniquement.  Aucune prise en charge d’Azure Active Directory ou d’Active Directory.
- La création d’un contrôleur de données sur OpenShift impose des contraintes de sécurité peu exigeantes.  Pour plus d'informations, reportez-vous à la documentation.
- Si vous utilisez Azure Kubernetes Service (AKS) sur Azure Stack Hub avec un contrôleur de données Azure Arc et des instances de base de données, la mise à niveau vers une version plus récente de Kubernetes n’est pas prise en charge. Avant de mettre à niveau le cluster Kubernetes, désinstallez le contrôleur de données Azure Arc et toutes les instances de base de données.
- Pour les clusters AKS qui s'étendent sur [plusieurs zones de disponibilité](../../aks/availability-zones.md), les services de données avec Azure Arc ne sont actuellement pas pris en charge. Pour contourner ce problème, lorsque vous créez le cluster AKS sur le portail Azure, si vous sélectionnez une région dans laquelle des zones sont disponibles, effacez toutes les zones du contrôle de sélection. Consultez le graphique suivant :

   :::image type="content" source="media/release-notes/aks-zone-selector.png" alt-text="Décochez les cases des différentes zones pour n'en spécifier aucune.":::


## <a name="next-steps"></a>Étapes suivantes

> **Vous voulez juste essayer ?**  
> Démarrez rapidement avec [Démarrage rapide d’Azure Arc](https://azurearcjumpstart.io/azure_arc_jumpstart/azure_arc_data/) sur AKS, AWS Elastic Kubernetes Service (EKS), Google Cloud Kubernetes Engine (GKE) ou sur une machine virtuelle Azure.

- [Installer les outils clients](install-client-tools.md)
- [Créer le contrôleur de données Azure Arc](create-data-controller.md) (nécessite l'installation préalable des outils clients)
- [Créer une instance gérée Azure SQL sur Azure Arc](create-sql-managed-instance.md) (nécessite la création préalable d’un contrôleur de données Azure Arc)
- [Créer un groupe de serveurs Azure Database pour PostgreSQL Hyperscale sur Azure Arc](create-postgresql-hyperscale-server-group.md) (nécessite la création préalable d’un contrôleur de données Azure Arc)
- [Fournisseurs de ressources pour les services Azure](../../azure-resource-manager/management/azure-services-resource-providers.md)
- [Notes de publication – Services de données activés par Azure Arc (préversion)](release-notes.md)
