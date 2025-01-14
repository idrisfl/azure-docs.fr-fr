---
title: Créer un magasin Azure App Configuration avec un modèle Azure Resource Manager (modèle ARM)
titleSuffix: Azure App Configuration
description: Découvrez comment créer un magasin Azure App Configuration à l’aide d’un modèle Azure Resource Manager (modèle ARM).
author: GrantMeStrength
ms.author: jken
ms.date: 10/16/2020
ms.service: azure-app-configuration
ms.topic: quickstart
ms.custom: subject-armqs
ms.openlocfilehash: c5976053e32bcc97e57ef8f74b3249df83d322c4
ms.sourcegitcommit: 32e0fedb80b5a5ed0d2336cea18c3ec3b5015ca1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2021
ms.locfileid: "105933234"
---
# <a name="quickstart-create-an-azure-app-configuration-store-by-using-an-arm-template"></a>Démarrage rapide : Créer un magasin Azure App Configuration avec un modèle Resource Manager

Ce guide de démarrage rapide explique comment :

- Déployer un magasin App Configuration à l’aide d’un modèle Azure Resource Manager (modèle ARM).
- Créer des paires clé/valeur dans un magasin App Configuration à l’aide d’un modèle ARM.
- Lire des paires clé/valeur dans un magasin App Configuration à partir d’un modèle ARM.

[!INCLUDE [About Azure Resource Manager](../../includes/resource-manager-quickstart-introduction.md)]

Si votre environnement remplit les prérequis et que vous êtes déjà familiarisé avec l’utilisation des modèles ARM, sélectionnez le bouton **Déployer sur Azure**. Le modèle s’ouvre dans le portail Azure.

[![Déployer sur Azure](../media/template-deployments/deploy-to-azure.svg)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-app-configuration-store-kv%2Fazuredeploy.json)

## <a name="prerequisites"></a>Prérequis

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

## <a name="review-the-template"></a>Vérifier le modèle

Le modèle utilisé dans ce démarrage rapide est tiré des [modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/101-app-configuration-store-kv/). Il crée un magasin App Configuration avec deux paires clé/valeur à l’intérieur de celui-ci. Il utilise ensuite la fonction `reference` pour générer les valeurs des deux ressources clé/valeur. La lecture de la valeur de la clé de cette manière permet de l’utiliser ailleurs dans le modèle.

Le guide de démarrage rapide utilise l’élément `copy` pour créer plusieurs instances de la ressource clé-valeur. Pour en savoir plus sur l’élément `copy`, consultez [Itération des ressources dans les modèles Resource Manager](../azure-resource-manager/templates/copy-resources.md).

> [!IMPORTANT]
> Ce modèle nécessite la version de fournisseur de ressources App Configuration `2020-07-01-preview` ou ultérieure. Cette version utilise la fonction `reference` pour lire les paires clé/valeur. La fonction `listKeyValue` qui était utilisée pour lire les paires clé/valeur dans la version précédente n’est pas disponible à partir de la version `2020-07-01-preview`.

:::code language="json" source="~/quickstart-templates/101-app-configuration-store-kv/azuredeploy.json":::

Deux ressources Azure sont définies dans le modèle :

- [Microsoft.AppConfiguration/configurationStores](/azure/templates/microsoft.appconfiguration/2020-07-01-preview/configurationstores) : crée un magasin App Configuration.
- [Microsoft.AppConfiguration/configurationStores/keyValues](/azure/templates/microsoft.appconfiguration/2020-07-01-preview/configurationstores/keyvalues) : crée une valeur de clé dans le magasin App Configuration.

> [!TIP]
> Le nom de la ressource `keyValues` est une combinaison de clé et d’étiquette. La clé et l’étiquette sont jointes par le délimiteur de `$`. L’étiquette est facultative. Dans l’exemple ci-dessus, la ressource `keyValues` portant le nom `myKey` crée une paire clé/valeur sans étiquette.
>
> L’encodage par pourcentage, également appelé encodage d’URL, permet aux clés ou aux étiquettes d’inclure des caractères qui ne sont pas autorisés dans les noms des ressources des modèles Resource Manager. `%` n’étant pas un caractère autorisé, `~` est utilisé à la place. Pour encoder correctement un nom, effectuez les étapes suivantes :
>
> 1. Appliquer l’encodage d’URL
> 2. Remplacer `~` par `~7E`
> 3. Remplacer `%` par `~`
>
> Par exemple, si vous souhaitez créer une paire clé-valeur avec un nom de clé `AppName:DbEndpoint` et un nom d’étiquette `Test`, le nom de la ressource doit être `AppName~3ADbEndpoint$Test`.

> [!NOTE]
> App Configuration permet l’accès aux données de valeur de clé via une [liaison privée](concept-private-endpoint.md) à partir de votre réseau virtuel. Par défaut, lorsque la fonctionnalité est activée, toutes les demandes de données App Configuration sur le réseau public sont refusées. Étant donné que le modèle ARM s’exécute en dehors de votre réseau virtuel, l’accès aux données à partir d’un modèle ARM n’est pas autorisé. Pour autoriser l’accès aux données à partir d’un modèle ARM quand une liaison privée est utilisée, vous pouvez activer l’accès au réseau public à l’aide de la commande Azure CLI suivante. Il est important de prendre en compte les implications en matière de sécurité de l’activation de l’accès au réseau public dans ce scénario.
>
> ```azurecli-interactive
> az appconfig update -g MyResourceGroup -n MyAppConfiguration --enable-public-network true
> ```

## <a name="deploy-the-template"></a>Déployer le modèle

Cliquez sur l’image ci-après pour vous connecter à Azure et ouvrir un modèle. Le modèle crée un magasin App Configuration avec deux paires clé/valeur à l’intérieur de celui-ci.

[![Déployer sur Azure](../media/template-deployments/deploy-to-azure.svg)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-app-configuration-store-kv%2Fazuredeploy.json)

Vous pouvez également déployer le modèle avec l’applet de commande PowerShell suivante. Les paires clé/valeur apparaîtront dans la sortie de la console PowerShell.

```azurepowershell-interactive
$projectName = Read-Host -Prompt "Enter a project name that is used for generating resource names"
$location = Read-Host -Prompt "Enter the location (i.e. centralus)"
$templateUri = "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-app-configuration-store-kv/azuredeploy.json"

$resourceGroupName = "${projectName}rg"

New-AzResourceGroup -Name $resourceGroupName -Location "$location"
New-AzResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateUri $templateUri

Read-Host -Prompt "Press [ENTER] to continue ..."
```

## <a name="review-deployed-resources"></a>Vérifier les ressources déployées

1. Connectez-vous au [portail Azure](https://portal.azure.com).
1. Dans la zone de recherche du portail Azure, tapez **App Configuration**. Sélectionnez **App Configuration** dans la liste.
1. Sélectionnez la ressource App Configuration tout juste créée.
1. Sous **Opérations**, cliquez sur **Explorateur de configurations**.
1. Vérifiez que deux paires clé/valeur existent.

## <a name="clean-up-resources"></a>Nettoyer les ressources

Quand vous n’en avez plus besoin, supprimez le groupe de ressources, le magasin App Configuration et toutes les ressources associées. Si vous envisagez de réutiliser le magasin App Configuration, ne le supprimez pas. Si vous n’avez plus besoin de ce magasin, supprimez toutes les ressources créées dans le cadre de ce guide de démarrage rapide en exécutant l’applet de commande suivante :

```azurepowershell-interactive
$resourceGroupName = Read-Host -Prompt "Enter the Resource Group name"
Remove-AzResourceGroup -Name $resourceGroupName
Write-Host "Press [ENTER] to continue..."
```

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur l’ajout d’un indicateur de fonctionnalité et d’une référence Key Vault à un magasin App Configuration, consultez les exemples de modèles ARM ci-dessous.

- [101-app-configuration-store-ff](https://github.com/Azure/azure-quickstart-templates/tree/master/101-app-configuration-store-ff)
- [101-app-configuration-store-keyvaultref](https://github.com/Azure/azure-quickstart-templates/tree/master/101-app-configuration-store-keyvaultref)