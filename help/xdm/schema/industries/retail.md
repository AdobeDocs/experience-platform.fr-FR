---
solution: Experience Platform
title: Modèle de données du secteur de la vente au détail
description: Affichez un modèle de données normalisé pour le secteur de la vente au détail, compatible avec le modèle de données d’expérience (XDM) à utiliser dans Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 8%

---

# [!UICONTROL Vente au détail] modèle de données du secteur

Le diagramme de relation d’entité suivant représente un modèle de données normalisé pour le secteur du commerce de détail. L’ERD est délibérément présenté de manière dénormalisée et en tenant compte de la manière dont les données sont stockées dans Adobe Experience Platform.

>[!NOTE]
>
>L’ERD tel que décrit est une recommandation sur la manière dont vous devez modéliser vos données pour ce cas d’utilisation du secteur. Pour utiliser ce modèle de données dans Experience Platform, vous devez créer vous-même les schémas recommandés et leurs relations. Consultez les guides sur la gestion des [schémas](../../ui/resources/schemas.md) et [relations](../../tutorials/relationship-ui.md) dans l’interface utilisateur pour plus d’informations.

Utilisez la légende suivante pour interpréter cet ERD :

* Chaque entité affichée dans est basée sur une classe [Modèle de données d’expérience (XDM)](../composition.md#class) sous-jacente.
* Les champs mis en retrait sous un champ parent représentent un champ enfant, ou sous-champ, appartenant au groupe de champs du parent.
* Les champs les plus importants pour une entité donnée sont surlignés en rouge.
* Toutes les propriétés pouvant être utilisées pour identifier des clients individuels sont marquées comme « identité », l’une de ces propriétés étant marquée comme « identité principale ».
* Les relations d’entité sont marquées comme non dépendantes, car les événements basés sur des cookies ne peuvent souvent pas déterminer la personne ou l’individu qui a effectué la transaction.

![Exemple d’ERD pour un modèle de données du secteur de la vente au détail](../../images/industries/retail.png)

>[!NOTE]
>
>L’entité Événement d’expérience comprend un champ « _ID », qui représente l’attribut d’identifiant unique (`_id`) fourni par la classe XDM ExperienceEvent. Consultez le document de référence sur [XDM ExperienceEvent](../../classes/experienceevent.md) pour plus d’informations sur ce qui est attendu pour cette valeur.

## Cas pratiques [!UICONTROL vente au détail]

Le tableau suivant décrit les classes et groupes de champs de schéma recommandés pour plusieurs cas d’utilisation courants de la vente au détail.

| Cas d’utilisation | Classes et groupes de champs recommandés |
| --- | --- |
| Combinez les sources de données en ligne et hors ligne et résolvez les problèmes d’identité entre appareils et en ligne/hors ligne afin de fournir un rapport holistique d’attribution entre canaux et entre appareils. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)** :<ul><li>[Détails Commerce](../../field-groups/event/commerce-details.md)</li><li>[Détails Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Produit](../../classes/product.md)** :<ul><li>[Catalogue des produits](../../field-groups/product/product-catalog.md)</li><li>[Catégorie de produits](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Proposez des expériences ciblées et personnalisées pour divers segments afin d’augmenter les recettes et d’améliorer la plateforme dans l’orchestration omnicanal. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)** :<ul><li>[Détails de la campagne marketing](../../field-groups/event/campaign-marketing-details.md)</li><li>[Informations sur le canal](../../field-groups/event/channel-details.md)</li><li>[Informations commerciales](../../field-groups/event/commerce-details.md)</li><li>[Détails de l’environnement](../../field-groups/event/environment-details.md)</li><li>[Détails Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Profil individuel XDM](../../classes/individual-profile.md)** :<ul><li>[Détails démographiques](../../field-groups/profile/demographic-details.md)</li><li>[Coordonnées personnelles](../../field-groups/profile/personal-contact-details.md)</li><li>[Détails du contact professionnel](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analysez l’attribution multipoint pour améliorer l’efficacité marketing. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)** :<ul><li>[Détails de la campagne marketing](../../field-groups/event/campaign-marketing-details.md)</li><li>[Informations sur le canal](../../field-groups/event/channel-details.md)</li><li>[Informations commerciales](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Profil individuel XDM](../../classes/individual-profile.md)** :<ul><li>[Détails démographiques](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Améliorez la pertinence des e-mails grâce à une segmentation améliorée pour les hommes et les femmes. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)** :<ul><li>[Détails Commerce](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Profil individuel XDM](../../classes/individual-profile.md)** :<ul><li>[Détails démographiques](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[Produit](../../classes/product.md)** :<ul><li>[Catalogue des produits](../../field-groups/product/product-catalog.md)</li><li>[Catégorie de produits](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Ingérez des données de fidélité (partenaires) pour augmenter les informations pertinentes sur les produits sur les canaux web, e-mail et marketing numérique. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)** :<ul><li>[Détails Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Profil individuel XDM](../../classes/individual-profile.md)** :<ul><li>[Détails démographiques](../../field-groups/profile/demographic-details.md)</li><li>[Détails de fidélité](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[Produit](../../classes/product.md)** :<ul><li>[Catalogue des produits](../../field-groups/product/product-catalog.md)</li><li>[Catégorie de produits](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Recibler les abandons de panier par le biais d’e-mails automatisés et personnalisés. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)** :<ul><li>[Détails Commerce](../../field-groups/event/commerce-details.md)</li><li>[Détails Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Produit](../../classes/product.md)** :<ul><li>[Catalogue des produits](../../field-groups/product/product-catalog.md)</li><li>[Catégorie de produits](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style="table-layout:auto"}
