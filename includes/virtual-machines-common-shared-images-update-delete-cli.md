---
title: Fichier include
description: Fichier Include
services: virtual-machines
author: cynthn
ms.service: virtual-machines
ms.topic: include
ms.date: 04/25/2019
ms.author: cynthn
ms.custom: include file, devx-track-azurecli
ms.openlocfilehash: 4392e7f146f13e581f722b94f13038ad8abff0ba
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2021
ms.locfileid: "102244606"
---
## <a name="update-resources"></a>Mettre à jour les ressources

Il existe certaines limitations concernant les éléments qui peuvent être mis à jour. Les éléments suivants peuvent être mis à jour : 

Galerie d’images partagées :
- Description

Définition d’image :
- Processeurs virtuels recommandés
- Mémoire recommandée
- Description
- Date de fin de vie

Version d’image :
- Nombre de réplicas régionaux
- Régions cibles
- Exclusion du dernier
- Date de fin de vie

Si vous prévoyez d’ajouter des régions de réplica, ne supprimez pas l’image managée source. En effet, elle est nécessaire pour la réplication de la version de l’image vers d’autres régions. 

Mettez à jour la description d’une galerie à l’aide de ([az sig update](/cli/azure/sig#az-sig-update). 

```azurecli-interactive
az sig update \
   --gallery-name myGallery \
   --resource-group myGalleryRG \
   --set description="My updated description."
```


Mettez à jour la description d’une définition d’image à l’aide de [az sig image-definition update](/cli/azure/sig/image-definition#az-sig-image-definition-update).

```azurecli-interactive
az sig image-definition update \
   --gallery-name myGallery\
   --resource-group myGalleryRG \
   --gallery-image-definition myImageDefinition \
   --set description="My updated description."
```

Mettez à jour une version de l’image pour ajouter une région à répliquer à l’aide de [az sig image-version update](/cli/azure/sig/image-definition#az-sig-image-definition-update). Cette modification prendra un certain temps, puisque l’image est répliquée vers la nouvelle région.

```azurecli-interactive
az sig image-version update \
   --resource-group myGalleryRG \
   --gallery-name myGallery \
   --gallery-image-definition myImageDefinition \
   --gallery-image-version 1.0.0 \
   --add publishingProfile.targetRegions  name=eastus
```

Cet exemple montre comment utiliser [az sig image-version update](/cli/azure/sig/image-definition#az-sig-image-definition-update) pour empêcher l’utilisation de cette version de l’image comme image *la plus récente*.

```azurecli-interactive
az sig image-version update \
   --resource-group myGalleryRG \
   --gallery-name myGallery \
   --gallery-image-definition myImageDefinition \
   --gallery-image-version 1.0.0 \
   --set publishingProfile.excludeFromLatest=true
```

Cet exemple montre comment utiliser [az sig image-version update](/cli/azure/sig/image-definition#az-sig-image-definition-update) pour que cette version de l’image soit considérée comme l’image *la plus récente*.

```azurecli-interactive
az sig image-version update \
   --resource-group myGalleryRG \
   --gallery-name myGallery \
   --gallery-image-definition myImageDefinition \
   --gallery-image-version 1.0.0 \
   --set publishingProfile.excludeFromLatest=false
```

## <a name="delete-resources"></a>Supprimer des ressources

Vous devez supprimer les ressources dans l’ordre inverse, en supprimant tout d’abord la version de l’image. Après avoir supprimé toutes les versions de l’image, vous pouvez supprimer la définition de l’image. Après avoir supprimé toutes les définitions de l’image, vous pouvez supprimer la galerie. 

Supprimez une version de l’image avec [az sig image-version delete](/cli/azure/sig/image-version#az-sig-image-version-delete).

```azurecli-interactive
az sig image-version delete \
   --resource-group myGalleryRG \
   --gallery-name myGallery \
   --gallery-image-definition myImageDefinition \
   --gallery-image-version 1.0.0 
```

Supprimez une définition de l’image avec [az sig image-definition delete](/cli/azure/sig/image-definition#az-sig-image-definition-delete).

```azurecli-interactive
az sig image-definition delete \
   --resource-group myGalleryRG \
   --gallery-name myGallery \
   --gallery-image-definition myImageDefinition
```


Supprimez une galerie d’images à l’aide de [az sig delete](/cli/azure/sig#az-sig-delete).

```azurecli-interactive
az sig delete \
   --resource-group myGalleryRG \
   --gallery-name myGallery
```