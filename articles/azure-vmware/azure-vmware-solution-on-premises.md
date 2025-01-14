---
title: Connecter Azure VMware Solution à votre environnement local
description: Apprenez à connecter Azure VMware Solution à votre environnement local.
ms.topic: tutorial
ms.date: 03/13/2021
ms.openlocfilehash: 0b26dc4756cb37544c2b2f8c5a75df0ac1a9d629
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2021
ms.locfileid: "103491790"
---
# <a name="connect-azure-vmware-solution-to-your-on-premises-environment"></a>Connecter Azure VMware Solution à votre environnement local

Dans cet article, vous allez continuer à utiliser les [informations recueillies lors de la planification](production-ready-deployment-steps.md) pour connecter Azure VMware Solution à votre environnement local.

Avant de commencer, sachez qu'il existe deux prérequis pour connecter Azure VMware Solution à votre environnement local :

- Un circuit ExpressRoute entre votre environnement local et Azure
- Un bloc d’adresses réseau CIDR /29 qui ne se chevauchent pas pour le peering d’ExpressRoute Global Reach, que vous avez défini dans le cadre de la [phase de planification](production-ready-deployment-steps.md)

>[!NOTE]
> Vous pouvez vous connecter par le biais d’un VPN. Cela dit, ce type de connexion n’est pas abordé dans ce guide de démarrage rapide.

## <a name="establish-an-expressroute-global-reach-connection"></a>Établir une connexion ExpressRoute Global Reach

Pour établir une connectivité locale avec votre cloud privé Azure VMware Solution à l'aide d'ExpressRoute Global Reach, suivez le tutoriel [​​Peering d'environnements locaux avec un cloud privé](tutorial-expressroute-global-reach-private-cloud.md).

Ce tutoriel aboutit à une connexion, comme indiqué dans le diagramme.

:::image type="content" source="media/pre-deployment/azure-vmware-solution-on-premises-diagram.png" alt-text="Diagramme de la connectivité du réseau local ExpressRoute Global Reach" lightbox="media/pre-deployment/azure-vmware-solution-on-premises-diagram.png" border="false":::

## <a name="verify-on-premises-network-connectivity"></a>Vérifier la connectivité réseau locale

Votre **routeur de périphérie local** doit maintenant indiquer où ExpressRoute connecte les segments de réseau NSX-T et les segments de gestion d'Azure VMware Solution.

>[!IMPORTANT]
>Chaque environnement est différent, et certains doivent autoriser ces itinéraires à se propager à nouveau sur le réseau local.  

Certains environnements sont dotés d’un pare-feu qui protège le circuit ExpressRoute.  En l’absence d’un pare-feu et d’une fonctionnalité de nettoyage des routes, vous pouvez effectuer un test ping pour votre serveur vCenter Azure VMware Solution ou pour une [machine virtuelle située sur le segment NSX-T](deploy-azure-vmware-solution.md#add-a-vm-on-the-nsx-t-network-segment) à partir de votre environnement local. En outre, vous pouvez accéder aux ressources de votre environnement local à partir de la machine virtuelle située sur le segment NSX-T.

## <a name="next-steps"></a>Étapes suivantes

Passez à la section suivante pour déployer et configurer VMware HCX

> [!div class="nextstepaction"]
> [Déployer et configurer VMware HCX](tutorial-deploy-vmware-hcx.md)