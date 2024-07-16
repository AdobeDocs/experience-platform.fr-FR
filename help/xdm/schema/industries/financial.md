---
solution: Experience Platform
title: ERD Modèle de données du secteur des services financiers
description: Affichez un diagramme des relations entre les entités (ERD) qui décrit un modèle de données normalisé pour le secteur bancaire, les services financiers et les assurances (BFSI). Ce modèle de données est compatible avec le modèle de données d’expérience (XDM) à utiliser dans Adobe Experience Platform.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 2%

---

# [!UICONTROL Services financiers] Modèle de données de l’industrie ERD

Le diagramme de relation des entités ci-après (DCE) représente un modèle de données normalisé pour le secteur bancaire, les services financiers et les assurances (BFSI). L’ERD est délibérément présenté de manière dénormalisée et en tenant compte de la manière dont les données sont stockées dans Adobe Experience Platform.

>[!NOTE]
>
>L’identifiant d’utilisateur (ERD) tel que décrit est une recommandation pour la manière dont vous devez modéliser vos données pour ce cas d’utilisation du secteur. Pour utiliser ce modèle de données dans Platform, vous devez construire vous-même les schémas recommandés et leurs relations. Pour plus d’informations, consultez les guides sur la gestion des [schémas](../../ui/resources/schemas.md) et des [relations](../../tutorials/relationship-ui.md) dans l’interface utilisateur.

Utilisez la légende suivante pour interpréter cet ERD :

* Chaque entité affichée dans est basée sur une [classe de modèle de données d’expérience (XDM)](../composition.md#class) sous-jacente.
* Pour une entité donnée, chaque ligne marquée en **bold** représente un groupe de champs ou un type de données, avec les champs pertinents qu’elle fournit ci-dessous dans le texte non en gras.
* Les champs les plus importants pour une entité donnée sont surlignés en rouge.
* Toutes les propriétés pouvant être utilisées pour identifier des clients individuels sont marquées comme &quot;identité&quot;, l’une de ces propriétés étant marquée comme &quot;identité principale&quot;.
* Les relations d’entité sont marquées comme étant non dépendantes, puisque les événements basés sur des cookies ne peuvent souvent pas déterminer la personne ou l’individu qui a effectué la transaction.

![](../../images/industries/financial.png)

>[!NOTE]
>
>L’entité Experience Event inclut un champ &quot;_ID&quot;, qui représente l’attribut unique (`_id`) fourni par la classe XDM ExperienceEvent. Consultez le document de référence sur [XDM ExperienceEvent](../../classes/experienceevent.md) pour plus d’informations sur ce qui est attendu pour cette valeur.

## Cas d’utilisation [!UICONTROL Services financiers]

Le tableau suivant décrit les classes recommandées et les groupes de champs de schéma pour plusieurs cas d’utilisation financière courants.

| Cas d’utilisation | Classes et groupes de champs recommandés |
| --- | --- |
| Personnalisation à grande échelle pour les segments préférés grâce aux rapports omnicanaux et à l’automatisation des parcours afin d’augmenter l’inscription à un programme de récompenses préféré. | <ul><li>**[[!UICONTROL Produit]](../../classes/product.md)** :<ul><li>[[!UICONTROL Catégorie de produits]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)** :<ul><li>[[!UICONTROL Actions de carte]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Détails de la demande de devis]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL Détails du dépôt]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Informations sur le canal]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL Transferts de solde]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Détails démographiques]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Détails de contact personnel]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Loyalty Details]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Optimisez la personnalisation cross-canal sur les canaux en ligne et hors ligne. | <ul><li>**[[!UICONTROL Produit]](../../classes/product.md)** :<ul><li>[[!UICONTROL Catégorie de produits]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)** :<ul><li>[[!UICONTROL Informations sur le canal]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Détails démographiques]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Détails de contact personnel]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Loyalty Details]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Stimuler les nouvelles opportunités de chiffre d’affaires en utilisant les informations acquises grâce à l’analyse des comportements cross-canal, en identifiant les schémas d’utilisation des produits susceptibles de conduire à de nouvelles offres de produits. | <ul><li>**[[!UICONTROL Politique]](../../classes/policy.md)**</li><li>**[[!UICONTROL Produit]](../../classes/product.md)** :<ul><li>[[!UICONTROL Catégorie de produits]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)** :<ul><li>[[!UICONTROL Actions de carte]](../../field-groups/event/card-actions.md)</li><li>[](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL Détails du dépôt]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Informations sur le canal]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Détails démographiques]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Détails de contact personnel]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Loyalty Details]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
