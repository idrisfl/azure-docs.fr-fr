---
title: Tutoriel pour configurer des paramètres réseau pour l’appareil Azure Stack Edge Pro R dans le portail Azure | Microsoft Docs
description: Le tutoriel pour déployer Azure Stack Edge Pro R vous explique comment configurer les paramètres du réseau, du réseau de calcul et du proxy web de votre appareil physique.
services: databox
author: alkohli
ms.service: databox
ms.subservice: edge
ms.topic: tutorial
ms.date: 02/04/2021
ms.author: alkohli
ms.openlocfilehash: a1f3966c8794b50f6ec369f1ea86905c4d8aaf3f
ms.sourcegitcommit: 73fb48074c4c91c3511d5bcdffd6e40854fb46e5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2021
ms.locfileid: "106059936"
---
# <a name="tutorial-configure-network-for-azure-stack-edge-pro-r"></a>Tutoriel : Configurer le réseau pour Azure Stack Edge Pro R

Ce tutoriel explique comment configurer le réseau pour votre appareil Azure Stack Edge Pro R en utilisant l’interface utilisateur web locale.

Le processus de connexion peut prendre environ 20 minutes.

Ce tutoriel vous fournira des informations sur :

> [!div class="checklist"]
>
> * Prérequis
> * Configurer le réseau
> * Activer le réseau de calcul
> * Configurer le proxy web


## <a name="prerequisites"></a>Prérequis

Avant de configurer et d’activer votre appareil Azure Stack Edge Pro R, vérifiez que :

* Vous avez installé l’appareil physique, comme indiqué dans [Installer Azure Stack Edge Pro R](azure-stack-edge-gpu-deploy-install.md).
* Vous vous êtes connecté à l’interface utilisateur web locale de l’appareil, comme indiqué dans [Se connecter à Azure Stack Edge Pro R](azure-stack-edge-gpu-deploy-connect.md).


## <a name="configure-network"></a>Configurer le réseau

La page **Bien démarrer** comprend les différents paramètres nécessaires à la configuration et à l’inscription de l’appareil physique auprès du service Azure Stack Edge. 

Procédez comme suit pour configurer le réseau de votre appareil.

1. Accédez à la page **Bien démarrer** de l’interface utilisateur web locale de votre appareil. 

2. Dans la vignette **Réseau**, sélectionnez **Configurer** pour accéder à la page **Réseau**. 
    
    <!--![Local web UI "Network settings" tile](./media/azure-stack-edge-gpu-deploy-configure-network-compute-web-proxy/network-1.png)-->

    Votre appareil physique comporte quatre interfaces réseau. Le PORT 1 et le PORT 2 sont des interfaces réseau de 1 Gbit/s. Le PORT 3 et le PORT 4 sont des interfaces réseau de 10/25 Gbits/s. Le PORT 1 est automatiquement configuré comme port réservé à la gestion, et les PORTS 2 à 4 sont tous des ports de données. La page **Réseau** est similaire à celle illustrée ci-dessous.
    
    ![Page « Paramètres réseau » de l’interface utilisateur web locale](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/network-2.png)

   
3. Pour modifier les paramètres réseau, sélectionnez un port et, dans le volet droit qui s’affiche, modifiez l’adresse IP, le sous-réseau, la passerelle, le DNS principal et le DNS secondaire. 

    - Si vous sélectionnez le Port 1, vous pouvez voir qu’il est préconfiguré comme statique. 

        ![Interface utilisateur web locale, « Paramètres réseau du Port 1 »](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/network-3.png)

    - Si vous sélectionnez le Port 2, 3 ou 4, tous ces ports sont configurés en tant que DHCP par défaut.

        ![Interface utilisateur web locale, « Paramètres réseau du Port 3 »](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/network-4.png)

    Lorsque vous configurez les paramètres réseau, gardez à l’esprit :

   * Si le protocole DHCP est activé dans votre environnement, les interfaces réseau sont configurées automatiquement. Une adresse IP, un sous-réseau, une passerelle et un DNS sont automatiquement attribués.
   * Si le protocole DHCP n’est pas activé, vous pouvez, le cas échéant, attribuer des adresses IP statiques.
   * Vous pouvez configurer votre interface réseau sur IPv4.
   * L’association de cartes d’interface réseau et l’agrégation de liens ne sont pas prises en charge avec Azure Stack Edge.
   * Le numéro de série d’un port correspond au numéro de série du nœud.
    <!--* On the 25-Gbps interfaces, you can set the RDMA (Remote Direct Access Memory) mode to iWarp or RoCE (RDMA over Converged Ethernet). Where low latencies are the primary requirement and scalability is not a concern, use RoCE. When latency is a key requirement, but ease-of-use and scalability are also high priorities, iWARP is the best candidate.-->
    Une fois le réseau de l’appareil configuré, la page est mise à jour comme indiqué ci-dessous.

    ![Page 2 « Paramètres réseau » de l’interface utilisateur web locale](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/network-2a.png)<!--change-->


     >[!NOTE]
     >
     > * Nous vous recommandons de ne pas remplacer Statique par DHCP pour l’adresse IP locale de l’interface réseau, sauf si vous disposez d’une autre adresse IP pour vous connecter à l’appareil. Si vous utilisez une seule interface réseau et que vous passez à DHCP, il n’y a aucun moyen de déterminer l’adresse DHCP. Si vous voulez passer à une adresse DHCP, attendez que l’appareil se soit activé auprès du service, puis faites la modification. Vous pouvez ensuite voir les adresses IP de tous les adaptateurs dans les **propriétés de l’appareil** dans le portail Azure pour votre service.


    Après avoir configuré et appliqué les paramètres réseau, sélectionnez **Suivant : Calcul** pour configurer le réseau de calcul.

## <a name="enable-compute-network"></a>Activer le réseau de calcul

Procédez comme suit pour activer le calcul et configurer le réseau de calcul. 

1. Dans la page **Calcul**, sélectionnez une interface réseau que vous souhaitez activer pour le calcul. 

    ![Page Calcul de l'interface utilisateur web locale 2](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/compute-network-2.png)

1. Dans la boîte de dialogue **Paramètres réseau**, sélectionnez **Activer**. Lorsque vous activez le calcul, un commutateur virtuel est créé sur votre appareil sur cette interface réseau. Le commutateur virtuel est utilisé pour l’infrastructure de calcul sur l’appareil. 
    
1. Affectez des **adresses IP aux nœuds Kubernetes**. Ces adresses IP statiques sont destinées à la machine virtuelle de calcul.  

    Pour un appareil à *n* nœuds, une plage contiguë d’au moins *n+1* adresses IPv4 (ou plus) est fournie pour la machine virtuelle de calcul en utilisant les adresses IP de début et de fin. Étant donné que Azure Stack Edge est un appareil à 1 nœud, un minimum de 2 adresses IPv4 contiguës sont fournies. Ces adresses IP doivent se trouver dans le même réseau que celui dans lequel vous avez activé le calcul et créé le commutateur virtuel.

    > [!IMPORTANT]
    > Kubernetes sur Azure Stack Edge utilise le sous-réseau 172.27.0.0/16 pour le pod, et le sous-réseau 172.28.0.0/16 pour le service. Vérifiez qu’ils ne sont pas actuellement utilisés sur votre réseau. Si ces sous-réseaux sont déjà utilisés sur votre réseau, vous pouvez modifier ces sous-réseaux en exécutant l’applet de commande `Set-HcsKubeClusterNetworkInfo` à partir de l’interface PowerShell de l’appareil. Pour plus d’informations, consultez [Modifier les sous-réseaux du pod et du service Kubernetes](azure-stack-edge-gpu-connect-powershell-interface.md#change-kubernetes-pod-and-service-subnets).


1. Affectez des **adresses IP des services externes Kubernetes**. Il s’agit également des adresses IP d’équilibrage de charge. Ces adresses IP contiguës sont destinées aux services que vous souhaitez exposer en dehors du cluster Kubernetes, et vous spécifiez la plage d’adresses IP statiques en fonction du nombre de services exposés. 
    
    > [!IMPORTANT]
    > Nous vous recommandons vivement de spécifier au moins 1 adresse IP pour le service Hub Azure Stack Edge Pro R afin d’avoir accès aux modules de calcul. Vous pouvez ensuite éventuellement spécifier des adresses IP supplémentaires pour d’autres services/modules IoT Edge (1 par service/module) qui doivent être accessibles à partir de l’extérieur du cluster. Les adresses IP du service peuvent être mises à jour ultérieurement. 
    
1. Sélectionnez **Appliquer**.

    ![Page Calcul dans l'interface utilisateur web locale 3](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/compute-network-3.png)

1. Quelques minutes sont nécessaires pour appliquer la configuration et une actualisation du navigateur peut être requise. Vous pouvez constater que le port spécifié est activé pour le calcul. 
 
    ![Page Calcul de l'interface utilisateur web locale 4](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/compute-network-4.png)

    Sélectionnez **Suivant : Proxy web** pour configurer le proxy web.  

  
## <a name="configure-web-proxy"></a>Configurer le proxy web

Cette configuration est facultative.

> [!IMPORTANT]
> * Si vous activez le calcul et utilisez le module IoT Edge sur votre appareil Azure Stack Edge Pro R, nous vous recommandons de définir l’authentification du proxy web sur **Aucune**. NTLM n’est pas pris en charge.
>* Les fichiers PAC ne sont pas pris en charge. Un fichier PAC définit la manière dont les navigateurs web et les autres agents utilisateurs peuvent choisir automatiquement le serveur proxy approprié (méthode d’accès) pour récupérer une URL donnée. Les proxys qui tentent d’intercepter et de lire tout le trafic (puis de tout resigner avec leur propre certification) ne sont pas compatibles, car le certificat du proxy n’est pas approuvé. En général, les proxys transparents fonctionnent bien avec Azure Stack Edge Pro R, alors que les proxys web non transparents ne sont pas pris en charge.


1. Dans la page **Paramètres du proxy web**, procédez comme suit :

    1. Dans la zone **URL de proxy Web**, entrez l’URL dans ce format : `http://host-IP address or FQDN:Port number`. Les URL HTTPS ne sont pas prises en charge.

    2. Sous **Authentification**, sélectionnez **Aucune** ou **NTLM**. Si vous activez le calcul et utilisez le module IoT Edge sur votre appareil Azure Stack Edge Pro R, nous vous recommandons de définir l’authentification du proxy web sur **Aucune**. **NTLM** n’est pas pris en charge.

    3. Si vous utilisez une authentification, entrez un nom d’utilisateur et un mot de passe.

    4. Cliquez sur **Appliquer** pour valider et appliquer les paramètres du proxy web que vous avez configurés.
    
   ![Page 2 « Paramètres du proxy web » de l’interface utilisateur web locale](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/web-proxy-2.png)

2. Une fois les paramètres appliqués, sélectionnez **Suivant : Appareil**.


## <a name="next-steps"></a>Étapes suivantes

Ce didacticiel vous à présenté les point suivants :

> [!div class="checklist"]
> * Prérequis
> * Configurer le réseau
> * Activer le réseau de calcul
> * Configurer le proxy web


Pour apprendre à configurer votre appareil Azure Stack Edge Pro R, consultez :

> [!div class="nextstepaction"]
> [Configurer les paramètres des appareils](./azure-stack-edge-pro-r-deploy-set-up-device-update-time.md)
