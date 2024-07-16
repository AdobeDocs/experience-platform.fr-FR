---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;réservation;repas;
title: Définition du groupe de champs de schéma de réservation
description: Découvrez le groupe de champs Définition du schéma de réservation .
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 13%

---

# Groupe de champs de schéma [!UICONTROL Définition de la réservation]

[!UICONTROL Réservation pour le dîner] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilisée pour capturer des informations concernant une réservation de repas.

Le groupe de champs est une extension du groupe de champs [!UICONTROL Détails de la réservation] et contient tous les mêmes champs sous un seul champ de type objet, `reservations`. Outre ces champs génériques, la [!UICONTROL réservation de repas] comprend également un tableau `diningReservations`. Ce tableau d’objets est utilisé pour décrire une ou plusieurs réservations avec des propriétés spécifiques à un restaurant.

>[!NOTE]
>
>Ce document couvre les détails du tableau `diningReservations`. Pour plus d’informations sur les autres champs fournis sous l’objet `reservations`, reportez-vous à la [[!UICONTROL référence du groupe de champs  Détails de la réservation]](./reservation-details.md).

![Définition de la structure de réservation](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` est un tableau d’objets qui représente une liste de réservations de restaurants. Si un événement de réservation implique des réservations dans plusieurs restaurants différents à des moments différents de la journée, par exemple, ces réservations peuvent être répertoriées comme des objets individuels sous `diningReservations` pour un seul événement.

La structure de chaque objet fourni sous `diningReservations` est fournie ci-dessous.

![structure de restaurantsRéservations](../../images/field-groups/dining-reservation/diningReservations.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `ID` | Chaîne | Numéro ou identifiant de la réservation. |
| `cancellation` | Nombre entier | Cette valeur est capturée lorsqu’une réservation a été annulée. |
| `confirmationNumber` | Chaîne | Numéro ou identifiant de confirmation de réservation. |
| `created` | Nombre entier | Cette valeur est capturée lorsqu’une réservation a été créée. |
| `cuisine` | Nombre entier | Le type de cuisine du restaurant. |
| `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour effectuer l’achat. |
| `deliveryPartners` | Chaîne | Partenaires de livraison disponibles pour le restaurant. |
| `diningOptions` | Chaîne | Options de livraison et de repas proposées par le restaurant. |
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
| `reservationTime` | DateTime | Heure de la réservation au restaurant. |
| `restaurantID` | Chaîne | Identifiant du restaurant ou de l’emplacement du restaurant. |
| `reservationStatus` | Chaîne | Le statut de la réservation. |
| `specialOccasion` | Booléen | Indique si la réservation est faite pour une occasion particulière. |
| `status` | Nombre entier | Statut de la réservation au restaurant. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
