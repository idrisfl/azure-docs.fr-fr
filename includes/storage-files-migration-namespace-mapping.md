---
title: Fichier include
description: Fichier include
services: storage
author: fauhse
ms.service: storage
ms.topic: include
ms.date: 2/20/2020
ms.author: fauhse
ms.custom: include file
ms.openlocfilehash: a8dd83a9584d218d56c7350d6d634bfe4610b790
ms.sourcegitcommit: 3ee3045f6106175e59d1bd279130f4933456d5ff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2021
ms.locfileid: "106075567"
---
Dans cette étape, vous évaluez le nombre de partages de fichiers Azure dont vous avez besoin. Une seule instance Windows Server (ou cluster) peut synchroniser jusqu’à 30 partages de fichiers Azure.

Vous pouvez avoir plus de dossiers dans vos volumes que ce que vous partagez actuellement localement en tant que partages SMB pour vos utilisateurs et applications. La solution la plus simple pour décrire ce scénario consiste à envisager un mappage 1:1 entre un partage local et un partage de fichiers Azure. Si vous avez un nombre suffisamment petit, inférieur à 30 pour une instance Windows Server, un mappage de 1:1 est recommandé.

Si vous avez plus de 30 partages, il est souvent inutile d’avoir un mappage 1:1 entre un partage local et un partage de fichiers Azure. Tenez compte des options suivantes.

#### <a name="share-grouping"></a>Regroupement de partages

Par exemple, si votre service des ressources humaines (RH) a un total de 15 partages, vous pouvez envisager de stocker toutes les données RH dans un seul partage de fichiers Azure. Le stockage de plusieurs partages locaux dans un partage de fichiers Azure ne vous empêche pas de créer les 15 partages SMB habituels sur votre instance locale de Windows Server. Cela signifie simplement que vous organisez les dossiers racine de ces 15 partages en sous-dossiers sous un dossier commun. Vous synchronisez ensuite ce dossier commun avec un partage de fichiers Azure. Ainsi, un seul partage de fichiers Azure dans le cloud est nécessaire pour ce groupe de partages locaux.

#### <a name="volume-sync"></a>Synchronisation de volume

Azure File Sync prend en charge la synchronisation de la racine d’un volume avec un partage de fichiers Azure. Si vous synchronisez la racine du volume, tous les sous-dossiers et fichiers se retrouvent dans le même partage de fichiers Azure.

La synchronisation de la racine du volume n’est pas toujours la meilleure réponse. Il y a des avantages à synchroniser plusieurs emplacements. Par exemple, cela permet de maintenir un nombre d’éléments plus bas par étendue de synchronisation. Bien que nous testions les partages de fichiers Azure et Azure File Sync avec 100 millions d’éléments (fichiers et dossiers) par partage, la meilleure pratique consiste à essayer de conserver un chiffre inférieur à 20 ou 30 millions d’éléments dans un même partage. La configuration d’Azure File Sync avec un nombre d’éléments inférieur n’est pas seulement avantageuse pour la synchronisation de fichiers. Un nombre inférieur d’éléments présente également des avantages pour d’autres scénarios comme :

* L’analyse initiale du contenu Cloud peut se terminer plus rapidement, ce qui réduit l’attente de l’affichage de l’espace de noms sur un serveur Azure File Sync.
* La restauration côté cloud à partir d’un instantané de partage de fichiers Azure sera plus rapide.
* La reprise d’activité d’un serveur local peut être considérablement accélérée.
* Les changements effectués directement dans un partage de fichiers Azure (en dehors de la synchronisation) peuvent être détectés et synchronisés plus rapidement.

> [!TIP]
> Si vous ne savez pas combien de fichiers et de dossiers vous avez, consultez l’outil d’arborescence de JAM Software GmbH.

#### <a name="a-structured-approach-to-a-deployment-map"></a>Approche structurée d’un plan de déploiement

Avant de déployer un stockage cloud par la suite, vous devez créer un mappage entre des dossiers locaux et des partages de fichiers Azure. Ce mappage indique ensuite le nombre et la nature des ressources de *groupe de synchronisation* Azure File Sync à provisionner. Un groupe de synchronisation lie le partage de fichiers Azure et le dossier sur votre serveur et établit une connexion de synchronisation.

Pour prendre la décision sur le nombre de partages de fichiers Azure dont vous avez besoin, passez en revue les limites et les meilleures pratiques suivantes. Cela vous permet d’optimiser votre mappage.

* Un serveur sur lequel l’agent Azure File Sync est installé peut se synchroniser avec un maximum de 30 partages de fichiers Azure.
* Un partage de fichiers Azure est déployé dans un compte de stockage. Ainsi, le compte de stockage est une cible de mise à l’échelle pour les numéros de performance tels que les IOPS et le débit.

  Un partage de fichier standard Azure peut théoriquement saturer les performances maximales d’un compte de stockage. Le fait de placer plusieurs partages dans un seul compte de stockage signifie que vous créez un pool partagé d’IOPS et de débit pour ces partages. Si vous envisagez de joindre uniquement Azure File Sync à ces partages de fichiers, le regroupement de plusieurs partages de fichiers Azure dans le même compte de stockage n’est pas un problème. Examinez les objectifs de performances du partage de fichiers Azure pour obtenir un aperçu approfondi sur les mesures pertinentes à prendre en compte. Ces limitations ne s’appliquent pas au stockage Premium, où les performances sont explicitement approvisionnées et garanties pour chaque partage.

  Si vous envisagez d’intégrer une application dans Azure qui utilisera le partage de fichiers Azure en mode natif, vous devrez peut-être augmenter les performances de votre partage de fichiers Azure. Si ce type d’utilisation est une éventualité, même future, la création d’un partage de fichiers Azure standard à son propre compte de stockage est préférable.
* Il existe une limite de 250 comptes de stockage par abonnement et par région Azure.

> [!TIP]
> Avec ces informations à l’esprit, il est souvent nécessaire de regrouper plusieurs dossiers de niveau supérieur sur vos volumes dans un répertoire racine commun et nouveau. Vous synchronisez ensuite ce nouveau répertoire racine et tous les dossiers que vous y avez regroupés dans un seul partage de fichiers Azure. Cette technique vous permet de rester dans la limite de 30 synchronisations de partage de fichiers Azure par serveur.
>
> Ce regroupement sous une racine commune n’a aucun impact sur l’accès à vos données. Vos listes de contrôle d’accès restent en l’état. Vous avez seulement besoin d’ajuster les chemins d’accès de partage (par exemple, des partages SMB ou NFS) que vous pouvez avoir sur les dossiers de serveur locaux et que vous avez désormais changés en racine commune. Rien d’autre ne change.

> [!IMPORTANT]
> Le vecteur d’échelle le plus important pour Azure File Sync est le nombre d’éléments (fichiers et dossiers) qui doivent être synchronisés. Pour plus d’informations, consultez [Cibles de mise à l’échelle Azure File Sync](../articles/storage/files/storage-files-scale-targets.md#azure-file-sync-scale-targets).

Il est recommandé de maintenir un petit nombre d’éléments par étendue de synchronisation. C’est un facteur important à prendre en compte quand vous mappez des dossiers aux partages de fichiers Azure. Azure File Sync est testé avec 100 millions d’éléments (fichiers et dossiers) par partage. Toutefois, il est souvent préférable de conserver le nombre d’éléments au-dessous de 20 ou 30 millions dans un même partage. Fractionnez votre espace de noms en plusieurs partages si vous commencez à dépasser ces nombres. Vous pouvez continuer à regrouper plusieurs partages locaux dans le même partage de fichiers Azure, à condition que vous restiez plus ou moins en dessous de ces chiffres. Cette méthode vous donne de la marge pour évoluer.

Dans votre situation, il est possible qu’un ensemble de dossiers puisse logiquement se synchroniser avec le même partage de fichiers Azure (à l’aide de la nouvelle approche de dossier racine commun mentionnée plus haut). Toutefois, il peut être préférable de regrouper les dossiers de manière à ce qu’ils se synchronisent avec deux partages de fichiers Azure au lieu d’un. Vous pouvez utiliser cette approche pour conserver l’équilibre entre le nombre de fichiers et de dossiers par partage de fichiers sur le serveur. Vous pouvez également fractionner vos partages locaux et synchroniser sur d’autres serveurs locaux, en ajoutant la possibilité de synchroniser avec 30 autres partages de fichiers Azure par serveur supplémentaire.

#### <a name="create-a-mapping-table"></a>Créer une table de mappage

:::row:::
    :::column:::
        [![Exemple d’une table de mappage. Téléchargez le fichier suivant pour découvrir et utiliser le contenu de cette image.](media/storage-files-migration-namespace-mapping/namespace-mapping.png)](media/storage-files-migration-namespace-mapping/namespace-mapping-expanded.png#lightbox)
    :::column-end:::
    :::column:::
        Combinez les concepts précédents pour déterminer le nombre de partages de fichiers Azure dont vous avez besoin, ainsi que les parties de vos données existantes finissant dans ces différents partages.
        
        Créez un tableau regroupant vos réflexions pour pouvoir vous y référer dès que nécessaire. Veillez à rester organisé pour ne perdre aucun détail de votre plan de mappage quand vous approvisionnez simultanément un grand nombre de ressources Azure. Pour vous aider à créer un mappage complet, vous pouvez télécharger un fichier Microsoft Excel en tant que modèle.

[//]: # (Le langage HTML se présente comme étant le seul moyen d’ajouter une table imbriquée à deux colonnes avec analyse des images de travail et texte/lien hypertexte sur la même ligne.)

<br>
<table>
    <tr>
        <td>
            <img src="media/storage-files-migration-namespace-mapping/excel.png" alt="Microsoft Excel file icon that helps to set the context for the type of file download for the link next to it.">
        </td>
        <td>
            <a href="https://download.microsoft.com/download/1/8/D/18DC8184-E7E2-45EF-823F-F8A36B9FF240/Azure File Sync - Namespace Mapping.xlsx">Téléchargez un modèle de mappage d’espace de noms.</a>
        </td>
    </tr>
</table>
    :::column-end:::
:::row-end:::
