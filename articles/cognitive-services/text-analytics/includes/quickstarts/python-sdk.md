---
author: aahill
ms.service: cognitive-services
ms.subservice: text-analytics
ms.topic: include
ms.date: 02/09/2021
ms.author: aahi
ms.openlocfilehash: 791591f3d98f9e6902e89a880c464e6a609e3a1f
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104599040"
---
<a name="HOLTop"></a>

# <a name="version-31-preview"></a>[Version préliminaire de la version 3.1](#tab/version-3-1)

[Documentation de référence v3.1](/python/api/azure-ai-textanalytics/azure.ai.textanalytics) | [Code source de la bibliothèque v3.1](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/textanalytics/azure-ai-textanalytics) | [Package v3.1 (PiPy)](https://pypi.org/project/azure-ai-textanalytics/) | [Exemples v3.1](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/textanalytics/azure-ai-textanalytics/samples)

# <a name="version-30"></a>[Version 3.0](#tab/version-3)

[Documentation de référence v3](/python/api/azure-ai-textanalytics/azure.ai.textanalytics) | [Code source de la bibliothèque v3](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/textanalytics) | [Package v3 (PiPy)](https://pypi.org/project/azure-ai-textanalytics/) | [Exemples v3](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/textanalytics/azure-ai-textanalytics/samples)

---

## <a name="prerequisites"></a>Prérequis

* Abonnement Azure - [En créer un gratuitement](https://azure.microsoft.com/free/cognitive-services)
* [Python 3.x](https://www.python.org/)
* Une fois que vous avez votre abonnement Azure, <a href="https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesTextAnalytics"  title="créez une ressource Analyse de texte"  target="_blank">Créer une ressource Analyse de texte </a> dans le portail Azure pour obtenir votre clé et votre point de terminaison. Une fois le déploiement effectué, cliquez sur **Accéder à la ressource**.
    * Vous aurez besoin de la clé et du point de terminaison de la ressource que vous créez pour connecter votre application à l’API Analyse de texte. Vous collerez votre clé et votre point de terminaison dans le code ci-dessous plus loin dans le guide de démarrage rapide.
    * Vous pouvez utiliser le niveau tarifaire Gratuit (`F0`) pour tester le service, puis passer par la suite à un niveau payant pour la production.
* Pour utiliser la fonctionnalité d’analyse, vous aurez besoin d’une ressource Analyse de texte avec le niveau tarifaire Standard (S).

## <a name="setting-up"></a>Configuration

### <a name="install-the-client-library"></a>Installer la bibliothèque de client

Après avoir installé Python, vous pouvez installer la bibliothèque de client avec :

# <a name="version-31-preview"></a>[Version préliminaire de la version 3.1](#tab/version-3-1)

```console
pip install azure-ai-textanalytics --pre
```

> [!TIP]
> Vous voulez voir l’intégralité du fichier de code de démarrage rapide à la fois ? Vous le trouverez [sur GitHub](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/python/TextAnalytics/python-v3-client-library.py), qui contient les exemples de code dans ce guide de démarrage rapide. 

# <a name="version-30"></a>[Version 3.0](#tab/version-3)

```console
pip install --upgrade azure-ai-textanalytics
```

> [!TIP]
> Vous voulez voir l’intégralité du fichier de code de démarrage rapide à la fois ? Vous le trouverez [sur GitHub](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/python/TextAnalytics/python-v3-client-library.py), qui contient les exemples de code dans ce guide de démarrage rapide. 


---

### <a name="create-a-new-python-application"></a>Créer une application Python

Créez un fichier Python et des variables pour le point de terminaison et la clé d’abonnement Azure de votre ressource.

[!INCLUDE [text-analytics-find-resource-information](../find-azure-resource-info.md)]

```python
key = "<paste-your-text-analytics-key-here>"
endpoint = "<paste-your-text-analytics-endpoint-here>"
```


## <a name="object-model"></a>Modèle objet

# <a name="version-31-preview"></a>[Version préliminaire de la version 3.1](#tab/version-3-1)

Le client Analyse de texte est un objet `TextAnalyticsClient` qui s’authentifie auprès d’Azure. Le client fournit plusieurs méthodes pour analyser le texte. 

Lorsque le traitement du texte est envoyé à l’API sous la forme d’une liste de `documents`, qui est une liste de chaînes, une liste de représentation de type dictée ou une liste de `TextDocumentInput/DetectLanguageInput`. Un objet `dict-like` contient une combinaison de `id`, de `text` et de `language/country_hint`. L’attribut `text` stocke le texte à analyser dans le `country_hint` d’origine, et vous pouvez utiliser n’importe quelle valeur pour `id`. 

L’objet Response est une liste contenant les informations d’analyse de chaque document. 

# <a name="version-30"></a>[Version 3.0](#tab/version-3)

Le client Analyse de texte est un objet `TextAnalyticsClient` qui s’authentifie auprès d’Azure à l’aide de votre clé. Le client fournit plusieurs méthodes pour analyser le texte en tant que lot. 

Pendant un traitement par lots, le texte est envoyé à l’API sous la forme d’une liste de `documents`, qui sont des objets `dictionary` contenant une combinaison d’attributs `id`, `text` et `language` en fonction de la méthode utilisée. L’attribut `text` stocke le texte à analyser dans le `language` d’origine, et vous pouvez utiliser n’importe quelle valeur pour `id`. 

L’objet Response est une liste contenant les informations analysées de chaque document. 

---

## <a name="code-examples"></a>Exemples de code

Ces extraits de code montrent comment effectuer les tâches suivantes avec la bibliothèque cliente Analyse de texte pour Python :

# <a name="version-31-preview"></a>[Version préliminaire de la version 3.1](#tab/version-3-1)

* [Authentifier le client](#authenticate-the-client)
* [Analyse des sentiments](#sentiment-analysis)
* [Exploration des opinions](#opinion-mining)
* [Détection de la langue](#language-detection)
* [Reconnaissance d’entité nommée](#named-entity-recognition-ner) 
* [Reconnaissance des informations d’identification personnelle](#personally-identifiable-information-recognition) 
* [Liaison d’entités](#entity-linking)
* [Extraction de phrases clés](#key-phrase-extraction)


# <a name="version-30"></a>[Version 3.0](#tab/version-3)

* [Authentifier le client](#authenticate-the-client)
* [Analyse des sentiments](#sentiment-analysis)
* [Détection de la langue](#language-detection)
* [Reconnaissance d’entité nommée](#named-entity-recognition-ner) 
* [Liaison d’entités](#entity-linking)
* [Extraction de phrases clés](#key-phrase-extraction)

---

## <a name="authenticate-the-client"></a>Authentifier le client

# <a name="version-31-preview"></a>[Version 3.1 preview](#tab/version-3-1)

Créez une fonction pour instancier l’objet `TextAnalyticsClient` avec vos `key` et `endpoint` créés plus haut. Ensuite, créez un client. 

```python
from azure.ai.textanalytics import TextAnalyticsClient
from azure.core.credentials import AzureKeyCredential

def authenticate_client():
    ta_credential = AzureKeyCredential(key)
    text_analytics_client = TextAnalyticsClient(
            endpoint=endpoint, 
            credential=ta_credential)
    return text_analytics_client

client = authenticate_client()
```

# <a name="version-30"></a>[Version 3.0](#tab/version-3)

Créez une fonction pour instancier l’objet `TextAnalyticsClient` avec vos `key` et `endpoint` créés plus haut. Ensuite, créez un client. Notez que `api_version=TextAnalyticsApiVersion.V3_0` doit être défini pour utiliser la version 3.0.

```python
# use this code if you're using SDK version is 5.0.0
from azure.ai.textanalytics import TextAnalyticsClient
from azure.core.credentials import AzureKeyCredential

def authenticate_client():
    ta_credential = AzureKeyCredential(key)
    text_analytics_client = TextAnalyticsClient(
            endpoint=endpoint, 
            credential=ta_credential) 
    return text_analytics_client

client = authenticate_client()
```

Si vous avez installé la version 5.1.0 de la bibliothèque de client à l’aide de `pip install azure-ai-textanalytics --pre`, vous pouvez spécifier la version 3.0 de l’API Analyse de texte avec le paramètre `api_version` du client. Utilisez uniquement la méthode `authenticate_client()` suivante si votre client est v5.1.0 ou version ultérieure.

```python
# Only use the following code sample if you're using v5.1.0 of the client library, 
# and are looking to specify v3.0 of the Text Analytics API for your client
from azure.ai.textanalytics import TextAnalyticsClient, TextAnalyticsApiVersion
from azure.core.credentials import AzureKeyCredential
def authenticate_client():
   ta_credential = AzureKeyCredential(key)
   text_analytics_client = TextAnalyticsClient(
     endpoint=endpoint,
     credential=ta_credential,
     api_version=TextAnalyticsApiVersion.V3_0
   )
   
client = authenticate_client()
```

--- 

## <a name="sentiment-analysis"></a>analyse de sentiments

# <a name="version-31-preview"></a>[Version préliminaire de la version 3.1](#tab/version-3-1)

Créez une fonction appelée `sentiment_analysis_example()` qui prend le client comme argument, puis appelle la fonction `analyze_sentiment()`. L’objet de réponse retourné contient l’étiquette de sentiment et le score de l’intégralité du document d’entrée ainsi qu’une analyse des sentiments pour chaque phrase.


```python
def sentiment_analysis_example(client):

    documents = ["I had the best day of my life. I wish you were there with me."]
    response = client.analyze_sentiment(documents=documents)[0]
    print("Document Sentiment: {}".format(response.sentiment))
    print("Overall scores: positive={0:.2f}; neutral={1:.2f}; negative={2:.2f} \n".format(
        response.confidence_scores.positive,
        response.confidence_scores.neutral,
        response.confidence_scores.negative,
    ))
    for idx, sentence in enumerate(response.sentences):
        print("Sentence: {}".format(sentence.text))
        print("Sentence {} sentiment: {}".format(idx+1, sentence.sentiment))
        print("Sentence score:\nPositive={0:.2f}\nNeutral={1:.2f}\nNegative={2:.2f}\n".format(
            sentence.confidence_scores.positive,
            sentence.confidence_scores.neutral,
            sentence.confidence_scores.negative,
        ))
          
sentiment_analysis_example(client)
```

### <a name="output"></a>Output

```console
Document Sentiment: positive
Overall scores: positive=1.00; neutral=0.00; negative=0.00 

Sentence: I had the best day of my life.
Sentence 1 sentiment: positive
Sentence score:
Positive=1.00
Neutral=0.00
Negative=0.00

Sentence: I wish you were there with me.
Sentence 2 sentiment: neutral
Sentence score:
Positive=0.21
Neutral=0.77
Negative=0.02
```

## <a name="opinion-mining"></a>Exploration des opinions

Pour effectuer une analyse des sentiments avec exploration des opinions, créez une fonction appelée `sentiment_analysis_with_opinion_mining_example()` qui prend le client comme argument, puis appelle la fonction `analyze_sentiment()` avec l’indicateur d’option `show_opinion_mining=True`. L’objet de réponse retourné contient non seulement l’étiquette de sentiment et le score de l’intégralité du document d’entrée avec une analyse des sentiments pour chaque phrase, mais aussi l’analyse des sentiments au niveau de l’aspect et de l’opinion.


```python
def sentiment_analysis_with_opinion_mining_example(client):

    documents = [
        "The food and service were unacceptable, but the concierge were nice"
    ]

    result = client.analyze_sentiment(documents, show_opinion_mining=True)
    doc_result = [doc for doc in result if not doc.is_error]

    positive_reviews = [doc for doc in doc_result if doc.sentiment == "positive"]
    negative_reviews = [doc for doc in doc_result if doc.sentiment == "negative"]

    positive_mined_opinions = []
    mixed_mined_opinions = []
    negative_mined_opinions = []

    for document in doc_result:
        print("Document Sentiment: {}".format(document.sentiment))
        print("Overall scores: positive={0:.2f}; neutral={1:.2f}; negative={2:.2f} \n".format(
            document.confidence_scores.positive,
            document.confidence_scores.neutral,
            document.confidence_scores.negative,
        ))
        for sentence in document.sentences:
            print("Sentence: {}".format(sentence.text))
            print("Sentence sentiment: {}".format(sentence.sentiment))
            print("Sentence score:\nPositive={0:.2f}\nNeutral={1:.2f}\nNegative={2:.2f}\n".format(
                sentence.confidence_scores.positive,
                sentence.confidence_scores.neutral,
                sentence.confidence_scores.negative,
            ))
            for mined_opinion in sentence.mined_opinions:
                target = mined_opinion.target
                print("......'{}' target '{}'".format(target.sentiment, target.text))
                print("......Target score:\n......Positive={0:.2f}\n......Negative={1:.2f}\n".format(
                    target.confidence_scores.positive,
                    target.confidence_scores.negative,
                ))
                for assessment in mined_opinion.assessments:
                    print("......'{}' assessment '{}'".format(assessment.sentiment, assessment.text))
                    print("......Assessment score:\n......Positive={0:.2f}\n......Negative={1:.2f}\n".format(
                        assessment.confidence_scores.positive,
                        assessment.confidence_scores.negative,
                    ))
            print("\n")
        print("\n")
          
sentiment_analysis_with_opinion_mining_example(client)
```

### <a name="output"></a>Output

```console
Document Sentiment: positive
Overall scores: positive=0.84; neutral=0.00; negative=0.16

Sentence: The food and service were unacceptable, but the concierge were nice
Sentence sentiment: positive
Sentence score:
Positive=0.84
Neutral=0.00
Negative=0.16

......'negative' target 'food'
......Target score:
......Positive=0.01
......Negative=0.99

......'negative' assessment 'unacceptable'
......Assessment score:
......Positive=0.01
......Negative=0.99

......'negative' target 'service'
......Target score:
......Positive=0.01
......Negative=0.99

......'negative' assessment 'unacceptable'
......Assessment score:
......Positive=0.01
......Negative=0.99

......'positive' target 'concierge'
......Target score:
......Positive=1.00
......Negative=0.00

......'positive' assessment 'nice'
......Assessment score:
......Positive=1.00
......Negative=0.00





Press any key to continue . . .

```

# <a name="version-30"></a>[Version 3.0](#tab/version-3)

Créez une fonction appelée `sentiment_analysis_example()` qui prend le client comme argument, puis appelle la fonction `analyze_sentiment()`. L’objet de réponse retourné contient l’étiquette de sentiment et le score de l’intégralité du document d’entrée ainsi qu’une analyse des sentiments pour chaque phrase.


```python
def sentiment_analysis_example(client):

    documents = ["I had the best day of my life. I wish you were there with me."]
    response = client.analyze_sentiment(documents = documents)[0]
    print("Document Sentiment: {}".format(response.sentiment))
    print("Overall scores: positive={0:.2f}; neutral={1:.2f}; negative={2:.2f} \n".format(
        response.confidence_scores.positive,
        response.confidence_scores.neutral,
        response.confidence_scores.negative,
    ))
    for idx, sentence in enumerate(response.sentences):
        print("Sentence: {}".format(sentence.text))
        print("Sentence {} sentiment: {}".format(idx+1, sentence.sentiment))
        print("Sentence score:\nPositive={0:.2f}\nNeutral={1:.2f}\nNegative={2:.2f}\n".format(
            sentence.confidence_scores.positive,
            sentence.confidence_scores.neutral,
            sentence.confidence_scores.negative,
        ))
          
sentiment_analysis_example(client)
```

### <a name="output"></a>Output

```console
Document Sentiment: positive
Overall scores: positive=1.00; neutral=0.00; negative=0.00 

Sentence: I had the best day of my life.
Sentence 1 sentiment: positive
Sentence score:
Positive=1.00
Neutral=0.00
Negative=0.00

Sentence: I wish you were there with me.
Sentence 2 sentiment: neutral
Sentence score:
Positive=0.21
Neutral=0.77
Negative=0.02
```

---

## <a name="language-detection"></a>Détection de la langue

# <a name="version-31-preview"></a>[Version préliminaire de la version 3.1](#tab/version-3-1)

Créez une fonction appelée `language_detection_example()` qui prend le client comme argument, puis appelle la fonction `detect_language()`. L’objet de réponse retourné contient la langue détectée dans `primary_language` si l’opération réussit et un `error` si ce n’est pas le cas.

> [!Tip]
> Dans certains cas, il peut être difficile de lever toute ambiguïté sur les langues en fonction de l’entrée. Vous pouvez utiliser le paramètre `country_hint` pour spécifier un code de pays à 2 lettres. L’API utilise « US » comme countryHint par défaut. Pour modifier ce comportement, vous pouvez réinitialiser ce paramètre en définissant cette valeur sur une chaîne vide `country_hint : ""`. 

```python
def language_detection_example(client):
    try:
        documents = ["Ce document est rédigé en Français."]
        response = client.detect_language(documents = documents, country_hint = 'us')[0]
        print("Language: ", response.primary_language.name)

    except Exception as err:
        print("Encountered exception. {}".format(err))
language_detection_example(client)
```


### <a name="output"></a>Output

```console
Language:  French
```

# <a name="version-30"></a>[Version 3.0](#tab/version-3)

Créez une fonction appelée `language_detection_example()` qui prend le client comme argument, puis appelle la fonction `detect_language()`. L’objet de réponse retourné contient la langue détectée dans `primary_language` si l’opération réussit et un `error` si ce n’est pas le cas.

> [!Tip]
> Dans certains cas, il peut être difficile de lever toute ambiguïté sur les langues en fonction de l’entrée. Vous pouvez utiliser le paramètre `country_hint` pour spécifier un code de pays à 2 lettres. L’API utilise « US » comme countryHint par défaut. Pour modifier ce comportement, vous pouvez réinitialiser ce paramètre en définissant cette valeur sur une chaîne vide `country_hint : ""`. 

```python
def language_detection_example(client):
    try:
        documents = ["Ce document est rédigé en Français."]
        response = client.detect_language(documents = documents, country_hint = 'us')[0]
        print("Language: ", response.primary_language.name)

    except Exception as err:
        print("Encountered exception. {}".format(err))
language_detection_example(client)
```


### <a name="output"></a>Output

```console
Language:  French
```


---

## <a name="named-entity-recognition-ner"></a>Reconnaissance d’entité nommée (NER)

# <a name="version-31-preview"></a>[Version préliminaire de la version 3.1](#tab/version-3-1)

> [!NOTE]
> Dans la version `3.1` : 
> * La liaison d’entités est une demande autre que NER.

Créez une fonction appelée `entity_recognition_example` qui prend le client comme argument, puis appelle la fonction `recognize_entities()` et effectue une itération dans les résultats. L’objet de réponse retourné contient la liste des entités détectées dans `entity` si l’opération réussit, et `error` si elle échoue. Pour chaque entité détectée, affichez sa catégorie et sa sous-catégorie, le cas échéant.

```python
def entity_recognition_example(client):

    try:
        documents = ["I had a wonderful trip to Seattle last week."]
        result = client.recognize_entities(documents = documents)[0]

        print("Named Entities:\n")
        for entity in result.entities:
            print("\tText: \t", entity.text, "\tCategory: \t", entity.category, "\tSubCategory: \t", entity.subcategory,
                    "\n\tConfidence Score: \t", round(entity.confidence_score, 2), "\tLength: \t", entity.length, "\tOffset: \t", entity.offset, "\n")

    except Exception as err:
        print("Encountered exception. {}".format(err))
entity_recognition_example(client)
```

### <a name="output"></a>Output

```console
Named Entities:

        Text:    trip   Category:        Event  SubCategory:     None
        Confidence Score:        0.61   Length:          4      Offset:          18

        Text:    Seattle        Category:        Location       SubCategory:     GPE
        Confidence Score:        0.82   Length:          7      Offset:          26

        Text:    last week      Category:        DateTime       SubCategory:     DateRange
        Confidence Score:        0.8    Length:          9      Offset:          34
```

### <a name="entity-linking"></a>Liaison d’entités

Créez une fonction appelée `entity_linking_example()` qui prend le client comme argument, puis appelle la fonction `recognize_linked_entities()` et effectue une itération dans les résultats. L’objet de réponse retourné contient la liste des entités détectées dans `entities` si l’opération réussit, et `error` si elle échoue. Les entités liées étant identifiées de manière unique, les occurrences d’une même entité sont regroupées sous un objet `entity` sous la forme d’une liste d’objets `match`.

```python
def entity_linking_example(client):

    try:
        documents = ["""Microsoft was founded by Bill Gates and Paul Allen on April 4, 1975, 
        to develop and sell BASIC interpreters for the Altair 8800. 
        During his career at Microsoft, Gates held the positions of chairman,
        chief executive officer, president and chief software architect, 
        while also being the largest individual shareholder until May 2014."""]
        result = client.recognize_linked_entities(documents = documents)[0]

        print("Linked Entities:\n")
        for entity in result.entities:
            print("\tName: ", entity.name, "\tId: ", entity.data_source_entity_id, "\tUrl: ", entity.url,
            "\n\tData Source: ", entity.data_source)
            print("\tMatches:")
            for match in entity.matches:
                print("\t\tText:", match.text)
                print("\t\tConfidence Score: {0:.2f}".format(match.confidence_score))
                print("\t\tOffset: {}".format(match.offset))
                print("\t\tLength: {}".format(match.length))
            
    except Exception as err:
        print("Encountered exception. {}".format(err))
entity_linking_example(client)
```

### <a name="output"></a>Output

```console
Linked Entities:

        Name:  Microsoft        Id:  Microsoft  Url:  https://en.wikipedia.org/wiki/Microsoft
        Data Source:  Wikipedia
        Matches:
                Text: Microsoft
                Confidence Score: 0.55
                Offset: 0
                Length: 9
                Text: Microsoft
                Confidence Score: 0.55
                Offset: 168
                Length: 9
        Name:  Bill Gates       Id:  Bill Gates         Url:  https://en.wikipedia.org/wiki/Bill_Gates
        Data Source:  Wikipedia
        Matches:
                Text: Bill Gates
                Confidence Score: 0.63
                Offset: 25
                Length: 10
                Text: Gates
                Confidence Score: 0.63
                Offset: 179
                Length: 5
        Name:  Paul Allen       Id:  Paul Allen         Url:  https://en.wikipedia.org/wiki/Paul_Allen
        Data Source:  Wikipedia
        Matches:
                Text: Paul Allen
                Confidence Score: 0.60
                Offset: 40
                Length: 10
        Name:  April 4  Id:  April 4    Url:  https://en.wikipedia.org/wiki/April_4
        Data Source:  Wikipedia
        Matches:
                Text: April 4
                Confidence Score: 0.32
                Offset: 54
                Length: 7
        Name:  BASIC    Id:  BASIC      Url:  https://en.wikipedia.org/wiki/BASIC
        Data Source:  Wikipedia
        Matches:
                Text: BASIC
                Confidence Score: 0.33
                Offset: 98
                Length: 5
        Name:  Altair 8800      Id:  Altair 8800        Url:  https://en.wikipedia.org/wiki/Altair_8800
        Data Source:  Wikipedia
        Matches:
                Text: Altair 8800
                Confidence Score: 0.88
                Offset: 125
                Length: 11
```

### <a name="personally-identifiable-information-recognition"></a>Reconnaissance des informations d’identification personnelle

Créez une fonction appelée `pii_recognition_example` qui prend le client comme argument, puis appelle la fonction `recognize_pii_entities()` et effectue une itération dans les résultats. L’objet de réponse retourné contient la liste des entités détectées dans `entity` si l’opération réussit, et `error` si elle échoue. Pour chaque entité détectée, affichez sa catégorie et sa sous-catégorie, le cas échéant.

```python
def pii_recognition_example(client):
    documents = [
        "The employee's SSN is 859-98-0987.",
        "The employee's phone number is 555-555-5555."
    ]
    response = client.recognize_pii_entities(documents, language="en")
    result = [doc for doc in response if not doc.is_error]
    for doc in result:
        print("Redacted Text: {}".format(doc.redacted_text))
        for entity in doc.entities:
            print("Entity: {}".format(entity.text))
            print("\tCategory: {}".format(entity.category))
            print("\tConfidence Score: {}".format(entity.confidence_score))
            print("\tOffset: {}".format(entity.offset))
            print("\tLength: {}".format(entity.length))
pii_recognition_example(client)
```

### <a name="output"></a>Output

```console
Redacted Text: The employee's SSN is ***********.
Entity: 859-98-0987
        Category: U.S. Social Security Number (SSN)
        Confidence Score: 0.65
        Offset: 22
        Length: 11
Redacted Text: The employee's phone number is ************.
Entity: 555-555-5555
        Category: Phone Number
        Confidence Score: 0.8
        Offset: 31
        Length: 12
```

# <a name="version-30"></a>[Version 3.0](#tab/version-3)

> [!NOTE]
> Dans la version `3.0` : 
> * La liaison d’entités est une demande autre que NER.

Créez une fonction appelée `entity_recognition_example` qui prend le client comme argument, puis appelle la fonction `recognize_entities()` et effectue une itération dans les résultats. L’objet de réponse retourné contient la liste des entités détectées dans `entity` si l’opération réussit, et `error` si elle échoue. Pour chaque entité détectée, affichez sa catégorie et sa sous-catégorie, le cas échéant.

```python
def entity_recognition_example(client):

    try:
        documents = ["I had a wonderful trip to Seattle last week."]
        result = client.recognize_entities(documents = documents)[0]

        print("Named Entities:\n")
        for entity in result.entities:
            print("\tText: \t", entity.text, "\tCategory: \t", entity.category, "\tSubCategory: \t", entity.subcategory,
                    "\n\tConfidence Score: \t", round(entity.confidence_score, 2), "\n")

    except Exception as err:
        print("Encountered exception. {}".format(err))
entity_recognition_example(client)
```

### <a name="output"></a>Output

```console
Named Entities:

        Text:    trip   Category:        Event  SubCategory:     None
        Confidence Score:        0.61

        Text:    Seattle        Category:        Location       SubCategory:     GPE
        Confidence Score:        0.82

        Text:    last week      Category:        DateTime       SubCategory:     DateRange
        Confidence Score:        0.8
```

### <a name="entity-linking"></a>Liaison d’entités

Créez une fonction appelée `entity_linking_example()` qui prend le client comme argument, puis appelle la fonction `recognize_linked_entities()` et effectue une itération dans les résultats. L’objet de réponse retourné contient la liste des entités détectées dans `entities` si l’opération réussit, et `error` si elle échoue. Les entités liées étant identifiées de manière unique, les occurrences d’une même entité sont regroupées sous un objet `entity` sous la forme d’une liste d’objets `match`.

```python
def entity_linking_example(client):

    try:
        documents = ["""Microsoft was founded by Bill Gates and Paul Allen on April 4, 1975, 
        to develop and sell BASIC interpreters for the Altair 8800. 
        During his career at Microsoft, Gates held the positions of chairman,
        chief executive officer, president and chief software architect, 
        while also being the largest individual shareholder until May 2014."""]
        result = client.recognize_linked_entities(documents = documents)[0]

        print("Linked Entities:\n")
        for entity in result.entities:
            print("\tName: ", entity.name, "\tId: ", entity.data_source_entity_id, "\tUrl: ", entity.url,
            "\n\tData Source: ", entity.data_source)
            print("\tMatches:")
            for match in entity.matches:
                print("\t\tText:", match.text)
                print("\t\tConfidence Score: {0:.2f}".format(match.confidence_score))
            
    except Exception as err:
        print("Encountered exception. {}".format(err))
entity_linking_example(client)
```

### <a name="output"></a>Output

```console
Linked Entities:

        Name:  Altair 8800      Id:  Altair 8800        Url:  https://en.wikipedia.org/wiki/Altair_8800
        Data Source:  Wikipedia
        Matches:
                Text: Altair 8800
                Confidence Score: 0.88
        Name:  Bill Gates       Id:  Bill Gates         Url:  https://en.wikipedia.org/wiki/Bill_Gates
        Data Source:  Wikipedia
        Matches:
                Text: Bill Gates
                Confidence Score: 0.63
                Text: Gates
                Confidence Score: 0.63
        Name:  Paul Allen       Id:  Paul Allen         Url:  https://en.wikipedia.org/wiki/Paul_Allen
        Data Source:  Wikipedia
        Matches:
                Text: Paul Allen
                Confidence Score: 0.60
        Name:  Microsoft        Id:  Microsoft  Url:  https://en.wikipedia.org/wiki/Microsoft
        Data Source:  Wikipedia
        Matches:
                Text: Microsoft
                Confidence Score: 0.55
                Text: Microsoft
                Confidence Score: 0.55
        Name:  April 4  Id:  April 4    Url:  https://en.wikipedia.org/wiki/April_4
        Data Source:  Wikipedia
        Matches:
                Text: April 4
                Confidence Score: 0.32
        Name:  BASIC    Id:  BASIC      Url:  https://en.wikipedia.org/wiki/BASIC
        Data Source:  Wikipedia
        Matches:
                Text: BASIC
                Confidence Score: 0.33
```

---

### <a name="key-phrase-extraction"></a>Extraction d’expressions clés

# <a name="version-31-preview"></a>[Version préliminaire de la version 3.1](#tab/version-3-1)

Créez une fonction appelée `key_phrase_extraction_example()` qui prend le client comme argument, puis appelle la fonction `extract_key_phrases()`. Le résultat contiendra la liste des expressions clés détectées dans `key_phrases` si l’opération réussit et un `error` si ce n’est pas le cas. Imprimez les expressions clés détectées.

```python
def key_phrase_extraction_example(client):

    try:
        documents = ["My cat might need to see a veterinarian."]

        response = client.extract_key_phrases(documents = documents)[0]

        if not response.is_error:
            print("\tKey Phrases:")
            for phrase in response.key_phrases:
                print("\t\t", phrase)
        else:
            print(response.id, response.error)

    except Exception as err:
        print("Encountered exception. {}".format(err))
        
key_phrase_extraction_example(client)
```


### <a name="output"></a>Output

```console
    Key Phrases:
         cat
         veterinarian
```

# <a name="version-30"></a>[Version 3.0](#tab/version-3)

Créez une fonction appelée `key_phrase_extraction_example()` qui prend le client comme argument, puis appelle la fonction `extract_key_phrases()`. Le résultat contiendra la liste des expressions clés détectées dans `key_phrases` si l’opération réussit et un `error` si ce n’est pas le cas. Imprimez les expressions clés détectées.

```python
def key_phrase_extraction_example(client):

    try:
        documents = ["My cat might need to see a veterinarian."]

        response = client.extract_key_phrases(documents = documents)[0]

        if not response.is_error:
            print("\tKey Phrases:")
            for phrase in response.key_phrases:
                print("\t\t", phrase)
        else:
            print(response.id, response.error)

    except Exception as err:
        print("Encountered exception. {}".format(err))
        
key_phrase_extraction_example(client)
```


### <a name="output"></a>Output

```console
    Key Phrases:
         cat
         veterinarian
```


---

## <a name="use-the-api-asynchronously-with-the-batch-analyze-operation"></a>Utiliser l’API de manière asynchrone avec l’opération d’analyse par lots

# <a name="version-31-preview"></a>[Version préliminaire de la version 3.1](#tab/version-3-1)

[!INCLUDE [Analyze operation pricing](../analyze-operation-pricing-caution.md)]

Créez une fonction appelée `analyze_batch_actions_example()` qui prend le client comme argument, puis appelle la fonction `begin_analyze_batch_actions()`. Il en résultera une opération durable qui sera interrogée pour obtenir des résultats.

```python
    def analyze_batch_actions_example(client):
        documents = [
            "Microsoft was founded by Bill Gates and Paul Allen."
        ]

        poller = text_analytics_client.begin_analyze_batch_actions(
            documents,
            display_name="Sample Text Analysis",
            entities_recognition_tasks=[EntitiesRecognitionTask()]
        )

        result = poller.result()
        action_results = [action_result for action_result in list(result) if not action_result.is_error]

        entities_recognition_task_result = action_results[0]
        print("Results of Entities Recognition action:")
        docs = [doc for doc in first_action_result.document_results if not doc.is_error]

        for idx, doc in enumerate(docs):
            print("\nDocument text: {}".format(documents[idx]))
            for entity in doc.entities:
                print("Entity: {}".format(entity.text))
                print("...Category: {}".format(entity.category))
                print("...Confidence Score: {}".format(entity.confidence_score))
                print("...Offset: {}".format(entity.offset))
            print("------------------------------------------")

analyze_example(client)
```

### <a name="output"></a>Sortie

```console
Results of Entities Recognition task:
Document text: Microsoft was founded by Bill Gates and Paul Allen.
Entity: Microsoft
...Category: Organization
...Confidence Score: 0.83
...Offset: 0
Entity: Bill Gates
...Category: Person
...Confidence Score: 0.85
...Offset: 25
Entity: Paul Allen
...Category: Person
...Confidence Score: 0.9
...Offset: 40
------------------------------------------
```

Vous pouvez également utiliser l’opération d’analyse par lots pour détecter les informations d’identification personnelle et exécuter une extraction de phrases clés. Consultez l’[exemple d’analyse par lots](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/textanalytics/azure-ai-textanalytics/samples/sample_analyze_batch_actions.py) sur GitHub.

# <a name="version-30"></a>[Version 3.0](#tab/version-3)

Cette fonctionnalité n’est pas disponible dans la version 3.0.

---
