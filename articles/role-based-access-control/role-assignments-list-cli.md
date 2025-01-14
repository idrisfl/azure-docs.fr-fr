---
title: Répertorier les attributions de rôle Azure à l’aide d’Azure CLI et de la fonctionnalité RBAC Azure
description: Découvrez comment déterminer les ressources, utilisateurs, groupes, principaux de service ou identités managées qui ont accès à Azure CLI ou au contrôle d’accès en fonction du rôle (RBAC) Azure.
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.assetid: 3483ee01-8177-49e7-b337-4d5cb14f5e32
ms.service: role-based-access-control
ms.devlang: na
ms.topic: how-to
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 10/30/2020
ms.author: rolyon
ms.reviewer: bagovind
ms.openlocfilehash: 2d30571b68ba7e38e9960d1e434cf7844f6be852
ms.sourcegitcommit: 4b0e424f5aa8a11daf0eec32456854542a2f5df0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/20/2021
ms.locfileid: "107780098"
---
# <a name="list-azure-role-assignments-using-azure-cli"></a>Répertorier les attributions de rôle Azure à l’aide d’Azure CLI

[!INCLUDE [Azure RBAC definition list access](../../includes/role-based-access-control/definition-list.md)] Cet article explique comment lister les attributions de rôles à l’aide d’Azure CLI.

> [!NOTE]
> Si votre organisation possède des fonctions de gestion externalisées pour un fournisseur de services qui utilise la [gestion des ressources déléguées Azure](../lighthouse/concepts/azure-delegated-resource-management.md), les attributions de rôles autorisées par ce fournisseur de services ne seront pas affichées ici.

## <a name="prerequisites"></a>Prérequis

- [Bash Azure Cloud Shell](../cloud-shell/overview.md) ou [Azure CLI](/cli/azure)

## <a name="list-role-assignments-for-a-user"></a>Répertorier les attributions de rôles pour un utilisateur

Pour lister les attributions de rôles d’un utilisateur déterminé, utilisez [az role assignment list](/cli/azure/role/assignment#az_role_assignment_list) :

```azurecli
az role assignment list --assignee {assignee}
```

Par défaut, seules les attributions de rôles de l'abonnement actuel sont affichées. Pour afficher les attributions de rôles de l’abonnement actuel et antérieur, ajoutez le paramètre `--all`. Pour afficher les attributions de rôles héritées, ajoutez le paramètre `--include-inherited`.

L’exemple suivant liste les attributions de rôles octroyées directement à l’utilisateur *patlong\@contoso.com* :

```azurecli
az role assignment list --all --assignee patlong@contoso.com --output json --query '[].{principalName:principalName, roleDefinitionName:roleDefinitionName, scope:scope}'
```

```json
[
  {
    "principalName": "patlong@contoso.com",
    "roleDefinitionName": "Backup Operator",
    "scope": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/pharma-sales"
  },
  {
    "principalName": "patlong@contoso.com",
    "roleDefinitionName": "Virtual Machine Contributor",
    "scope": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/pharma-sales"
  }
]
```

## <a name="list-role-assignments-for-a-resource-group"></a>Lister les attributions de rôles pour un groupe de ressources

Pour lister les attributions de rôle qui existent dans l’étendue d’un groupe de ressources, utilisez [az role assignment list](/cli/azure/role/assignment#az_role_assignment_list) :

```azurecli
az role assignment list --resource-group {resourceGroup}
```

L’exemple suivant liste les attributions de rôles du groupe de ressources *pharma-sales* :

```azurecli
az role assignment list --resource-group pharma-sales --output json --query '[].{principalName:principalName, roleDefinitionName:roleDefinitionName, scope:scope}'
```

```json
[
  {
    "principalName": "patlong@contoso.com",
    "roleDefinitionName": "Backup Operator",
    "scope": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/pharma-sales"
  },
  {
    "principalName": "patlong@contoso.com",
    "roleDefinitionName": "Virtual Machine Contributor",
    "scope": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/pharma-sales"
  },
  
  ...

]
```

## <a name="list-role-assignments-for-a-subscription"></a>Répertorier les attributions de rôles pour un abonnement

Pour lister toutes les attributions de rôle dans l’étendue d’un abonnement, utilisez [az role assignment list](/cli/azure/role/assignment#az_role_assignment_list). Pour obtenir l’ID d’abonnement, accédez au panneau **Abonnements** du portail Azure ou utilisez [az account list](/cli/azure/account#az_account_list).

```azurecli
az role assignment list --subscription {subscriptionNameOrId}
```

Exemple :

```azurecli
az role assignment list --subscription 00000000-0000-0000-0000-000000000000 --output json --query '[].{principalName:principalName, roleDefinitionName:roleDefinitionName, scope:scope}'
```

```json
[
  {
    "principalName": "admin@contoso.com",
    "roleDefinitionName": "Owner",
    "scope": "/subscriptions/00000000-0000-0000-0000-000000000000"
  },
  {
    "principalName": "Subscription Admins",
    "roleDefinitionName": "Owner",
    "scope": "/subscriptions/00000000-0000-0000-0000-000000000000"
  },
  {
    "principalName": "alain@contoso.com",
    "roleDefinitionName": "Reader",
    "scope": "/subscriptions/00000000-0000-0000-0000-000000000000"
  },

  ...

]
```

## <a name="list-role-assignments-for-a-management-group"></a>Lister les attributions de rôles pour un groupe d’administration

Pour lister toutes les attributions de rôle dans l’étendue d’un groupe d’administration, utilisez [az role assignment list](/cli/azure/role/assignment#az_role_assignment_list). Pour obtenir l’ID du groupe d’administration, accédez au panneau **Groupes d’administration** dans le portail Azure ou utilisez [az account management-group list](/cli/azure/account/management-group#az_account_management_group_list).

```azurecli
az role assignment list --scope /providers/Microsoft.Management/managementGroups/{groupId}
```

Exemple :

```azurecli
az role assignment list --scope /providers/Microsoft.Management/managementGroups/sales-group --output json --query '[].{principalName:principalName, roleDefinitionName:roleDefinitionName, scope:scope}'
```

```json
[
  {
    "principalName": "admin@contoso.com",
    "roleDefinitionName": "Owner",
    "scope": "/providers/Microsoft.Management/managementGroups/sales-group"
  },
  {
    "principalName": "alain@contoso.com",
    "roleDefinitionName": "Reader",
    "scope": "/providers/Microsoft.Management/managementGroups/sales-group"
  }
]
```

## <a name="list-role-assignments-for-a-managed-identity"></a>Lister les attributions de rôles pour une identité managée

1. Récupérez l’ID du principal de l’identité managée affectée par le système ou par l’utilisateur.

    Pour obtenir l’ID du principal d’une identité managée affectée par l’utilisateur, vous pouvez utiliser [az ad sp list](/cli/azure/ad/sp#az_ad_sp_list) ou [az identity list](/cli/azure/identity#az_identity_list).

    ```azurecli
    az ad sp list --display-name "{name}" --query [].objectId --output tsv
    ```

    Pour obtenir l’ID du principal d’une identité managée affectée par le système, vous pouvez utiliser [az ad sp list](/cli/azure/ad/sp#az_ad_sp_list).

    ```azurecli
    az ad sp list --display-name "{vmname}" --query [].objectId --output tsv
    ```

1. Pour lister les attributions de rôles, utilisez [az role assignment list](/cli/azure/role/assignment#az_role_assignment_list).

    Par défaut, seules les attributions de rôles de l'abonnement actuel sont affichées. Pour afficher les attributions de rôles de l’abonnement actuel et antérieur, ajoutez le paramètre `--all`. Pour afficher les attributions de rôles héritées, ajoutez le paramètre `--include-inherited`.

    ```azurecli
    az role assignment list --assignee {objectId}
    ```

## <a name="next-steps"></a>Étapes suivantes

- [Attribuer des rôles Azure à l’aide d’Azure CLI](role-assignments-cli.md)