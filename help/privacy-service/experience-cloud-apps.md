---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Applications Privacy Service et Experience Cloud
topic-legacy: overview
description: Ce document fournit une référence pour la configuration de différentes applications Experience Cloud pour les opérations liées à la confidentialité.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
translation-type: tm+mt
source-git-commit: e226990fc84926587308077b32b128bfe334e812
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 58%

---

# [!DNL Privacy Service] et  [!DNL Experience Cloud] applications

Adobe Experience Platform [!DNL Privacy Service] est conçu pour prendre en charge les demandes de confidentialité pour plusieurs applications Adobe Experience Cloud. Chaque application est compatible avec différentes valeurs et différents identifiants de produit pour l’identification des titulaires de données.

Ce document sert de référence à la documentation de l&#39;application [!DNL Experience Cloud] qui décrit comment configurer cette application pour des opérations liées à la confidentialité. Cela inclut les formats et les libellés de vos données. Deux catégories d’applications sont traitées :

* [Applications intégrées au Privacy Service](#integrated) : Applications capables d’envoyer des demandes d’accès, de suppression ou d’exclusion à  [!DNL Privacy Service].
* [Les applications en libre-service](#self-serve)[!DNL Privacy Service] : ce sont des applications qui doivent gérer leurs requêtes de confidentialité en interne et qui ne peuvent pas communiquer directement avec 

Consultez la documentation de vos applications [!DNL Experience Cloud] pour savoir comment formater vos demandes de confidentialité et quelles valeurs sont prises en charge pour ces demandes.

## Applications intégrées à [!DNL Privacy Service] {#integrated}

Vous trouverez ci-dessous une liste d&#39;applications [!DNL Experience Cloud] intégrées à [!DNL Privacy Service], y compris les fonctionnalités [!DNL Privacy Service] avec lesquelles elles sont compatibles, et des liens vers la documentation pour plus d&#39;informations.

| Application | Accès/suppression | Opposition | Documentation et considérations |
| --- | :---: | :---: | --- |
| Adobe Advertising Cloud | ✓ | obj | <ul><li>[Accès/suppression de la documentation pour GDPR](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Accès/suppression de la documentation de l’ACPCP](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Documentation sur l’exclusion de la vente pour l’ACFPC](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | obj | obj | <ul><li>[Documentation sur l’accès et la suppression](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>[!DNL Analytics] gère les requêtes d’opposition à l’aide de [variables de reporting sur la confidentialité](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/consent-variables.html).</li></ul> |
| Adobe Audience Manager | obj | obj | <ul><li>[Documentation sur l’accès et la suppression](https://docs.adobe.com/content/help/fr-FR/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentation sur l’opposition](https://docs.adobe.com/content/help/fr-FR/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | obj | obj | <ul><li>[Documentation sur l’accès et la suppression](https://docs.campaign.adobe.com/doc/standard/getting_started/fr/ACS_GDPR.html)</li><li>[Documentation sur l’opposition](../segmentation/honoring-opt-outs.md)</li></ul> |
| Attributs du client Adobe (CRS) | obj | N/A | <ul><li>[Accès/suppression de la documentation pour GDPR](https://docs.adobe.com/content/help/fr-FR/core-services/interface/customer-attributes/gdpr.html)</li><li>[Accès/suppression de la documentation de l’ACPCP](https://docs.adobe.com/content/help/fr-FR/core-services/interface/customer-attributes/ccpa.html)</li><li>Les attributs du client n’ont pas la capacité de transférer des données. Par conséquent, les demandes d’exclusion de la vente ne sont pas applicables.</li></ul> |
| Adobe Experience Platform | obj | obj | <ul><li>[Documentation sur l’accès et la suppression pour le lac de données](../catalog/privacy.md)</li><li>[Documentation sur l’accès et la suppression pour Real-time Customer Profile](../profile/privacy.md)</li><li>[!DNL Experience Platform] honore les demandes d’ [exclusion pour les segments](../segmentation/honoring-opt-outs.md) d’audience.</li></ul> |
| Adobe Primetime Authentication | obj | S/O | <ul><li>[Documentation sur l’accès et la suppression](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] n’a pas la capacité de transférer des données. Par conséquent, les requêtes d’opposition ne sont pas applicables.</li></ul> |
| Adobe Target | obj | S/O | <ul><li>[Documentation sur l’accès et la suppression](https://docs.adobe.com/content/help/fr-FR/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] n’a pas la capacité de transférer des données. Par conséquent, les requêtes d’opposition ne sont pas applicables.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Applications en libre-service {#self-serve}

Vous trouverez ci-dessous une liste d&#39;applications [!DNL Experience Cloud] qui ne sont pas intégrées à [!DNL Privacy Service] et qui doivent gérer leurs problèmes de confidentialité en interne. Vous trouverez des liens vers la documentation de chaque application, ainsi qu’une description du contenu de la documentation.

| Application | Description de la documentation |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/FR/ACC_GDPR.html) | Présentation des fonctionnalités relatives au RGPD pour Adobe Campaign Classic. |
| [Adobe Dynamic Tag Manager](https://docs.adobe.com/content/help/fr-FR/dtm/using/tools/opt-in.html) | Étapes pour empêcher le déclenchement des balises Adobe jusqu’à l’obtention du consentement. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | Présentation de la gestion des requêtes RGPD par l’administrateur de la confidentialité client ou l’administrateur AEM. |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Étapes pour créer des requêtes RGPD d’accès et de suppression à l’aide de Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Comment les développeurs peuvent-ils utiliser les extensions et le créateur de règles pour définir les solutions d’accords préalables et de droits d’opposition ? |

{style=&quot;table-layout:auto&quot;}
