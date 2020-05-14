---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Privacy Service et les applications Experience Cloud
topic: overview
translation-type: tm+mt
source-git-commit: f4a007b66806cb0d322226e1e1837cfce7ca4095
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 18%

---


# Privacy Service et les applications Experience Cloud

Adobe Experience Platform Privacy Service est conçu pour prendre en charge les demandes de confidentialité pour plusieurs applications Adobe Experience Cloud. Chaque application prend en charge différentes valeurs et identifiants de produit pour identifier les personnes concernées.

Ce document sert de référence à la documentation de l’application Experience Cloud qui décrit comment configurer cette application pour des opérations liées à la confidentialité. Cela inclut la manière de formater et d’étiqueter vos données. Deux catégories de demandes sont traitées :

* [Applications intégrées à Privacy Service](#integrated): Applications capables d’envoyer des demandes d’accès, de suppression ou d’exclusion à Privacy Service.
* [Applications](#self-serve)en libre-service : Les applications qui doivent gérer leurs demandes de confidentialité en interne et qui ne peuvent pas communiquer directement avec Privacy Service.

Consultez la documentation relative à vos applications Experience Cloud pour savoir comment formater vos requêtes de confidentialité et connaître les valeurs prises en charge pour ces requêtes.

## Applications intégrées à Privacy Service {#integrated}

Vous trouverez ci-dessous une liste des applications Experience Cloud intégrées à Privacy Service, y compris les fonctionnalités Privacy Service avec lesquelles elles sont compatibles, et des liens vers la documentation pour plus d’informations.

| Application | Accès/suppression | Exclusion de la vente | Documentation et considérations |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[Accès/suppression de la documentation](https://docs.adobe.com/content/help/en/advertising-cloud/all/privacy/ad-cloud-gdpr.html) </li><li>Advertising Cloud exploite les fonctionnalités d’exclusion globales existantes fournies par le Centre de traitement des données personnelles d’Adobe. Pour plus d’informations, consultez le guide sur l’ [exécution de demandes](https://docs.adobe.com/content/help/fr-FR/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests) de confidentialité de données.</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[Accès/suppression de la documentation](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>Analytics gère les demandes d’exclusion en utilisant les variables de rapports de [confidentialité.](https://docs.adobe.com/content/help/fr-FR/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[Accès/suppression de la documentation](https://docs.adobe.com/content/help/fr-FR/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentation d’exclusion](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[Accès/suppression de la documentation](https://docs.campaign.adobe.com/doc/standard/getting_started/fr/ACS_GDPR.html)</li><li>[Documentation d’exclusion](../segmentation/honoring-opt-outs.md)</li></ul> |
| Attributs du client Adobe (CRS) | ✓ | S.O. | <ul><li>[Accès/suppression de la documentation pour GDPR](https://docs.adobe.com/content/help/en/core-services/interface/customer-attributes/gdpr.html)</li><li>[Accès/suppression de la documentation de l’ACPCP](https://docs.adobe.com/content/help/en/core-services/interface/customer-attributes/ccpa.html)</li><li>Les attributs du client n’ont pas la capacité de transférer des données. Par conséquent, les demandes d’exclusion de la vente ne sont pas applicables.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Accès/suppression de la documentation relative au lac Data](../catalog/privacy.md)</li><li>[Accès/suppression de la documentation pour le Profil client en temps réel](../profile/privacy.md)</li><li>Experience Platform honore les demandes d’ [exclusion pour les segments](../segmentation/honoring-opt-outs.md)d’audience.</li></ul> |
| Authentification Adobe Primetime | ✓ | S.O. | <ul><li>[Accès/suppression de la documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Primetime n’a pas la capacité de transférer des données, par conséquent les demandes d’exclusion de la vente ne sont pas applicables.</li></ul> |
| Adobe Target | ✓ | S.O. | <ul><li>[Accès/suppression de la documentation](https://docs.adobe.com/content/help/fr-FR/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.translate.html)</li><li>La Cible n’a pas la capacité de transférer des données, par conséquent les demandes d’exclusion de la vente ne sont pas applicables.</li></ul> |


## Applications en libre-service {#self-serve}

Voici une liste des applications Experience Cloud qui ne sont pas intégrées à Privacy Service et doivent gérer leurs problèmes de confidentialité en interne. Des liens vers la documentation de chaque application sont fournis, ainsi que des descriptions du contenu de la documentation.

| Application | Description de la documentation |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/FR/ACC_GDPR.html) | Présentation des fonctionnalités du RGPD pour Adobe Campaign Classic. |
| [Adobe Dynamic Tag Manager](https://docs.adobe.com/content/help/en/dtm/using/tools/opt-in.html) | Cette section décrit la procédure à suivre pour empêcher le déclenchement des balises Adobe jusqu’à ce que le consentement soit obtenu. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | Présentation de la manière dont un administrateur de la confidentialité du client ou un administrateur AEM peut traiter les demandes GDPR. |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Cette section décrit la procédure à suivre pour autoriser l’accès à GDPR et supprimer des requêtes à l’aide de Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Comment les développeurs peuvent-ils utiliser les extensions et le créateur de règles pour définir les solutions d’accords préalables et de droits d’opposition ? |
