---
author: mikben
ms.service: azure-communication-services
ms.topic: include
ms.date: 03/10/2021
ms.author: mikben
ms.openlocfilehash: 22a9cf3338f422341928a77f2bf14c497aa2ba31
ms.sourcegitcommit: 32e0fedb80b5a5ed0d2336cea18c3ec3b5015ca1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2021
ms.locfileid: "105563772"
---
## <a name="prerequisites"></a>Prérequis

- Compte Azure avec un abonnement actif. [Créez un compte gratuitement](https://azure.microsoft.com/free/dotnet/).
- Installer [l’interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/install-azure-cli-windows?tabs=azure-cli) 

## <a name="create-azure-communication-resource"></a>Créer une ressource Azure Communication

Pour créer une ressource Azure Communication Services, [connectez-vous à Azure CLI](/cli/azure/authenticate-azure-cli). Pour ce faire, vous pouvez utiliser le terminal et la commande ```az login```, puis fournir vos informations d’identification. Exécutez la commande suivante pour créer la ressource :

```azurecli
az communication create --name "<communicationName>" --location "Global" --data-location "United States" --resource-group "<resourceGroup>"
```

Si vous souhaitez sélectionner un abonnement particulier, vous pouvez également spécifier l’indicateur ```--subscription``` et fournir l’ID d’abonnement.
```
az communication create --name "<communicationName>" --location "Global" --data-location "United States" --resource-group "<resourceGroup> --subscription "<subscriptionID>"
```

Vous pouvez configurer votre ressource Communication Services avec les options suivantes :

* Groupe de ressources
* Nom de la ressource Communication Services
* Zone géographique à laquelle associer la ressource

À l’étape suivante, vous pouvez attribuer des étiquettes à la ressource. Les étiquettes peuvent être utiles pour organiser vos ressources Azure. Pour plus d’informations sur les étiquettes, consultez la [documentation sur l’étiquetage des ressources](../../../azure-resource-manager/management/tag-resources.md).

## <a name="manage-your-communication-services-resource"></a>Gérer la ressource Communication Services

Pour ajouter des balises à votre ressource Communication Services, exécutez les commandes suivantes : Vous pouvez également cibler un abonnement spécifique.

```azurecli
az communication update --name "<communicationName>" --tags newTag="newVal1" --resource-group "<resourceGroup>"

az communication update --name "<communicationName>" --tags newTag="newVal2" --resource-group "<resourceGroup>" --subscription "<subscriptionID>"

az communication show --name "<communicationName>" --resource-group "<resourceGroup>"

az communication show --name "<communicationName>" --resource-group "<resourceGroup>" --subscription "<subscriptionID>"
```

Pour plus d’informations sur des commandes supplémentaires, consultez [az communication](/cli/azure/ext/communication/communication).
