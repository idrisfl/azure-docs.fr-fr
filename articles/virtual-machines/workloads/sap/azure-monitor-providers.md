---
title: Fournisseurs Azure Monitor pour solutions SAP | Microsoft Docs
description: Cet article fournit des réponses aux questions fréquemment posées sur Azure Monitor pour fournisseurs de solutions SAP.
author: rdeltcheva
ms.service: virtual-machines-sap
ms.topic: article
ms.date: 06/30/2020
ms.author: radeltch
ms.openlocfilehash: 93e97f1f04aea2a31b62b2014a88a5aaa998ed2d
ms.sourcegitcommit: 2654d8d7490720a05e5304bc9a7c2b41eb4ae007
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107376084"
---
# <a name="azure-monitor-for-sap-solutions-providers-preview"></a>Fournisseurs Azure Monitor pour solutions SAP (préversion)

## <a name="overview"></a>Vue d’ensemble  

Dans le contexte de Azure Monitor pour solutions SAP, un *type fournisseur*  fait référence à un *fournisseur* spécifique. Par exemple *SAP HANA*, qui est configuré pour un composant spécifique au sein du paysage SAP, comme la base de données SAP HANA. Un fournisseur contient les informations de connexion pour le composant correspondant et permet de collecter des données de télémétrie à partir de ce composant. Une ressource Azure Monitor pour solutions SAP (également appelée ressource du moniteur SAP) peut être configurée avec plusieurs fournisseurs du même type fournisseur ou plusieurs fournisseurs de plusieurs types fournisseur.
   
Les clients peuvent choisir de configurer différents types fournisseur pour activer la collecte des données à partir du composant correspondant dans leur paysage SAP. Par exemple, les clients peuvent configurer un fournisseur pour le type fournisseur SAP HANA, un autre fournisseur pour le type fournisseur de cluster haute disponibilité, etc.  

Les clients peuvent également choisir de configurer plusieurs fournisseurs d’un type fournisseur spécifique pour réutiliser la même ressource du moniteur SAP et le groupe géré associé. Apprenez-en davantage sur le groupe de ressources managé. Pour la préversion publique, les types fournisseur suivants sont pris en charge :   
- SAP HANA
- Cluster haute disponibilité
- Microsoft SQL Server
- SAP NetWeaver

![Fournisseurs Azure Monitor pour solutions SAP](./media/azure-monitor-sap/azure-monitor-providers.png)

Il est recommandé aux clients de configurer au moins un fournisseur à partir des types fournisseur disponibles au moment du déploiement de la ressource du moniteur SAP. En configurant un fournisseur, les clients lancent la collecte de données à partir du composant correspondant pour lequel le fournisseur est configuré.   

Si les clients ne configurent aucun fournisseur au moment du déploiement de la ressource du moniteur SAP, bien que la ressource du moniteur SAP soit déployée avec succès, aucune donnée de télémétrie n’est collectée. Les clients ont la possibilité d’ajouter des fournisseurs après le déploiement via la ressource du moniteur SAP au sein de Portail Azure. Les clients peuvent ajouter ou supprimer des fournisseurs de la ressource du moniteur SAP à tout moment.

> [!Tip]
> Si vous souhaitez que Microsoft implémente un fournisseur spécifique, laissez vos commentaires via le lien à la fin de ce document ou contactez votre équipe de compte.  

## <a name="provider-type-sap-hana"></a>Type fournisseur SAP HANA

Les clients peuvent configurer un ou plusieurs fournisseurs de type fournisseur *SAP HANA* pour activer la collecte des données à partir de la base de données SAP HANA. Le fournisseur SAP HANA se connecte à la base de données SAP HANA sur le port SQL, extrait les données de télémétrie de la base de données et les envoie (push) à l’espace de travail Log Analytics de l’abonnement client. Le fournisseur SAP HANA collecte des données toutes les minutes depuis la base de données SAP HANA.  

En préversion publique, les clients peuvent s’attendre à voir les données suivantes avec le fournisseur SAP HANA : Utilisation de l’infrastructure sous-jacente, état de l’hôte SAP HANA, réplication du système SAP HANA et données de télémétrie de Sauvegarde Microsoft Azure SAP HANA. Pour configurer le fournisseur SAP HANA, l’adresse IP de l’hôte, le numéro de port SQL HANA et le nom d’utilisateur et le mot de passe SYSTEMDB sont requis. Il est recommandé aux clients de configurer le fournisseur SAP HANA par rapport à SYSTEMDB. Toutefois, d’autres fournisseurs peuvent être configurés pour d’autres locataires de base de données.

![Fournisseurs Azure Monitor pour solutions SAP : SAP HANA](./media/azure-monitor-sap/azure-monitor-providers-hana.png)

## <a name="provider-type-high-availability-cluster"></a>Type fournisseur de cluster haute disponibilité
Les clients peuvent configurer un ou plusieurs fournisseurs de type fournisseur de *cluster haute disponibilité* pour activer la collecte de données à partir du cluster Pacemaker dans le paysage SAP. Le fournisseur de cluster haute disponibilité se connecte à Pacemaker, à l’aide du point de terminaison [ha_cluster_exporter](https://github.com/ClusterLabs/ha_cluster_exporter), extrait les données de télémétrie de la base de données et les envoie (push) à l’espace de travail Log Analytics de l’abonnement client. Le fournisseur de cluster haute disponibilité collecte les données toutes les 60 secondes depuis Pacemaker.  

En préversion publique, les clients peuvent s’attendre à voir les données suivantes avec le fournisseur de cluster :   
 - État du cluster représenté sous la forme d’un regroupement du nœud et de l’état de la ressource 
 - [autres](https://github.com/ClusterLabs/ha_cluster_exporter/blob/master/doc/metrics.md) 

![Fournisseurs Azure Monitor pour solutions SAP : cluster haute disponibilité](./media/azure-monitor-sap/azure-monitor-providers-pacemaker-cluster.png)

Pour configurer un fournisseur de cluster haute disponibilité, deux étapes principales sont nécessaires :

1. Installer [ha_cluster_exporter](https://github.com/ClusterLabs/ha_cluster_exporter) dans *chaque* nœud dans le cluster Pacemaker.

   Vous avez deux options pour installer ha_cluster_exporter :
   
   - Utilisez des scripts Azure Automation pour déployer un cluster haute disponibilité. Les scripts installent [ha_cluster_exporter](https://github.com/ClusterLabs/ha_cluster_exporter) sur chaque nœud de cluster.  
   - Effectuez une [installation manuelle](https://github.com/ClusterLabs/ha_cluster_exporter#manual-clone--build). 

2. Configurez un fournisseur de cluster haute disponibilité dans *chaque* nœud dans le cluster Pacemaker.

   Pour configurer le fournisseur de cluster haute disponibilité, vous devez fournir les informations suivantes :
   
   - **Nom**. Nom de ce fournisseur. Il doit être unique pour cette instance de solutions Azure Monitor pour SAP.
   - **Point de terminaison Prometheus**. http\://\<servername or ip address\>:9664/metrics.
   - **SID**. Pour les systèmes SAP, utilisez le SID SAP. Pour les autres systèmes (par exemple, les clusters NFS), utilisez un nom à trois caractères pour le cluster. Le SID doit être différent des autres clusters qui sont surveillés.   
   - **Nom du cluster**. Nom du rôle utilisé lors de la création du cluster. Le nom du cluster se trouve dans la propriété du cluster `cluster-name`.
   - **Hostname**. Nom d'hôte Linux de la machine virtuelle.  


## <a name="provider-type-os-linux"></a>Système d’exploitation de type fournisseur (Linux)
Les clients peuvent configurer un ou plusieurs fournisseurs de système d’exploitation de type fournisseur (Linux) pour activer la collecte de données à partir de BareMetal ou de VM Nodes. Le fournisseur de système d’exploitation (Linux) se connecte à BareMetal ou à VM Nodes, à l’aide du point de terminaison [Node_Exporter](https://github.com/prometheus/node_exporter) , tire (pull) les données de télémétrie de Nodes et les envoie (push) à l’espace de travail Log Analytics de l’abonnement client. Le fournisseur de système d’exploitation (Linux) collecte auprès de Nodes des données toutes les 60 secondes pour la plupart des métriques. 

En préversion publique, les clients peuvent s’attendre à voir les données suivantes avec le fournisseur de système d’exploitation (Linux) : 
   - Utilisation du processeur, Utilisation du processeur par processus 
   - Utilisation du disque, Lecture et écriture d’E/S 
   - Distribution de la mémoire, Utilisation de la mémoire, Utilisation de la mémoire d’échange 
   - Utilisation du réseau, Informations sur le trafic réseau entrant et sortant 

La configuration d’un fournisseur de système d’exploitation (Linux) passe par deux étapes principales :
1. Installez [Node_Exporter](https://github.com/prometheus/node_exporter) sur chaque instance BareMetal ou VM Nodes.
   Il existe deux options pour l’installation de [Node_Exporter](https://github.com/prometheus/node_exporter) : 
      - Pour une installation Automation avec Ansible, utilisez [Node_Exporter](https://github.com/prometheus/node_exporter) sur chaque instance BareMetal ou VM Nodes pour installer le fournisseur de système d’exploitation (Linux).  
      - Effectuez une [installation manuelle](https://prometheus.io/docs/guides/node-exporter/).

2. Configurez un fournisseur de système d’exploitation (Linux) pour chaque instance BareMetal ou VM Nodes dans votre environnement. 
   Les informations suivantes sont nécessaires pour configurer le fournisseur de système d’exploitation (Linux) : 
      - Nom. Nom de ce fournisseur. Il doit être unique pour cette instance de solutions Azure Monitor pour SAP. 
      - Point de terminaison Node_Exporter, généralement http://<servername or ip address>:9100/metrics 

> [!NOTE]
> 9100 est un port exposé au point de terminaison Node_Exporter.

> [!Warning]
> Vérifiez que Node_Exporter continue à s’exécuter après le redémarrage du nœud. 


## <a name="provider-type-microsoft-sql-server"></a>Type fournisseur Microsoft SQL Server

Les clients peuvent configurer un ou plusieurs fournisseurs de type fournisseur *Microsoft SQL Server* pour activer la collecte des données à partir de [SQL Server sur les machines virtuelles](https://azure.microsoft.com/services/virtual-machines/sql-server/). Le fournisseur SQL Server se connecte à Microsoft SQL Server sur le port SQL, extrait les données de télémétrie de la base de données et les envoie (push) à l’espace de travail Log Analytics de l’abonnement client. Le SQL Server doit être configuré pour l’authentification SQL et un compte de connexion SQL Server, avec la base de données SAP comme base de données par défaut du fournisseur, doit être créé. Le fournisseur SQL Server collecte des données entre toutes les 60 secondes à toutes les heures, à partir de SQL Server.  

En préversion publique, les clients peuvent s’attendre à voir les données suivantes avec le fournisseur SQL Server : utilisation de l’infrastructure sous-jacente, instructions SQL principales, table la plus grande, problèmes enregistrés dans les journaux d’erreurs SQL Server, processus bloquants, etc.  

L’ID du système SAP, l’adresse IP de l’hôte, le numéro de port SQL Server ainsi que le nom de connexion et le mot de passe SQL Server sont nécessaires pour configurer le fournisseur Microsoft SQL Server.

![Fournisseurs Azure Monitor pour solutions SAP : SQL](./media/azure-monitor-sap/azure-monitor-providers-sql.png)

## <a name="provider-type-sap-netweaver"></a>Type fournisseur SAP NetWeaver

Les clients peuvent configurer un ou plusieurs fournisseurs de type fournisseur SAP NetWeaver pour activer la collecte des données à partir de la couche SAP NetWeaver. Le fournisseur AMS NetWeaver utilise l’interface [SAPControl WebService](https://www.sap.com/documents/2016/09/0a40e60d-8b7c-0010-82c7-eda71af511fa.html) existante pour récupérer les informations de télémétrie appropriées.

Pour la version actuelle, voici les méthodes web SOAP prêtes à l’emploi standard appelées par AMS.
|méthode Web|    ABAP|   Java|   Mesures|
|--|--|--|--|
|GetSystemInstanceList| X|  X|  Disponibilité de l’instance, serveur de messages, passerelle, ICM, disponibilité ABAP|
|GetProcessList|    X|  X|  Si la liste d’instances est rouge, nous pouvons déterminer le processus à l’origine de ce serveur en rouge|
|GetQueueStatistic| X|  X|  Statistiques de file d’attente (DIA/BATCH/UPD)|
|ABAPGetWPTable|    X|   -| Utilisation du processus de travail|
|EnqGetStatistic|   X   |X  |Verrous|

En préversion publique, les clients peuvent s’attendre à voir les données suivantes avec le fournisseur SAP NetWeaver : 
- Disponibilité du système et des instances
- Utilisation du processus de travail
- Utilisation de la file d’attente
- Statistiques de verrous empilés.

![image](https://user-images.githubusercontent.com/75772258/114581825-a9f2eb00-9c9d-11eb-8e6f-79cee7c5093f.png)

## <a name="next-steps"></a>Étapes suivantes

- Créez votre première ressource Azure Monitor pour solutions SAP.
- Avez-vous des questions sur Azure Monitor pour solutions SAP ? Consultez la section [FAQ](./azure-monitor-faq.md)
