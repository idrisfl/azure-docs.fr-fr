---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 08/18/2020
ms.author: inhenkel
ms.custom: CLI, devx-track-azurecli
ms.openlocfilehash: e16e3dc6788fb30a87a78fd6d6077087f461cfa7
ms.sourcegitcommit: afb79a35e687a91270973990ff111ef90634f142
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107511014"
---
<!--Create a media services asset CLI-->

La commande Azure CLI suivante crée un actif multimédia Media Services. Remplacez les valeurs `assetName`, `amsAccountName` et `resourceGroup` par les valeurs que vous utilisez actuellement.

```azurecli
az ams asset create -n assetName -a amsAccountName -g resourceGroup
```
