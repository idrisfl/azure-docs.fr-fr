---
title: Utiliser les API et les kits SDK Azure Digital Twins
titleSuffix: Azure Digital Twins
description: Découvrez comment utiliser les API Azure Digital Twins, y compris par le biais du SDK.
author: baanders
ms.author: baanders
ms.date: 06/04/2020
ms.topic: how-to
ms.service: digital-twins
ms.openlocfilehash: f4f3fc8c928cd284088cc51120f1a7b485b4fac0
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2021
ms.locfileid: "104595343"
---
# <a name="use-the-azure-digital-twins-apis-and-sdks"></a>Utiliser les API et les kits SDK Azure Digital Twins

Azure Digital Twins est fourni avec les **API de plan de contrôle** et les **API de plan de données**, qui permettent de gérer votre instance et les éléments qu’elle contient. 
* Les API de plan de contrôle sont des API [Azure Resource Manager (ARM)](../azure-resource-manager/management/overview.md) qui couvrent les opérations de gestion des ressources, telles que la création et la suppression de votre instance. 
* Les API de plan de données sont des API Azure Digital Twins qui sont utilisées pour les opérations de gestion des données, telles que la gestion des modèles, des représentations et du graphique.

Cet article donne une vue d’ensemble des API disponibles, ainsi que des méthodes permettant d’interagir avec celles-ci. Vous pouvez utiliser les API REST directement avec les Swaggers qui y sont associés (via un outil tel que [Postman](how-to-use-postman.md)), ou via un Kit de développement logiciel (SDK).

## <a name="overview-control-plane-apis"></a>Vue d’ensemble : API de plan de contrôle

Les API de plan de contrôle sont des API [ARM](../azure-resource-manager/management/overview.md) utilisées pour la gestion de votre instance Azure Digital Twins dans son ensemble. Elles permettent donc d’effectuer des opérations telles que la création ou la suppression de votre instance dans son intégralité. Elles permettent également de créer et de supprimer des points de terminaison.

La version la plus récente de l’API de plan de contrôle est _**2020-12-01**_.

Pour utiliser les API de plan de contrôle :
* Vous pouvez appeler les API directement en référençant le dossier Swagger le plus récent dans le [référentiel Swagger du plan de contrôle](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/digitaltwins/resource-manager/Microsoft.DigitalTwins/stable). Ce dossier contient également un dossier d’exemples qui en montrent l’utilisation.
* Vous pouvez accéder aux SDK des API de contrôle en...
  - [ **.NET (C#)**](https://www.nuget.org/packages/Microsoft.Azure.Management.DigitalTwins/) ([référence [générée automatiquement]](/dotnet/api/overview/azure/digitaltwins/management)) ([source](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/digitaltwins/Microsoft.Azure.Management.DigitalTwins))
  - [**Java**](https://search.maven.org/search?q=a:azure-mgmt-digitaltwins) ([référence [générée automatiquement]](/java/api/overview/azure/digitaltwins)) ([source](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/digitaltwins))
  - [**JavaScript**](https://www.npmjs.com/package/@azure/arm-digitaltwins) ([source](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/digitaltwins/arm-digitaltwins))
  - [**Python**](https://pypi.org/project/azure-mgmt-digitaltwins/) ([source](https://github.com/Azure/azure-sdk-for-python/tree/release/v3/sdk/digitaltwins/azure-mgmt-digitaltwins))
  - [**Go**](https://pkg.go.dev/github.com/Azure/azure-sdk-for-go/services/digitaltwins/mgmt) ([source](https://github.com/Azure/azure-sdk-for-go/tree/master/services/digitaltwins/mgmt))

Vous pouvez également utiliser des API de plan de contrôle en interagissant avec Azure Digital Twins via le [portail Azure](https://portal.azure.com) et l’[interface de ligne de commande](how-to-use-cli.md).

## <a name="overview-data-plane-apis"></a>Vue d’ensemble : API de plan de données

Les API de plan de données sont les API Azure Digital Twins utilisées pour gérer les éléments compris dans votre instance Azure Digital Twins. Elles permettent d’effectuer des opérations telles que la création de routes, le chargement de modèles, la création de relations et la gestion des jumeaux. Elles peuvent être réparties dans les catégories suivantes :
* **DigitalTwinModels** : la catégorie DigitalTwinModels contient des API permettant de gérer des [modèles](concepts-models.md) dans une instance Azure Digital Twins. Les activités de gestion incluent le chargement, la validation, la récupération et la suppression des modèles créés dans DTDL.
* **DigitalTwins** : la catégorie DigitalTwins contient les API qui permettent aux développeurs de créer, de modifier et de supprimer les [jumeaux numériques](concepts-twins-graph.md) et leurs relations dans une instance Azure Digital Twins.
* **Query** : la catégorie Query permet aux développeurs de [trouver des jeux de jumeaux numériques dans le graphe jumeau](how-to-query-graph.md) parmi les relations.
* **Event Routes** : la catégorie Event Routes contient des API permettant d’[acheminer des données](concepts-route-events.md) via le système et vers les services en aval.

La version la plus récente de l’API de plan de données est _**2020-10-31**_.

Pour utiliser les API de plan de données :
* Vous pouvez appeler les API REST en...
   - référençant le dossier Swagger le plus récent dans le [référentiel Swagger du plan de données](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/digitaltwins/data-plane/Microsoft.DigitalTwins). Ce dossier contient également un dossier d’exemples qui en montrent l’utilisation. 
   - vous servant de la [documentation de référence d’API](/rest/api/azure-digitaltwins/).
* Vous pouvez utiliser le **SDK .NET (C#)** . Pour utiliser le SDK .NET...
   - Vous pouvez afficher et ajouter le package à partir de NuGet : [Azure.DigitalTwins.Core](https://www.nuget.org/packages/Azure.DigitalTwins.Core). 
   - vous pouvez consulter la [documentation de référence du SDK](/dotnet/api/overview/azure/digitaltwins/client).
   - vous pouvez trouver la source du SDK, y compris un dossier d’exemples, sur GitHub : [Bibliothèque de client Azure IoT Digital Twins pour .NET](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/digitaltwins/Azure.DigitalTwins.Core). 
   - Vous pouvez obtenir des informations détaillées et des exemples d’utilisation en passant à la section [*SDK .NET (C#) (plan de données)*](#net-c-sdk-data-plane) de cet article.
* Vous pouvez utiliser le **SDK Java**. Pour utiliser le Kit de développement logiciel (SDK) Java…
   - vous pouvez afficher et installer le package à partir de Maven : [`com.azure:azure-digitaltwins-core`](https://search.maven.org/artifact/com.azure/azure-digitaltwins-core/1.0.0/jar).
   - vous pouvez consulter la [documentation de référence du Kit de développement logiciel (SDK)](/java/api/overview/azure/digitaltwins/client).
   - vous pouvez trouver la source du Kit de développement logiciel (SDK) dans GitHub : [Bibliothèque de client Azure IoT Digital Twins pour Java](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/digitaltwins/azure-digitaltwins-core).
* Vous pouvez utiliser le **SDK JavaScript**. Pour utiliser le SDK JavaScript...
   - Vous pouvez afficher et installer le package à partir de npm : [Bibliothèque de client Core Azure Digital Twins pour JavaScript](https://www.npmjs.com/package/@azure/digital-twins-core).
   - vous pouvez consulter la [documentation de référence du SDK](/javascript/api/@azure/digital-twins-core/).
   - vous pouvez trouver la source du Kit de développement logiciel (SDK) dans GitHub : [Bibliothèque de client Core Azure Digital Twins pour JavaScript](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/digitaltwins/digital-twins-core)
* Vous pouvez utiliser le **SDK Python**. Pour utiliser le Kit de développement logiciel (SDK) Python…
   - Vous pouvez afficher et installer le package à partir de PyPi : [Bibliothèque de client Core Azure Digital Twins pour Python](https://pypi.org/project/azure-digitaltwins-core/).
   - vous pouvez consulter la [documentation de référence du SDK](/python/api/azure-digitaltwins-core/azure.digitaltwins.core).
   - vous pouvez trouver la source du Kit de développement logiciel (SDK) dans GitHub : [Bibliothèque de client Core Azure Digital Twins pour Python](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/digitaltwins/azure-digitaltwins-core)
* Vous pouvez générer un SDK pour un autre langage à l’aide d’AutoRest. Suivez les instructions fournies dans [*Procédure : Créer des kits SDK personnalisés pour Azure Digital Twins avec AutoRest*](how-to-create-custom-sdks.md).

Vous pouvez également utiliser des API de plan de données en interagissant avec Azure Digital Twins via l’[interface de ligne de commande](how-to-use-cli.md).

## <a name="net-c-sdk-data-plane"></a>SDK .NET (C#) (plan de données)

Le SDK .NET (C#) Azure Digital Twins fait partie du SDK Azure pour .NET. Il est open source et est basé sur les API de plan de données Azure Digital Twins.

> [!NOTE]
> Pour obtenir des informations détaillées sur la conception des kit de développement logiciel (SDK), consultez les [principes de conception pour les kits de développement logiciel (SDK) Azure](https://azure.github.io/azure-sdk/general_introduction.html) généraux, ainsi que les [instructions de conception de .NET](https://azure.github.io/azure-sdk/dotnet_introduction.html) spécifiques.

Pour utiliser le SDK, incluez le package NuGet **Azure.DigitalTwins.Core** dans votre projet. Vous aurez également besoin de la dernière version du package **Azure.Identity**. Dans Visual Studio, vous pouvez ajouter ces packages à l’aide du gestionnaire de package NuGet (accessible via *Outils > Gestionnaire de package NuGet > Gérer les packages NuGet pour la solution*). Vous pouvez également utiliser l’outil de ligne de commande .NET avec les commandes disponibles dans les liens des packages NuGet ci-dessous pour les ajouter à votre projet :
* [**Azure.DigitalTwins.Core**](https://www.nuget.org/packages/Azure.DigitalTwins.Core). Il s’agit du package pour le [SDK Azure Digital Twins pour .NET](/dotnet/api/overview/azure/digitaltwins/client). 
* [**Azure.Identity**](https://www.nuget.org/packages/Azure.Identity). Cette bibliothèque fournit des outils pour faciliter l’authentification auprès d’Azure.

Pour obtenir une procédure détaillée de l’utilisation des API dans la pratique, consultez le [*Tutoriel : Coder une application cliente*](tutorial-code.md). 

### <a name="net-sdk-usage-examples"></a>Exemples d’utilisation du SDK .NET

Voici quelques exemples de code illustrant l’utilisation du SDK .NET.

S’authentifier auprès du service :

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/authentication.cs" id="DefaultAzureCredential_basic":::

[!INCLUDE [Azure Digital Twins: local credentials note](../../includes/digital-twins-local-credentials-note.md)] 

Charger un modèle :

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/model_operations.cs" id="CreateModel":::

Lister les modèles :

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/model_operations.cs" id="GetModels":::

Créer des jumeaux :

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/twin_operations_sample.cs" id="CreateTwin_withHelper":::

Interroger les jumeaux et parcourir les résultats :

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/queries.cs" id="FullQuerySample":::

Consultez le [*Tutoriel : Coder une application cliente*](tutorial-code.md) pour une procédure détaillée de cet exemple de code d’application. 

Vous trouverez d’autres exemples dans le [dépôt GitHub du SDK .NET (C#)](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/digitaltwins/Azure.DigitalTwins.Core/samples).

#### <a name="serialization-helpers"></a>Applications d’assistance de sérialisation

Les assistances de sérialisation sont des fonctions d’assistance disponibles dans le kit de développement logiciel (SDK) pour créer ou désérialiser rapidement des données de jumeaux pour accéder à des informations de base. Étant donné que les méthodes principales du kit de développement logiciel (SDK) retournent des données de jumeaux au format JSON par défaut, il peut être utile d’utiliser ces classes d’assistance pour décomposer les données de jumeaux.

Les classes d’assistance disponibles sont les suivantes :
* `BasicDigitalTwin` : représente de façon générique les données de base d’un jumeau numérique
* `BasicDigitalTwinComponent` : représente de façon générique un composant dans les propriétés `Contents` d’un `BasicDigitalTwin`
* `BasicRelationship` : représente de façon générique les données de base d’une relation
* `DigitalTwinsJsonPropertyName` : contient les constantes de chaîne à utiliser dans la sérialisation et la désérialisation JSON pour les types de jumeaux numériques personnalisés

##### <a name="deserialize-a-digital-twin"></a>Désérialiser un jumeau numérique

Vous pouvez toujours désérialiser des données de jumeau à l’aide de la bibliothèque JSON de votre choix, comme `System.Text.Json` ou `Newtonsoft.Json`. Si vous avez besoin d’un accès de base à un jumeau, les classes d’assistance peuvent vous faciliter la tâche.

La classe d’assistance `BasicDigitalTwin` vous donne également accès aux propriétés définies dans le jumeau, par le biais d’un `Dictionary<string, object>`. Pour lister les propriétés du jumeau, vous pouvez utiliser ceci :

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/twin_operations_sample.cs" id="GetTwin":::

> [!NOTE]
> `BasicDigitalTwin` utilise des attributs `System.Text.Json`. Pour pouvoir utiliser `BasicDigitalTwin` avec votre [DigitalTwinsClient](/dotnet/api/azure.digitaltwins.core.digitaltwinsclient?view=azure-dotnet&preserve-view=true), vous devez initialiser le client avec le constructeur par défaut. Si vous voulez personnaliser l’option du sérialiseur, utilisez [JsonObjectSerializer](/dotnet/api/azure.core.serialization.jsonobjectserializer?view=azure-dotnet&preserve-view=true).

##### <a name="create-a-digital-twin"></a>Créer un jumeau numérique

À l’aide de la classe `BasicDigitalTwin`, vous pouvez préparer des données pour créer une instance de jumeau :

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/twin_operations_sample.cs" id="CreateTwin_withHelper":::

Le code ci-dessus équivaut à la variante « manuelle » suivante :

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/twin_operations_other.cs" id="CreateTwin_noHelper":::

##### <a name="deserialize-a-relationship"></a>Désérialiser une relation

Vous pouvez toujours désérialiser les données de relation vers le type de votre choix. Pour un accès de base à une relation, utilisez le type `BasicRelationship`.

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graph_operations_sample.cs" id="GetRelationshipsCall":::

La classe d’assistance `BasicRelationship` vous donne également accès aux propriétés définies dans la relation, par le biais d’un `IDictionary<string, object>`. Pour lister les propriétés, vous pouvez utiliser ceci :

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graph_operations_other.cs" id="ListRelationshipProperties":::

##### <a name="create-a-relationship"></a>Créer une relation

À l’aide de la classe `BasicRelationship`, vous pouvez également préparer des données pour créer des relations dans une instance de jumeau :

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graph_operations_other.cs" id="CreateRelationship_short":::

##### <a name="create-a-patch-for-twin-update"></a>Créer un correctif pour une mise à jour de jumeau

Les appels de mise à jour pour les jumeaux et les relations utilisent une structure de [correctif JSON](http://jsonpatch.com/). Pour créer des listes d’opérations de correctif JSON, vous pouvez utiliser le `JsonPatchDocument`, comme indiqué ci-dessous.

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/twin_operations_other.cs" id="UpdateTwin":::

## <a name="general-apisdk-usage-notes"></a>Remarques générales sur l’utilisation des API et des SDK

> [!NOTE]
> Notez qu’Azure Digital Twins ne prend pas actuellement en charge **Partage des ressources cross-origin (CORS)** . Pour plus d’informations sur les stratégies d’impact et de résolution, consultez la section [*Partage des ressources cross-origin (CORS)*](concepts-security.md#cross-origin-resource-sharing-cors) de la rubrique *Concepts : Sécurité pour les solutions Azure Digital Twins*.

La liste suivante fournit des instructions générales et des détails supplémentaires concernant l’utilisation des API et des SDK.

* Vous pouvez utiliser un outil de test REST HTTP comme Postman pour effectuer des appels directs aux API Azure Digital Twins. Pour plus d’informations sur ce processus, consultez [*Procédure : Faire des demandes avec Postman*](how-to-use-postman.md).
* Pour utiliser le SDK, instanciez la classe `DigitalTwinsClient`. Le constructeur exige des informations d’identification qui peuvent être obtenues avec diverses méthodes d’authentification dans le package `Azure.Identity`. Pour plus d’informations sur `Azure.Identity`, consultez la [documentation sur son espace de noms](/dotnet/api/azure.identity). 
* Vous pourrez trouver `InteractiveBrowserCredential` utile dans les débuts. Toutefois, il existe plusieurs autres options, comme les informations d’identification pour l’[identité managée](/dotnet/api/azure.identity.interactivebrowsercredential), qui permettent d’authentifier les [fonctions Azure configurées avec MSI](../app-service/overview-managed-identity.md?tabs=dotnet) dans Azure Digital Twins. Pour plus d’informations sur `InteractiveBrowserCredential`, consultez la [documentation sur sa classe](/dotnet/api/azure.identity.interactivebrowsercredential).
* Tous les appels d’API de service sont exposés comme des fonctions membres dans la classe `DigitalTwinsClient`.
* Toutes les fonctions de service existent dans une version synchrone et une version asynchrone.
* Toutes les fonctions de service lèvent une exception pour tout état de retour de 400 (ou supérieur). Veillez à wrapper les appels dans une section `try` et à intercepter au moins `RequestFailedExceptions`. Pour plus d’informations sur ce type d’exception, [cliquez ici](/dotnet/api/azure.requestfailedexception).
* La plupart des méthodes de service retournent `Response<T>` (ou `Task<Response<T>>` pour les appels asynchrones), où `T` correspond à la classe de l’objet de retour pour l’appel de service. La classe [`Response`](/dotnet/api/azure.response-1) encapsule le retour de service et présente les valeurs de retour dans son champ `Value`.  
* Les méthodes de service ayant des résultats paginés retournent des résultats `Pageable<T>` ou `AsyncPageable<T>`. Pour plus d’informations sur la classe `Pageable<T>`, [cliquez ici](/dotnet/api/azure.pageable-1). Pour plus d’informations sur `AsyncPageable<T>`, [cliquez ici](/dotnet/api/azure.asyncpageable-1).
* Vous pouvez effectuer une itération sur des résultats paginés à l’aide d’une boucle `await foreach`. Pour plus d’informations sur ce processus, [cliquez ici](/archive/msdn-magazine/2019/november/csharp-iterating-with-async-enumerables-in-csharp-8).
* Le SDK sous-jacent est `Azure.Core`. Pour plus d’informations sur l’infrastructure et les types de SDK, consultez la [documentation sur les espaces de noms Azure](/dotnet/api/azure).

Les méthodes de service retournent des objets fortement typés dès que cela est possible. Toutefois, étant donné qu’Azure Digital Twins est basé sur des modèles personnalisés configurés par l’utilisateur au moment de l’exécution (via des modèles DTDL chargés dans le service), de nombreuses API de service acceptent et retournent des données de jumeau au format JSON.

## <a name="monitor-api-metrics"></a>Superviser les métriques d’API

Les métriques d’API, comme celles concernant les requêtes, la latence et le taux d’échec, peuvent être affichées dans le [portail Azure](https://portal.azure.com/). 

Dans la page d’accueil du portail, recherchez votre instance Azure Digital Twins pour consulter les informations la concernant. Sélectionnez l’option **Métriques** dans le menu de l’instance Azure Digital Twins pour afficher la page *Métriques*.

:::image type="content" source="media/troubleshoot-metrics/azure-digital-twins-metrics.png" alt-text="Capture d’écran montrant la page des métriques pour Azure Digital Twins":::

À partir de là, vous pouvez afficher les métriques de votre instance et créer des vues personnalisées.

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment adresser des demandes directes aux API à l’aide de Postman :
* [*Guide pratique : Faire des demandes avec Postman*](how-to-use-postman.md)

Ou bien, dans la pratique, utilisez le Kit de développement logiciel (SDK) .NET en créant une application cliente à l’aide de ce tutoriel :
* [*Tutoriel : Coder une application cliente*](tutorial-code.md)