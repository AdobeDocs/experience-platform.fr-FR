---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;réservation;hébergement;
title: Groupe de champs de schéma de réservation d’hébergement
description: Découvrez le groupe de champs Schéma de réservation de logement .
exl-id: f0eafc83-21f1-483d-9397-1133e3777699
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 6%

---

# [!UICONTROL Réservation logement] groupe de champs de schéma

[!UICONTROL Réservation logement] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) utilisé pour capturer des informations sur une réservation de logement.

Le groupe de champs est une extension de la variable [!UICONTROL Détails de la réservation] groupe de champs et contient tous les mêmes champs sous un seul champ de type objet, `reservations`. En plus de ces champs génériques, [!UICONTROL Réservation logement] inclut également `lodgingReservations` tableau. Ce tableau d’objets est utilisé pour décrire une ou plusieurs réservations avec des propriétés propres au logement.

>[!NOTE]
>
>Ce document couvre les détails du `lodgingReservations` tableau. Pour plus d’informations sur les autres champs fournis sous le `reservations` , reportez-vous à la section [[!UICONTROL Détails de la réservation] référence de groupe de champs](./reservation-details.md).

![Logement Structure de la réservation](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` est un tableau d’objets qui représente une liste de réservations. Si un événement de réservation implique des réservations dans plusieurs hôtels différents le long du parcours d’un voyage, par exemple, ces réservations peuvent être répertoriées comme des objets individuels sous `lodgingReservations` pour un seul événement.

La structure de chaque objet fournie sous `lodgingReservations` est fourni ci-dessous.

![structure lodgingReserve](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL Devise]](../../data-types/currency.md) | Le prix moyen journalier de la chambre d&#39;hôtel. |
| `lodgingCheckIn` | Objet | Objet décrivant les détails de l’archivage. Inclut les valeurs suivantes :<ul><li>`digitalKey`: (nombre entier) indique lorsqu’un invité sélectionne l’utilisation d’une clé numérique lors de son archivage.</li><li>`earlyCheckInRequested`: (nombre entier) indique lorsqu’un invité demande à s’archiver avant les heures d’archivage normales.</li><li>`lateCheckInRequested`: (nombre entier) indique lorsqu’un invité demande à s’archiver plus tard que les heures d’enregistrement normales.</li><li>`noRoomCheckIn`: (entier). Cette valeur est capturée lorsqu’un invité termine son archivage lorsqu’aucune pièce n’est disponible à ce moment-là.</li><li>`oneRoomCheckIn`: (entier). Cette valeur est capturée lorsqu’un invité termine son enregistrement lorsqu’une seule pièce est disponible à ce moment-là.</li><li>`roomKeys`: (nombre entier) nombre de clés de chambre standard fournies lors de l’archivage.</li><li>`userSelectedRoom`: (booléen). Indique si l’invité a sélectionné sa chambre à l’enregistrement.</li></ul> |
| `rackrate` | [[!UICONTROL Devise]](../../data-types/currency.md) | Le coût d’une réservation le même jour sans réservation préalable. |
| `ID` | Chaîne | Numéro ou identifiant de la réservation. |
| `agentID` | Chaîne | ID d’agent associé à la réservation de l’hôtel. |
| `basePrice` | Chaîne | Le prix de base avant toute remise. |
| `bookingID` | Chaîne | ID de réservation associé à la réservation de l’hôtel. |
| `cancellation` | Nombre entier | Cette valeur est capturée lorsqu’une réservation a été annulée. |
| `checkInDate` | DateTime | La date d’enregistrement de la réservation de la chambre. |
| `checkOutDate` | DateTime | Date de passage pour la réservation de la chambre. |
| `confirmationNumber` | Chaîne | Numéro ou identifiant de confirmation de réservation. |
| `couponCode` | Chaîne | Code coupon associé à la réservation de l’hôtel. |
| `created` | Nombre entier | Cette valeur est capturée lorsqu’une réservation a été créée. |
| `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour effectuer l’achat. |
| `discountPercent` | Double | Pourcentage de remise associé à la réservation. |
| `freeCancelation` | Booléen | Indique si la chambre a une politique d’annulation gratuite. |
| `guestID` | Chaîne | ID d’invité associé à la réservation de l’hôtel. |
| `length` | Nombre entier | Nombre total de jours pour la réservation. |
| `loyaltyID` | Chaîne | L’identifiant du programme de fidélité de l’invité répertorié dans la réservation. |
| `modification` | Nombre entier | Cette valeur est capturée lorsqu’une réservation a été modifiée. |
| `modificationDate` | DateTime | Heure de la dernière modification de la réservation. |
| `numberOfAdults` | Nombre entier | Nombre d’adultes associés à la réservation. |
| `numberOfChildren` | Nombre entier | Nombre d’enfants associés à la réservation. |
| `numberOfRooms` | Nombre entier | Nombre de chambres associées à la réservation. |
| `propertyID` | Chaîne | Identifiant de l’hôtel ou du complexe pour la réservation. |
| `propertyName` | Chaîne | Nom de l’hôtel ou du complexe pour la réservation. |
| `purpose` | Chaîne | L’objet de la réservation, généralement professionnel ou personnel. |
| `ratePlan` | Chaîne | La transaction de taux sur laquelle la pièce a été vendue. |
| `refundable` | Booléen | Indique si la chambre est remboursable. |
| `reservationStatus` | Chaîne | Le statut de la réservation. |
| `roomAccessibilityType` | Chaîne | Type d’accessibilité de la pièce, tel que la mobilité, l’audition ou autre. |
| `roomCapacity` | Nombre entier | Nombre de personnes que contient la chambre d’hôtel. |
| `roomType` | Chaîne | Le type de chambre réservé. |
| `smoking` | Booléen | Indique si la pièce permet de fumer. |
| `tripType` | Chaîne | Indique si la réservation est pour un aller simple, un aller-retour ou un voyage dans plusieurs villes. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
