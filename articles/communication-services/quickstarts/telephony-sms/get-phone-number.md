---
title: 'Démarrage rapide : Gérer les numéros de téléphone avec Azure Communication Services'
description: Découvrez comment gérer les numéros de téléphone avec Azure Communication Services
author: prakulka
manager: nmurav
services: azure-communication-services
ms.author: prakulka
ms.date: 03/10/2021
ms.topic: quickstart
ms.service: azure-communication-services
ms.custom: references_regions
zone_pivot_groups: acs-azp-java-net-python-csharp-js
ms.openlocfilehash: 19bb79f9a4deaebfacc75918c46a5516d2d398be
ms.sourcegitcommit: 3b5cb7fb84a427aee5b15fb96b89ec213a6536c2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107498189"
---
# <a name="quickstart-manage-phone-numbers"></a>Démarrage rapide : Gérer les numéros de téléphone

[!INCLUDE [Regional Availability Notice](../../includes/regional-availability-include.md)]

[!INCLUDE [Bulk Acquisition Instructions](../../includes/phone-number-special-order.md)]

::: zone pivot="platform-azp"
[!INCLUDE [Azure portal](./includes/phone-numbers-portal.md)]
::: zone-end

::: zone pivot="programming-language-csharp"
[!INCLUDE [Azure portal](./includes/phone-numbers-net.md)]
::: zone-end

::: zone pivot="programming-language-java"
[!INCLUDE [Java](./includes/phone-numbers-java.md)]
::: zone-end

::: zone pivot="programming-language-python"
[!INCLUDE [Python](./includes/phone-numbers-python.md)]
::: zone-end

::: zone pivot="programming-language-javascript"
[!INCLUDE [JavaScript](./includes/phone-numbers-js.md)]
::: zone-end

## <a name="troubleshooting"></a>Dépannage

Questions et problèmes courantes :

- L’achat de téléphone est pris en charge uniquement aux États-Unis. Pour acheter des numéros de téléphone, vérifiez les points suivants :
  - L’adresse de facturation de l’abonnement Azure associé se trouve aux États-Unis. Actuellement, vous ne pouvez pas déplacer une ressource vers un autre abonnement.
  - Votre ressource Communication Services est approvisionnée dans l’emplacement de données États-Unis. Actuellement, vous ne pouvez pas déplacer une ressource vers un autre emplacement de données.

- Quand un numéro de téléphone est libéré, sa libération effective ou son rachat éventuel n’intervient pas avant la fin du cycle de facturation.

- Quand une ressource Communication Services est supprimée, les numéros de téléphone associés à cette ressource sont, dans le même temps, automatiquement libérés.

## <a name="next-steps"></a>Étapes suivantes

Dans ce guide de démarrage rapide, vous avez appris comment :

> [!div class="checklist"]
> * Acheter un numéro de téléphone
> * Gérer votre numéro de téléphone
> * Libérer un numéro de téléphone

> [!div class="nextstepaction"]
> [Envoyer un SMS](../telephony-sms/send.md)
> [Bien démarrer avec les appels](../voice-video-calling/getting-started-with-calling.md)
