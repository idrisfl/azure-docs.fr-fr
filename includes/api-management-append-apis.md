---
author: vladvino
ms.service: api-management
ms.topic: include
ms.date: 11/09/2018
ms.author: vlvinogr
ms.openlocfilehash: 2bfa356deeede1c16bd5a464ea7081132a67faf6
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2021
ms.locfileid: "96183818"
---
## <a name="append-other-apis"></a>Ajouter d’autres API

Une API peut être composée d’API exposées par différents services, y compris la spécification OpenAPI, une API SOAP, la fonctionnalité API Apps d’Azure App Service, Azure Function App, Azure Logic Apps et Azure Service Fabric.

![Importer une API](./media/api-management-append-apis/import.png)

Pour ajouter une autre API à votre API existante, effectuez les étapes ci-dessous. Une fois que vous avez importé une autre API, les opérations sont ajoutées à votre API actuelle.

1. Accédez à votre instance Gestion des API Azure dans le portail Azure.
2. Sélectionnez **API** dans le menu de gauche.
3. Cliquez sur **...** à côté de l’API à laquelle vous souhaitez ajouter une autre API.
4. Sélectionnez **Importer** dans le menu déroulant.
5. Sélectionnez un service à partir duquel importer une API.