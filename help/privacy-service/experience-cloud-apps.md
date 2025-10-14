---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Applications Privacy Service et Experience Cloud
description: Ce document fournit une référence sur la manière de configurer différentes applications Experience Cloud pour les opérations liées à la confidentialité.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 21%

---

# [!DNL Privacy Service] et [!DNL Experience Cloud] des applications

Adobe Experience Platform [!DNL Privacy Service] est conçu pour prendre en charge les demandes d’accès à des informations personnelles pour plusieurs applications Adobe Experience Cloud. Chaque application est compatible avec différentes valeurs et différents identifiants de produit pour l’identification des titulaires de données.

Ce document sert de référence pour [!DNL Experience Cloud] documentation de l’application qui décrit comment configurer cette application pour les opérations liées à la confidentialité. Cela inclut les formats et les libellés de vos données. Deux catégories d’applications sont traitées :

* [Applications intégrées à Privacy Service](#integrated) : applications capables d’envoyer des demandes d’accès, de suppression ou d’exclusion à [!DNL Privacy Service].
* [Applications en libre-service](#self-serve) : applications qui doivent gérer leurs demandes d’accès à des informations personnelles en interne et ne peuvent pas communiquer directement avec [!DNL Privacy Service].

Veuillez consulter la documentation de vos applications [!DNL Experience Cloud] pour savoir comment formater vos demandes d’accès à des informations personnelles et quelles valeurs sont prises en charge pour ces demandes.

## Applications intégrées à [!DNL Privacy Service] {#integrated}

Vous trouverez ci-dessous une liste des applications [!DNL Experience Cloud] intégrées à [!DNL Privacy Service], y compris les fonctionnalités de [!DNL Privacy Service] avec lesquelles elles sont compatibles, leurs protocoles de traitement des demandes de suppression et des liens vers la documentation pour plus d’informations.

>[!NOTE]
>
>Tous les produits intégrés répondent aux demandes de confidentialité en 30 jours ou moins.

| Application | Accès/suppression | Opposition | Comportement de suppression | Documentation et autres considérations |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | L’ID de cookie ou l’ID d’appareil du titulaire de données est supprimé du système, ainsi que toutes les données de coût, de clic et de chiffre d’affaires associées au cookie. | <ul><li>[Accéder/supprimer la documentation pour le RGPD](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html?lang=fr)</li><li>[Accéder à la documentation relative au CCPA/la supprimer](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html?lang=fr)</li><li>[Documentation d’opposition à la vente pour le CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html?lang=fr)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics fournit des outils pour libeller les données en fonction de leur sensibilité et des restrictions contractuelles. Les libellés constituent une étape importante pour les éléments suivants :<ol><li>Identification Des Titulaires De Données.</li><li>Détermination des données à renvoyer dans le cadre d’une demande d’accès.</li><li>Identifier les champs de données qui doivent être supprimés dans le cadre d’une demande de suppression.</li></ol> | <ul><li>[Workflow de confidentialité](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html?lang=fr)</li><li>[Étiquetage Analytics](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html?lang=fr)</li><li>[Désinscription d’Analytics](https://experienceleague.adobe.com/docs/analytics/components/dimensions/cm-opt-out.html?lang=fr)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | Toutes les caractéristiques et tous les segments associés à l’identifiant Audience Manager inclus dans la requête sont supprimés. En outre, les identifiants respectifs de l&#39;individu sont exclus de la collecte d&#39;autres données et les mappages d&#39;identifiants respectifs sont supprimés. | <ul><li>Documentation [Access](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html?lang=fr#access-data) / [delete](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html?lang=fr#delete-data)</li><li>[Documentation sur l’opposition](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html?lang=fr#opt-out-calls)</li><li>[Requêtes d’opt-out](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html?lang=fr#opt-out-requests)</li></ul> |
| Adobe Campaign Classic | ✓ | ✓ | Les données stockées du titulaire de données sont supprimées du système. | <ul><li>[Gestion de la confidentialité](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=fr)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | Les données stockées du titulaire de données sont supprimées du système. | <ul><li>[Documentation sur l’accès et la suppression](https://experienceleague.adobe.com/fr/docs/campaign-standard/using/getting-started/privacy/privacy-management#right-access-forgotten)</li><li>[Documentation sur l’opposition](https://experienceleague.adobe.com/fr/docs/campaign-standard/using/profiles-and-audiences/understanding-opt-in-and-opt-out-processes/about-opt-in-and-opt-out-in-campaign)</li></ul> |
| Attributs du client Adobe (CRS) | ✓ | N/A | Les attributs du titulaire de données sont supprimés du système. | <ul><li>[Accéder/supprimer la documentation pour le RGPD](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html?lang=fr)</li><li>[Accéder à la documentation relative au CCPA/la supprimer](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html?lang=fr)</li><li>Les attributs du client ne sont pas en mesure de transférer des données. Par conséquent, les requêtes d’opposition à la vente ne sont pas applicables.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | Lorsqu’Experience Platform reçoit une demande de suppression de Privacy Service, Experience Platform envoie une confirmation à Privacy Service pour confirmer que la demande a été reçue et que les données concernées ont été marquées pour suppression. Les enregistrements sont ensuite supprimés du lac de données ou de la banque de profils une fois la tâche de confidentialité terminée. Avant la fin de la tâche, les données sont supprimées de manière réversible et ne sont donc accessibles par aucun service Experience Platform. | <ul><li>[Documentation sur l’accès et la suppression pour le lac de données](../catalog/privacy.md)</li><li>[Accéder à la documentation d’Identity Service et la supprimer](../identity-service/privacy.md)</li><li>[Accéder à la documentation et la supprimer pour le profil client en temps réel](../profile/privacy.md)</li><li>[!DNL Experience Platform] honore les [demandes d’exclusion pour les segments d’audience](../segmentation/tutorials/consents.md).</li></ul> |
| Adobe Journey Optimizer | ✓ | N/A | Les données stockées du titulaire de données sont supprimées du système. | <ul><li>[Documentation sur l’accès et la suppression](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/privacy/requests)</li></ul> |
| Authentification Adobe Pass | ✓ | N/A | Les données stockées du titulaire de données sont supprimées du système. | <ul><li>[Documentation sur l’accès et la suppression](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Pass ne dispose pas de la capacité de transférer des données. Par conséquent, les demandes d’opposition à la vente ne sont pas applicables.</li></ul> |
| Adobe Target | ✓ | N/A | Toutes les données associées à l’ID du titulaire de données sont supprimées de son profil du visiteur. Les données agrégées ou anonymisées qui n’identifient pas l’individu ou qui ne sont pas liées d’une autre manière (comme les données de contenu) ne s’appliquent pas aux requêtes de suppression. | <ul><li>[Documentation sur l’accès et la suppression](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=fr)</li><li>[!DNL Target] ne dispose pas de la capacité de transférer des données. Par conséquent, les demandes d’opposition à la vente ne sont pas applicables.</li></ul> |
| Commerce (Personalization) | ✓ | N/A | Privacy Service supprime les données [!DNL Commerce] stockées dans les services SaaS Commerce à des fins marketing, ce qui signifie que les profils et les commandes des titulaires de données ne sont plus envoyés aux applications marketing Adobe pour être utilisés dans les campagnes et les parcours clients. Cependant, Privacy Service ne supprime pas les données de l’application [!DNL Commerce], car elles peuvent toujours être nécessaires pour les besoins transactionnels des commerçants. Les commerçants sont responsables de toutes les demandes de suppression/d’accès aux données dans l’application [!DNL Commerce]. | <ul><li>[Accéder à la documentation de Commerce/la supprimer](https://experienceleague.adobe.com/fr/docs/commerce-merchant-services/data-connection/handle-privacy-request)</li></ul> |
| Marketo Engage | ✓ | N/A | Les données stockées du titulaire de données sont supprimées du système. | <ul><li>[Documentation sur l’accès et la suppression](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html?lang=fr)</li><li>[!DNL Marketo] ne dispose pas de la capacité de transférer des données. Par conséquent, les demandes d’opposition à la vente ne sont pas applicables.</li></ul> |

{style="table-layout:auto"}

## Applications en libre-service {#self-serve}

Voici une liste des applications [!DNL Experience Cloud] qui ne sont pas intégrées à [!DNL Privacy Service] et qui doivent gérer leurs problèmes de confidentialité en interne. Vous trouverez des liens vers la documentation de chaque application, ainsi qu’une description du contenu de la documentation.

| Application | Description de la documentation |
| ------- | ----------- |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html?lang=fr) | Présentation de la gestion des requêtes RGPD par l’administrateur de la confidentialité client ou l’administrateur AEM. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html?lang=fr) | Étapes pour créer des requêtes RGPD d’accès et de suppression à l’aide de Livefyre. |
| [Adobe Commerce](https://experienceleague.adobe.com/fr/docs/commerce-operations/security-and-compliance/overview) | Assurez-vous que vos installations Adobe Commerce sont conformes aux exigences des législations spécifiques en matière de confidentialité. |
| [&#x200B; Balises dans Adobe Experience Platform &#x200B;](../tags/ui/client-side/consent.md) | Comment les développeurs peuvent-ils utiliser les extensions et le créateur de règles pour définir les solutions d’accords préalables et de droits d’opposition ? |
| [Workfront](https://www.workfront.com/privacy-notice) | Découvrez comment Workfront collecte des données personnelles et comment une personne concernée peut soumettre une demande d’accès à des informations personnelles via un formulaire. |

{style="table-layout:auto"}
