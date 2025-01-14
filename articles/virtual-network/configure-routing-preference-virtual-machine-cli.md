---
title: Configurer la préférence de routage pour une machine virtuelle – Azure CLI
description: Apprenez à créer une machine virtuelle avec une adresse IP publique et choix d’une préférence de routage à l’aide d’Azure CLI.
services: virtual-network
documentationcenter: na
author: KumudD
manager: mtillman
ms.service: virtual-network
ms.devlang: na
ms.topic: how-to
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2021
ms.author: mnayak
ms.custom: devx-track-azurecli
ms.openlocfilehash: ad8f2d150c3cf17c4b24c6dc92188be9017dcfa9
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2021
ms.locfileid: "101666008"
---
# <a name="configure-routing-preference-for-a-vm-using-azure-cli"></a>Configurer la préférence de routage pour une machine virtuelle à l’aide d’Azure CLI

Cet article explique comment configurer la préférence de routage pour une machine virtuelle. Le trafic lié à Internet à partir de la machine virtuelle est routé via le réseau du fournisseur de services Internet lorsque vous choisissez l’option de préférence de routage **Internet**. Le routage par défaut passe par le réseau Microsoft mondial.

Cet article explique comment créer une machine virtuelle avec une adresse IP publique définie pour acheminer le trafic via le réseau Internet public à l’aide d’Azure CLI.

## <a name="create-a-resource-group"></a>Créer un groupe de ressources
1. Si vous utilisez Cloud Shell, passez à l’étape 2. Ouvrez une session de commande et connectez-vous à Azure avec `az login`.
2. Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#az-group-create). L’exemple suivant crée un groupe de ressources dans la région Azure USA Est :

    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```

## <a name="create-a-public-ip-address"></a>Créer une adresse IP publique
Pour accéder à vos machines virtuelles à partir d’Internet, vous devez créer une adresse IP publique. Créez une adresse IP publique avec la commande [az network public-ip create](/cli/azure/network/public-ip). L’exemple suivant crée une adresse IP publique de type de préférence routage *Internet* dans la région *USA Est* :

```azurecli
az network public-ip create \
--name MyRoutingPrefIP \
--resource-group MyResourceGroup \
--location eastus \
--ip-tags 'RoutingPreference=Internet' \
--sku STANDARD \
--allocation-method static \
--version IPv4
```

## <a name="create-network-resources"></a>Créer des ressources réseau

Avant de déployer un machine virtuelle, vous devez créer des ressources réseau associées (groupe de sécurité réseau, réseau virtuel et carte réseau virtuelle).

### <a name="create-a-network-security-group"></a>Créer un groupe de sécurité réseau

Créez un groupe de sécurité réseau pour les règles qui régiront les communications entrantes et sortantes dans votre VNet avec la commande [az network nsg create](/cli/azure/network/nsg#az-network-nsg-create)

```azurecli
az network nsg create \
--name myNSG  \
--resource-group MyResourceGroup \
--location eastus
```

### <a name="create-a-virtual-network"></a>Créez un réseau virtuel

Créez un réseau virtuel avec la commande [az network vnet create](/cli/azure/network/vnet#az-network-vnet-create). L’exemple suivant crée un réseau virtuel nommé *myVNET* avec des sous-réseaux nommés *mySubNet* :

```azurecli
# Create a virtual network
az network vnet create \
--name myVNET \
--resource-group MyResourceGroup \
--location eastus

# Create a subnet
az network vnet subnet create \
--name mySubNet \
--resource-group MyResourceGroup \
--vnet-name myVNET \
--address-prefixes "10.0.0.0/24" \
--network-security-group myNSG
```

### <a name="create-a-nic"></a>Créer une carte réseau

Créez une carte réseau virtuelle pour la machine virtuelle avec la commande [az network nic create](/cli/azure/network/nic#az-network-nic-create). L’exemple suivant crée une carte réseau virtuelle qui sera attachée à la machine virtuelle.

```azurecli-interactive
# Create a NIC
az network nic create \
--name mynic  \
--resource-group MyResourceGroup \
--network-security-group myNSG  \
--vnet-name myVNET \
--subnet mySubNet  \
--private-ip-address-version IPv4 \
--public-ip-address MyRoutingPrefIP
```

## <a name="create-a-virtual-machine"></a>Création d'une machine virtuelle

Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#az-vm-create). L’exemple suivant crée une machine virtuelle Windows Server 2019, ainsi que les composants de réseau virtuel nécessaires s’ils n’existent pas.

```azurecli
az vm create \
--name myVM \
--resource-group MyResourceGroup \
--nics mynic \
--size Standard_A2 \
--image MicrosoftWindowsServer:WindowsServer:2019-Datacenter:latest \
--admin-username myUserName
```

## <a name="clean-up-resources"></a>Nettoyer les ressources

Quand vous n’avez plus besoin d’un groupe de ressources, vous pouvez utiliser [az group delete](/cli/azure/group#az-group-delete) pour le supprimer, ainsi que toutes les ressources qu’il contient :

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur la [préférence de routage dans les adresses IP publiques](routing-preference-overview.md).
- En savoir plus sur les [adresses IP publiques](./public-ip-addresses.md#public-ip-addresses) dans Azure.
- En savoir plus sur les [paramètres d’adresse IP publique](virtual-network-public-ip-address.md#create-a-public-ip-address).
