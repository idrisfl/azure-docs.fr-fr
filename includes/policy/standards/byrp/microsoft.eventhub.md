---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 04/14/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: cca378322d6ced73ecdfecf038aa4231699a280d
ms.sourcegitcommit: 3b5cb7fb84a427aee5b15fb96b89ec213a6536c2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107496643"
---
## <a name="azure-security-benchmark"></a>Benchmark de sécurité Azure

Le [benchmark de sécurité Azure](../../../../articles/security/benchmarks/overview.md) fournit des recommandations sur la façon dont vous pouvez sécuriser vos solutions cloud sur Azure. Pour voir comment ce service est entièrement mappé au benchmark de sécurité Azure, consultez les [fichiers de mappage du benchmark de sécurité Azure](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines).

Pour passer en revue la façon dont les composants intégrés Azure Policy disponibles pour tous les services Azure sont mappés à ce standard de conformité, consultez [Conformité réglementaire Azure Policy - Benchmark de sécurité Azure](../../../../articles/governance/policy/samples/azure-security-benchmark.md).

|Domain |ID du contrôle |Titre du contrôle |Policy<br /><sub>(Portail Azure)</sub> |Version de la stratégie<br /><sub>(GitHub)</sub>  |
|---|---|---|---|---|
|Journalisation et détection des menaces |LT-4 |Activer la journalisation pour les ressources Azure |[Les journaux de ressources dans Event Hub doivent être activés](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F83a214f7-d01a-484b-91a9-ed54470c9a6a) |[4.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Event%20Hub/EventHub_AuditDiagnosticLog_Audit.json) |

## <a name="azure-security-benchmark-v1"></a>Azure Security Benchmark v1

Le [benchmark de sécurité Azure](../../../../articles/security/benchmarks/overview.md) fournit des recommandations sur la façon dont vous pouvez sécuriser vos solutions cloud sur Azure. Pour voir comment ce service est entièrement mappé au benchmark de sécurité Azure, consultez les [fichiers de mappage du benchmark de sécurité Azure](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines).

Pour passer en revue la façon dont les composants intégrés Azure Policy disponibles pour tous les services Azure sont mappés à ce standard de conformité, consultez [Conformité réglementaire Azure Policy - Benchmark de sécurité Azure](../../../../articles/governance/policy/samples/azure-security-benchmark.md).

|Domain |ID du contrôle |Titre du contrôle |Policy<br /><sub>(Portail Azure)</sub> |Version de la stratégie<br /><sub>(GitHub)</sub>  |
|---|---|---|---|---|
|Sécurité réseau |1.1 |Protéger les ressources à l'aide de groupes de sécurité réseau ou du Pare-feu Azure sur votre réseau virtuel |[Event Hub doit utiliser un point de terminaison de service de réseau virtuel](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd63edb4a-c612-454d-b47d-191a724fcbf0) |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Network/VirtualNetworkServiceEndpoint_EventHub_AuditIfNotExists.json) |
|Journalisation et supervision |2.3 |Activer la journalisation d’audit pour les ressources Azure |[Les journaux de ressources dans Event Hub doivent être activés](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F83a214f7-d01a-484b-91a9-ed54470c9a6a) |[4.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Event%20Hub/EventHub_AuditDiagnosticLog_Audit.json) |

## <a name="cis-microsoft-azure-foundations-benchmark-130"></a>CIS Microsoft Azure Foundations Benchmark 1.3.0

Pour voir comment les composants intégrés Azure Policy disponibles pour tous les services Azure correspondent à ce standard de conformité, consultez [Conformité réglementaire Azure Policy – CIS Microsoft Azure Foundations Benchmark 1.3.0](../../../../articles/governance/policy/samples/cis-azure-1-3-0.md).
Pour plus d’informations sur cette norme de conformité, consultez [CIS Microsoft Azure Foundations Benchmark](https://www.cisecurity.org/benchmark/azure/).

|Domain |ID du contrôle |Titre du contrôle |Policy<br /><sub>(Portail Azure)</sub> |Version de la stratégie<br /><sub>(GitHub)</sub>  |
|---|---|---|---|---|
|Journalisation et supervision |5.3 |Vérifiez que les journaux de diagnostic sont activés pour tous les services qui le prennent en charge. |[Les journaux de ressources dans Event Hub doivent être activés](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F83a214f7-d01a-484b-91a9-ed54470c9a6a) |[4.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Event%20Hub/EventHub_AuditDiagnosticLog_Audit.json) |

## <a name="hipaa-hitrust-92"></a>HIPAA HITRUST 9.2

Pour voir comment les composants intégrés Azure Policy disponibles pour tous les services Azure correspondent à ce standard de conformité, consultez [Conformité réglementaire Azure Policy – HIPAA HITRUST 9.2](../../../../articles/governance/policy/samples/hipaa-hitrust-9-2.md).
Pour plus d’informations sur cette norme de conformité, consultez [HIPAA HITRUST 9.2](https://www.hhs.gov/hipaa/for-professionals/security/laws-regulations/index.html).

|Domain |ID du contrôle |Titre du contrôle |Policy<br /><sub>(Portail Azure)</sub> |Version de la stratégie<br /><sub>(GitHub)</sub>  |
|---|---|---|---|---|
|Séparation dans les réseaux |0805.01m1Organizational.12 - 01.m |Les passerelles de sécurité de l’organisation (par exemple, les pare-feu) appliquent des stratégies de sécurité et sont configurées pour filtrer le trafic entre les domaines, bloquent l’accès non autorisé et sont utilisées pour assurer la séparation entre les segments de réseaux câblés internes, sans fil internes et externes (par exemple, Internet), y compris les zones DMZ et appliquent des stratégies de contrôle d’accès pour chacun des domaines. |[Event Hub doit utiliser un point de terminaison de service de réseau virtuel](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd63edb4a-c612-454d-b47d-191a724fcbf0) |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Network/VirtualNetworkServiceEndpoint_EventHub_AuditIfNotExists.json) |
|Séparation dans les réseaux |0806.01m2Organizational.12356 - 01.m |Le réseau de l’organisation est logiquement et physiquement segmenté avec un périmètre de sécurité défini et un ensemble de contrôles gradué, notamment des sous-réseaux pour les composants système accessibles publiquement qui sont logiquement séparés du réseau interne, en fonction des exigences de l’organisation ; et le trafic est contrôlé suivant les fonctionnalités requises et la classification des données/systèmes en fonction d’une évaluation des risques et de leurs exigences de sécurité respectives. |[Event Hub doit utiliser un point de terminaison de service de réseau virtuel](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd63edb4a-c612-454d-b47d-191a724fcbf0) |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Network/VirtualNetworkServiceEndpoint_EventHub_AuditIfNotExists.json) |
|Séparation dans les réseaux |0894.01m2Organizational.7 - 01.m |Les réseaux sont séparés des réseaux de niveau production lors de la migration de serveurs physiques, d’applications ou de données vers des serveurs virtualisés. |[Event Hub doit utiliser un point de terminaison de service de réseau virtuel](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd63edb4a-c612-454d-b47d-191a724fcbf0) |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Network/VirtualNetworkServiceEndpoint_EventHub_AuditIfNotExists.json) |
|Journalisation d’audit |1207.09aa2System.4 - 09.aa |Les enregistrements d’audit sont conservés pendant 90 jours, tandis que les enregistrements d’audit plus anciens sont archivés pendant un an. |[Les journaux de ressources dans Event Hub doivent être activés](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F83a214f7-d01a-484b-91a9-ed54470c9a6a) |[4.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Event%20Hub/EventHub_AuditDiagnosticLog_Audit.json) |
|Contrôles réseau |0863.09m2Organizational.910 - 09.m |L’organisation crée une configuration de pare-feu qui limite les connexions entre les réseaux non approuvés et les composants système de l’environnement des informations couvertes ; toutes les modifications apportées à la configuration du pare-feu sont mises à jour dans le diagramme du réseau. |[Event Hub doit utiliser un point de terminaison de service de réseau virtuel](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd63edb4a-c612-454d-b47d-191a724fcbf0) |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Network/VirtualNetworkServiceEndpoint_EventHub_AuditIfNotExists.json) |

