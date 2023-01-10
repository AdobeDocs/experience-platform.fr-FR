---
solution: Experience Platform
title: Modèle de données du secteur de la vente au détail
description: Affichez un modèle de données normalisé pour le secteur de la vente au détail, compatible avec le modèle de données d’expérience (XDM) à utiliser dans Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 16%

---

# [!UICONTROL Vente au détail] modèle de données du secteur

Le diagramme de relation d’entité suivant (ERD) représente un modèle de données normalisé pour le secteur de la vente au détail. L’ERD est délibérément présenté de manière dénormalisée et en tenant compte de la manière dont les données sont stockées dans Adobe Experience Platform.

>[!NOTE]
>
>L’identifiant d’utilisateur (ERD) tel que décrit est une recommandation pour la manière dont vous devez modéliser vos données pour ce cas d’utilisation du secteur. Pour utiliser ce modèle de données dans Platform, vous devez construire vous-même les schémas recommandés et leurs relations. Consultez les guides de gestion [schémas](../../ui/resources/schemas.md) et [relations](../../tutorials/relationship-ui.md) pour plus d’informations.

Utilisez la légende suivante pour interpréter cet ERD :

* Chaque entité affichée dans repose sur un sous-jacent [Classe de modèle de données d’expérience (XDM)](../composition.md#class).
* Pour une entité donnée, chaque ligne marquée dans **gras** représente un groupe de champs ou un type de données, avec les champs pertinents qu’il fournit ci-dessous dans le texte non en gras.
* Les champs les plus importants pour une entité donnée sont surlignés en rouge.
* Toutes les propriétés pouvant être utilisées pour identifier des clients individuels sont marquées comme &quot;identité&quot;, l’une de ces propriétés étant marquée comme &quot;identité Principale&quot;.
* Les relations d’entité sont marquées comme étant non dépendantes, puisque les événements basés sur des cookies ne peuvent souvent pas déterminer la personne ou l’individu qui a effectué la transaction.

![](../../images/industries/retail.png)

>[!NOTE]
>
>L’entité Événement d’expérience comprend un champ &quot;_ID&quot;, qui représente l’identifiant unique (`_id`) fourni par la classe XDM ExperienceEvent. Consultez le document de référence sur [XDM ExperienceEvent](../../classes/experienceevent.md) pour plus d’informations sur ce qui est attendu pour cette valeur.

## [!UICONTROL Vente au détail] cas d’utilisation

Le tableau suivant décrit les classes recommandées et les groupes de champs de schéma pour plusieurs cas pratiques courants de vente au détail.

| Cas d’utilisation | Classes et groupes de champs recommandés |
| --- | --- |
| Combinez des sources de données en ligne et hors ligne et résolvez les identités inter-appareils et en ligne/hors ligne afin de fournir des rapports d’attribution cross-canal et inter-appareils holistiques. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Informations commerciales](../../field-groups/event/commerce-details.md)</li><li>[Détails web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Produit](../../classes/product.md)**:<ul><li>[Catalogue de produits](../../field-groups/product/product-catalog.md)</li><li>[Catégorie de produits](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| proposer des expériences ciblées et personnalisées à différents segments afin d’augmenter les recettes et d’augmenter la plate-forme dans l’orchestration omnicanal. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Détails de la campagne marketing](../../field-groups/event/campaign-marketing-details.md)</li><li>[Informations sur le canal](../../field-groups/event/channel-details.md)</li><li>[Informations commerciales](../../field-groups/event/commerce-details.md)</li><li>[Détails de l’environnement](../../field-groups/event/environment-details.md)</li><li>[Détails web](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Détails démographiques](../../field-groups/profile/demographic-details.md)</li><li>[Détails du contact personnel](../../field-groups/profile/personal-contact-details.md)</li><li>[Détails du contact professionnel](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analysez l’attribution multi-touch pour améliorer l’efficacité marketing. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Détails de la campagne marketing](../../field-groups/event/campaign-marketing-details.md)</li><li>[Informations sur le canal](../../field-groups/event/channel-details.md)</li><li>[Informations commerciales](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Détails démographiques](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Améliorez la pertinence des emails grâce à une meilleure segmentation masculine et féminine. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Informations commerciales](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Détails démographiques](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[Produit](../../classes/product.md)**:<ul><li>[Catalogue de produits](../../field-groups/product/product-catalog.md)</li><li>[Catégorie de produits](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Ingérez des données de fidélité (partenaire) afin d’augmenter les informations pertinentes sur les produits sur les canaux web, email et marketing numérique. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Détails web](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)**:<ul><li>[Détails démographiques](../../field-groups/profile/demographic-details.md)</li><li>[Détails de fidélité](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[Produit](../../classes/product.md)**:<ul><li>[Catalogue de produits](../../field-groups/product/product-catalog.md)</li><li>[Catégorie de produits](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Reciblez les abandons de panier par le biais d’emails automatisés et personnalisés. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Informations commerciales](../../field-groups/event/commerce-details.md)</li><li>[Détails web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Produit](../../classes/product.md)**:<ul><li>[Catalogue de produits](../../field-groups/product/product-catalog.md)</li><li>[Catégorie de produits](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

*\*Bien qu’une classe de produits standard soit prévue pour une prochaine version, les schémas de produits doivent actuellement être créés à l’aide d’une classe personnalisée à la place. Vous devez donc créer manuellement la structure de la classe du schéma, ainsi que celle de tous les groupes de champs que vous lui ajoutez. Voir la section sur [création d’une classe personnalisée](../../ui/resources/classes.md#create) pour plus d’informations.*
