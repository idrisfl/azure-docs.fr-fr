---
title: 'Démarrage rapide : Connecter un cluster Kubernetes existant à Azure Arc'
description: Dans ce guide de démarrage rapide, découvrez comment connecter un cluster Kubernetes avec Azure Arc.
author: mgoedtel
ms.author: magoedte
ms.service: azure-arc
ms.topic: quickstart
ms.date: 03/03/2021
ms.custom: template-quickstart, references_regions, devx-track-azurecli
keywords: Kubernetes, Arc, Azure, cluster
ms.openlocfilehash: 21ec5000ed7ef9df1805fa6ec43e20efc0f82182
ms.sourcegitcommit: afb79a35e687a91270973990ff111ef90634f142
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107481240"
---
# <a name="quickstart-connect-an-existing-kubernetes-cluster-to-azure-arc"></a>Démarrage rapide : Connecter un cluster Kubernetes existant à Azure Arc 

Dans ce guide de démarrage rapide, nous allons tirer parti des avantages de Kubernetes avec Azure Arc pour connecter un cluster Kubernetes existant à Azure Arc. Pour un aperçu conceptuel de la connexion de clusters à Azure Arc, consultez l’[article sur l’architecture des agents Kubernetes avec Azure Arc](./conceptual-agent-architecture.md).

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment.md](../../../includes/azure-cli-prepare-your-environment.md)]

* Un cluster Kubernetes fonctionnel. Si vous n'en avez pas, vous pouvez créer un cluster en utilisant l'une des options suivantes :
    * [Kubernetes dans Docker (KIND)](https://kind.sigs.k8s.io/)
    * Créer un cluster Kubernetes à l’aide de Docker pour [Mac](https://docs.docker.com/docker-for-mac/#kubernetes) ou [Windows](https://docs.docker.com/docker-for-windows/#kubernetes)
    * Cluster Kubernetes automanagé utilisant l'[API Cluster](https://cluster-api.sigs.k8s.io/user/quick-start.html)

    >[!NOTE]
    > Le cluster doit disposer d'au moins un nœud de système d'exploitation et d'une architecture de type `linux/amd64`. Les clusters uniquement dotés de nœuds `linux/arm64` ne sont pas encore pris en charge.
    
* Fichier `kubeconfig` et contexte pointant vers votre cluster.
* Autorisations d'accès en « lecture » et en « écriture » sur le type de ressource Kubernetes avec Azure Arc (`Microsoft.Kubernetes/connectedClusters`).

* Installez la [dernière version de Helm 3](https://helm.sh/docs/intro/install).

- [Procédez à l'installation ou à la mise à niveau d'Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) vers la version >= 2.16.0
* Installez l'extension `connectedk8s` d'Azure CLI, version >= 1.0.0 :
  
  ```azurecli
  az extension add --name connectedk8s
  ```

>[!TIP]
> Si l'extension `connectedk8s` est déjà installée, mettez-la à jour vers la version la plus récente à l'aide de la commande suivante - `az extension update --name connectedk8s`


>[!NOTE]
>La liste des régions prises en charge par Kubernetes avec Azure Arc est disponible [ici](https://azure.microsoft.com/global-infrastructure/services/?products=azure-arc).

>[!NOTE]
> Si vous souhaitez utiliser des emplacements personnalisés sur le cluster, utilisez les régions USA Est ou Europe Ouest pour la connexion de votre cluster, car pour le moment les emplacements personnalisés sont uniquement disponibles dans ces régions. Les autres fonctionnalités Kubernetes avec Azure Arc sont disponibles dans toutes les régions répertoriées ci-dessus.

## <a name="meet-network-requirements"></a>Répondre à la configuration réseau nécessaire

>[!IMPORTANT]
>Les agents Azure Arc requièrent les protocoles/ports/URL sortantes suivants pour fonctionner :
>* TCP sur le port 443 : `https://:443`
>* TCP sur le port 9418 : `git://:9418`
  
| Point de terminaison (DNS) | Description |  
| ----------------- | ------------- |  
| `https://management.azure.com`                                                                                 | Requis pour que l’agent se connecte à Azure et inscrive le cluster.                                                        |  
| `https://<region>.dp.kubernetesconfiguration.azure.com` | Point de terminaison du plan de données permettant à l’agent d’envoyer (push) le statut et de récupérer (fetch) les informations de configuration.                                      |  
| `https://login.microsoftonline.com`                                                                            | Requis pour extraire et mettre à jour des jetons Azure Resource Manager.                                                                                    |  
| `https://mcr.microsoft.com`                                                                            | Requis pour extraire des images conteneurs pour les agents Azure Arc.                                                                  |  
| `https://eus.his.arc.azure.com`, `https://weu.his.arc.azure.com`, `https://wcus.his.arc.azure.com`, `https://scus.his.arc.azure.com`, `https://sea.his.arc.azure.com`, `https://uks.his.arc.azure.com`, `https://wus2.his.arc.azure.com`, `https://ae.his.arc.azure.com`, `https://eus2.his.arc.azure.com`, `https://ne.his.arc.azure.com` |  Indispensable à l’extraction des certificats attribués par le système dans le cadre des identités managées pour les ressources Azure.                                                                  |

## <a name="register-the-two-providers-for-azure-arc-enabled-kubernetes"></a>Inscription des deux fournisseurs pour Kubernetes avec Azure Arc

1. Entrez les commandes suivantes :
    ```azurecli
    az provider register --namespace Microsoft.Kubernetes
    az provider register --namespace Microsoft.KubernetesConfiguration
    az provider register --namespace Microsoft.ExtendedLocation
    ```
2. Supervisez le processus d’inscription. L’inscription peut prendre jusqu’à 10 minutes.
    ```azurecli
    az provider show -n Microsoft.Kubernetes -o table
    az provider show -n Microsoft.KubernetesConfiguration -o table
    az provider show -n Microsoft.ExtendedLocation -o table
    ```

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créez un groupe de ressources :  

```console
az group create --name AzureArcTest -l EastUS -o table
```

```output
Location    Name
----------  ------------
eastus      AzureArcTest
```

## <a name="connect-an-existing-kubernetes-cluster"></a>Connecter un cluster Kubernetes existant

1. Connectez votre cluster Kubernetes à Azure Arc à l’aide de la commande suivante :
    ```console
    az connectedk8s connect --name AzureArcTest1 --resource-group AzureArcTest
    ```

    ```output
    Helm release deployment succeeded

    {
      "aadProfile": {
        "clientAppId": "",
        "serverAppId": "",
        "tenantId": ""
      },
      "agentPublicKeyCertificate": "xxxxxxxxxxxxxxxxxxx",
      "agentVersion": null,
      "connectivityStatus": "Connecting",
      "distribution": "gke",
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/AzureArcTest/providers/Microsoft.Kubernetes/connectedClusters/AzureArcTest1",
      "identity": {
        "principalId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "tenantId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "type": "SystemAssigned"
      },
      "infrastructure": "gcp",
      "kubernetesVersion": null,
      "lastConnectivityTime": null,
      "location": "eastus",
      "managedIdentityCertificateExpirationTime": null,
      "name": "AzureArcTest1",
      "offering": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "AzureArcTest",
      "tags": {},
      "totalCoreCount": null,
      "totalNodeCount": null,
      "type": "Microsoft.Kubernetes/connectedClusters"
    }
    ```

> [!TIP]
> La commande ci-dessus sans paramètre d’emplacement spécifié crée la ressource Kubernetes avec Azure Arc dans le même emplacement que le groupe de ressources. Pour créer la ressource Kubernetes avec Azure Arc dans un emplacement différent, spécifiez `--location <region>` ou `-l <region>` lors de l’exécution de la commande `az connectedk8s connect`.

## <a name="verify-cluster-connection"></a>Vérifier la connexion du cluster

Visualisez la liste de vos clusters connectés avec la commande suivante :  

```console
az connectedk8s list -g AzureArcTest -o table
```

```output
Name           Location    ResourceGroup
-------------  ----------  ---------------
AzureArcTest1  eastus      AzureArcTest
```

> [!NOTE]
> Après l’intégration du cluster, il faut environ 5 à 10 minutes pour que les métadonnées du cluster (version du cluster, version de l’agent, nombre de nœuds, etc.) soient visibles sur la page Vue d’ensemble de la ressource Kubernetes avec Azure Arc sur le Portail Azure.

## <a name="connect-using-an-outbound-proxy-server"></a>Se connecter à l’aide d’un serveur proxy sortant

Si votre cluster se trouve derrière un serveur proxy sortant, Azure CLI et les agents Kubernetes avec Azure Arc doivent router leurs requêtes via ce serveur proxy sortant. 


1. Définissez les variables d’environnement nécessaires pour Azure CLI afin d’utiliser le serveur proxy sortant :

    * Si vous utilisez bash, exécutez la commande suivante avec les valeurs appropriées :

        ```bash
        export HTTP_PROXY=<proxy-server-ip-address>:<port>
        export HTTPS_PROXY=<proxy-server-ip-address>:<port>
        export NO_PROXY=<cluster-apiserver-ip-address>:<port>
        ```

    * Si vous utilisez PowerShell, exécutez la commande suivante avec les valeurs appropriées :

        ```powershell
        $Env:HTTP_PROXY = "<proxy-server-ip-address>:<port>"
        $Env:HTTPS_PROXY = "<proxy-server-ip-address>:<port>"
        $Env:NO_PROXY = "<cluster-apiserver-ip-address>:<port>"
        ```

2. Exécutez la commande connect avec les paramètres de proxy spécifiés :

    ```console
    az connectedk8s connect -n <cluster-name> -g <resource-group> --proxy-https https://<proxy-server-ip-address>:<port> --proxy-http http://<proxy-server-ip-address>:<port> --proxy-skip-range <excludedIP>,<excludedCIDR> --proxy-cert <path-to-cert-file>
    ```

> [!NOTE]
> * Spécifiez `excludedCIDR` sous `--proxy-skip-range` pour vérifier si la communication des agents au sein du cluster n’est pas interrompue.
> * `--proxy-http`, `--proxy-https` et `--proxy-skip-range` sont attendus pour la plupart des environnements de serveurs proxy sortants. `--proxy-cert` est nécessaire *uniquement* si vous devez injecter les certificats approuvés attendus par le serveur proxy dans le magasin de certificats approuvés des pods d’agents.

## <a name="view-azure-arc-agents-for-kubernetes"></a>Voir les agents Azure Arc pour Kubernetes

Un Kubernetes à extension Azure Arc déploie quelques opérateurs dans l’espace de noms `azure-arc`. 

1. Visualisez ces déploiements et ces pods à l’aide de :

    ```console
    kubectl -n azure-arc get deployments,pods
    ```

1. Vérifiez que tous les pods sont à l’état `Running`.

    ```output
    NAME                                        READY      UP-TO-DATE  AVAILABLE  AGE
    deployment.apps/cluster-metadata-operator     1/1             1        1      16h
    deployment.apps/clusteridentityoperator       1/1             1        1      16h
    deployment.apps/config-agent                  1/1             1        1      16h
    deployment.apps/controller-manager            1/1             1        1      16h
    deployment.apps/flux-logs-agent               1/1             1        1      16h
    deployment.apps/metrics-agent                 1/1             1        1      16h
    deployment.apps/resource-sync-agent           1/1             1        1      16h

    NAME                                           READY    STATUS   RESTART AGE
    pod/cluster-metadata-operator-7fb54d9986-g785b  2/2     Running  0       16h
    pod/clusteridentityoperator-6d6678ffd4-tx8hr    3/3     Running  0       16h
    pod/config-agent-544c4669f9-4th92               3/3     Running  0       16h
    pod/controller-manager-fddf5c766-ftd96          3/3     Running  0       16h
    pod/flux-logs-agent-7c489f57f4-mwqqv            2/2     Running  0       16h
    pod/metrics-agent-58b765c8db-n5l7k              2/2     Running  0       16h
    pod/resource-sync-agent-5cf85976c7-522p5        3/3     Running  0       16h
    ```

## <a name="clean-up-resources"></a>Nettoyer les ressources

Vous pouvez supprimer la ressource Kubernetes avec Azure Arc, toutes les ressources de configuration associées *et* tous les agents s’exécutant sur le cluster à l’aide d’Azure CLI et de la commande suivante :

```azurecli
az connectedk8s delete --name AzureArcTest1 --resource-group AzureArcTest
```

>[!NOTE]
>La suppression de la ressource Kubernetes avec Azure Arc à l’aide du portail Azure entraîne la suppression de toutes les ressources de configuration associées mais *pas* des agents s’exécutant sur le cluster. Il est recommandé de suivre la bonne pratique qui consiste à supprimer la ressource Kubernetes avec Azure Arc via `az connectedk8s delete` au d’utiliser le portail Azure.

## <a name="next-steps"></a>Étapes suivantes

Passez à l’article suivant pour savoir comment déployer des configurations sur votre cluster Kubernetes connecté à l’aide de GitOps.
> [!div class="nextstepaction"]
> [Déployer des configurations à l’aide de GitOps](tutorial-use-gitops-connected-cluster.md)
