---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Applications Privacy Service et Experience Cloud
topic-legacy: overview
description: Ce document fournit une référence pour la configuration de différentes applications Experience Cloud pour les opérations liées à la confidentialité.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 55d6d8ad7b0fc5457dc0fdc981aaa92717adbe68
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 44%

---

# [!DNL Privacy Service] et  [!DNL Experience Cloud] applications

Adobe Experience Platform [!DNL Privacy Service] est conçu pour prendre en charge les demandes d’accès à des informations personnelles pour plusieurs applications Adobe Experience Cloud. Chaque application est compatible avec différentes valeurs et différents identifiants de produit pour l’identification des titulaires de données.

Ce document sert de référence à la documentation de l’application [!DNL Experience Cloud] qui explique comment configurer cette application pour des opérations liées à la confidentialité. Cela inclut les formats et les libellés de vos données. Deux catégories d’applications sont traitées :

* [Applications intégrées à Privacy Service](#integrated) : Applications capables d’envoyer des demandes d’accès, de suppression ou d’exclusion à  [!DNL Privacy Service].
* [Les applications en libre-service](#self-serve)[!DNL Privacy Service] : ce sont des applications qui doivent gérer leurs requêtes de confidentialité en interne et qui ne peuvent pas communiquer directement avec 

Consultez la documentation de vos applications [!DNL Experience Cloud] pour savoir comment formater vos demandes d’accès à des informations personnelles et quelles valeurs sont prises en charge pour ces demandes.

## Applications intégrées à [!DNL Privacy Service] {#integrated}

Vous trouverez ci-dessous une liste des applications [!DNL Experience Cloud] intégrées à [!DNL Privacy Service], notamment les fonctionnalités [!DNL Privacy Service] avec lesquelles elles sont compatibles, ainsi que des liens vers la documentation pour plus d’informations.

| Application | Accès/suppression | Opposition | Documentation et considérations |
| --- | :---: | :---: | --- |
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[Documentation sur l’accès et la suppression pour le RGPD](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Documentation sur l’accès et la suppression pour le CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Documentation sur l’exclusion de la vente pour le CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[Documentation sur l’accès et la suppression](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html?lang=fr)</li><li>[!DNL Analytics] gère les requêtes d’opposition à l’aide de [variables de reporting sur la confidentialité](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/consent-variables.html).</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[Documentation sur l’accès et la suppression](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentation sur l’opposition](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[Documentation sur l’accès et la suppression](https://docs.campaign.adobe.com/doc/standard/getting_started/fr/ACS_GDPR.html)</li><li>[Documentation sur l’opposition](../segmentation/consents.md)</li></ul> |
| Adobe des attributs du client (CRS) | ✓ | N/A | <ul><li>[Documentation sur l’accès et la suppression pour le RGPD](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[Documentation sur l’accès et la suppression pour le CCPA](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>Les attributs du client n’ont pas la capacité de transférer des données. Par conséquent, les demandes d’opposition ne sont pas applicables.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Documentation sur l’accès et la suppression pour le lac de données](../catalog/privacy.md)</li><li>[Documentation sur l’accès et la suppression pour Real-time Customer Profile](../profile/privacy.md)</li><li>[!DNL Experience Platform] honore les demandes d’ [exclusion pour les segments d’audience](../segmentation/consents.md).</li></ul> |
| Adobe Primetime Authentication | ✓ | N/A | <ul><li>[Documentation sur l’accès et la suppression](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] n’a pas la capacité de transférer des données. Par conséquent, les requêtes d’opposition ne sont pas applicables.</li></ul> |
| Adobe Target | ✓ | N/A | <ul><li>[Documentation sur l’accès et la suppression](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=fr)</li><li>[!DNL Target] n’a pas la capacité de transférer des données. Par conséquent, les requêtes d’opposition ne sont pas applicables.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Applications en libre-service {#self-serve}

Vous trouverez ci-dessous une liste des applications [!DNL Experience Cloud] qui ne sont pas intégrées à [!DNL Privacy Service] et qui doivent gérer leurs problèmes de confidentialité en interne. Vous trouverez des liens vers la documentation de chaque application, ainsi qu’une description du contenu de la documentation.

| Application | Description de la documentation |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html) | Présentation des fonctionnalités relatives au RGPD pour Adobe Campaign Classic. |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | Présentation de la gestion des requêtes RGPD par l’administrateur de la confidentialité client ou l’administrateur AEM. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Étapes pour créer des requêtes RGPD d’accès et de suppression à l’aide de Livefyre. |
| [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/client-side-info/deploy-javascript-tags-to-opt-in-to-launch.html) | Comment les développeurs peuvent-ils utiliser les extensions et le créateur de règles pour définir les solutions d’accords préalables et de droits d’opposition ? |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | Assurez-vous que vos installations de Magento Commerce sont conformes aux exigences des législations spécifiques sur la confidentialité. |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | Découvrez comment les réglementations de confidentialité s’appliquent à Marketo. |
| [Workfront](https://www.workfront.com/privacy-notice) | Découvrez comment Workfront collecte des données personnelles et comment un sujet des données peut envoyer une demande d’accès à des informations personnelles via un formulaire. |

{style=&quot;table-layout:auto&quot;}
