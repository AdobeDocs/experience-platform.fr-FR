---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Privacy Service et les applications Experience Cloud
topic: overview
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# Privacy Service et les applications Experience Cloud

Le service de confidentialité d’Adobe Experience Platform est conçu pour prendre en charge les demandes de confidentialité pour plusieurs applications Adobe Experience Cloud. Chaque application prend en charge différentes valeurs et identifiants de produit pour l’identification des personnes concernées.

Ce sert de référence à la documentation de l’application Experience Cloud qui explique comment configurer cette application pour des opérations liées à la confidentialité. Cela inclut la manière de formater et d’étiqueter vos données. Deux  de demandes sont traitées :

* [Applications intégrées à Privacy Service](#integrated): Applications capables d’envoyer des demandes d’accès, de suppression ou d’exclusion à Privacy Service.
* [Applications](#self-serve)en libre-service : Les applications qui doivent gérer leurs demandes de confidentialité en interne et qui ne peuvent pas communiquer directement avec le service de confidentialité.

Consultez la documentation de vos applications Experience Cloud pour savoir comment formater vos requêtes de confidentialité et quelles valeurs sont prises en charge pour ces requêtes.

## Applications intégrées à Privacy Service {#integrated}

Voici un  des applications Experience Cloud intégrées à Privacy Service, y compris les fonctionnalités Privacy Service avec lesquelles elles sont compatibles, et des liens vers la documentation pour plus d’informations.

| Application | Accès/suppression | Exclusion de la vente | Documentation et considérations |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[Accès/suppression de la documentation](https://docs.adobe.com/content/help/en/advertising-cloud/all/privacy/ad-cloud-gdpr.html) </li><li>Advertising Cloud tire parti des fonctionnalités d’exclusion globales existantes fournies par le Centre de traitement des données personnelles d’Adobe. Pour plus d’informations, consultez le guide sur l’ [exécution de demandes](https://docs.adobe.com/content/help/fr-FR/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests) de confidentialité de données.</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[Accès/suppression de la documentation](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/index.html)</li><li>Analytics gère les demandes d’exclusion en utilisant des variables de de [confidentialité](https://docs.adobe.com/content/help/fr-FR/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[Accès/suppression de la documentation](https://marketing.adobe.com/resources/help/en_US/aam/aam-gdpr.html)</li><li>[Documentation d’exclusion](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[Accès/suppression de la documentation](https://docs.campaign.adobe.com/doc/standard/getting_started/fr/ACS_GDPR.html)</li><li>[Documentation d’exclusion](../segmentation/honoring-opt-outs.md)</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Accès/suppression de la documentation pour Data Lake](../catalog/privacy.md)</li><li>[Accès/suppression de la documentation pour les  de clients en temps réel](../profile/privacy.md)</li><li>La plateforme d’expérience honore les demandes d’ [exclusion pour  segments](../segmentation/honoring-opt-outs.md) de.</li></ul> |
| Authentification Adobe Primetime | ✓ | S.O. | <ul><li>[Accès/suppression de la documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Primetime n’a pas la capacité de transférer des données. Par conséquent, les demandes d’exclusion de la vente ne sont pas applicables.</li></ul> |
| Adobe Target | ✓ | S.O. | <ul><li>[Accès/suppression de la documentation](https://marketing.adobe.com/resources/help/en_US/target/target/privacy-and-general-data-protection-regulation.html)</li><li> n’est pas en mesure de transférer des données, les demandes d’exclusion de la vente ne sont donc pas applicables.</li></ul> |

<!-- (To include once access/delete documentation is available)
Adobe Customer Attributes (CRS) | ✓ | N/A | <ul><li>Customer Attributes does not have the capability to transfer data, therefore opt-out-of-sale requests are not applicable.</li></ul>
-->

## Applications en libre-service {#self-serve}

Voici un  des applications Experience Cloud qui ne sont pas intégrées à Privacy Service et qui doivent gérer leurs problèmes de confidentialité en interne. Des liens vers la documentation de chaque application sont fournis, ainsi que des descriptions du contenu de la documentation.

| Application | Description de la documentation |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/FR/ACC_GDPR.html) | Présentation des fonctionnalités de GDPR pour  Adobe Campaign Classic. |
| [Adobe Dynamic Tag Manager](https://marketing.adobe.com/resources/help/fr_FR/dtm/opt-in.html) | Cette section décrit la procédure à suivre pour empêcher le déclenchement des balises Adobe jusqu’à l’obtention du consentement. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | Présentation de la manière dont un administrateur de la confidentialité des clients ou un administrateur AEM peut traiter les demandes GDPR. |
| [Adobe Experience Manager Livefyre](https://marketing.adobe.com/resources/help/en_US/livefyre/c_gdpr_compliance.html) | Cette section décrit la procédure à suivre pour autoriser l’accès à GDPR et supprimer des requêtes à l’aide de Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Comment les développeurs peuvent-ils utiliser les extensions et le créateur de règles pour définir les solutions d’accords préalables et de droits d’opposition ? |
| [Adobe Social](https://marketing.adobe.com/resources/help/en_US/social/c_gdpr-request.html) | Cette section décrit la procédure à suivre pour utiliser le formulaire de demande GDPR afin d’accéder aux données collectées par Social ou de les supprimer. |