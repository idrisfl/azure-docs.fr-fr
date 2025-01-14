---
title: Vue d’ensemble de Kubernetes avec Azure Arc
services: azure-arc
ms.service: azure-arc
ms.date: 03/03/2021
ms.topic: overview
author: mlearned
ms.author: mlearned
description: Cet article offre une vue d’ensemble de Kubernetes avec Azure Arc.
keywords: Kubernetes, Arc, Azure, conteneurs
ms.custom: references_regions
ms.openlocfilehash: 69e9886f214d0076c8e66231fd6ad15bb060828f
ms.sourcegitcommit: 56b0c7923d67f96da21653b4bb37d943c36a81d6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/06/2021
ms.locfileid: "106449645"
---
# <a name="what-is-azure-arc-enabled-kubernetes"></a>Qu’est-ce que Kubernetes avec Azure Arc ?

Grâce à Kubernetes avec Azure Arc, vous pouvez attacher et configurer des clusters Kubernetes situés à l’intérieur ou à l’extérieur d’Azure. Quand vous connectez un cluster Kubernetes à Azure Arc :
* Il apparaît dans le portail Azure avec un ID Azure Resource Manager et une identité managée. 
* Il est placé dans un abonnement et un groupe de ressources Azure.
* Il reçoit des étiquettes comme n’importe quelle autre ressource Azure. 

Pour connecter un cluster Kubernetes à Azure, l’administrateur du cluster doit déployer des agents. Ces agents :
* S’exécutent dans l’`azure-arc`espace de noms Kubernetes en tant que déploiements Kubernetes standard.
* Gèrent la connectivité à Azure.
* Collectent les journaux et métriques Azure Arc.
* Surveillent les demandes de configuration. 

Kubernetes avec Azure Arc prend en charge le protocole SSL standard pour sécuriser les données en transit. Par ailleurs, les données sont chiffrées au repos dans une base de données Azure Cosmos DB pour garantir leur confidentialité.

## <a name="supported-kubernetes-distributions"></a>Distributions Kubernetes prises en charge

Kubernetes avec Azure Arc fonctionne pour tous les clusters Kubernetes certifiés CNCF (Cloud Native Computing Foundation). L’équipe d’Azure Arc s’est associée à [des partenaires clés du secteur pour valider la conformité](./validation-program.md) des distributions Kubernetes avec Azure Arc.

## <a name="supported-scenarios"></a>Scénarios pris en charge 

Kubernetes avec Azure Arc prend en charge les scénarios suivants : 

* Connecter un cluster Kubernetes s’exécutant en dehors d’Azure pour l’inventaire, le regroupement et l’étiquetage.

* Déployer des applications et appliquer une configuration à l’aide de la gestion de la configuration basée sur GitOps. 

* Voir et superviser vos clusters à l’aide d’Azure Monitor pour les conteneurs.

* Appliquer une protection contre les menaces à l'aide d'Azure Defender pour Kubernetes.

* Appliquer des stratégies à l’aide d’Azure Policy pour Kubernetes.

[!INCLUDE [azure-lighthouse-supported-service](../../../includes/azure-lighthouse-supported-service.md)]

## <a name="supported-regions"></a>Régions prises en charge 

Kubernetes avec Azure Arc est actuellement pris en charge dans ces régions : 

* USA Est
* Europe Ouest
* Centre-USA Ouest
* États-Unis - partie centrale méridionale
* Asie Sud-Est
* Sud du Royaume-Uni
* USA Ouest 2
* Australie Est
* USA Est 2
* Europe Nord

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment connecter un cluster à Azure Arc.
> [!div class="nextstepaction"]
> [Connecter un cluster à Azure Arc](./quickstart-connect-cluster.md)
