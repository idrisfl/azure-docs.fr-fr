---
title: Fonctionnalités de transaction de la place de marché commerciale de Microsoft
description: Cet article décrit les considérations sur les prix, la facturation et le paiement pour l’option de transaction de la place de marché commerciale.
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: conceptual
ms.date: 04/06/2021
ms.author: mingshen
author: mingshen-ms
ms.openlocfilehash: 0a25e1b50455cad5bdbe5b76b2a291f2a1c11940
ms.sourcegitcommit: 5f482220a6d994c33c7920f4e4d67d2a450f7f08
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/08/2021
ms.locfileid: "107107004"
---
# <a name="commercial-marketplace-transact-capabilities"></a>Fonctionnalités de transaction de la place de marché commerciale

Cet article décrit les considérations sur les prix, la facturation et le paiement pour la place de marché commerciale de Microsoft.

## <a name="transactions-by-listing-option"></a>Transactions par option de liste

Il incombe à l’éditeur ou à Microsoft de gérer les transactions de licences logicielles pour les offres de la place de marché commerciale. L’option de liste que vous choisissez pour votre offre détermine qui gère la transaction. Pour obtenir la disponibilité de chaque option de publication et obtenir des explications à son sujet, consultez [Présentation des options de référencement](determine-your-listing-type.md).

### <a name="contact-me-free-trial-and-byol-options"></a>Me contacter, version d’évaluation gratuite et options BYOL

Les éditeurs peuvent choisir les options _Me contacter_ et _Évaluation gratuite_, à des fins de promotion et d’acquisition d’utilisateurs. Pour certains types d’offre, les éditeurs peuvent choisir l’option _BYOL_ (apportez votre propre licence) pour permettre aux clients d’acheter un abonnement associé à votre offre à l’aide d’une licence qu’ils ont achetée directement. Avec ces options, Microsoft ne participe pas directement aux transactions de licence logicielle des éditeurs et ne facture rien sur ces transactions, afin que les éditeurs puissent conserver l’ensemble de ces revenus.

Grâce à ces options, les éditeurs sont responsables de la prise en charge de tous les aspects de la transaction de licence logicielle. Cela comprend, entre autres, la commande, la réalisation, le contrôle, la facturation, le paiement et la collecte. Avec les options de liste et Me contacter, les éditeurs conservent 100 % du montant collecté auprès du client en paiement des frais de licence logicielle.

### <a name="transact-publishing-option"></a>Option de publication Transaction

Le choix de vendre via le réseau Microsoft tire parti des fonctionnalités de transactions commerciales de Microsoft et fournit une expérience de bout en bout, de la découverte et l’évaluation à l’achat et l’implémentation. Une offre _pouvant faire l’objet d’une transaction_ est une offre en lien avec laquelle Microsoft facilite l’échange d’argent contre une licence logicielle au nom de l’éditeur. Les offres de transaction sont facturées en fonction d’un abonnement Microsoft existant ou sur une carte de crédit, ce qui permet à Microsoft d’héberger des transactions de la place de marché dans le cloud pour le compte de l’éditeur.

Vous choisissez l’option de transaction au moment de la création d’une offre dans l’Espace partenaires. Cette option s’affiche seulement si la transaction est disponible pour votre type d’offre.

## <a name="transact-overview"></a>Présentation de l’option Transaction

Lorsque vous choisissez l’option Transaction, Microsoft permet la vente de logiciels tiers et le déploiement de certains types d’offres dans l’abonnement Azure du client. Pour choisir le modèle de tarification d’une offre, l’éditeur doit prendre en compte la facturation des frais d’infrastructure et ses propres frais de licence logicielle.

L’option de publication Transaction est actuellement disponible pour ces types d’offres :

| Type d’offre | Cadence de facturation | Facturation à l’usage | Modèle de tarification |
| ------------ | ------------- | ------------- | ------------- |
| Azure Application<br>(Application managée) | Mensuelle | Oui | Basés sur l’utilisation |
| Machine virtuelle Azure | Mensuellement * | Non | Basé sur l’utilisation, BYOL |
| SaaS (software as a service) | Mensuelle et annuelle | Oui | Tarification fixe, par utilisateur, basée sur l’utilisation. |
|||||

`*` La machine virtuelle Azure offre une prise en charge des plans de facturation basés sur l’utilisation. Ces plans sont facturés mensuellement pour l’utilisation horaire de l’abonnement en fonction de l’utilisation par cœur, par taille de cœur, ou par marché et par taille de cœur.

### <a name="metered-billing"></a>Facturation à l’usage

Le _service de mesure de la Place de marché_ vous permet de spécifier des frais de paiement à l’utilisation (basés sur la consommation) en plus des frais mensuels ou annuels inclus dans le contrat (droit d’utilisation). Vous pouvez facturer les coûts d’utilisation selon les dimensions du service de mesure de la Place de marché que vous spécifiez, telles que la bande passante, les tickets ou les e-mails traités. Pour plus d’informations sur la facturation à l’usage pour les offres SaaS, consultez [Facturation à l’usage pour SaaS à l’aide du service de mesure de la consommation de la Place de marché commerciale](./partner-center-portal/saas-metered-billing.md). Pour plus d’informations sur la facturation à l’usage pour les offres Azure Application, consultez la page [Facturation des applications managées basée sur des mesures](./partner-center-portal/azure-app-metered-billing.md).

### <a name="billing-infrastructure-costs"></a>Facturation des coûts d’infrastructure

Pour les **machines virtuelles** et les **applications Azure**, des frais d’utilisation de l’infrastructure Azure sont facturés sur l’abonnement Azure du client. Ils sont détaillés et présentés séparément des frais de licence logicielle du fournisseur sur la facture du client.

Pour les offres **Applications SaaS**, l’éditeur doit regrouper les frais d’utilisation de l’infrastructure Azure et les frais de licence logicielle dans le même élément de coût. Ils font facturés au client selon un tarif fixe. L’utilisation de l’infrastructure Azure est présentée et facturée directement à l’éditeur. Les frais réels d’utilisation de l’infrastructure ne sont pas visibles par le client. Les éditeurs choisissent généralement d’inclure les frais d’utilisation de l’infrastructure Azure dans leurs tarifs de licence logicielle. Les frais de licence des logiciels ne sont pas mesurés ni basés sur la consommation des utilisateurs.

## <a name="pricing-models"></a>Modèles tarifaires

Selon l’option Transaction choisie, les frais d’abonnement se présentent ainsi :

- **Obtenir maintenant (gratuit)**  : aucuns frais ne sont facturés pour les licences logicielles. Les offres gratuites ne peuvent pas être converties en offre payante. Les clients doivent commander une offre payante.
- **BYOL** (Bring your own license) : si une offre est répertoriée dans la Place de marché commerciale, les frais applicables aux licences logicielles sont gérés directement entre le serveur de publication et le client. Microsoft facture uniquement les frais d’utilisation de l’infrastructure Azure applicables au compte d’abonnement Azure du client.
- **Tarification par abonnement** : les frais de licence logicielle sont facturés mensuellement ou annuellement dans le cadre d’un abonnement selon un tarif fixe ou par poste. Les frais d’abonnement récurrents ne sont pas calculés au prorata en cas d’annulation en cours de trimestre ou en cas de services non utilisés. Les frais d’abonnement réactualisés peuvent être facturés au prorata si le client met à niveau ou rétrograde son abonnement au milieu de la durée de l’abonnement.
- **Tarification basée sur l’utilisation** : pour les offres de machines virtuelles Azure, les clients sont facturés en fonction de l’étendue de leur utilisation de l’offre. Pour les images Machines Virtuelles, les frais Place de marché Azure facturés aux clients sont basés sur l’utilisation réelle des machines virtuelles déployées à partir de ces images de machine virtuelle, selon un tarif horaire convenu par les éditeurs. Le tarif horaire peut être fixe ou variable en fonction de la taille des machines virtuelles. Les heures non terminées sont facturées à la minute. Les plans sont facturés tous les mois.
- **Tarification limitée** : pour les offres Azure Application et les offres SaaS, les éditeurs peuvent utiliser le [service de mesure de la place de marché Microsoft Azure](./partner-center-portal/marketplace-metering-service-apis.md) pour facturer la consommation en fonction des dimensions de mesure personnalisées qu’ils configurent. Ces modifications s’ajoutent aux frais mensuels ou annuels inclus dans le contrat (droit d’utilisation). Exemples de dimensions de mesure personnalisée : bande passante, tickets ou e-mails. Les éditeurs peuvent définir une ou plusieurs dimensions mesurables pour chaque plan, avec un maximum de 30 par offre. Les éditeurs sont chargés d’effectuer le suivi personnel de l’utilisation pour chaque mesure définie dans l’offre. Les événements doivent être signalés à Microsoft dans un délai d’une heure. Celui-ci facture ensuite les clients en fonction des informations collectées par les éditeurs pour la période de facturation applicable.
- **Essai gratuit** : gratuit pour les licences logicielles dont la durée varie entre 30 jours et six mois, selon le type d’offre. Si les éditeurs proposent une version d’évaluation gratuite de plusieurs plans au sein de la même offre, les clients peuvent passer à une version d’évaluation gratuite sur un autre plan, mais la période d’évaluation ne redémarre pas. Pour les offres de machines virtuelles, les clients sont facturés aux coûts d’infrastructure Azure pour l’utilisation de l’offre pendant une période d’évaluation gratuite. À l’expiration de la période d’évaluation, les clients sont facturés automatiquement pour le dernier plan qu’ils ont essayé en fonction des tarifs standard, sauf s’ils annulent avant la fin de la période d’évaluation.

> [!NOTE]
> Les offres qui sont facturées en fonction de la consommation après l’utilisation d’une solution ne sont pas éligibles à un remboursement.

Les éditeurs qui souhaitent modifier les frais d’utilisation associés à une offre doivent tout d’abord supprimer l’offre (ou le plan spécifique de l’offre) de la place de marché commerciale. Cette suppression doit se faire conformément aux dispositions du [Contrat d’Éditeur Microsoft](https://go.microsoft.com/fwlink/?LinkID=699560). L’éditeur peut ensuite publier une nouvelle offre (ou un plan intégré à une offre) avec les nouveaux frais d’utilisation. Pour plus d’informations sur la suppression d’une offre ou d’un plan, consultez [Arrêter la vente d’une offre ou d’un plan](./partner-center-portal/update-existing-offer.md#stop-selling-an-offer-or-plan).

### <a name="free-contact-me-and-bring-your-own-license-byol-pricing"></a>Options tarifaires Gratuit, Me contacter et BYOL (apportez votre propre licence)

Quand vous publiez une offre Transaction avec l’option Obtenir maintenant (gratuit), Me contacter ou BYOL (apportez votre propre licence), Microsoft n’intervient pas pour faciliter la transaction des ventes pour vos frais de licence logicielle. L’éditeur conserve 100 % des frais de licence logicielle.

### <a name="usage-based-and-subscription-pricing"></a>Tarification basée sur l’utilisation et les abonnements

Quand vous publiez une offre basée sur l’utilisateur ou une transaction d’abonnement, Microsoft fournit la technologie et les services nécessaires pour traiter les achats, retours et rétrofacturations des licences logicielles. Dans ce scénario, l’éditeur autorise Microsoft à agir en tant qu’agent. L’éditeur permet à Microsoft de faciliter la transaction de gestion des licences logicielles. L’éditeur conserve votre désignation en tant que vendeur, fournisseur, distributeur et concédant de licence.

Microsoft permet aux clients de commander, d’acquérir sous licence et d’utiliser votre logiciel selon les conditions générales de la place de marché commerciale Microsoft et de votre contrat de licence utilisateur final. Vous êtes tenu de fournir votre contrat de licence utilisateur final ou de sélectionner le [contrat Standard](./standard-contract.md) lors de la création de l’offre.

### <a name="free-software-trials"></a>Essai logiciel gratuit

Dans les scénarios de publication d’offres Transaction, vous pouvez proposer gratuitement une licence logicielle pendant une période de 30 ou 120 jours selon l’abonnement. Les clients seront modifiés pour l’utilisation de l’infrastructure Azure applicable.

### <a name="examples-of-pricing-and-store-fees"></a>Exemples de tarifs et de frais de stockage

**Basés sur l’utilisation**

La tarification basée sur l’utilisation présente la structure de coûts suivante :

| **Coût de votre licence** | **1 $/heure** |
|---------|---------|
| Coût d’utilisation Azure (D1/1 cœur) | 0,14 $/heure |
| _Microsoft facture au client le montant suivant :_ | _1,14 $/heure_ |
||

Dans ce scénario, Microsoft facture 1,14 $ l’heure d’utilisation de votre image de machine virtuelle publiée.

| **Microsoft facture** | **1,14 $/heure**  |
|---------|---------|
| Microsoft vous verse 80 % des revenus générés par les licences | 0,80 $/heure |
| Microsoft conserve 20 % des revenus générés par les licences  |  0,20 $/heure |
| Microsoft conserve 100 % des revenus générés par l’utilisation d’Azure | 0,14 $/heure |
||

**BYOL (apportez votre propre licence)**

L’option BYOL a la structure de coûts suivante :

| **Coût de votre licence** | **Frais de licence négociés et facturés par vos soins** |
|---------|---------|
|Coût d’utilisation Azure (D1/1 cœur)    |   0,14 $/heure     |
| _Microsoft facture au client le montant suivant :_ | _0,14 $/heure_ |
||

Dans ce scénario, Microsoft facture 0,14 $ l’heure d’utilisation de votre image de machine virtuelle publiée.

| **Microsoft facture** | **0,14 $/heure** |
|---------|---------|
| Microsoft conserve les revenus générés par l’utilisation Azure | 0,14 $/heure |
| Microsoft conserve 0 % des revenus générés par les licences | 0 $/heure |
||

**Abonnement Application SaaS**

Les abonnements SaaS peuvent être tarifés selon une tarification fixe ou par utilisateur sur une base mensuelle ou annuelle. Si vous activez l’option **Vendre via Microsoft** pour une offre SaaS, vous obtenez la structure de coûts suivante :

| **Coût de votre licence** | **100 $/mois** |
|--------------|---------|
| Coût d’utilisation Azure (D1/1 cœur) | Facturé directement à l’éditeur au lieu du client |
| _Microsoft facture au client le montant suivant :_ | _100 $/mois (l’éditeur doit inclure les coûts d’infrastructure encourus ou transmis dans les frais de licence)_ |
||

Dans ce scénario, Microsoft facture 100 $ pour votre licence logicielle et vous paie 80 € ou 90 € , selon que l’offre est éligible ou non à une réduction des frais de service en magasin.

| **Microsoft facture** | **100 $/mois** |
|---------|---------|
| Microsoft vous verse 80 % des revenus générés par les licences <br> \* Microsoft paie 90 % de vos coûts de licence pour les applications SaaS qualifiées | 80 $/mois <br> \* 90 $/mois |
| Microsoft conserve 20 % des revenus générés par les licences <br> \* Microsoft conserve 10 % de vos coûts de licence pour les applications SaaS qualifiées | 20 $/mois <br> \* 10 $ |

### <a name="commercial-marketplace-service-fees"></a>Frais de service de la Place de marché commerciale

Nous facturons un tarif de 20 % pour le service de magasin standard quand les clients achètent votre offre à partir de la Place de marché commerciale. Pour plus d’informations sur ces frais, consultez la section 5c du [Contrat de l’éditeur Microsoft](https://go.microsoft.com/fwlink/?LinkID=699560).

Pour certaines offres de transaction que vous publiez sur la Place de marché commerciale, vous pouvez bénéficier d’un tarif de service de magasin réduit de 10 %. Pour que votre offre soit éligible, elle doit avoir été désignée par Microsoft comme étant une _offre de co-vente Azure IP incitative_. L’éligibilité doit être respectée pendant au moins cinq jours ouvrés avant la fin de chaque mois civil pour bénéficier des frais de service réduits sur le marketplace. Une fois le droit d’éligibilité atteint, les frais de service réduits sont accordés à toutes les transactions effectives le premier jour du mois suivant jusqu’à ce que l’état de la _co-vente d’Azure IP encouragés_ soit perdu. Pour plus d’informations sur l’éligibilité à la co-vente IP, consultez [Prérequis relatifs à l’état de co-vente](/legal/marketplace/certification-policies#3000-requirements-for-co-sell-status).

Les frais de service réduits de la Place de marché s’appliquent aux offres SaaS de co-vente Azure IP incitatives, aux machines virtuelles, aux applications managées et à toutes les autres solutions IaaS payantes éligibles qui sont mises à disposition via la Place de marché commerciale. Les offres SaaS payantes associées à une application Microsoft Teams ou au moins deux compléments Microsoft 365 (Excel, PowerPoint, Word, Outlook et SharePoint) et publiées sur Microsoft AppSource peuvent également bénéficier de cette remise.

### <a name="customer-invoicing-payment-billing-and-collections"></a>Tarification, paiement, facturation et collecte côté client

**Facturation et paiement** : vous pouvez appliquer la méthode de facturation par défaut du client pour présenter les frais de licence logicielle avec abonnement ou [paiement à l’utilisation](https://azure.microsoft.com/pricing/purchase-options/pay-as-you-go/).

**Contrat Entreprise** : si la méthode de facturation par défaut du client est un Contrat Entreprise Microsoft, les frais de licence logicielle sont facturés selon cette méthode et présentés de manière détaillée et séparée des coûts propres à l’utilisation d’Azure.

**Cartes de crédit et facture mensuelle** : les clients peuvent payer à l’aide d’une carte de crédit et d’une facture mensuelle. Dans ce cas, vos frais de licence logicielle sont facturés comme dans le scénario du Contrat Entreprise, c’est-à-dire de manière détaillée et séparée des coûts de l’utilisation d’Azure.

**Crédits gratuits et engagement financier** : certains clients choisissent de prépayer l’utilisation d’Azure avec un engagement financier dans le Contrat Entreprise, ou ont obtenu des crédits gratuits à utiliser avec Azure. Ces crédits peuvent servir à payer l’utilisation d’Azure, mais pas les frais de licence logicielle de l’éditeur.

**Facturation et collections** : les licences logicielles des éditeurs sont facturées avec la méthode de facturation choisie par le client et selon le calendrier de facturation établi. Les clients sans Contrat Entreprise sont facturés au mois pour les licences logicielles de la Place de marché. Les clients ayant un Contrat Entreprise sont facturés au mois, mais reçoivent une seule facture par trimestre.

Quand les modèles tarifaires Abonnement ou Paiement à l'utilisation sont sélectionnés, Microsoft agit en tant qu’agent de l’éditeur et est responsable de tous les aspects de la facturation, du paiement et de la collecte.

### <a name="publisher-payout-and-reporting"></a>Paiement de l’éditeur et rapports

Les frais de licence logicielle collectés par Microsoft en tant qu’agent sont soumis à des frais de transaction de 20 %, sauf indication contraire, et sont déduits du moment payé à l’éditeur.

Les clients achètent généralement avec un Contrat Entreprise, ou par carte de crédit dans le cadre d’un contrat de paiement à l’utilisation. Le type de contrat détermine la tarification, la facturation, la collecte et le calendrier de paiement.

>[!NOTE]
>Tous les rapports et insights associés à l’option de publication Transaction sont disponibles dans la section Analytiques de l’Espace partenaires.

#### <a name="billing-questions-and-support"></a>Questions et support sur la facturation

Pour obtenir plus d’informations et connaître les règles juridiques, consultez le [Contrat d’éditeur Microsoft](https://go.microsoft.com/fwlink/?LinkID=699560). Pour obtenir de l’aide sur les questions de facturation, contactez le [support de l’éditeur de la place de marché commerciale](https://aka.ms/marketplacepublishersupport).

## <a name="transact-requirements"></a>Exigences relatives aux offres Transaction

Cette section décrit la configuration requise pour les différents types d’offres.

### <a name="requirements-for-all-offer-types"></a>Exigences applicables à tous les types d’offres

- Un compte Microsoft et des informations financières sont requis pour l’offre de publication Transaction, quel que soit son modèle de tarification.
- Les informations financières obligatoires comprennent un compte de paiement et un profil fiscal.

Pour plus d’informations sur la configuration de ces comptes, consultez [Gestion de votre compte de la place de marché commerciale dans l’Espace partenaires](manage-account.md).

### <a name="requirements-for-specific-offer-types"></a>Exigences applicables à certains types d’offres

La possibilité d’effectuer des transactions par le biais de Microsoft est disponible uniquement pour les types d’offres de la place de marché commerciale. Cette liste indique les conditions requises pour que ces types d’offre puissent faire l’objet d’une transaction dans la place de marché commerciale.

- **L’application Azure (modèle de solution et plans d’application managée)**  : dans certains cas, les frais d’utilisation de l’infrastructure Azure sont dissociés des frais de licence logicielle, mais ils sont présentés au client sur la même facture. Toutefois, si vous configurez un plan d’application managée pour les frais d’infrastructure ISV, les ressources Azure sont facturées à l’éditeur et le client se voit présenter un tarif fixe incluant le coût de l’infrastructure, des licences logicielles et des services de gestion.

- **Machine virtuelle Azure** : sélectionner entre les modèles de facturation gratuits, BYOL ou basés sur l’utilisation. Sur la facture Azure du client, Microsoft présente les frais de licence logicielle de l’éditeur séparément des frais d’infrastructure Azure sous-jacents. Les frais d’utilisation de l’infrastructure Azure sont occasionnés par l’utilisation du logiciel de l’éditeur.

- **Application SaaS** : il doit s’agir d’une solution multilocataire, qui utilise [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) pour l’authentification et s’intègre aux [API d’approvisionnement SaaS](partner-center-portal/pc-saas-fulfillment-api-v2.md). L’utilisation de l’infrastructure Azure est gérée et vous est facturée directement (en tant qu’éditeur). Vous devez donc considérer ces frais et les frais de licence logicielle comme un seul poste de coût. Pour plus d’informations, consultez [Comment planifier une offre SaaS pour la place de marché commerciale](plan-saas-offer.md#plans).

## <a name="private-plans"></a>Plans privés

Vous pouvez créer un plan privé pour une offre, compléter avec une tarification négociée et spécifique à l’offre ou des configurations personnalisées.

Les plans privés vous permettent de fournir des tarifs supérieurs ou inférieurs à des clients spécifiques par rapport à l’offre publiquement disponible. Les plans privés permettent d’appliquer une remise ou d’ajouter un supplément à une offre. Ils peuvent être proposés à un ou plusieurs clients en mentionnant leur abonnement Azure au niveau de l’offre.

## <a name="next-steps"></a>Étapes suivantes

- Passez en revue les modèles de publication par magasin en ligne pour obtenir des exemples sur la manière dont votre solution correspond à un type d’offre et à une configuration.
- [Guide de publication par type d’offre](publisher-guide-by-offer-type.md).
