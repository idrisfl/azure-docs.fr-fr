---
title: Base de référence de sécurité Azure pour Azure Sentinel
description: La base de référence de sécurité Azure Sentinel fournit des instructions et des ressources pour la mise en œuvre des recommandations de sécurité spécifiées dans le benchmark de sécurité Azure.
author: msmbaldwin
ms.service: azure-sentinel
ms.topic: conceptual
ms.date: 03/16/2021
ms.author: mbaldwin
ms.custom: subject-security-benchmark
ms.openlocfilehash: a827268444fdbc2cdbbe5ac1220ad7d49a2a254f
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104604234"
---
# <a name="azure-security-baseline-for-azure-sentinel"></a>Base de référence de sécurité Azure pour Azure Sentinel

Cette base de référence de sécurité applique les conseils du [benchmark de sécurité Azure version 1.0](../security/benchmarks/overview-v1.md) à Azure Sentinel. Le benchmark de sécurité Azure fournit des recommandations sur la façon dont vous pouvez sécuriser vos solutions cloud sur Azure.
Le contenu est regroupé par les **contrôles de sécurité** définis par le Benchmark de sécurité Azure et les conseils associés applicables à Azure Sentinel. Les **contrôles** non applicables à Azure Sentinel ont été exclus.

 
Pour voir comment Azure Sentinel est entièrement mappé au benchmark de sécurité Azure, consultez le [fichier de mappage complet de la base de référence de sécurité Azure Sentinel](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines).

## <a name="network-security"></a>Sécurité réseau

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : sécurité réseau](../security/benchmarks/security-control-network-security.md).*

### <a name="11-protect-azure-resources-within-virtual-networks"></a>1.1 : Protéger les ressources Azure au sein des réseaux virtuels

**Conseils** : Vous ne pouvez pas associer un réseau virtuel, un sous-réseau ou un groupe de sécurité réseau directement à Azure Sentinel. Vous pouvez cependant activer une instance Azure Private Endpoint pour l’espace de travail Log Analytics associé à Azure Sentinel afin de limiter la communication vers et depuis vos réseaux privés.

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="111-use-automated-tools-to-monitor-network-resource-configurations-and-detect-changes"></a>1.11 : Utiliser des outils automatisés pour superviser les configurations des ressources réseau et détecter les modifications

**Aide** : Utilisez le journal d’activité Azure pour surveiller les configurations des ressources réseau et détecter les modifications des ressources réseau associées à votre espace de travail Azure Sentinel. Créez des alertes dans Azure Monitor, qui se déclenchent en cas de modification des ressources critiques.

- [Guide pratique pour activer l’audit dans Azure Sentinel](resources.md)

- [Guide pratique pour consulter et récupérer les événements du journal d’activité Azure](https://docs.microsoft.com/azure/azure-monitor/essentials/activity-log#view-the-activity-log)
 

- [Guide pratique pour créer des alertes dans Azure Monitor](../azure-monitor/alerts/alerts-activity-log.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

## <a name="logging-and-monitoring"></a>Journalisation et supervision

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : journalisation et supervision](../security/benchmarks/security-control-logging-monitoring.md).*

### <a name="22-configure-central-security-log-management"></a>2.2 : Configurer la gestion des journaux de sécurité centrale

**Aide** : Les journaux d’audit Azure Sentinel sont conservés dans les journaux d'activité Azure. Vous pouvez afficher ces données en les transmettant en continu du journal d’activité Azure vers Azure Sentinel, d’où vous pouvez ensuite effectuer des recherches et des analyses à partir de ces données.

- [Guide pratique pour activer l’audit dans Azure Sentinel](resources.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="23-enable-audit-logging-for-azure-resources"></a>2.3 : Activer la journalisation d’audit pour les ressources Azure

**Aide** : Les journaux d’audit pour Azure Sentinel sont conservés dans les journaux d'activité Azure. Vous pouvez afficher ces données en les transmettant en continu du journal d’activité Azure vers Azure Sentinel, d’où vous pouvez ensuite effectuer des recherches et des analyses à partir de ces données.

- [Guide pratique pour activer l’audit dans Azure Sentinel](resources.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="25-configure-security-log-storage-retention"></a>2.5 : Configurer la conservation du stockage des journaux de sécurité

**Conseils** : Dans Azure Monitor, définissez la période de conservation des journaux pour les espaces de travail Log Analytics associés à vos espaces de travail Azure Sentinel conformément aux réglementations de conformité de votre organisation.

- [Guide pratique pour définir les paramètres de conservation des journaux](https://docs.microsoft.com/azure/azure-monitor/logs/manage-cost-storage#change-the-data-retention-period)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="26-monitor-and-review-logs"></a>2.6 : Superviser et examiner les journaux

**Aide** : Les journaux d’audit Azure Sentinel sont conservés dans les journaux d'activité Azure. Vous pouvez afficher ces données en les transmettant en continu du journal d’activité Azure vers Azure Sentinel, d’où vous pouvez ensuite effectuer des recherches et des analyses à partir de ces données. Analysez et supervisez les journaux de vos instances de journal d’activité Azure Sentinel pour rechercher un comportement anormal. Utilisez la section « journaux » de votre espace de travail Azure Sentinel pour exécuter des requêtes, ou créez des alertes basées sur vos journaux Sentinel.

- [Guide pratique pour activer l’audit dans Azure Sentinel](resources.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="27-enable-alerts-for-anomalous-activities"></a>2.7 : Activer les alertes d’activité anormale

**Aide** : Les journaux d’audit Azure Sentinel sont conservés dans les journaux d'activité Azure. Vous pouvez afficher ces données en les transmettant en continu du journal d’activité Azure vers Azure Sentinel, d’où vous pouvez ensuite effectuer des recherches et des analyses à partir de ces données. Analysez et supervisez les journaux de vos instances de journal d’activité Azure Sentinel pour rechercher un comportement anormal. Utilisez la section « journaux » de votre espace de travail Azure Sentinel pour exécuter des requêtes, ou créez des alertes basées sur vos journaux Sentinel.

- [Guide pratique pour activer l’audit dans Azure Sentinel](resources.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

## <a name="identity-and-access-control"></a>Contrôle des accès et des identités

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : contrôle des accès et des identités](../security/benchmarks/security-control-identity-access-control.md).*

### <a name="31-maintain-an-inventory-of-administrative-accounts"></a>3.1 : Tenir un inventaire des comptes d’administration

**Aide** : conservez un inventaire des comptes d’utilisateur qui ont un accès d’administration au plan de contrôle (par exemple, le portail Azure) de votre espace de travail Azure Sentinel. 

Vous pouvez utiliser le volet de gestion des identités et des accès dans le portail Azure de votre abonnement afin de configurer un contrôle d’accès en fonction du rôle Azure (RBAC Azure). Les rôles sont appliqués aux utilisateurs, aux groupes, aux principaux de service et aux identités managées dans Azure Active Directory (Azure AD). Azure Sentinel utilise également Azure RBAC pour fournir des rôles d’administration intégrés, tels que celui de contributeur Azure Sentinel, qui peuvent être attribués à des utilisateurs, des groupes et des services dans Azure. 

- [Comprendre les rôles personnalisés](../role-based-access-control/custom-roles.md)

- [Comprendre Azure RBAC dans Azure Sentinel](roles.md)

- [Comment configurer Azure RBAC pour les classeurs](quickstart-get-visibility.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="33-use-dedicated-administrative-accounts"></a>3.3 : Utiliser des comptes d’administration dédiés

**Conseils** : Créez des procédures standard autour de l’utilisation de comptes d’administration dédiés. Utilisez la gestion des identités et des accès dans Azure Security Center pour superviser le nombre de comptes d’administration.

En outre, pour vous aider à suivre les comptes d’administration dédiés, vous pouvez utiliser des recommandations d’Azure Security Center ou des stratégies Azure intégrées, telles que les suivantes :

- Plusieurs propriétaires doivent être affectés à votre abonnement
- Les comptes dépréciés disposant d’autorisations de propriétaire doivent être supprimés de votre abonnement
- Les comptes externes disposant d’autorisations de propriétaire doivent être supprimés de votre abonnement

Des informations supplémentaires sont disponibles sur les liens référencés.

- [Utilisation d’Azure Security Center pour superviser l’identité et l’accès (préversion)](../security-center/security-center-identity-access.md)

- [Utilisation d’Azure Policy](../governance/policy/tutorials/create-and-manage.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="34-use-azure-active-directory-single-sign-on-sso"></a>3.4 : Utiliser l’authentification unique (SSO) Azure Active Directory

**Aide** : L’accès au plan de contrôle de votre espace de travail Azure Sentinel (portail Azure, par exemple) est disponible via l’API REST et prend en charge l’authentification unique. Pour vous authentifier, définissez l’en-tête d’autorisation pour vos demandes sur un jeton web JSON que vous obtenez auprès d’Azure Active Directory (Azure AD).

- [Comprendre l’API REST Azure Log Analytics](/rest/api/loganalytics/)

- [Présentation de l’authentification SSO avec Azure AD](../active-directory/manage-apps/what-is-single-sign-on.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="35-use-multi-factor-authentication-for-all-azure-active-directory-based-access"></a>3.5 : Utiliser l’authentification multifacteur pour tous les accès basés sur Azure Active Directory

**Conseils** : activez l’authentification multifacteur Azure Active Directory (Azure AD), puis suivez les recommandations relatives à la gestion des identités et des accès d’Azure Security Center.

- [Guide pratique pour activer l’authentification multifacteur dans Azure](../active-directory/authentication/howto-mfa-getstarted.md)

- [Guide pratique pour superviser les identités et les accès dans Azure Security Center](../security-center/security-center-identity-access.md)

**Responsabilité** : Customer

**Supervision d’Azure Security Center** : Aucune

### <a name="36-use-secure-azure-managed-workstations-for-administrative-tasks"></a>3.6 : Utiliser des stations de travail sécurisées et gérées par Azure pour les tâches administratives

**Aide** : utilisez une station de travail à accès privilégié avec l’authentification multifacteur (MFA) Azure AD activée pour vous connecter à vos ressources Azure Sentinel et les configurer. 
 

 
- [Stations de travail d’accès privilégié](https://4sysops.com/archives/understand-the-microsoft-privileged-access-workstation-paw-security-model/)
 

 
- [Planification d’un déploiement cloud de l’authentification multifacteur Azure AD](../active-directory/authentication/howto-mfa-getstarted.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="37-log-and-alert-on-suspicious-activities-from-administrative-accounts"></a>3.7 : Journaliser et générer des alertes en cas d’activités suspectes sur des comptes d’administration

**Aide** : Utilisez Azure Active Directory (Azure AD) Privileged Identity Management (PIM) pour générer des journaux et des alertes quand des activités suspectes ou potentiellement dangereuses se produisent dans l’environnement.

Utilisez également les détections de risque Azure AD pour visualiser les alertes et des rapports sur les comportements à risque des utilisateurs.

- [Déploiement de Privileged Identity Management (PIM)](../active-directory/privileged-identity-management/pim-deployment-plan.md)

- [Présentation des détections de risques Azure AD](../active-directory/identity-protection/overview-identity-protection.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="38-manage-azure-resources-from-only-approved-locations"></a>3.8 : Gérer les ressources Azure à partir des emplacements approuvés uniquement

**Conseils** : Utilisez des emplacements nommés avec accès conditionnel pour autoriser l’accès au Portail Azure uniquement à partir de regroupements logiques spécifiques de plages d’adresses IP ou de pays/régions.

- [Guide pratique pour configurer des emplacements nommés dans Azure](../active-directory/reports-monitoring/quickstart-configure-named-locations.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="39-use-azure-active-directory"></a>3.9 : Utiliser Azure Active Directory

**Aide** : Utilisez Azure Active Directory (Azure AD) comme système central d’authentification et d’autorisation pour vos instances Azure Sentinel. Azure AD protège les données en utilisant un chiffrement fort pour les données au repos et en transit. De plus, AAD sale, hache et stocke de manière sécurisée les informations d’identification utilisateur.

- [Créer et configurer un locataire Azure AD](../active-directory/fundamentals/active-directory-access-create-new-tenant.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="310-regularly-review-and-reconcile-user-access"></a>3.10 : Examiner et rapprocher régulièrement l’accès utilisateur

**Aide** : Azure Active Directory (Azure AD) fournit des journaux pour vous aider à découvrir les comptes obsolètes. De plus, utilisez les révisions d’accès des identités Azure pour gérer efficacement les appartenances aux groupes, les accès aux applications d’entreprise et les attributions de rôles. L’accès des utilisateurs peut être passé en revue régulièrement pour vérifier que seules les utilisateurs appropriés continuent de bénéficier d’un accès.

- [Présentation des rapports Azure AD](/azure/active-directory/reports-monitoring)

- [Comment utiliser les révisions d’accès des identités Azure](../active-directory/governance/access-reviews-overview.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="311-monitor-attempts-to-access-deactivated-credentials"></a>3.11 : Superviser les tentatives d’accès à des informations d’identification désactivées

**Aide** : utilisez Azure Active Directory (Azure AD) en tant que système central d’authentification et d’autorisation pour vos espaces de travail Azure Sentinel. Azure AD protège les données en utilisant un chiffrement fort pour les données au repos et en transit. De plus, AAD sale, hache et stocke de manière sécurisée les informations d’identification utilisateur.

Vous avez accès aux sources des journaux d’activité, d’audit et d’événements à risque d’Azure AD, ce qui vous permet d’opérer une intégration avec à Azure Sentinel ou des informations système tierces, ainsi qu’à une solution de gestion des événements.

Vous pouvez simplifier ce processus en créant des paramètres de diagnostic pour les comptes d’utilisateur Azure AD et en envoyant les journaux d’audit et les journaux de connexion à un espace de travail Log Analytics. Vous pouvez configurer les alertes de journal souhaitées dans un espace de travail Log Analytics.

- [Guide pratique pour intégrer des journaux d’activité Azure dans Azure Monitor](/azure/active-directory/reports-monitoring/howto-integrate-activity-logs-with-log-analytics)

- [Procédure d’intégration d’Azure Sentinel](quickstart-onboard.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="312-alert-on-account-sign-in-behavior-deviation"></a>3.12 : Alerter en cas d’écart de comportement de connexion à un compte

**Conseil** : En cas d’écart de comportement des connexions au compte dans le plan de contrôle (par exemple le Portail Azure), utilisez Azure Active Directory (Azure AD) Identity Protection et les fonctionnalités de détection de risque pour configurer des réponses automatisées aux actions suspectes détectées en lien avec l’identité des utilisateurs. Vous pouvez également ingérer des données dans Azure Sentinel pour approfondir votre examen.

- [Guide pratique pour afficher une connexion risquée Azure AD](../active-directory/identity-protection/overview-identity-protection.md)

- [Guide pratique pour configurer et activer des stratégies de risque Identity Protection](../active-directory/identity-protection/howto-identity-protection-configure-risk-policies.md)

- [Guide pratique pour intégrer Azure Sentinel](quickstart-onboard.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="313-provide-microsoft-with-access-to-relevant-customer-data-during-support-scenarios"></a>3.13 : Fournir à Microsoft un accès aux données client pertinentes pendant les scénarios de support

**Aide** : Actuellement non disponible ; Customer Lockbox n’est pas encore pris en charge pour l’espace de travail Azure Sentinel ou Log Analytics.

- [Liste des services pris en charge pour Customer Lockbox](https://docs.microsoft.com/azure/security/fundamentals/customer-lockbox-overview#supported-services-and-scenarios-in-general-availability)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

## <a name="data-protection"></a>Protection des données

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : protection des données](../security/benchmarks/security-control-data-protection.md).*

### <a name="41-maintain-an-inventory-of-sensitive-information"></a>4.1 : Conserver un inventaire des informations sensibles

**Conseils** : Utilisez des étiquettes pour faciliter le suivi des ressources Azure qui stockent ou traitent des informations sensibles.

- [Guide pratique pour créer et utiliser des étiquettes](../azure-resource-manager/management/tag-resources.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="42-isolate-systems-storing-or-processing-sensitive-information"></a>4.2 : Isoler les systèmes qui stockent ou traitent les informations sensibles

**Aide** : implémentez des abonnements pour inclure éventuellement des groupes d’administration distincts pour les espaces de travail de développement, de test et de production de Sentinel.

- [Guide pratique pour créer des abonnements Azure supplémentaires](../cost-management-billing/manage/create-subscription.md)

- [Guide pratique pour créer des groupes d’administration](../governance/management-groups/create-management-group-portal.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="44-encrypt-all-sensitive-information-in-transit"></a>4.4 : Chiffrer toutes les informations sensibles en transit

**Conseils** : Si vous utilisez une machine virtuelle Azure ou locale en tant que redirecteur Syslog, vous devez configurer le démon Syslog (rsyslog ou syslog-ng) pour qu’il communique dans TLS.

- [Connectez votre solution externe en utilisant le format CEF](connect-common-event-format.md)

**Responsabilité** : Partagé

**Supervision Azure Security Center** : Aucune

### <a name="45-use-an-active-discovery-tool-to-identify-sensitive-data"></a>4.5 : Utiliser un outil de découverte actif pour identifier les données sensibles

**Aide** : les fonctionnalités d’identification, de classification et de protection contre la perte des données ne sont pas encore disponibles dans Azure. Implémentez une solution tierce si nécessaire à des fins de conformité.

Pour la plateforme sous-jacente managée par Microsoft, Microsoft considère tout le contenu client comme sensible et met tout en œuvre pour empêcher la perte et l’exposition des données client. Pour garantir la sécurité des données client dans Azure, Microsoft a implémenté et tient à jour une suite de contrôles et de fonctionnalités de protection des données robustes.

- [Présentation de la protection des données client dans Azure](../security/fundamentals/protection-customer-data.md)

**Responsabilité** : Partagé

**Supervision Azure Security Center** : Aucune

### <a name="46-use-role-based-access-control-to-control-access-to-resources"></a>4.6 : Utiliser le contrôle d’accès en fonction du rôle pour contrôler l’accès aux ressources

**Aide** : Vous pouvez utiliser le volet de gestion des identités et des accès (IAM) dans le portail Azure afin de configurer le contrôle d’accès en fonction du rôle d’Azure (Azure RBAC). Les rôles sont appliqués aux utilisateurs, aux groupes, aux principaux de service et aux identités gérées dans Active Directory. Vous pouvez utiliser des rôles intégrés Azure ou des rôles personnalisés pour les individus et les groupes. 

Azure Sentinel utilise le Azure RBAC pour fournir des rôles intégrés susceptibles d’être attribués à des utilisateurs, des groupes et des services dans Azure. L’utilisation d’Azure RBAC vous permet d’utiliser et de créer des rôles au sein de votre équipe en charge des opérations de sécurité pour accorder l’accès approprié à Azure Sentinel. En fonction des rôles, vous bénéficiez d’un contrôle précis sur ce que les utilisateurs disposant d’un accès à Azure Sentinel peuvent voir. Vous pouvez attribuer des rôles Azure directement dans l’espace de travail Azure Sentinel, ou bien à un abonnement ou à un groupe de ressources auquel appartient l’espace de travail. Il existe trois rôles Azure Sentinel intégrés spécifiques :

- Lecteur Azure Sentinel
- Répondeur Azure Sentinel
- Contributeur Azure Sentinel

Outre les rôles Azure dédiés à Azure Sentinel, il existe des rôles intégrés à Azure et Log Analytics qui peuvent accorder un ensemble plus large d’autorisations qui incluent l’accès à votre espace de travail Azure Sentinel et à d’autres ressources :

Les rôles Azure incluent les rôles Propriétaire, Collaborateur et Lecteur. Les rôles Azure accordent l’accès à l’ensemble de vos ressources Azure, notamment aux espaces de travail Log Analytics et aux ressources Azure Sentinel.

Les rôles Log Analytics incluent les rôles Contributeur Log Analytics et Lecteur Log Analytics. Les rôles Log Analytics accordent l’accès à l’ensemble de vos espaces de travail Log Analytics.

En outre, chaque classeur Sentinel constitue une ressource Azure et vous pouvez attribuer des rôles aux utilisateurs à des fins de gestion de l’accès.

- [Comment configurer Azure RBAC](../role-based-access-control/role-assignments-portal.md)

- [Comprendre les rôles personnalisés](../role-based-access-control/custom-roles.md)

- [Comprendre les rôles dans Sentinel et Log Analytics](roles.md)

- [Comment configurer Azure RBAC pour les classeurs](quickstart-get-visibility.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="48-encrypt-sensitive-information-at-rest"></a>4.8 : Chiffrer des informations sensibles au repos

**Aide** : Actuellement, les espaces de travail Azure Sentinel and Azure Monitor Log Analytics utilisent des clés gérées par Microsoft pour chiffrer les données contenues au repos. La possibilité d’apporter votre propre clé n’est pas encore entièrement prise en charge pour Sentinel, mais le sera prochainement. 

 
- [Présentation des clés gérées par le client dans Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/logs/customer-managed-keys#customer-managed-key-overview) 

 
- [Comprendre les clés gérées par le client dans Azure Sentinel (préversion)](customer-managed-keys.md)

**Responsabilité** : Partagé

**Supervision Azure Security Center** : Aucune

### <a name="49-log-and-alert-on-changes-to-critical-azure-resources"></a>4.9 : Consigner et alerter les modifications apportées aux ressources Azure critiques

**Aide** : Les journaux d’audit Azure Sentinel sont conservés dans les journaux d'activité Azure. Vous pouvez afficher ces données en les transmettant en continu du journal d’activité Azure vers Azure Sentinel, d’où vous pouvez ensuite effectuer des recherches et des analyses à partir de ces données. La section « Journaux » de votre espace de travail Azure Sentinel vous permet de créer des alertes lorsque des modifications sont apportées aux espaces de travail Azure Sentinel de production, ainsi qu’à d’autres ressources critiques ou connexes.

- [Guide pratique pour activer l’audit dans Azure Sentinel](resources.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

## <a name="inventory-and-asset-management"></a>Gestion des stocks et des ressources

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : Gestion des stocks et des ressources](../security/benchmarks/security-control-inventory-asset-management.md).*

### <a name="61-use-automated-asset-discovery-solution"></a>6.1 : Utiliser la solution de détection automatisée des ressources

**Aide** : Utilisez Azure Resource Graph pour interroger/découvrir toutes les ressources (telles que calcul, stockage, réseau, ports et protocoles) dans vos abonnements. Vérifiez les autorisations (lecture) appropriées dans votre locataire et répertoriez tous les abonnements Azure, ainsi que les ressources dans vos abonnements.

Bien que les ressources Azure classiques puissent être découvertes via Resource Graph, il est vivement recommandé de créer et d’utiliser des ressources Azure Resource Manager à l’avenir.

- [Guide pratique pour créer des requêtes avec Azure Resource Graph](../governance/resource-graph/first-query-portal.md)

- [Guide pratique pour afficher ses abonnements Azure](/powershell/module/az.accounts/get-azsubscription)

- [Présentation d’Azure RBAC](../role-based-access-control/overview.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="62-maintain-asset-metadata"></a>6.2 : Gérer les métadonnées de ressources

**Conseils** : Appliquez des balises aux ressources Azure en fournissant des métadonnées pour les organiser de façon logique par catégories.

- [Guide pratique pour créer et utiliser des étiquettes](../azure-resource-manager/management/tag-resources.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="63-delete-unauthorized-azure-resources"></a>6.3 : Supprimer des ressources Azure non autorisées

**Aide** : Utilisez des étiquettes, des groupes d’administration et des abonnements distincts, le cas échéant, pour organiser et suivre les ressources Azure. Rapprochez régulièrement l’inventaire et assurez-vous que les ressources non autorisées sont supprimées de l’abonnement en temps utile.

Appliquez également des restrictions quant au type de ressources pouvant être créées dans les abonnements clients, en utilisant Azure Policy avec les définitions de stratégie intégrées suivantes :

- Types de ressources non autorisés
- Types de ressources autorisés

Des informations supplémentaires sont disponibles sur les liens référencés.

- [Guide pratique pour créer des abonnements Azure supplémentaires](../cost-management-billing/manage/create-subscription.md)

- [Guide pratique pour créer des groupes d’administration](../governance/management-groups/create-management-group-portal.md)

- [Guide pratique pour créer et utiliser des étiquettes](../azure-resource-manager/management/tag-resources.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="65-monitor-for-unapproved-azure-resources"></a>6.5 : Analyser les ressources Azure non approuvées

**Aide** : Utilisez Azure Policy pour appliquer des restrictions quant au type de ressources pouvant être créées dans vos abonnements.

Utilisez Azure Resource Graph pour interroger/découvrir des ressources dans leurs abonnements.  Vérifiez que toutes les ressources Azure présentes dans l’environnement sont approuvées.

- [Guide pratique pour configurer et gérer Azure Policy](../governance/policy/tutorials/create-and-manage.md)

- [Guide pratique pour créer des requêtes avec Azure Graph](../governance/resource-graph/first-query-portal.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="69-use-only-approved-azure-services"></a>6.9 : Utiliser des services Azure approuvés uniquement

**Conseils** : Appliquez des restrictions quant au type de ressources pouvant être créées dans les abonnements clients, en utilisant Azure Policy avec les définitions intégrées suivantes :

- Types de ressources non autorisés
- Types de ressources autorisés

- [Guide pratique pour configurer et gérer Azure Policy](../governance/policy/tutorials/create-and-manage.md)

- [Guide pratique pour refuser un type de ressource spécifique avec Azure Policy](https://docs.microsoft.com/azure/governance/policy/samples/built-in-policies#general)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="611-limit-users-ability-to-interact-with-azure-resource-manager"></a>6.11 : Limiter la capacité des utilisateurs à interagir avec Azure Resource Manager

**Aide** : Configurez l’accès conditionnel Azure pour limiter la capacité des utilisateurs à interagir avec Azure Resource Manager en configurant « Bloquer l’accès » pour l’application « Gestion Microsoft Azure ».

- [Configuration de l’accès conditionnel pour bloquer l’accès à Azure Resource Manager](../role-based-access-control/conditional-access-azure-management.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

## <a name="secure-configuration"></a>Configuration sécurisée

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : Configuration sécurisée](../security/benchmarks/security-control-secure-configuration.md).*

### <a name="71-establish-secure-configurations-for-all-azure-resources"></a>7.1 : Établir des configurations sécurisées pour toutes les ressources Azure

**Aide** : Définissez et implémentez des configurations de sécurité standard pour votre espace de travail Log Analytics associé à votre espace de travail Sentinel à l’aide d’Azure Policy. Utilisez des alias Azure Policy dans l’espace de noms « Microsoft.OperationalInsights » pour créer des stratégies personnalisées d’audit ou d’application de configuration pour vos espaces de travail Log Analytics.
 

- [Affichage des alias Azure Policy disponibles](/powershell/module/az.resources/get-azpolicyalias)

- [Guide pratique pour configurer et gérer Azure Policy](../governance/policy/tutorials/create-and-manage.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="73-maintain-secure-azure-resource-configurations"></a>7.3 : Gérer les configurations de ressources Azure sécurisées

**Conseils** : Utilisez les effets Azure Policy [refuser] et [déployer s’il n’existe pas] pour appliquer des paramètres sécurisés à vos ressources Azure.

- [Guide pratique pour configurer et gérer Azure Policy](../governance/policy/tutorials/create-and-manage.md)

- [Présentation des effets d’Azure Policy](../governance/policy/concepts/effects.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="75-securely-store-configuration-of-azure-resources"></a>7.5 : Stocker en toute sécurité la configuration des ressources Azure

**Conseils** : Si vous utilisez des définitions de stratégie Azure personnalisées, utilisez Azure DevOps ou Azure Repos pour stocker et gérer votre code en toute sécurité.
 

- [Stocker du code dans Azure DevOps](/azure/devops/repos/git/gitworkflow)

 
- [Documentation Azure Repos](/azure/devops/repos/)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="77-deploy-configuration-management-tools-for-azure-resources"></a>7.7 : Déployer des outils de gestion de la configuration pour les ressources Azure

**Aide** : Utilisez les définitions Azure Policy intégrées ainsi que des alias Azure Policy dans l’espace de noms « Microsoft.OperationalInsights » pour créer des stratégies personnalisées d’alerte, d’audit ou d’application de configurations système. En outre, développez un processus et un pipeline pour la gestion des exceptions de stratégie.

- [Guide pratique pour configurer et gérer Azure Policy](../governance/policy/tutorials/create-and-manage.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="79-implement-automated-configuration-monitoring-for-azure-resources"></a>7.9 : Mettre en place une supervision automatisée de la configuration pour les ressources Azure

**Conseils** : Utilisez les définitions Azure Policy intégrées ainsi que des alias Azure Policy dans l’espace de noms « Microsoft.OperationalInsights » pour créer des stratégies personnalisées d’alerte, d’audit ou d’application de configurations système. Utilisez les effets [auditer], [refuser] et [déployer si n’existe pas] d’Azure Policy pour appliquer automatiquement des configurations pour vos ressources Azure.

- [Guide pratique pour configurer et gérer Azure Policy](../governance/policy/tutorials/create-and-manage.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="711-manage-azure-secrets-securely"></a>7.11 : Gérer les secrets Azure en toute sécurité

**Aide** : Azure Sentinel prend en charge la collecte des journaux à partir de nombreuses sources à l’aide de différents connecteurs. Certains de ces connecteurs doivent être installés avec une clé d’espace de travail Log Analytics. Lors de la configuration de ces connecteurs, utilisez Azure Key Vault pour stocker vos clés afin de simplifier la gestion des secrets et éviter toute exposition accidentelle des informations d’identification.

- [Connecter Sentinel à des sources de données](connect-data-sources.md)

- [Créer un coffre de clés](../key-vault/secrets/quick-create-portal.md)

- [Fournir une authentification Key Vault avec une identité managée](../key-vault/general/assign-access-policy-portal.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="713-eliminate-unintended-credential-exposure"></a>7.13 : Éliminer l’exposition involontaire des informations d’identification

**Conseils** : Exécuter le moteur d’analyse des informations d’identification pour identifier les informations d’identification dans le code. Le moteur d’analyse des informations d’identification encourage également le déplacement des informations d’identification découvertes vers des emplacements plus sécurisés, tels qu’Azure Key Vault.

- [Configurer Credential Scanner](https://secdevtools.azurewebsites.net/helpcredscan.html)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

## <a name="malware-defense"></a>Défense contre les programmes malveillants

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : Défense contre les programmes malveillants](../security/benchmarks/security-control-malware-defense.md).*

### <a name="82-pre-scan-files-to-be-uploaded-to-non-compute-azure-resources"></a>8.2 : Pré-analyser les fichiers à charger sur des ressources Azure non liées au calcul

**Aide** : Microsoft Antimalware est activé sur l’hôte sous-jacent qui prend en charge les services Azure (par exemple, Azure Sentinel et Log Analytics), mais il ne s’exécute pas sur du contenu de client. 

Il vous incombe de pré-analyser tout contenu chargé vers des ressources Azure autres que de calcul, notamment l’espace de travail Log Analytics. Microsoft ne peut pas accéder aux données client et ne peut donc pas effectuer d’analyses anti-programme malveillant du contenu client en votre nom.

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

## <a name="data-recovery"></a>Récupération des données

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : récupération de données](../security/benchmarks/security-control-data-recovery.md).*

### <a name="94-ensure-protection-of-backups-and-customer-managed-keys"></a>9.4 : Garantir la protection des sauvegardes et des clés managées par le client

**Aide** : Activez la suppression réversible dans Key Vault pour protéger les clés contre une suppression accidentelle ou malveillante. Si un utilisateur révoque la clé de chiffrement principale, soit en la supprimant, soit en enlevant l’accès à Azure Sentinel, ce dernier prend en compte la modification dans l’heure qui suit, se comportant alors comme si les données n’étaient plus disponibles. À ce stade, toute opération qui utilise des ressources de stockage persistantes, telle que l’ingestion de données, la modification de configuration persistante et la création d’incident, est empêchée. Les données déjà stockées ne sont pas supprimées, mais restent inaccessibles. Les données inaccessibles sont régies par la stratégie de conservation des données et sont vidées conformément à cette stratégie.

La seule opération possible une fois que la clé de chiffrement est révoquée ou supprimée est la suppression du compte.

Si l’accès est restauré après la révocation, Azure Sentinel restaure l’accès aux données dans l’heure qui suit.

- [Activer la suppression réversible dans Key Vault](../storage/blobs/soft-delete-blob-overview.md)

- [Comprendre les clés gérées par le client dans Azure Sentinel](customer-managed-keys.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

## <a name="incident-response"></a>Réponse aux incidents

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : réponse aux incidents](../security/benchmarks/security-control-incident-response.md).*

### <a name="101-create-an-incident-response-guide"></a>10.1 : Créer un guide de réponse aux incidents

**Conseils** : Créez un guide de réponse aux incidents pour votre organisation. Assurez-vous qu’il existe des plans de réponse aux incidents écrits qui définissent tous les rôles du personnel, ainsi que les phases de gestion des incidents, depuis la détection jusqu’à la revue une fois l’incident terminé.

- [Comment configurer des automatisations de workflow dans Azure Security Center](../security-center/security-center-planning-and-operations-guide.md)

- [Aide sur la création de votre propre processus de réponse aux incidents de sécurité](https://msrc-blog.microsoft.com/2019/07/01/inside-the-msrc-building-your-own-security-incident-response-process/)

- [Anatomie d’un incident dans le centre de réponse aux incidents de sécurité Microsoft](https://msrc-blog.microsoft.com/2019/07/01/inside-the-msrc-building-your-own-security-incident-response-process/)

- [Le client peut également tirer parti du guide de gestion des incidents de sécurité informatique du NIST pour faciliter la création de son propre plan de réponse aux incidents](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="102-create-an-incident-scoring-and-prioritization-procedure"></a>10.2 : Créer une procédure de notation et de classement des incidents

**Conseils** : Security Center attribue un niveau de gravité à chaque alerte pour vous aider à hiérarchiser celles devant être examinées en premier. La gravité dépend du niveau de confiance que Security Center accorde à la recherche ou à l’analytique utilisées pour émettre l’alerte, mais aussi de l’intention malveillante estimée de l’activité à l’origine de l’alerte.

 

En outre, marquez clairement les abonnements (par ex. production, non production) et créez un système d’attribution de noms pour identifier et classer les ressources Azure de façon claire.

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="103-test-security-response-procedures"></a>10.3 : Tester les procédures de réponse de sécurité

**Conseils** : Exécutez des exercices pour tester les fonctionnalités de réponse aux incidents de vos systèmes de façon régulière. Identifiez les points faibles et les lacunes, et révisez le plan en fonction des besoins.

- [Reportez-vous à la publication du NIST : Guide to Test, Training, and Exercise Programs for IT Plans and Capabilities (Guide de test, d’entraînement et d’utilisation des programmes destinés aux plans et fonctionnalités informatiques)](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-84.pdf)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="104-provide-security-incident-contact-details-and-configure-alert-notifications-for-security-incidents"></a>10.4 : Fournir des informations de contact pour les incidents de sécurité et configurer des notifications d’alerte pour les incidents de sécurité

**Conseils** : Les informations de contact d’incident de sécurité seront utilisées par Microsoft pour vous contacter si Microsoft Security Response Center (MSRC) découvre que les données du client ont été utilisées par un tiers illégal ou non autorisé.  Examinez les incidents après les faits pour vous assurer que les problèmes sont résolus.

- [Comment définir le contact de sécurité d’Azure Security Center](../security-center/security-center-provide-security-contact-details.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="105-incorporate-security-alerts-into-your-incident-response-system"></a>10.5 : Intégrer des alertes de sécurité à votre système de réponse aux incidents

**Conseils** : Exportez vos alertes et recommandations d’Azure Security Center à l’aide de la fonctionnalité d’exportation continue. L’exportation continue vous permet d’exporter les alertes et les recommandations manuellement, ou automatiquement de manière continue. Vous pouvez utiliser le connecteur de données Azure Security Center pour diffuser en continu les alertes vers Azure Sentinel.

 

- [Comment configurer l’exportation continue](../security-center/continuous-export.md)

- [Comment envoyer des alertes à Azure Sentinel](connect-azure-security-center.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

### <a name="106-automate-the-response-to-security-alerts"></a>10.6 : Automatiser la réponse aux alertes de sécurité

**Conseils** : Utilisez la fonctionnalité d’automatisation du workflow dans Azure Security Center pour déclencher automatiquement des réponses via « Logic Apps » sur les alertes et recommandations de sécurité.

- [Comment configurer l’automatisation des workflows et Logic Apps](../security-center/workflow-automation.md)

**Responsabilité** : Customer

**Supervision Azure Security Center** : Aucune

## <a name="penetration-tests-and-red-team-exercises"></a>Tests d’intrusion et exercices Red Team

*Pour plus d’informations, consultez [Benchmark de sécurité Azure : tests d’intrusion et exercices Red Team](../security/benchmarks/security-control-penetration-tests-red-team-exercises.md).*

### <a name="111-conduct-regular-penetration-testing-of-your-azure-resources-and-ensure-remediation-of-all-critical-security-findings"></a>11.1 : Procéder régulièrement à des tests d’intrusion des ressources Azure et veiller à corriger tous les problèmes de sécurité critiques détectés

**Aide** : Suivez les règles d’engagement de pénétration du cloud Microsoft pour vous assurer que vos tests d’intrusion sont conformes aux stratégies de Microsoft. Utilisez la stratégie et l’exécution de Red Teaming de Microsoft ainsi que les tests d’intrusion de site actif sur l’infrastructure cloud, les services et les applications gérés par Microsoft. 

- [Règles d’engagement des tests d’intrusion](https://www.microsoft.com/msrc/pentest-rules-of-engagement?rtc=1) 

- [Microsoft Cloud Red Teaming](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)

**Responsabilité** : Partagé

**Supervision Azure Security Center** : Aucune

## <a name="next-steps"></a>Étapes suivantes

- Consultez [Vue d’ensemble d’Azure Security Benchmark V2](/azure/security/benchmarks/overview)
- En savoir plus sur les [bases de référence de la sécurité Azure](/azure/security/benchmarks/security-baselines-overview)
