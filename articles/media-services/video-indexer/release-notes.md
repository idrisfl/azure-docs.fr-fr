---
title: Notes de publication d’Azure Media Services Video Indexer | Microsoft Docs
description: Pour vous informer des développements les plus récents, cet article détaille les toutes dernières mises à jour concernant Azure Media Services Video Indexer.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.subservice: video-indexer
ms.workload: na
ms.topic: article
ms.custom: references_regions
ms.date: 03/30/2021
ms.author: juliako
ms.openlocfilehash: b3602d421718cbd1de3509751491ec6db65b1b01
ms.sourcegitcommit: 49b2069d9bcee4ee7dd77b9f1791588fe2a23937
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/16/2021
ms.locfileid: "107532904"
---
# <a name="azure-media-services-video-indexer-release-notes"></a>Notes de publication d’Azure Media Services Video Indexer

>Soyez notifié de la disponibilité des mises à jour sur cette page en faisant un copier-coller de cette URL : `https://docs.microsoft.com/api/search/rss?search=%22Azure+Media+Services+Video+Indexer+release+notes%22&locale=en-us` dans votre lecteur de flux RSS.

Pour vous informer des développements les plus récents, cet article détaille les thèmes suivants :

* Versions les plus récentes
* Problèmes connus
* Résolution des bogues
* Fonctionnalités dépréciées

## <a name="march-2021"></a>Mars 2021

### <a name="audio-analysis"></a>Analyse audio 

L’analyse audio est désormais disponible dans un nouveau pack supplémentaire de fonctionnalités audio à différents prix. Le nouveau préréglage d’analyse **Audio de base** est une option économique qui permet uniquement d’extraire les transcriptions de discours, les traductions et de mettre en forme des légendes et des sous-titres de sortie. Le préréglage **Audio de base** produira deux compteurs distincts sur votre facture, y compris une ligne de transcription et une ligne séparée pour la mise en forme des légendes et des sous-titres. Pour plus d’informations sur les tarifs, consultez la page [Tarifs d’Azure Media Services](https://azure.microsoft.com/pricing/details/media-services/).

Le pack nouvellement ajouté est disponible lors de l’indexation ou de la réindexation de votre fichier en choisissant le préréglage **Option avancée** -> **Audio de base** (sous la zone de liste déroulante **Vidéo + indexation audio**).

### <a name="new-developer-portal"></a>Nouvelle version du Developer Portal 

Video Indexer dispose d’une nouvelle version du [Developer Portal](https://api-portal.videoindexer.ai/). Essayez les nouvelles API Video Indexer et trouvez toutes les ressources pertinentes au même endroit : [dépôt GitHub](https://github.com/Azure-Samples/media-services-video-indexer), [Stack Overflow](https://stackoverflow.com/questions/tagged/video-indexer), [Communauté technique de Video Indexer](https://techcommunity.microsoft.com/t5/azure-media-services/bg-p/AzureMediaServices/label-name/Video%20Indexer) avec les billets de blog associés, [Questions fréquentes (FAQ) sur Video Indexer](faq.md), [User Voice](https://feedback.azure.com/forums/932041-cognitive-services?category_id=399016) pour envoyer vos commentaires et suggérer des fonctionnalités, et [lien « CodePen »](https://codepen.io/videoindexer) accompagné d’exemples de code de widgets. 
 
### <a name="advanced-customization-capabilities-for-insight-widget"></a>Fonctionnalités avancées de personnalisation pour le widget d’insight 

Le kit SDK est désormais disponible pour incorporer le widget d’insights de Video Indexer dans votre propre service ainsi que pour personnaliser son style et ses données. Le kit SDK prend en charge le widget d’insights Video Indexer standard et un widget d’insights entièrement personnalisable. Un exemple de code est disponible dans le [dépôt GitHub de Video Indexer](https://github.com/Azure-Samples/media-services-video-indexer/tree/master/Embedding%20widgets/widget-customization). Grâce à ces fonctionnalités de personnalisation avancées, le développeur de solutions peut appliquer un style personnalisé, utiliser les propres données d’IA du client et les présenter dans le widget d’insight (avec ou sans insights Video Indexer). 

### <a name="video-indexer-deployed-in-the-us-north-central--us-west-and-canada-central"></a>Déploiement de Video Indexer dans les régions USA Centre Nord, USA Ouest et Canada Centre 

Vous pouvez désormais créer un compte payant Video Indexer dans les régions USA Centre Nord, USA Ouest et Canada Centre
 
### <a name="new-source-languages-support-for-speech-to-text-stt-translation-and-search"></a>Prise en charge de nouvelles langues sources pour la conversion de parole en texte, la traduction et la recherche 

Video Indexer prend désormais en charge la conversion de parole en texte, la traduction et la recherche en danois (« da-DK »), norvégien (« nb-NO »), suédois (« sv-SE »), finnois (« fi-FI »), français canadien (« fr-CA »), thaïlandais (« th-TH »), arabe (« ar-BH », « ar-EG », « ar-IQ », « ar-JO », « ar-KW », « ar-LB », « ar-OM », « ar-QA », « ar-S » et « ar-SY ») et turc (« tr-TR »). Ces langues sont disponibles dans l’API et sur le site web Video Indexer. 
 
### <a name="search-by-topic-in-video-indexer-website"></a>Rechercher par sujet sur le site web Video Indexer 

Vous pouvez désormais utiliser la fonctionnalité de recherche, en haut de la page du [site web Video Indexer](https://www.videoindexer.ai/account/login), pour rechercher des vidéos sur des sujets spécifiques. 

## <a name="february-2021"></a>Février 2021

### <a name="multiple-account-owners"></a>Plusieurs propriétaires du compte 

Le rôle Propriétaire du compte a été ajouté à Video Indexer. Vous pouvez ajouter, modifier et supprimer des utilisateurs ainsi que modifier leur rôle. Pour plus d’informations sur le partage d’un compte, consultez [Inviter des utilisateurs](invite-users.md).

### <a name="audio-event-detection-public-preview"></a>Détection d’événements audio (préversion publique)

> [!NOTE]
> Cette fonctionnalité n’est disponible que pour les comptes en version d’essai. 

Video Indexer détecte maintenant les effets audio suivants dans les segments non vocaux du contenu : coup de feu, éclat de verre, alarme, sirène, explosion, aboiement, hurlement, rire, réactions de foule (encouragements, applaudissements et huées) et silence. 

La fonctionnalité des effets audio récemment ajoutée est disponible lors de l’indexation de votre fichier en choisissant le prégéglage **Option avancée** -> **Audio avancé** (sous l’indexation Vidéo + audio). L’indexation Standard inclut uniquement le **silence** et les **réactions de foule**. 

Le type d’événement **applaudissements** qui a été inclus dans le modèle d’effets audio précédent, est maintenant extrait une partie du type d’événement **réactions de foule**.

Lorsque vous choisissez d’afficher des **Insights** sur votre vidéo sur le site web [Video Indexer](https://www.videoindexer.ai/), les effets audio s’affichent sur la page.

:::image type="content" source="./media/release-notes/audio-detection.png" alt-text="Détection des événements audio":::

### <a name="named-entities-enhancement"></a>Amélioration des entités nommées  

La liste extraite des personnes et de l’emplacement a été étendue et mise à jour. 

De plus, le modèle comprend désormais des personnes et des emplacements dans le contexte qui ne sont pas célèbres, comme un « Sam » ou une « maison » dans la vidéo. 

## <a name="january-2021"></a>Janvier 2021

### <a name="video-indexer-is-deployed-on-us-government-cloud"></a>Video Indexer est déployé sur le cloud US Government 

Vous pouvez maintenant créer un compte Video Indexer payant sur le cloud US Government dans les régions Virginie et Arizona. L’offre d’essai gratuit de Video Indexer n’est pas disponible dans la région mentionnée. Pour plus d’informations, accédez à la documentation de Video Indexer. 

### <a name="video-indexer-deployed-in-the-india-central-region"></a>Video Indexer déployé dans la région Inde Centre 

Vous pouvez maintenant créer un compte Video Indexer payant dans la région Inde Centre. 

### <a name="new-dark-mode-for-the-video-indexer-website-experience"></a>Nouveau mode sombre pour l’expérience du site web de Video Indexer

L’expérience du site web de Video Indexer est désormais disponible en mode sombre. Pour activer le mode sombre, ouvrez le panneau Paramètres et activez l’option **Mode sombre**. 

:::image type="content" source="./media/release-notes/dark-mode.png" alt-text="Paramètre du mode sombre":::

## <a name="december-2020"></a>Décembre 2020

### <a name="video-indexer-deployed-in-the-switzerland-west-and-switzerland-north"></a>Video Indexer déployé dans les régions Suisse Ouest et Suisse Nord

Vous pouvez maintenant créer un compte Video Indexer payant dans les régions Suisse Ouest et Suisse Nord.

## <a name="october-2020"></a>Octobre 2020

### <a name="animated-character-identification-improvements"></a>Améliorations de l’identification des caractères animés  

Video Indexer prend en charge la détection, le regroupement et la reconnaissance de personnages dans le contenu animé via l’intégration à Cognitive Services Custom Vision. Nous avons ajouté à cet algorithme IA une amélioration majeure au niveau de la détection et de la reconnaissance des caractères ; la précision des insights et les caractères identifiés s’en trouvent ainsi considérablement enrichis.

### <a name="planned-video-indexer-website-authenticatication-changes"></a>Changements planifiés relatifs à l’authentification sur le site web Video Indexer

À partir du 1er mars 2021, vous ne pourrez plus vous inscrire ni vous connecter au [portail des développeurs](video-indexer-use-apis.md) du [site web de Video Indexer](https://www.videoindexer.ai/) par l’intermédiaire de Facebook ou de LinkedIn.

Votre inscription et votre connexion s’effectueront au moyen de l’un de ces fournisseurs : Azure AD, Microsoft et Google.

> [!NOTE]
> Les comptes Video Indexer connectés à LinkedIn et Facebook ne seront plus accessibles après le 1er mars 2021. 
> 
> Vous devez [inviter](invite-users.md) une adresse e-mail Azure AD, Microsoft ou Google dont vous êtes propriétaire au compte Video Indexer afin d’y avoir toujours accès. Vous pouvez ajouter un propriétaire supplémentaire des fournisseurs pris en charge, comme décrit dans [inviter](invite-users.md). <br/>
> Vous pouvez également créer un compte payant et migrer les données.

## <a name="august-2020"></a>Août 2020

### <a name="mobile-design-for-the-video-indexer-website"></a>Conception mobile pour le site web Video Indexer

L’expérience du site web Video Indexer prend désormais en charge les appareils mobiles. L’expérience utilisateur s’adapte à la taille de votre écran mobile (à l’exception des interfaces utilisateur de personnalisation). 

### <a name="accessibility-improvements-and-bug-fixes"></a>Améliorations de l’accessibilité et résolution des bogues 

Dans le cadre des directives WCAG (Web Content Accessibility Guidelines), l’expérience du site web Video Indexer est alignée avec la classe C, conformément aux normes d’accessibilité de Microsoft. Plusieurs bogues et améliorations liés à la navigation au clavier, à l’accès par programme et au lecteur d’écran ont été résolus. 

## <a name="july-2020"></a>Juillet 2020

### <a name="ga-for-multi-language-identification"></a>Disponibilité générale pour l’identification multilingue

L’identification multilingue passe du mode Préversion au mode Disponibilité générale et est prête pour une utilisation en production.

Ce passage du mode Préversion au mode Disponibilité générale n'a aucun impact sur les prix.

### <a name="video-indexer-website-improvements"></a>Améliorations du site web Video Indexer

#### <a name="adjustments-in-the-video-gallery"></a>Réglages dans la galerie de vidéos

Une nouvelle barre de recherche pour la recherche d’insights avec des fonctionnalités de filtrage supplémentaires a été ajoutée. Les résultats de la recherche ont également été améliorés.

Nouvelle vue liste avec possibilité de trier et de gérer des archives vidéo avec plusieurs fichiers.

#### <a name="new-panel-for-easy-selection-and-configuration"></a>Nouveau panneau pour faciliter la sélection et la configuration

Un panneau latéral pour faciliter la sélection et la configuration utilisateur a été ajouté, ce qui permet de créer et de partager un compte, et de définir la configuration, simplement et rapidement.

Le panneau latéral est également utilisé pour les préférences utilisateur et l’aide.

## <a name="june-2020"></a>Juin 2020

### <a name="search-by-topics"></a>Rechercher par sujets

Vous pouvez maintenant utiliser l'API de recherche pour rechercher des vidéos traitant de sujets spécifiques (API uniquement).

Les sujets sont ajoutés dans le cadre du `textScope` (paramètre facultatif). Pour plus d'informations, consultez [API](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Search-Videos).  

### <a name="labels-enhancement"></a>Amélioration des étiquettes

Le créateur d'étiquettes a été mis à niveau et comporte désormais davantage d'étiquettes visuelles identifiables.

## <a name="may-2020"></a>Mai 2020

### <a name="video-indexer-deployed-in-the-east-us"></a>Video Indexer déployé dans la région USA Est

Vous pouvez maintenant créer un compte Video Indexer payant dans la région USA Est.
 
### <a name="video-indexer-url"></a>URL de Video Indexer

Les points de terminaison régionaux de Video Indexer ont tous été unifiés pour démarrer uniquement avec www. Aucun élément d’action n’est requis.

À partir de maintenant, vous atteignez www.videoindexer.ai, qu’il s’agisse d’incorporer des widgets ou de se connecter à des applications web Video Indexer.

En outre, wus.videoindexer.ai est redirigé vers www. Pour plus d’informations, consultez [Incorporer des widgets Video Indexer dans vos applications](video-indexer-embed-widgets.md).

## <a name="april-2020"></a>Avril 2020

### <a name="new-widget-parameters-capabilities"></a>Nouvelles capacités de paramètres pour les widgets

Le widget **Insights** comprend de nouveaux paramètres : `language` et `control`.

Le widget **Lecteur** a un nouveau paramètre `locale`. Les paramètres `locale` et `language` contrôlent la langue d’affichage du lecteur.

Pour plus d’informations, consultez la section [Types de widgets](video-indexer-embed-widgets.md#widget-types). 

### <a name="new-player-skin"></a>Nouvelle apparence de lecteur

Une nouvelle apparence de lecteur a été lancée avec une conception mise à jour.

### <a name="prepare-for-upcoming-changes"></a>Préparer les modifications à venir

* Aujourd’hui, les API suivantes retournent un objet de compte :

    * [Create-Paid-Account](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Paid-Account)
    * [Get-Account](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Account)
    * [Get-Accounts-Authorization](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Accounts-Authorization)
    * [Get-Accounts-With-Token](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Accounts-With-Token)
 
    L’objet Compte contient un champ `Url` pointant vers l’emplacement du [site web de Video Indexer](https://www.videoindexer.ai/).
Pour les comptes payants, le champ `Url` pointe actuellement vers une URL interne au lieu du site web public.
Dans les semaines à venir, nous changerons cela et renverrons l’URL du [site web de Video Indexer](https://www.videoindexer.ai/) pour tous les comptes (version d’évaluation et payante).

    N’utilisez pas les URL internes, vous devez utiliser les [API publiques Video Indexer](https://api-portal.videoindexer.ai/).
* Si vous incorporez des URL Video Indexer dans vos applications et que celles-ci ne pointent pas vers le [site web de Video Indexer](https://www.videoindexer.ai/) ou le point de terminaison d’API Video indexer (`https://api.videoindexer.ai`), mais vers un point de terminaison régional (par exemple, `https://wus2.videoindexer.ai`), régénérez les URL.

   Pour ce faire, vous pouvez soit :

    * remplacer l’URL par une URL pointant vers les API du widget Video Indexer (par exemple, le [widget Insights](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Insights-Widget))
    * utiliser le site web de Video Indexer pour générer une nouvelle URL incorporée :
         
         Appuyez sur **Lire** pour accéder à la page de votre vidéo -> cliquez sur le bouton **&lt;/&gt;Incorporer** -> copiez l’URL dans votre application :
   
    Les URL régionales ne sont pas prises en charge et seront bloquées dans les semaines à venir.

## <a name="january-2020"></a>Janvier 2020
 
### <a name="custom-language-support-for-additional-languages"></a>Prise en charge linguistique personnalisée pour d’autres langues

Video Indexer prend désormais en charge des modèles de langage personnalisés pour les langues `ar-SY`, `en-UK` et `en-AU` (API uniquement).
 
### <a name="delete-account-timeframe-action-update"></a>Mise à jour de la plage de temps de l’action de suppression de compte

L’action de suppression de compte supprime désormais le compte dans les 90 jours au lieu des 48 heures.
 
### <a name="new-video-indexer-github-repository"></a>Nouveau dépôt GitHub pour Video Indexer

Un nouveau dépôt GitHub pour Video Indexer avec différents projets, des guides de prise en main et des exemples de code est désormais disponible : https://github.com/Azure-Samples/media-services-video-indexer
 
### <a name="swagger-update"></a>Mise à jour du fichier Swagger

**Authentications** et **opérations** de Video Indexer unifiées dans une seule [Spécification OpenAPI de Video Indexer (swagger)](https://api-portal.videoindexer.ai/api-details#api=Operations&operation). Les API sont accessibles aux développeurs sur le portail [Video Indexer Developer Portal](https://api-portal.videoindexer.ai/).

## <a name="december-2019"></a>Décembre 2019

### <a name="update-transcript-with-the-new-api"></a>Mettre à jour la transcription avec la nouvelle API

Mettez à jour une section spécifique dans la transcription à l’aide de l’API [Update-Video-index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Video-Index).

### <a name="fix-account-configuration-from-the-video-indexer-portal"></a>Corriger la configuration du compte à partir du portail Video Indexer

Vous pouvez maintenant mettre à jour la configuration de la connexion à Media Services pour favoriser la résolution autonome des problèmes tels que : 

* ressource Azure Media Services incorrecte
* modifications de mot de passe
* les ressources Media Services ont été déplacées dans un autre abonnement  

Pour corriger la configuration du compte, rendez-vous sur le portail Video Indexer et accédez à Paramètres > onglet Compte (en tant que propriétaire).

### <a name="configure-the-custom-vision-account"></a>Configurer le compte Custom Vision

Configurez le compte Custom Vision sur les comptes payants à l’aide du portail Video Indexer (auparavant pris en charge uniquement par l’API). Pour cela, connectez-vous au portail Video Indexer, choisissez Personnalisation du modèle > Personnages animés > Configurer. 

### <a name="scenes-shots-and-keyframes--now-in-one-insight-pane"></a>Scènes, plans et images clés, maintenant dans un seul volet d’informations

Les scènes, les plans et les images clés sont désormais fusionnés en un seul aperçu pour une consommation et une navigation plus faciles. Lorsque vous sélectionnez la scène souhaitée, vous pouvez voir les plans et les images clés qui la composent. 

### <a name="notification-about-a-long-video-name"></a>Notification concernant un nom de vidéo long

Lorsqu’un nom de vidéo contient plus de 80 caractères, Video Indexer affiche une erreur descriptive lors du chargement.

### <a name="streaming-endpoint-is-disabled-notification"></a>Notification de désactivation du point de terminaison de streaming

Lorsque le point de terminaison de streaming est désactivé, Video Indexer affiche une erreur descriptive sur la page du lecteur.

### <a name="error-handling-improvement"></a>Amélioration de la gestion des erreurs

Le code d’état 409 est désormais renvoyé à partir des API [Re-Index Video](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Re-Index-Video) (Réindexer une vidéo) et [Update Video Index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Video-Index) (Mettre à jour l’index d’une vidéo) en cas d’indexation active d’une vidéo, pour éviter de remplacer les modifications de réindexation en cours par accident.

## <a name="november-2019"></a>Novembre 2019
 
* Prise en charge des modèles de langage personnalisés en coréen

    Video Indexer prend désormais en charge les modèles de langage personnalisés coréens (`ko-KR`) à la fois dans l’API et le portail. 
* Nouvelles langues prises en charge pour la reconnaissance vocale (STT)

    Les API Video Indexer prennent désormais en charge STT en Arabe levantin (ar-SY), en dialecte anglais britannique (en-GB) et en dialecte anglais australien (en-AU).
    
    Pour le téléchargement de vidéos, nous avons remplacé zh-HANS par zh-CN. Les deux sont pris en charge, mais zh-CN est recommandé et plus précis.
    
## <a name="october-2019"></a>2 octobre 2019
 
* Rechercher des caractères animés dans la galerie

    Lorsque vous indexez des caractères animés, vous pouvez à présent les rechercher dans la galerie vidéo du compte. Pour plus d’informations, consultez [Reconnaissance de personnages animés](animated-characters-recognition.md).

## <a name="september-2019"></a>Septembre 2019
 
Plusieurs améliorations ont été annoncées au salon IBC 2019 :
 
* Reconnaissance de caractères animés (préversion publique)

    Possibilité de détecter, regrouper et reconnaître les caractères dans un contenu animé, par le biais de l’intégration à une vision personnalisée. Pour plus d’informations, consultez [Détection de personnages animés](animated-characters-recognition.md).
* Identification multilingue (préversion publique)

    Détectez les segments en plusieurs langues dans la piste audio et créez une transcription multilingue à partir de ces derniers. Prise en charge initiale : anglais, espagnol, allemand et français. Pour plus d’informations, consultez [Identifier et transcrire automatiquement un contenu multilingue](multi-language-identification-transcription.md).
* Extraction d’entité nommée pour les personnes et la localisation

    extrait des marques, des emplacements et des personnes à partir de la reconnaissance vocale et du texte visuel via le traitement en langage naturel (NLP).
* Classification des types de plans éditoriaux

    Étiquetage des plans avec des types éditoriaux tels que gros plan, plan moyen, deux plans, intérieur, extérieur, etc. Pour plus d’informations, consultez [Détection du type de plan éditorial](scenes-shots-keyframes.md#editorial-shot-type-detection).
* Amélioration de l’inférence de rubrique, avec à présent couverture du niveau 2
    
    Le modèle d’inférence de rubrique prend maintenant en charge la précision plus profonde de la taxonomie IPTC. Pour plus d’informations, consultez [Azure Media Services new AI-powered innovation](https://azure.microsoft.com/blog/azure-media-services-new-ai-powered-innovation/).

## <a name="august-2019"></a>Août 2019
 
### <a name="video-indexer-deployed-in-uk-south"></a>Déploiement de Video Indexer dans la région Royaume-Uni Sud

Vous pouvez maintenant créer un compte Video Indexer payant dans la région Royaume-Uni Sud.

### <a name="new-editorial-shot-type-insights-available"></a>Nouvelles informations éditoriales disponibles

De nouvelles balises ajoutées aux séquences vidéo fournissent des « types de prises de vue » éditoriales pour les identifier à l'aide de phrases éditoriales courantes utilisées dans le processus de création de contenu, par exemple : gros plan extrême, gros plan, large, moyen, deux plans, extérieur, intérieur, face gauche et face droite (disponible dans le fichier JSON).

### <a name="new-people-and-locations-entities-extraction-available"></a>Extraction de nouvelles entités Personnes et Lieux disponible

Video Indexer identifie les lieux et les personnes nommés via le traitement automatique du langage naturel (TALN) à partir de la reconnaissance optique de caractères et de la transcription de la vidéo. Video Indexer utilise un algorithme d'apprentissage automatique pour reconnaître le moment où certains lieux (par exemple, la Tour Eiffel) ou certaines personnes (par exemple, Monsieur Dupont) sont appelés dans une vidéo.

### <a name="keyframes-extraction-in-native-resolution"></a>Extraction d'images clés en résolution native

Les images clés extraites par Video Indexer sont disponibles dans la résolution d'origine de la vidéo.
 
### <a name="ga-for-training-custom-face-models-from-images"></a>Lancement du mode Disponibilité générale pour la formation de modèles de visage personnalisés à partir d'images

Passage du mode Préversion au mode Disponibilité générale pour la formation des visages à partir d'images (disponible via l'API et sur le portail).

> [!NOTE]
> Ce passage du mode Préversion au mode Disponibilité générale n'a aucun impact sur les prix.

### <a name="hide-gallery-toggle-option"></a>Option Masquer la galerie

L'utilisateur peut choisir de masquer l'onglet de la galerie sur le portail (comme pour l'onglet des exemples).
 
### <a name="maximum-url-size-increased"></a>Augmentation de la taille maximale des URL

Prise en charge de la chaîne de requête d'URL de 4096 (au lieu de 2048) pour l'indexation d'une vidéo.
 
### <a name="support-for-multi-lingual-projects"></a>Prise en charge des projets multilingues

Les projets peuvent maintenant être créés à partir de vidéos indexées dans différents langages (API uniquement).

## <a name="july-2019"></a>Juillet 2019

### <a name="editor-as-a-widget"></a>Éditeur en tant que widget

L’Éditeur IA Video Indexer est désormais disponible en tant que widget pour être incorporé dans les applications clientes.

### <a name="update-custom-language-model-from-closed-caption-file-from-the-portal"></a>Mise à jour du modèle de langage personnalisé à partir du fichier de sous-titres à partir du portail

Les clients peuvent fournir des fichiers aux formats VTT, SRT et TTML comme entrée pour les modèles de langage dans la page de personnalisation du portail.

## <a name="june-2019"></a>Juin 2019

### <a name="video-indexer-deployed-to-japan-east"></a>Video Indexer déployé dans la région Japon Est

Vous pouvez maintenant créer un compte payé Video Indexer dans la région Japon Est.

### <a name="create-and-repair-account-api-preview"></a>API de création et de réparation de compte (préversion)

Ajout d’une nouvelle API qui vous permet de [mettre à jour la clé ou le point de terminaison de connexion Azure Media Services](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Paid-Account-Azure-Media-Services).

### <a name="improve-error-handling-on-upload"></a>Amélioration de la gestion des erreurs lors du chargement 

Un message descriptif est retourné en cas de configuration incorrecte du compte Azure Media Services sous-jacent.

### <a name="player-timeline-keyframes-preview"></a>Affichage d’un aperçu des images clés dans la chronologie du lecteur 

Vous pouvez maintenant afficher un aperçu de l’image pour chaque instant sur la chronologie du lecteur.

### <a name="editor-semi-select"></a>Semi-sélection dans l’éditeur

Vous pouvez maintenant afficher un aperçu de tous les insights qui sont sélectionnés suite au choix d’une période d’insight spécifique dans l’éditeur.

## <a name="may-2019"></a>Mai 2019

### <a name="update-custom-language-model-from-closed-caption-file"></a>Mise à jour du modèle de langage personnalisé à partir du fichier de sous-titres

Les API de [création de modèle de langage personnalisé](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Language-Model) et de [mise à jour des modèles de langage personnalisés](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Language-Model) prennent désormais en charge les formats de fichier VTT, SRT et TTML comme entrée pour les modèles de langage.

Quand vous appelez l’[API Update Video Transcript](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Video-Transcript), la transcription est ajoutée automatiquement. Le modèle d’entraînement associé à la vidéo est également mis à jour automatiquement. Pour plus d’informations sur la façon de personnaliser et d’entraîner vos modèles de langage, consultez [Personnaliser un modèle de langage avec Video Indexer](customize-language-model-overview.md).

### <a name="new-download-transcript-formats--txt-and-csv"></a>Nouveaux formats de téléchargement de transcription – TXT et CSV

Outre le format de sous-titrage déjà pris en charge (SRT VTT et TTML), Video Indexer prend désormais en charge le téléchargement de la transcription aux formats TXT et CSV.

## <a name="next-steps"></a>Étapes suivantes

[Vue d'ensemble](video-indexer-overview.md)
