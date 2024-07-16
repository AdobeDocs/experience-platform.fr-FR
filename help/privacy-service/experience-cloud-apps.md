---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Applications Privacy Service et Experience Cloud
description: Ce document fournit une référence pour la configuration de différentes applications Experience Cloud pour les opérations liées à la confidentialité.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 46ca46460de9211c3e876454c986d030b964646e
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 26%

---

# Applications [!DNL Privacy Service] et [!DNL Experience Cloud]

Adobe Experience Platform [!DNL Privacy Service] est conçu pour prendre en charge les demandes d’accès à des informations personnelles pour plusieurs applications Adobe Experience Cloud. Chaque application est compatible avec différentes valeurs et différents identifiants de produit pour l’identification des titulaires de données.

Ce document sert de référence à la documentation de l’application [!DNL Experience Cloud] qui explique comment configurer cette application pour les opérations liées à la confidentialité. Cela inclut les formats et les libellés de vos données. Deux catégories d’applications sont traitées :

* [Applications intégrées à Privacy Service](#integrated) : applications capables d’envoyer des demandes d’accès, de suppression ou d’exclusion à [!DNL Privacy Service].
* [Applications en libre-service](#self-serve) : applications qui doivent gérer leurs demandes d’accès à des informations personnelles en interne et qui ne peuvent pas communiquer directement avec [!DNL Privacy Service].

Consultez la documentation de vos applications [!DNL Experience Cloud] pour savoir comment formater vos demandes d’accès à des informations personnelles et quelles valeurs sont prises en charge pour ces demandes.

## Applications intégrées à [!DNL Privacy Service] {#integrated}

Vous trouverez ci-dessous une liste des applications [!DNL Experience Cloud] intégrées à [!DNL Privacy Service], notamment les fonctionnalités [!DNL Privacy Service] avec lesquelles elles sont compatibles, leurs protocoles de traitement des demandes de suppression et des liens vers la documentation pour plus d’informations.

>[!NOTE]
>
>Tous les produits intégrés répondent aux demandes d’accès à des informations personnelles en 30 jours ou moins.

| Application | Accès/suppression | Opposition | Supprimer le comportement | Documentation et autres considérations |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | L’ID de cookie du sujet de données ou l’ID d’appareil est supprimé du système, ainsi que toutes les données de coût, de clic et de recettes associées au cookie. | <ul><li>[Documentation d’accès/de suppression pour le RGPD](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Documentation d’accès/de suppression pour le CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Documentation sur l’exclusion de la vente pour le CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics fournit des outils d’étiquetage des données en fonction de leur sensibilité et des restrictions contractuelles. Les libellés constituent une étape importante pour :<ol><li>Identification des titulaires de données</li><li>Déterminer les données à renvoyer dans le cadre d’une demande d’accès.</li><li>Identification des champs de données à supprimer dans le cadre d’une demande de suppression.</li></ol> | <ul><li>[Processus de confidentialité](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)</li><li>[Étiquetage Analytics](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html)</li><li>[Exclusion Analytics](https://experienceleague.adobe.com/docs/analytics/components/dimensions/cm-opt-out.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | Toutes les caractéristiques et tous les segments associés à l’identifiant d’Audience Manager inclus dans la requête sont supprimés. En outre, les identifiants respectifs de l’individu sont désinscrits de la collecte de données ultérieure et les mappages d’identifiants respectifs sont supprimés. | <ul><li>[Accéder](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#access-data) / [supprimer](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#delete-data) documentation</li><li>[Documentation sur l’opposition](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html#opt-out-calls)</li><li>[Demandes d’exclusion](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests)</li></ul> |
| Adobe Campaign Classic | ✓ | ✓ | Les données stockées du sujet de données sont supprimées du système. | <ul><li>[Gestion de la confidentialité](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=fr).</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | Les données stockées du sujet de données sont supprimées du système. | <ul><li>[Documentation sur l’accès et la suppression](https://docs.campaign.adobe.com/doc/standard/getting_started/fr/ACS_GDPR.html)</li><li>[Documentation sur l’opposition](../segmentation/consents.md)</li></ul> |
| Adobe des attributs du client (CRS) | ✓ | N/A | Les attributs du sujet de données sont supprimés du système. | <ul><li>[Documentation d’accès/de suppression pour le RGPD](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html?lang=fr)</li><li>[Documentation d’accès/de suppression pour le CCPA](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html?lang=fr)</li><li>Les attributs du client n’ont pas la capacité de transférer des données. Par conséquent, les demandes d’opposition ne sont pas applicables.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | Lorsqu’Experience Platform reçoit une demande de suppression de la part de Privacy Service, Platform envoie une confirmation à Privacy Service pour confirmer que la demande a été reçue et que les données concernées ont été marquées pour suppression. Les enregistrements sont ensuite supprimés du lac de données ou de la banque de profils une fois la tâche de confidentialité terminée. Avant la fin de la tâche, les données sont supprimées en douceur et ne sont donc accessibles par aucun service Platform. | <ul><li>[Documentation sur l’accès et la suppression pour le lac de données](../catalog/privacy.md)</li><li>[Documentation d’accès/de suppression pour Identity Service](../identity-service/privacy.md)</li><li>[Documentation d’accès/de suppression pour Real-time Customer Profile](../profile/privacy.md)</li><li>[!DNL Experience Platform] honore les [demandes d’opposition pour les segments ciblés](../segmentation/consents.md).</li></ul> |
| Adobe Journey Optimizer | ✓ | N/A | Les données stockées du sujet de données sont supprimées du système. | <ul><li>[Documentation sur l’accès et la suppression](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/requests)</li></ul> |
| Authentification Adobe Pass | ✓ | N/A | Les données stockées du sujet de données sont supprimées du système. | <ul><li>[Documentation sur l’accès et la suppression](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Pass n’a pas la capacité de transférer des données. Par conséquent, les demandes d’opposition ne sont pas applicables.</li></ul> |
| Adobe Target | ✓ | N/A | Toutes les données associées à l’identifiant du sujet de données sont supprimées de son profil du visiteur. Les données agrégées ou rendues anonymes qui n’identifient pas l’individu ou qui ne sont pas liées d’une autre manière (telles que les données de contenu) ne s’appliquent pas aux requêtes de suppression. | <ul><li>[Documentation sur l’accès et la suppression](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=fr)</li><li>[!DNL Target] n’a pas la capacité de transférer des données. Par conséquent, les demandes d’opposition ne sont pas applicables.</li></ul> |
| Marketo Engage | ✓ | N/A | Les données stockées du sujet de données sont supprimées du système. | <ul><li>[Documentation sur l’accès et la suppression](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] n’a pas la capacité de transférer des données. Par conséquent, les demandes d’opposition ne sont pas applicables.</li></ul> |

{style="table-layout:auto"}

## Applications en libre-service {#self-serve}

Voici une liste des applications [!DNL Experience Cloud] qui ne sont pas intégrées à [!DNL Privacy Service] et qui doivent gérer leurs problèmes de confidentialité en interne. Vous trouverez des liens vers la documentation de chaque application, ainsi qu’une description du contenu de la documentation.

| Application | Description de la documentation |
| ------- | ----------- |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | Présentation de la gestion des requêtes RGPD par l’administrateur de la confidentialité client ou l’administrateur AEM. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Étapes pour créer des requêtes RGPD d’accès et de suppression à l’aide de Livefyre. |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | Assurez-vous que vos installations de Magento Commerce sont conformes aux exigences des législations spécifiques sur la confidentialité. |
| [Balises dans Adobe Experience Platform](../tags/ui/client-side/consent.md) | Comment les développeurs peuvent-ils utiliser les extensions et le créateur de règles pour définir les solutions d’accords préalables et de droits d’opposition ? |
| [Workfront](https://www.workfront.com/privacy-notice) | Découvrez comment Workfront collecte des données personnelles et comment un sujet des données peut envoyer une demande d’accès à des informations personnelles via un formulaire. |

{style="table-layout:auto"}
