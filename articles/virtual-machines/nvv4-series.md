---
title: Série NVv4
description: Spécifications pour les machines virtuelles de la série NVv4.
author: vikancha-MSFT
ms.service: virtual-machines
ms.subservice: vm-sizes-gpu
ms.topic: conceptual
ms.date: 01/12/2020
ms.author: vikancha
ms.openlocfilehash: 2d0f82565ec4010d03003ed902e9aba819e93bc3
ms.sourcegitcommit: b4fbb7a6a0aa93656e8dd29979786069eca567dc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107303183"
---
# <a name="nvv4-series"></a>Série NVv4 

Les machines virtuelles de la série NVv4 sont alimentées par des GPU [AMD Radeon Instinct MI25](https://www.amd.com/en/products/professional-graphics/instinct-mi25) et des processeurs AMD EPYC 7V12(Rome). Avec la série NVv4, Azure introduit des machines virtuelles avec des GPU partiels. Choisissez la machine virtuelle à la bonne taille pour les applications graphiques accélérées GPU et les bureaux virtuels depuis 1/8ème d’un GPU avec une mémoire tampon de trame de 2 Gio jusqu’à un GPU complet avec une mémoire tampon de trame de 16 Gio. Les machines virtuelles NVv4 prennent actuellement en charge uniquement le système d’exploitation invité Windows.

<br>

[ACU](acu.md) : 230-260<br>
[Stockage Premium](premium-storage-performance.md) : Pris(e) en charge<br>
[Mise en cache du Stockage Premium](premium-storage-performance.md) : Pris(e) en charge<br>
[Disques Ultra](disks-types.md#ultra-disk) : pris en charge ([En savoir plus](https://techcommunity.microsoft.com/t5/azure-compute/ultra-disk-storage-for-hpc-and-gpu-vms/ba-p/2189312) sur la disponibilité, l’utilisation et les performances) <br>
[Migration dynamique](maintenance-and-updates.md) : Non pris en charge<br>
[Mises à jour avec préservation de la mémoire](maintenance-and-updates.md) : Non pris en charge<br>
[Génération de machine virtuelle prise en charge](generation-2.md) : Génération 1 et 2<br>
[Performances réseau accélérées](../virtual-network/create-vm-accelerated-networking-cli.md) : Pris en charge<br>
[Disques de système d’exploitation éphémères](ephemeral-os-disks.md) : Pris en charge <br>
<br>

| Taille | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | GPU | Mémoire GPU : Gio | Disques de données max. | Nombre max. de cartes réseau / Bande passante réseau attendue (Mbits/s) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_NV4as_v4 |4 |14 |88 | 1/8 | 2 | 4 | 2 / 1 000 |
| Standard_NV8as_v4 |8 |28 |176 | 1/4 | 4 | 8 | 4 / 2 000 |
| Standard_NV16as_v4 |16 |56 |352 | 1/2 | 8 | 16 | 8 / 4 000 |
| Standard_NV32as_v4 |32 |112 |704 | 1 | 16 | 32 | 8 / 8000 |

<sup>1</sup> Les machines virtuelles de la série NVv4 sont dotées de la technologie SMT (Simultaneous MultiThreading) AMD

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../includes/virtual-machines-common-sizes-table-defs.md)]

## <a name="supported-operating-systems-and-drivers"></a>Systèmes d’exploitation et pilotes pris en charge

Pour tirer parti des fonctionnalités GPU des machines virtuelles de la série NVv4 Azure exécutant Windows, installez des pilotes GPU AMD.

Pour installer manuellement les pilotes GPU AMD, consultez [Configuration des pilotes GPU AMD de série N pour Windows](./windows/n-series-amd-driver-setup.md) pour connaître les systèmes d’exploitation pris en charge, les pilotes et les étapes d’installation et de vérification.

## <a name="other-sizes"></a>Autres tailles

- [Usage général](sizes-general.md)
- [Mémoire optimisée](sizes-memory.md)
- [Optimisé pour le stockage](sizes-storage.md)
- [Optimisé pour le GPU](sizes-gpu.md)
- [Calcul haute performance](sizes-hpc.md)
- [Générations précédentes](sizes-previous-gen.md)

## <a name="next-steps"></a>Étapes suivantes

Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.
