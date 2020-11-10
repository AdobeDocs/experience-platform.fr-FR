---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Applications Privacy Service et Experience Cloud
topic: overview
translation-type: tm+mt
source-git-commit: 4cd7b9d3ca542c2fba83d066197b92775c053729
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 62%

---


# [!DNL Privacy Service] et les [!DNL Experience Cloud] applications

Adobe Experience Platform [!DNL Privacy Service] is built to support privacy requests for several Adobe Experience Cloud applications. Chaque application est compatible avec différentes valeurs et différents identifiants de produit pour l’identification des titulaires de données.

This document serves as a reference for [!DNL Experience Cloud] application documentation that outlines how to configure that application for privacy-related operations. Cela inclut les formats et les libellés de vos données. Deux catégories d’applications sont traitées :

* [Applications intégrées au Privacy Service](#integrated): Applications capables d’envoyer des demandes d’accès, de suppression ou d’exclusion à [!DNL Privacy Service].
* [Les applications en libre-service](#self-serve)[!DNL Privacy Service] : ce sont des applications qui doivent gérer leurs requêtes de confidentialité en interne et qui ne peuvent pas communiquer directement avec 

Please review the documentation for your [!DNL Experience Cloud] applications to learn how to format your privacy requests, and which values are supported for those requests.

## Applications integrated with [!DNL Privacy Service] {#integrated}

The following is a list of [!DNL Experience Cloud] applications that are integrated with [!DNL Privacy Service], including the [!DNL Privacy Service] capabilities they are compatible with, and links to documentation for more information.

| Application | Accès/suppression | Opposition | Documentation et considérations |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[Accès/suppression de la documentation pour GDPR](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Accès/suppression de la documentation de l’ACPCP](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Documentation sur l’exclusion de la vente pour l’ACFPC](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[Documentation sur l’accès et la suppression](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>[!DNL Analytics] gère les requêtes d’opposition à l’aide de [variables de reporting sur la confidentialité](https://docs.adobe.com/content/help/fr-FR/analytics/admin/data-governance/consent-variables.html).</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[Documentation sur l’accès et la suppression](https://docs.adobe.com/content/help/fr-FR/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentation sur l’opposition](https://docs.adobe.com/content/help/fr-FR/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[Documentation sur l’accès et la suppression](https://docs.campaign.adobe.com/doc/standard/getting_started/fr/ACS_GDPR.html)</li><li>[Documentation sur l’opposition](../segmentation/honoring-opt-outs.md)</li></ul> |
| Attributs du client Adobe (CRS) | ✓ | N/A | <ul><li>[Accès/suppression de la documentation pour GDPR](https://docs.adobe.com/content/help/fr-FR/core-services/interface/customer-attributes/gdpr.html)</li><li>[Accès/suppression de la documentation de l’ACPCP](https://docs.adobe.com/content/help/fr-FR/core-services/interface/customer-attributes/ccpa.html)</li><li>Les attributs du client n’ont pas la capacité de transférer des données. Par conséquent, les demandes d’exclusion de la vente ne sont pas applicables.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Documentation sur l’accès et la suppression pour le lac de données](../catalog/privacy.md)</li><li>[Documentation sur l’accès et la suppression pour Real-time Customer Profile](../profile/privacy.md)</li><li>[!DNL Experience Platform] honore les demandes d’ [exclusion pour les segments](../segmentation/honoring-opt-outs.md)d’audience.</li></ul> |
| Adobe Primetime Authentication | ✓ | N/A | <ul><li>[Documentation sur l’accès et la suppression](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] n’a pas la capacité de transférer des données. Par conséquent, les requêtes d’opposition ne sont pas applicables.</li></ul> |
| Adobe Target | ✓ | N/A | <ul><li>[Documentation sur l’accès et la suppression](https://docs.adobe.com/content/help/fr-FR/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] n’a pas la capacité de transférer des données. Par conséquent, les requêtes d’opposition ne sont pas applicables.</li></ul> |


## Applications en libre-service {#self-serve}

The following is a list of [!DNL Experience Cloud] applications that are not integrated with [!DNL Privacy Service] and must manage their privacy concerns internally. Vous trouverez des liens vers la documentation de chaque application, ainsi qu’une description du contenu de la documentation.

| Application | Description de la documentation |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/FR/ACC_GDPR.html) | Présentation des fonctionnalités relatives au RGPD pour Adobe Campaign Classic. |
| [Adobe Dynamic Tag Manager](https://docs.adobe.com/content/help/fr-FR/dtm/using/tools/opt-in.html) | Étapes pour empêcher le déclenchement des balises Adobe jusqu’à l’obtention du consentement. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | Présentation de la gestion des requêtes RGPD par l’administrateur de la confidentialité client ou l’administrateur AEM. |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Étapes pour créer des requêtes RGPD d’accès et de suppression à l’aide de Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Comment les développeurs peuvent-ils utiliser les extensions et le créateur de règles pour définir les solutions d’accords préalables et de droits d’opposition ? |
