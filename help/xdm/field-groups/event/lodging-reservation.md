---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;réservation;hébergement;
title: Groupe de champs de schéma de réservation d’hébergement
description: Ce document présente un aperçu du groupe de champs Schéma de réservation de logement .
source-git-commit: d230cfa9e74eb96aa44e8b83ca8f2306db4ba4ec
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 6%

---


# [!UICONTROL Groupe de champs ] de schéma de réservation

[!UICONTROL La ] réservation d’hébergement est un groupe de champs de schéma standard pour la  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) classe afin de capturer des informations concernant une réservation d’hébergement.

Le groupe de champs est une extension du groupe de champs [!UICONTROL Détails de la réservation] et contient tous les mêmes champs sous un seul champ de type objet, `reservations`. Outre ces champs génériques, [!UICONTROL Réservation logement] comprend également le tableau `lodgingReservations`. Ce tableau d’objets est utilisé pour décrire une ou plusieurs réservations avec des propriétés propres au logement.

>[!NOTE]
>
>Ce document couvre les détails du tableau `lodgingReservations`. Pour plus d’informations sur les autres champs fournis sous l’objet `reservations`, reportez-vous à la [[!UICONTROL Référence du groupe de champs ] ](./reservation-details.md).

![Logement Structure de la réservation](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` est un tableau d’objets qui représente une liste de réservations. Si un événement de réservation implique des réservations dans plusieurs hôtels différents le long de la route d’un voyage, par exemple, ces réservations peuvent être répertoriées comme des objets individuels sous `lodgingReservations` pour un seul événement.

La structure de chaque objet fournie sous `lodgingReservations` est fournie ci-dessous.

![structure lodgingReserve](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL Devise]](../../data-types/currency.md) | Prix moyen journalier de la chambre d&#39;hôtel. |
| `lodgingCheckIn` | Objet | Objet décrivant les détails de l’archivage. Inclut les valeurs suivantes :<ul><li>`digitalKey`: (Entier) Indique lorsqu’un invité sélectionne l’utilisation d’une clé numérique lors de son archivage.</li><li>`earlyCheckInRequested`: (Entier) Indique lorsqu’un invité demande à s’archiver avant les heures d’archivage normales.</li><li>`lateCheckInRequested`: (Entier) Indique lorsqu’un invité demande à s’archiver plus tard que les heures d’enregistrement normales.</li><li>`noRoomCheckIn`: (Entier) Cette valeur est capturée lorsqu’un invité termine son archivage lorsqu’il n’y a aucune pièce disponible à ce moment.</li><li>`oneRoomCheckIn`: (Entier) Cette valeur est capturée lorsqu’un invité termine son enregistrement lorsqu’une seule pièce est disponible à ce moment.</li><li>`roomKeys`: (Entier) Nombre de clés de chambre standard fournies lors de l’archivage.</li><li>`userSelectedRoom`: (Booléen) Indique si l’invité a sélectionné sa chambre à l’enregistrement.</li></ul> |
| `rackrate` | [[!UICONTROL Devise]](../../data-types/currency.md) | Le coût d’une réservation le même jour sans réservation préalable. |
| `ID` | Chaîne | Numéro ou identifiant de la réservation. |
| `agentID` | Chaîne | L’ID d’agent associé à la réservation de l’hôtel. |
| `basePrice` | Chaîne | Le prix de base avant toute remise. |
| `bookingID` | Chaîne | ID de réservation associé à la réservation de l’hôtel. |
| `cancellation` | Entier | Cette valeur est capturée lorsqu’une réservation a été annulée. |
| `checkInDate` | DateTime | La date d’enregistrement de la réservation de la chambre. |
| `checkOutDate` | DateTime | Date de passage pour la réservation de la chambre. |
| `confirmationNumber` | Chaîne | Numéro ou identifiant de confirmation de réservation. |
| `couponCode` | Chaîne | Code coupon associé à la réservation de l’hôtel. |
| `created` | Entier | Cette valeur est capturée lorsqu’une réservation a été créée. |
| `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour effectuer l’achat. |
| `discountPercent` | Double | Pourcentage de remise associé à la réservation. |
| `freeCancelation` | Booléen | Indique si la chambre a une politique d’annulation gratuite. |
| `guestID` | Chaîne | ID d’invité associé à la réservation de l’hôtel. |
| `length` | Entier | Nombre total de jours pour la réservation. |
| `loyaltyID` | Chaîne | L’identifiant du programme de fidélité de l’invité répertorié dans la réservation. |
| `modification` | Entier | Cette valeur est capturée lorsqu’une réservation a été modifiée. |
| `modificationDate` | DateTime | Heure à laquelle la réservation a été modifiée pour la dernière fois. |
| `numberOfAdults` | Entier | Nombre d’adultes associés à la réservation. |
| `numberOfChildren` | Entier | Nombre d’enfants associés à la réservation. |
| `numberOfRooms` | Entier | Nombre de chambres associées à la réservation. |
| `propertyID` | Chaîne | Identifiant de l’hôtel ou du complexe pour la réservation. |
| `propertyName` | Chaîne | Nom de l’hôtel ou du complexe pour la réservation. |
| `purpose` | Chaîne | L’objet de la réservation, généralement professionnel ou personnel. |
| `ratePlan` | Chaîne | La transaction de taux sur laquelle la pièce a été vendue. |
| `refundable` | Booléen | Indique si la chambre est remboursable. |
| `reservationStatus` | Chaîne | Le statut de la réservation. |
| `roomAccessibilityType` | Chaîne | Type d’accessibilité de la pièce, tel que la mobilité, l’audition ou autre. |
| `roomCapacity` | Entier | Nombre de personnes que contient la chambre d’hôtel. |
| `roomType` | Chaîne | Le type de chambre réservé. |
| `smoking` | Booléen | Indique si la pièce permet de fumer. |
| `tripType` | Chaîne | Indique si la réservation est pour un aller simple, un aller-retour ou un voyage dans plusieurs villes. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
