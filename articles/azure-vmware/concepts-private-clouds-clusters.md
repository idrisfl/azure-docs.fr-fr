---
title: Concepts – Clusters et clouds privés
description: Découvrez les principales fonctionnalités des centres de données à définition logicielle Azure VMware Solution et des clusters vSphere.
ms.topic: conceptual
ms.date: 03/13/2021
ms.openlocfilehash: aff66e01ae4b056eb082d2000611718b1a5cf66a
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2021
ms.locfileid: "104773916"
---
#  <a name="azure-vmware-solution-private-cloud-and-cluster-concepts"></a>Concepts de cloud privé et de cluster Azure VMware Solution

Azure VMware Solution fournit des clouds privés basés sur VMware dans Azure. Les clouds privés contiennent des clusters créés avec des hôtes Azure nus dédiés. Ils sont déployés et gérés via le portail Azure, l’interface CLI ou PowerShell.  Les clusters approvisionnés dans des clouds privés incluent les logiciels VMware vSphere, vCenter, vSAN et NSX. Les déploiements de logiciels et composants matériels de cloud privé Azure VMware Solution sont entièrement intégrés et automatisés dans Azure.

Il existe une relation logique entre les abonnements Azure, les clouds privés Azure VMware Solution, les clusters vSAN et les hôtes. Le diagramme montre un abonnement Azure avec deux clouds privés représentant l’environnement de développement et de production.  Chacun de ces clouds privés comprend deux clusters. 

Cet article décrit tous ces concepts.

![Image de deux clouds privés dans un abonnement client](./media/hosts-clusters-private-clouds-final.png)


## <a name="private-clouds"></a>Clouds privés

Les clouds privés contiennent des clusters vSAN créés avec des hôtes Azure nus dédiés. Chaque cloud privé peut avoir plusieurs clusters gérés par les mêmes serveur vCenter et NSX-T Manager. Vous pouvez déployer et gérer des clouds privés dans le portail, l’interface CLI ou PowerShell. 

Comme avec d’autres ressources, les clouds privés sont installés et gérés à partir d’un abonnement Azure. Le nombre de clouds privés au sein d’un abonnement est évolutif. Au départ, il existe une limite d’un cloud privé par abonnement.

## <a name="clusters"></a>Clusters
Pour chaque cloud privé créé, il existe un cluster vSAN par défaut. Vous pouvez ajouter, supprimer et mettre à l’échelle des clusters à l’aide du portail Azure ou via l’API.  Tous les clusters ont une taille par défaut de trois hôtes et peuvent se mettre à l’échelle pour inclure jusqu’à 16 hôtes. Vous pouvez avoir jusqu’à quatre clusters par cloud privé.

Les clusters d’évaluation sont disponibles pour évaluation et limités à trois hôtes. Il existe un cluster d’évaluation unique par cloud privé. Vous pouvez mettre à l’échelle un cluster d’évaluation à l’aide d’un seul hôte au cours de la période d’évaluation.

Vous utilisez vSphere et NSX-T Manager pour gérer la plupart des autres aspects de la configuration ou de l’exploitation du cluster. Tout le stockage local de chaque hôte dans un cluster est contrôlé par le logiciel vSAN.

## <a name="hosts"></a>Hôtes

Les clusters Azure VMware Solution sont basés sur une infrastructure nue hyperconvergée. Le tableau suivant indique les capacités de mémoire RAM, de processeur et de disque de l’ordinateur hôte.

| Type d’hôte              |             UC             |   RAM (Go)   |  Niveau de cache du vSAN NVMe (To, RAW)  |  Niveau de capacité du vSAN SSD (To, RAW)  |
| :---                   |            :---:            |    :---:     |               :---:              |                :---:               |
| AVS36          |  Deux processeurs Intel 18 cœurs cadencés à 2,3 GHz  |     576      |                3.2               |                15,20               |

Les hôtes utilisés pour créer ou mettre à l’échelle des clusters proviennent d’un pool isolé d’hôtes. Ces hôtes ont passé des tests matériels et toutes leurs données ont été effacées de manière sécurisée. 

## <a name="vmware-software-versions"></a>Versions des logiciels VMware

[!INCLUDE [vmware-software-versions](includes/vmware-software-versions.md)]

## <a name="update-frequency"></a>Fréquence de mise à jour

[!INCLUDE [vmware-software-update-frequency](includes/vmware-software-update-frequency.md)]

## <a name="host-maintenance-and-lifecycle-management"></a>Maintenance de l’hôte et gestion du cycle de vie

La maintenance et la gestion du cycle de vie de l’hôte n’ont aucune incidence sur la capacité ou les performances des clusters du cloud privé.  Les mises à niveau de microprogramme et la réparation ou le remplacement de matériel sont des exemples de maintenance automatisée de l’hôte.

Microsoft est responsable de la gestion du cycle de vie d’appliances NSX-T, telles que NSX-T Manager et NSX-T Edge. Microsoft est également responsable du démarrage de la configuration réseau, comme la création de la passerelle de niveau 0 et l’activation du routage Nord-Sud. Vous êtes responsable de la configuration du SDN NSX-T. Par exemple, des segments réseau, des règles de pare-feu distribuées, des passerelles de niveau 1 et des équilibreurs de charge.

## <a name="backup-and-restoration"></a>Sauvegarde et restauration

Les configurations de vCenter et de NSX-T sont effectuées sur une planification de sauvegarde horaire.  Les sauvegardes sont conservées pendant trois jours. Si vous devez effectuer une restauration à partir d’une sauvegarde, ouvrez une [demande de support](https://rc.portal.azure.com/#create/Microsoft.Support) dans le portail Azure pour demander une restauration.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez abordé les concepts de cloud privé d’Azure VMware Solution, vous pouvez en apprendre davantage sur les sujets suivants : 

- [Concepts de mise en réseau et d’interconnexion d’Azure VMware Solution](concepts-networking.md).
- [Concepts de stockage pour Azure VMware Solution](concepts-storage.md).
- [Comment activer la ressource Azure VMware Solution](enable-azure-vmware-solution.md).

<!-- LINKS - internal -->
[concepts-networking]: ./concepts-networking.md

<!-- LINKS - external-->
[VCSA versions]: https://kb.vmware.com/s/article/2143838
[ESXi versions]: https://kb.vmware.com/s/article/2143832
[vSAN versions]: https://kb.vmware.com/s/article/2150753

