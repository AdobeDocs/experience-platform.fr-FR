---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;réservation;repas;
title: Définition du groupe de champs de schéma de réservation
description: Découvrez le groupe de champs Définition du schéma de réservation .
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 6%

---

# [!UICONTROL Définition de la réservation] groupe de champs de schéma

[!UICONTROL Définition de la réservation] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) utilisé pour capturer des informations sur une réservation de repas.

Le groupe de champs est une extension de la variable [!UICONTROL Détails de la réservation] groupe de champs et contient tous les mêmes champs sous un seul champ de type objet, `reservations`. En plus de ces champs génériques, [!UICONTROL Définition de la réservation] inclut également `diningReservations` tableau. Ce tableau d’objets est utilisé pour décrire une ou plusieurs réservations avec des propriétés spécifiques à un restaurant.

>[!NOTE]
>
>Ce document couvre les détails du `diningReservations` tableau. Pour plus d’informations sur les autres champs fournis sous le `reservations` , reportez-vous à la section [[!UICONTROL Détails de la réservation] référence de groupe de champs](./reservation-details.md).

![Définition de la structure de réservation](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` est un tableau d’objets qui représente une liste de réservations de restaurants. Si un événement de réservation implique des réservations dans plusieurs restaurants différents à des moments différents de la journée, par exemple, ces réservations peuvent être répertoriées comme des objets individuels sous `diningReservations` pour un seul événement.

La structure de chaque objet fournie sous `diningReservations` est fourni ci-dessous.

![structure de restaurants](../../images/field-groups/dining-reservation/diningReservations.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `ID` | Chaîne | Numéro ou identifiant de la réservation. |
| `cancellation` | Nombre entier | Cette valeur est capturée lorsqu’une réservation a été annulée. |
| `confirmationNumber` | Chaîne | Numéro ou identifiant de confirmation de réservation. |
| `created` | Nombre entier | Cette valeur est capturée lorsqu’une réservation a été créée. |
| `cuisine` | Nombre entier | Le type de cuisine du restaurant. |
| `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour effectuer l’achat. |
| `deliveryPartners` | Chaîne | Partenaires de diffusion disponibles depuis le restaurant. |
| `diningOptions` | Chaîne | Options de livraison et de restauration disponibles au restaurant. |
| `groupReservation` | Booléen | Indique si la réservation est faite pour un groupe. |
| `length` | Nombre entier | Nombre total de jours pour la réservation. |
| `loyaltyID` | Chaîne | L’identifiant du programme de fidélité de l’invité répertorié dans la réservation. |
| `modification` | Nombre entier | Cette valeur est capturée lorsqu’une réservation a été modifiée. |
| `modificationDate` | DateTime | Heure de la dernière modification de la réservation. |
| `numberOfAdults` | Nombre entier | Nombre d’adultes associés à la réservation. |
| `numberOfChildren` | Nombre entier | Nombre d’enfants associés à la réservation. |
| `numberOfRooms` | Nombre entier | Nombre de chambres associées à la réservation. |
| `partySize` | Nombre entier | Le nombre d&#39;individus dans la fête. |
| `priceCategory` | Chaîne | La catégorie de prix de la réservation en cours. |
| `purpose` | Chaîne | L’objet de la réservation, généralement professionnel ou personnel. |
| `reservationTime` | DateTime | Heure pour laquelle la réservation de repas est effectuée. |
| `restaurantID` | Chaîne | Identifiant du restaurant ou de l’emplacement du restaurant. |
| `reservationStatus` | Chaîne | Le statut de la réservation. |
| `specialOccasion` | Booléen | Indique si la réservation est faite pour une occasion particulière. |
| `status` | Nombre entier | Statut de la réservation du repas. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
