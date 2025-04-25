---
product: adobe experience platform
solution: Real-Time Customer Data Platform
audience: user
user-guide-title: Guide de Real-Time Customer Data Platform
user-guide-description: Regroupez les données connues et anonymes provenant de plusieurs entreprises sources afin de créer des profils clients, puis des audiences à partir de ces profils et enfin d’activer ces segments vers des destinations tierces.
role: Admin
source-git-commit: ba2154e84f24ddf4ec270121bdcbb6dd5d3dff42
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 62%

---


# Aide sur Real-Time Customer Data Platform {#rtcdp}

* [Documentation de Real-Time CDP](home.md)
* Commencer {#intro}
   * Real-Time CDP {#rtcdp-intro}
      * [Présentation de Real-Time CDP](overview.md)
      * [Commencer avec Real-Time CDP](get-started.md)
      * [Page d’accueil](home-page-dashboards.md)
   * Édition B2B de Real-Time CDP {#rtcdpb2b-intro}
      * [Présentation de l’édition B2B de Real-Time CDP](b2b-overview.md)
      * [Exemple de cas d’utilisation](./b2b-use-case.md)
      * [Tutoriel de bout en bout](./b2b-tutorial.md)
      * [Barrières de sécurité de l’édition B2B de Real-Time CDP](b2b-guardrails.md)
* Audience Manager et Real-Time CDP {#evolution}
   * [Évolution à partir d’Audience Manager](aam-to-rtcdp.md)
* Profils de compte {#account}
   * [Présentation des profils de compte](accounts/account-profile-overview.md)
   * [Guide de l’interface utilisateur des profils de compte](accounts/account-profile-ui-guide.md)
* Administration {#admin}
   * [Présentation de l’administration](administration/admin-overview.md)
* Audiences et segmentation {#segmentation}
   * [Présentation de la segmentation](segmentation/segmentation-overview.md)
   * [Guide d’Audience Builder](segmentation/audience-builder.md)
   * [Segmentation dans l’édition B2B de Real-Time CDP](segmentation/b2b.md)
   * [IA dédiée aux clients](segmentation/customer-ai.md)
* Jeux de données {#datasets}
   * [Jeux de données](datasets/dataset.md)
   * [Qualité des données dans Experience Platform](datasets/data-quality.md)
* Destinations {#destinations}
   * [Présentation des destinations](destinations/overview.md)
   * [Destinations dans l’édition B2B de Real-Time CDP](destinations/b2b.md)
* Mécanismes de sécurisation {#guardrails}
   * [Présentation des mécanismes de sécurisation de Real-Time CDP](guardrails/overview.md)
   * [Mécanismes de sécurisation pour l’ingestion de données](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html){target="_blank"}
   * [Mécanismes de sécurisation pour  [!DNL Edge Network API]](https://developer.adobe.com/data-collection-apis/docs/getting-started/guardrails/){target="_blank"}
   * [Mécanismes de sécurisation pour  [!DNL Real-Time Customer Profile]  données et la segmentation](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=fr){target="_blank"}
   * [Mécanismes de sécurisation pour  [!DNL Identity Service]  données](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html){target="_blank"}
   * [Mécanismes de sécurisation pour  [!DNL Query Service]](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html){target="_blank"}
   * [Mécanismes de sécurisation pour l’activation des données via les destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html){target="_blank"}
* Identités {#identity}
   * [Identités et espaces de noms d’identité](profile/identities-overview.md)
* Politiques de fusion {#merge-policies}
   * [Présentation des politiques de fusion](profile/merge-policies.md)
* Confidentialité et gouvernance des données {#privacy}
   * [Présentation de la confidentialité](privacy/privacy-overview.md)
   * [Présentation de la gouvernance des données](privacy/data-governance-overview.md)
* Profils {#profile}
   * [Présentation des profils](profile/profile-overview.md)
   * [Parcourir les profils](profile/profile-browse.md)
* Services d’IA/ML de Real-Time CDP B2B edition {#b2b-cdp-ai-ml}
   * [Comptes associés](b2b-ai-ml-services/related-accounts.md)
   * [Correspondance du prospect et du compte](b2b-ai-ml-services/lead-to-account-matching.md)
   * Notation prédictive des prospects et des comptes {#predictive-lead-and-account-scoring-intro}
      * [Présentation de la notation prédictive des prospects et des comptes](b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
      * [Gérer la notation prédictive des prospects et des comptes](b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md)
* Schémas {#schemas}
   * [Présentation des schémas](schemas/overview.md)
   * [Schémas dans l’édition B2B de Real-Time CDP](schemas/b2b.md)
* Sources {#sources}
   * [Présentation des sources](sources/sources-overview.md)
   * [Sources dans l’édition B2B de Real-Time CDP](sources/b2b.md)
* Cas d’utilisation {#use-cases}
   * [Présentation d’exemples de cas d’utilisation](/help/rtcdp/use-case-guides/overview.md)
   * Acquisition des clients {#customer-acquisition}
      * [Interagir et acquérir de nouveaux clients sans dépendre de cookies tiers](/help/rtcdp/partner-data/prospecting.md)
      * [Personnaliser des expériences sur site pour les visiteurs inconnus à l’aide de la reconnaissance des visiteurs assistée par des partenaires](/help/rtcdp/partner-data/onsite-personalization.md)
      * [Reciblage hors site d’utilisateurs non authentifiés](./partner-data/offsite-retargeting.md)
      * [Reciblage côté serveur non authentifié](./partner-data/unauthenticated-retargeting.md)
   * Enrichissement du profil {#profile-enrichment}
      * [Complémenter les profils propriétaires avec des attributs fournis par le partenaire](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
   * Informations personnalisées et engagement {#personalization-insights-engagement}
      * [Faire évoluer la valeur client unique vers la valeur de durée de vie](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/evolve-one-time-value-to-lifetime-value.md)
      * [Réengager intelligemment vos clients](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)
      * [Rétablir l’engagement de vos clients de manière intelligente : exemples Luma](/help/rtcdp/use-case-guides/intelligent-re-engagement/use-cases-luma.md)
* [Notes de mise à jour d’Experience Platform](https://experienceleague.adobe.com/fr/docs/experience-platform/release-notes/latest)
* [Glossaire Experience Platform](https://docs.adobe.com/content/help/fr-FR/experience-platform/landing/glossary.html)