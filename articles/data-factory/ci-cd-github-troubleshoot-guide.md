---
title: Résoudre les problèmes liés à CI-CD, Azure DevOps et GitHub dans ADF
description: Utilisez différentes méthodes pour résoudre les problèmes liés à CI-CD dans ADF.
author: ssabat
ms.author: susabat
ms.reviewer: susabat
ms.service: data-factory
ms.topic: troubleshooting
ms.date: 03/12/2021
ms.openlocfilehash: 2b6f97f0966cb2c92dbd88c4a70188282ed3ed27
ms.sourcegitcommit: ba3a4d58a17021a922f763095ddc3cf768b11336
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104802031"
---
# <a name="troubleshoot-ci-cd-azure-devops-and-github-issues-in-adf"></a>Résoudre les problèmes liés à CI-CD, Azure DevOps et GitHub dans ADF 

[!INCLUDE[appliesto-adf-asa-md](includes/appliesto-adf-asa-md.md)]

Cet article explore les méthodes courantes pour résoudre les problèmes d’intégration continue/de déploiement continu (CI-CD), d’Azure DevOps et de GitHub dans Azure Data Factory.

Si vous avez des questions ou des problèmes lors de l’utilisation de techniques de contrôle de code source ou DevOps, voici quelques articles qui pourront vous être utiles :

- Reportez-vous à [Contrôle de code source dans ADF](source-control.md) pour savoir comment le contrôle de code source est utilisé dans ADF. 
- Reportez-vous à  [CI-CD dans ADF](continuous-integration-deployment.md) pour en savoir plus sur la façon dont DevOps CI-CD est utilisé dans ADF.
 
## <a name="common-errors-and-messages"></a>Erreurs et messages courants

### <a name="connect-to-git-repository-failed-due-to-different-tenant"></a>Échec de la connexion au référentiel Git en raison d’un locataire différent

#### <a name="issue"></a>Problème
    
Vous rencontrez parfois des problèmes d’authentification, par exemple l’état HTTP 401. En particulier, si vous avez plusieurs locataires avec un compte invité, les choses peuvent devenir plus compliquées.

#### <a name="cause"></a>Cause

Nous avons observé que le jeton a été obtenu à partir du locataire d’origine, mais que ADF se trouve dans le locataire invité et tente d’utiliser le jeton pour accéder à DevOps dans le locataire invité. Ce n’est pas le comportement normal.

#### <a name="recommendation"></a>Recommandation

Vous devez plutôt utiliser le jeton émis par le locataire invité. Par exemple, vous devez affecter le même Azure Active Directory à votre locataire invité, ainsi qu’à votre DevOps, afin qu’il puisse définir correctement le comportement des jetons et utiliser le locataire approprié.

### <a name="template-parameters-in-the-parameters-file-are-not-valid"></a>Les paramètres de modèle dans le fichier de paramètres ne sont pas valides

#### <a name="issue"></a>Problème

Si vous supprimez un déclencheur dans la branche Dev, qui est déjà disponible dans une branche Test ou Production avec la **même** configuration (par exemple, la fréquence et l’intervalle), le déploiement du pipeline de mise en production se déroule correctement et le déclencheur correspondant est supprimé dans les environnements respectifs. Toutefois, si vous utilisez une configuration **différente** (par exemple la fréquence et l’intervalle) pour le déclencheur dans les environnements Test/Production et supprimez le même déclencheur dans Dev, le déploiement échoue avec une erreur.

#### <a name="cause"></a>Cause

Le pipeline CI/CD échoue avec l’erreur suivante :

`
2020-07-20T11:19:02.1276769Z ##[error]Deployment template validation failed: 'The template parameters 'Trigger_Salesforce_properties_typeProperties_recurrence_frequency, Trigger_Salesforce_properties_typeProperties_recurrence_interval, Trigger_Salesforce_properties_typeProperties_recurrence_startTime, Trigger_Salesforce_properties_typeProperties_recurrence_timeZone' in the parameters file are not valid; they are not present in the original template and can therefore not be provided at deployment time. The only supported parameters for this template are 'factoryName, PlanonDWH_connectionString, PlanonKeyVault_properties_typeProperties_baseUrl
`

#### <a name="recommendation"></a>Recommandation

L’erreur se produit parce que nous supprimons souvent un déclencheur, qui est paramétré. Par conséquent, les paramètres ne sont pas disponibles dans le modèle ARM (car le déclencheur n’existe plus). Comme le paramètre ne figure plus dans le modèle ARM, nous devons mettre à jour les paramètres substitués dans le pipeline DevOps. Sinon, chaque fois que les paramètres du modèle ARM changent, ils doivent mettre à jour les paramètres substitués dans le pipeline DevOps (dans la tâche de déploiement).

### <a name="updating-property-type-is-not-supported"></a>La mise à jour du type de propriété n’est pas prise en charge

#### <a name="issue"></a>Problème

Le pipeline de mise en production CI/CD échoue avec l’erreur suivante :

`
2020-07-06T09:50:50.8716614Z There were errors in your deployment. Error code: DeploymentFailed.
2020-07-06T09:50:50.8760242Z ##[error]At least one resource deployment operation failed. Please list deployment operations for details. Please see https://aka.ms/DeployOperations for usage details.
2020-07-06T09:50:50.8771655Z ##[error]Details:
2020-07-06T09:50:50.8772837Z ##[error]DataFactoryPropertyUpdateNotSupported: Updating property type is not supported.
2020-07-06T09:50:50.8774148Z ##[error]DataFactoryPropertyUpdateNotSupported: Updating property type is not supported.
2020-07-06T09:50:50.8775530Z ##[error]Check out the troubleshooting guide to see if your issue is addressed: https://docs.microsoft.com/azure/devops/pipelines/tasks/deploy/azure-resource-group-deployment#troubleshooting
2020-07-06T09:50:50.8776801Z ##[error]Task failed while creating or updating the template deployment.
`

#### <a name="cause"></a>Cause

Cela est dû à un runtime d’intégration portant le même nom dans la fabrique cible, mais avec un type différent. Le runtime d'intégration doit être du même type lors du déploiement.

#### <a name="recommendation"></a>Recommandation

- Reportez-vous aux meilleures pratiques ci-dessous pour CI/CD :

    https://docs.microsoft.com/azure/data-factory/continuous-integration-deployment#best-practices-for-cicd 
- Les runtimes d’intégration ne changent pas souvent et sont similaires dans toutes les phases de CI/CD. Ainsi, Data Factory s’attend à ce que vous ayez le même nom et le même type de runtime d’intégration dans toutes les phases de CI/CD. Si le nom, les types et les propriétés diffèrent, assurez-vous qu’ils correspondent à la configuration du runtime d’intégration source et cible, puis déployez le pipeline de mise en production.
- Si vous voulez partager les runtimes d’intégration dans toutes les phases, envisagez d’utiliser une fabrique ternaire qui contiendra uniquement les runtimes d’intégration partagés. Vous pouvez utiliser cette fabrique partagée dans tous vos environnements en tant que type de runtime d’intégration lié.

### <a name="document-creation-or-update-failed-because-of-invalid-reference"></a>Échec de la création ou de la mise à jour du document en raison d’une référence non valide

#### <a name="issue"></a>Problème

Lorsque vous tentez de publier des modifications apportées à une fabrique de données, vous recevez le message d’erreur suivant :

`
"error": {
        "code": "BadRequest",
        "message": "The document creation or update failed because of invalid reference '<entity>'.",
        "target": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/<rgname>/providers/Microsoft.DataFactory/factories/<datafactory>/pipelines/<pipeline>",
        "details": null
    }
`
### <a name="cause"></a>Cause

Vous avez détaché la configuration Git et l’avez reconfigurée avec l’indicateur « Importer des ressources » sélectionné, qui définit la fabrique de données comme étant « synchronisée ». Cela signifie qu’il n’y a aucune modification à publier.

#### <a name="resolution"></a>Résolution

Détachez la configuration Git et redéfinissez-la en veillant à ne PAS activer la case à cocher « Importer des ressources existantes ».

### <a name="data-factory-move-failing-from-one-resource-group-to-another"></a>La fabrique de données n’a pas pu passer d’un groupe de ressources à un autre

#### <a name="issue"></a>Problème

Vous ne parvenez pas à déplacer une fabrique de données d’un groupe de ressources à un autre, l’opération échoue avec l’erreur suivante :

`
{
    "code": "ResourceMoveProviderValidationFailed",
    "message": "Resource move validation failed. Please see details. Diagnostic information: timestamp 'xxxxxxxxxxxxZ', subscription id 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', tracking id 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', request correlation id 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'.",
    "details": [
        {
            "code": "BadRequest",
            "target": "Microsoft.DataFactory/factories",
            "message": "One of the resources contain integration runtimes that are either SSIS-IRs in starting/started/stopping state, or Self-Hosted IRs which are shared with other resources. Resource move is not supported for those resources."
        }
    ]
}
`

#### <a name="resolution"></a>Résolution

Vous devez supprimer le runtime d'intégration SSIS et les runtimes d'intégration partagés pour permettre l’opération de déplacement. Si vous ne souhaitez pas supprimer les runtimes d’intégration, le meilleur moyen consiste à copier et cloner le document pour effectuer la copie et, une fois la copie terminée, à supprimer l’ancienne fabrique de données.

###  <a name="unable-to-export-and-import-arm-template"></a>Impossible d’exporter et importer un modèle ARM

#### <a name="issue"></a>Problème

Impossible d’exporter et importer un modèle ARM. Aucune erreur ne s’est produite sur le portail. Toutefois, dans la trace du navigateur, vous pouvez voir l’erreur suivante :

`Failed to load resource: the server responded with a status code of 401 (Unauthorized)`

#### <a name="cause"></a>Cause

Vous avez créé un rôle client en tant qu’utilisateur et il n’a pas l’autorisation nécessaire. Lorsque la fabrique est chargée dans l’interface utilisateur, une série de valeurs de contrôle d’exposition pour la fabrique est vérifiée. Dans ce cas, le rôle d’accès de l’utilisateur n’a pas l’autorisation d’accéder à l’API *queryFeaturesValue*. Pour accéder à cette API, la fonctionnalité des paramètres globaux est désactivée. Le chemin d’accès du code d’exportation ARM repose en partie sur la fonctionnalité des paramètres globaux.

#### <a name="resolution"></a>Résolution

Pour résoudre le problème, vous devez ajouter l’autorisation suivante à votre rôle : *Microsoft.DataFactory/factories/queryFeaturesValue/action*. Cette autorisation doit être incluse par défaut dans le rôle « Contributeur de fabrique de données ».

###  <a name="cannot-automate-publishing-for-cicd"></a>Impossible d’automatiser la publication pour CI/CD 

#### <a name="cause"></a>Cause

Jusqu’à récemment, la seule manière de publier un pipeline ADF pour les déploiements consistait à utiliser le bouton du portail ADF. À présent, vous pouvez rendre le processus automatique. 

#### <a name="resolution"></a>Résolution

Le processus CI/CD a été amélioré. La fonctionnalité **Publication automatisée** prend, valide et exporte toutes les fonctionnalités de modèle Azure Resource Manager (ARM) de l’expérience utilisateur d’ADF. Elle rend la logique consommable par le biais d’un package npm disponible publiquement [@microsoft/azure-data-factory-utilities](https://www.npmjs.com/package/@microsoft/azure-data-factory-utilities). Cela vous permet de déclencher ces actions par programmation au lieu de devoir accéder à l’interface utilisateur d’ADF et de cliquer sur un bouton. Cela donne à vos pipelines de CI/CD une **véritable** expérience d’intégration continue. Pour plus d’informations, suivez les [améliorations apportées au processus de publication pour CI/CD ADF](./continuous-integration-deployment-improvements.md). 

###  <a name="cannot-publish-because-of-4mb-arm-template-limit"></a>Publication impossible en raison d’une limite de 4 Mo pour le modèle ARM  

#### <a name="issue"></a>Problème

Vous ne pouvez pas effectuer de déploiement, car vous avez atteint la limite Azure Resource Manager de 4 Mo pour la taille du modèle. Vous avez besoin d’une solution pour que le déploiement puisse avoir lieu une fois la limite franchie. 

#### <a name="cause"></a>Cause

Azure Resource Manager limite la taille du modèle à 4 Mo. Limitez la taille de votre modèle à 4 Mo et celle de chaque fichier de paramètres à 64 ko. La limite de 4 Mo s’applique à l’état final du modèle une fois développé avec les définitions des ressources itératives et les valeurs des variables et des paramètres. Toutefois, vous avez franchi la limite. 

#### <a name="resolution"></a>Résolution

Pour les solutions petites et moyennes, un modèle unique est plus facile à comprendre et à gérer. Vous pouvez voir toutes les ressources et valeurs dans un même fichier. Pour des scénarios avancés, les modèles liés permettent de diviser la solution en composants ciblés. Suivez les bonnes pratiques indiquées à la page [Utilisation de modèles liés et imbriqués](../azure-resource-manager/templates/linked-templates.md?tabs=azure-powershell).

### <a name="cannot-connect-to-git-enterprise"></a>Impossible de se connecter à GIT Enterprise  

##### <a name="issue"></a>Problème

Vous ne pouvez pas vous connecter à GIT Enterprise en raison de problèmes d’autorisation. Vous pouvez voir une erreur telle que **422 - Impossible de traiter l’entité**.

#### <a name="cause"></a>Cause

* Vous n’avez pas configuré Oauth pour l’ADF. 
* Votre URL est mal configurée.

##### <a name="resolution"></a>Résolution

D’abord, vous accordez l’accès Oauth à l’ADF. Ensuite, vous devez utiliser l’URL correcte pour vous connecter à GIT Enterprise. La configuration doit être définie sur la ou les organisations clientes. Par exemple, ADF essaiera d’abord *https://hostname/api/v3/search/repositories?q=user%3<customer credential>...* et échouera. Ensuite, il tentera *https://hostname/api/v3/orgs/<org>/<repo>...* , et réussira. 
 
### <a name="cannot-recover-from-a-deleted-data-factory"></a>Impossible de récupérer à partir d’une fabrique de données supprimée

#### <a name="issue"></a>Problème
Le client a supprimé la fabrique de données ou le groupe de ressources contenant la fabrique de données. Il souhaite savoir comment restaurer une fabrique de données supprimée.

#### <a name="cause"></a>Cause

Il est possible de récupérer la fabrique de données uniquement si le client a un contrôle de code source configuré (DevOps ou Git). Cette opération apporte la dernière ressource publiée et **ne restaure pas** le pipeline, le jeu de données et le service lié non publiés.

À défaut de contrôle de code source, la récupération d’une fabrique de données supprimée à partir du serveur principal n’est pas possible car, après que le service a reçu la commande delete, l’instance a été supprimée et aucune sauvegarde n’a été stockée.

#### <a name="resolution"></a>Résolution

Pour récupérer la fabrique de données supprimée qui a le contrôle de code source, consultez les étapes ci-dessous :

 * Créer une Azure Data Factory

 * Reconfigurez Git avec les mêmes paramètres, mais veillez à importer les ressources de fabrique de données existantes dans le référentiel sélectionné, puis choisissez Nouvelle branche.

 * Créez une demande de tirage pour fusionner les modifications apportées à la branche de collaboration, puis publier.

 * Si le client disposait d’un runtime d’intégration auto-hébergé dans l’ADF supprimée, il devra créer une instance dans la nouvelle ADF, désinstaller et réinstaller l’instance sur sa machine locale/machine virtuelle à l’aide de la nouvelle clé obtenue. Une fois la configuration du runtime d’intégration terminée, le client devra modifier le service lié pour qu’il pointe vers le nouveau runtime et tester la connexion, sans quoi il échouera avec l’erreur **Référence non valide**.



## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la résolution des problèmes, essayez les ressources suivantes :

*  [Blog Data Factory](https://azure.microsoft.com/blog/tag/azure-data-factory/)
*  [Demandes de fonctionnalités Data Factory](https://feedback.azure.com/forums/270578-data-factory)
*  [Vidéos Azure](https://azure.microsoft.com/resources/videos/index/?sort=newest&services=data-factory)
*  [Forum Stack Overflow pour Data Factory](https://stackoverflow.com/questions/tagged/azure-data-factory)
*  [Informations Twitter sur Data Factory](https://twitter.com/hashtag/DataFactory)
