---
solution: Experience Platform
title: Modèle de données du secteur du voyage et de l’hôtellerie ERD
description: Affichez un diagramme de relation d’entité (ERD) qui décrit un modèle de données normalisé pour le secteur du voyage et de l’hôtellerie, compatible avec le modèle de données d’expérience (XDM) à utiliser dans Adobe Experience Platform.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 4%

---

# [!UICONTROL Voyage et hospitalité] modèle de données du secteur ERD

Le diagramme de relation des entités ci-après représente un modèle de données normalisé pour le secteur du voyage et de l’hôtellerie. L’ERD est délibérément présenté de manière dénormalisée et en tenant compte de la manière dont les données sont stockées dans Adobe Experience Platform.

>[!NOTE]
>
>L’identifiant d’utilisateur (ERD) tel que décrit est une recommandation pour la manière dont vous devez modéliser vos données pour ce cas d’utilisation du secteur. Pour utiliser ce modèle de données dans Platform, vous devez construire vous-même les schémas recommandés et leurs relations. Pour plus d’informations, consultez les guides sur la gestion des [schémas](../../ui/resources/schemas.md) et des [relations](../../tutorials/relationship-ui.md) dans l’interface utilisateur.

Utilisez la légende suivante pour interpréter cet ERD :

* Chaque entité affichée dans est basée sur une [classe de modèle de données d’expérience (XDM)](../composition.md#class) sous-jacente.
* Pour une entité donnée, chaque ligne marquée en **bold** représente un groupe de champs ou un type de données, avec les champs pertinents qu’elle fournit ci-dessous dans le texte non en gras.
* Les champs les plus importants pour une entité donnée sont surlignés en rouge.
* Toutes les propriétés pouvant être utilisées pour identifier des clients individuels sont marquées comme &quot;identité&quot;, l’une de ces propriétés étant marquée comme &quot;identité principale&quot;.
* Les relations d’entité sont marquées comme étant non dépendantes, puisque les événements basés sur des cookies ne peuvent souvent pas déterminer la personne ou l’individu qui a effectué la transaction.

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>L’entité Experience Event inclut un champ &quot;_ID&quot;, qui représente l’attribut unique (`_id`) fourni par la classe XDM ExperienceEvent. Consultez le document de référence sur [XDM ExperienceEvent](../../classes/experienceevent.md) pour plus d’informations sur ce qui est attendu pour cette valeur.

## [!UICONTROL Cas d’utilisation de voyages et d’hospitalité]

Le tableau suivant présente les classes et les groupes de champs recommandés pour plusieurs cas d’utilisation courants dans le domaine du voyage et de l’hôtellerie.

| Cas d’utilisation | Classes et groupes de champs recommandés |
| --- | --- |
| Vente croisée de restaurants et d&#39;autres attractions de la région à des clients du marché et à des clients qui réservent prochainement des hôtels. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)** :<ul><li>[Détails de la réservation](../../field-groups/event/reservation-details.md)</li><li>[Réservation de logement](../../field-groups/event/lodging-reservation.md)</li><li>[Réservation de restaurant](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)** :<ul><li>[Détails démographiques](../../field-groups/profile/demographic-details.md)</li><li>[Détails de contact personnel](../../field-groups/profile/personal-contact-details.md)</li><li>[Détails du contact professionnel](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Vendre des repas et d’autres attractions de la région à des clients du marché et à des clients qui réservent prochainement des hôtels. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)** :<ul><li>[Détails de la réservation](../../field-groups/event/reservation-details.md)</li><li>[Réservation de restaurant](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)** :<ul><li>[Détails démographiques](../../field-groups/profile/demographic-details.md)</li><li>[Détails de contact personnel](../../field-groups/profile/personal-contact-details.md)</li><li>[Détails du contact professionnel](../../field-groups/profile/work-contact-details.md)</li><li>[Loyalty Details](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Vendez des hôtels et d’autres attractions résidentielles à vos invités et à vos invités sur le marché avec les réservations à venir dans les hôtels. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)** :<ul><li>[Détails de la réservation](../../field-groups/event/reservation-details.md)</li><li>[Réservation de logement](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)** :<ul><li>[Détails démographiques](../../field-groups/profile/demographic-details.md)</li><li>[Détails de contact personnel](../../field-groups/profile/personal-contact-details.md)</li><li>[Détails du contact professionnel](../../field-groups/profile/work-contact-details.md)</li><li>[Loyalty Details](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Vendre à des clients du marché ou à des clients qui réservent à l&#39;hôtel des billets d&#39;avion ou d&#39;autres attractions de la région. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)** :<ul><li>[Détails de la réservation](../../field-groups/event/reservation-details.md)</li><li>[Réservation de vol](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[XDM Individual Profile](../../classes/individual-profile.md)** :<ul><li>[Détails démographiques](../../field-groups/profile/demographic-details.md)</li><li>[Détails de contact personnel](../../field-groups/profile/personal-contact-details.md)</li><li>[Détails du contact professionnel](../../field-groups/profile/work-contact-details.md)</li><li>[Loyalty Details](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
