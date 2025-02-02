---
title: Créer un contrôleur de données dans Azure Data Studio
description: Créer un contrôleur de données dans Azure Data Studio
services: azure-arc
ms.service: azure-arc
ms.subservice: azure-arc-data
author: twright-msft
ms.author: twright
ms.reviewer: mikeray
ms.date: 12/09/2020
ms.topic: how-to
ms.openlocfilehash: f2d44cc769e9673eeb75828126f806d2b2308a17
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2021
ms.locfileid: "103573878"
---
# <a name="create-data-controller-in-azure-data-studio"></a>Créer un contrôleur de données dans Azure Data Studio

Vous pouvez créer un contrôleur de données en utilisant Azure Data Studio via l’Assistant Déploiement et des notebooks.

[!INCLUDE [azure-arc-data-preview](../../../includes/azure-arc-data-preview.md)]

## <a name="prerequisites"></a>Prérequis

- Vous devez avoir accès à un cluster Kubernetes et votre fichier kubeconfig doit être configuré pour pointer vers le cluster Kubernetes sur lequel vous voulez déployer.
- Vous devez [installer les outils clients](install-client-tools.md), notamment **Azure Data Studio** et les extensions Azure Data Studio appelées **Azure Arc** et **[!INCLUDE [azure-data-cli-azdata](../../../includes/azure-data-cli-azdata.md)]** .
- Vous devez vous connecter à Azure dans Azure Data Studio.  Pour cela, tapez Ctrl/Cmd+Maj+P pour ouvrir la fenêtre de texte de commande, puis tapez **Azure**.  Choisissez **Azure : Sign in**.   Dans le volet qui s’affiche, cliquez sur l’icône + en haut à droite pour ajouter un compte Azure.

## <a name="use-the-deployment-wizard-to-create-azure-arc-data-controller"></a>Utiliser l’Assistant Déploiement pour créer un contrôleur de données Azure Arc

Suivez ces étapes pour créer un contrôleur de données Azure Arc en utilisant l’Assistant Déploiement.

1. Dans Azure Data Studio, cliquez sur l’onglet Connexions dans le volet de navigation gauche.
2. Cliquez sur le bouton **...** en haut du panneau Connexions, puis choisissez **Nouveau déploiement...**
3. Dans le nouvel Assistant Déploiement, choisissez **Contrôleur de données Azure Arc** et cliquez sur le bouton **Sélectionner** situé en bas.
4. Vérifiez que les outils requis sont disponibles et satisfont aux versions requises. Cliquez sur **Suivant**.
5. Utilisez le fichier kubeconfig par défaut ou sélectionnez-en un autre.  Cliquez sur **Suivant**.
6. Choisissez un contexte de cluster Kubernetes. Cliquez sur **Suivant**.
7. Choisissez un profil de configuration de déploiement en fonction de votre cluster Kubernetes cible. Cliquez sur **Suivant**.
8. Si vous utilisez la plateforme de conteneur Azure Red Hat OpenShift ou Red Hat OpenShift, appliquez les contraintes de contexte de sécurité. Suivez les instructions de la rubrique [Appliquer une contrainte de contexte de sécurité pour les services de données avec Azure Arc sur OpenShift](how-to-apply-security-context-constraint.md).

   >[!IMPORTANT]
   >Sur la plateforme de conteneur Azure Red Hat OpenShift ou Red Hat OpenShift, vous devez appliquer la contrainte de contexte de sécurité avant de créer le contrôleur de données.

1. Choisissez l’abonnement et le groupe de ressources souhaités.
1. Sélectionnez un emplacement Azure.
   
   L’emplacement Azure sélectionné ici est l’emplacement dans Azure où les *métadonnées* sur le contrôleur de données et les instances de base de données qu’il gère seront stockées. Les instances de contrôleur de données et de base de données seront créées sur votre cluster Kubernetes, où qu’il soit.

10. Sélectionnez le mode de connectivité approprié. En savoir plus sur les [modes de connectivité](./connectivity.md). Cliquez sur **Suivant**.

    Si vous sélectionnez le mode de connectivité directe, les informations d’identification du principal de service sont requises, comme décrit dans [Créer un principal de service](upload-metrics-and-logs-to-azure-monitor.md#create-service-principal).

11. Entrez un nom pour le contrôleur de données et pour l’espace de noms dans lequel le contrôleur de données sera créé.

    Le nom du contrôleur de données et de l’espace de noms sont utilisés pour créer une ressource personnalisée dans le cluster Kubernetes : ils doivent donc être conformes aux [conventions de nommage de Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names).
    
    Si l’espace de noms existe déjà, il sera utilisé si l’espace de noms ne contient pas déjà d’autres objets Kubernetes, comme des pods, etc.  Si l’espace de noms n’existe pas, une tentative de création de l’espace de noms sera effectuée.  La création d’un espace de noms dans un cluster Kubernetes nécessite des privilèges d’administrateur du cluster Kubernetes.  Si vous ne disposez pas de privilèges d’administrateur du cluster Kubernetes, demandez à l’administrateur de votre cluster Kubernetes d’effectuer les premières étapes décrites dans l’article [Créer un contrôleur de données en utilisant des outils natifs Kubernetes](./create-data-controller-using-kubernetes-native-tools.md) qui doivent être exécutées par un administrateur Kubernetes avant que vous puissiez utiliser cet Assistant.


12. Sélectionnez la classe de stockage dans laquelle le contrôleur de données sera déployé. 
13.  Entrez un nom d’utilisateur et un mot de passe, puis confirmez le mot de passe pour le compte d’administrateur du contrôleur de données. Cliquez sur **Suivant**.

14. Examinez la configuration du déploiement.
15. Cliquez sur **Déployer** pour déployer la configuration souhaitée ou l’option **Script en bloc-notes** pour consulter les instructions de déploiement ou apporter les modifications nécessaires, comme les noms de classes de stockage ou les types de services. Cliquez sur **Exécuter tout** en haut du notebook.

## <a name="monitoring-the-creation-status"></a>Surveillance de l’état de la création

La création du contrôleur prend plusieurs minutes. Vous pouvez superviser la progression dans une autre fenêtre de terminal avec les commandes suivantes :

> [!NOTE]
>  Les exemples de commandes ci-dessous supposent que vous avez créé un contrôleur de données et un espace de noms Kubernetes avec le nom « arc ».  Si vous avez utilisé un autre nom pour le contrôleur de données/espace de noms, vous pouvez remplacer « arc » par ce nom.

```console
kubectl get datacontroller/arc --namespace arc
```

```console
kubectl get pods --namespace arc
```

Vous pouvez également vérifier l’état de la création de n’importe quel pod en exécutant une commande comme celle qui figure ci-dessous.  C’est particulièrement utile pour résoudre les problèmes.

```console
kubectl describe po/<pod name> --namespace arc

#Example:
#kubectl describe po/control-2g7bl --namespace arc
```

## <a name="troubleshooting-creation-problems"></a>Résolution des problèmes de création

Si vous rencontrez des problèmes avec la création, consultez le [Guide de résolution des problèmes](troubleshoot-guide.md).
