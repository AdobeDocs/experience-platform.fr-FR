---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;réservation;vol;
title: Groupe de champs de schéma de réservation de vol
description: Ce document présente un aperçu du groupe de champs du schéma de réservation de vol.
exl-id: df4bb525-c2d3-4e1d-921f-903142a570ac
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 5%

---

# [!UICONTROL Réservation en vol] groupe de champs de schéma

[!UICONTROL Réservation en vol] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) utilisé pour capturer des informations concernant une réservation de vol.

Le groupe de champs est une extension de la variable [!UICONTROL Détails de la réservation] groupe de champs et contient tous les mêmes champs sous un seul champ de type objet, `reservations`. En plus de ces champs génériques, [!UICONTROL Réservation en vol] inclut également `flightReservations` tableau. Ce tableau d’objets est utilisé pour décrire une ou plusieurs réservations avec des propriétés propres au transport aérien.

>[!NOTE]
>
>Ce document couvre les détails de la variable `flightReservations` tableau. Pour plus d’informations sur les autres champs fournis sous le `reservations` , reportez-vous à la section [[!UICONTROL Détails de la réservation] référence de groupe de champs](./reservation-details.md).

![Structure de la réservation de vol](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` est un tableau d’objets qui représente une liste de réservations de vols. Si un événement de réservation implique des réservations pour plusieurs vols de correspondance lors d&#39;un voyage, par exemple, ces réservations peuvent être répertoriées comme des objets individuels sous `flightReservations` pour un seul événement.

La structure de chaque objet fournie sous `flightReservations` est fourni ci-dessous.

![Structure de flightReserve](../../images/field-groups/flight-reservation/flightReservations.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `flightCheckIn` | Objet | Capture les détails de l’enregistrement en vol. L’objet comprend les propriétés suivantes :<ul><li>`arrivalAirportCode`: (Chaîne) Code d’aéroport de la ville d’arrivée.</li><li>`boardingGroup`: (Chaîne) Indicateur de commande d’embarquement spécifique à la compagnie aérienne.</li><li>`checkInMethod`: (Chaîne) Méthode utilisée pour l’archivage, comme le compteur, en ligne, le kiosque ou le libre-service.</li><li>`checkedBags`: (Nombre entier) Nombre de sacs vérifiés pour le vol.</li><li>`checkedPassengers`: (Nombre entier) Nombre de passagers enregistrés pour le vol, s’il existe plusieurs passagers pour le même numéro de réservation.</li><li>`confirmationNumber`: (Chaîne) Numéro de confirmation de réservation ou identifiant.</li><li>`departureAirportCode`: (Chaîne) Code d’aéroport de la ville de départ.</li><li>`flightNumber`: (Chaîne) Numéro de vol du vol réservé.</li></ul> |
| `flightStatusSearch` | Objet | Capture les détails renvoyés lors de la recherche de l’état du vol. L’objet comprend les propriétés suivantes :<ul><li>`arrivalAirportCode`: (Chaîne) Code d’aéroport de la ville d’arrivée.</li><li>`boardingGroup`: (Chaîne) Indicateur de commande d’embarquement spécifique à la compagnie aérienne.</li><li>`departureAirportCode`: (Chaîne) Code d’aéroport de la ville de départ.</li><li>`departureDate`: (DateTime) Date de départ du vol réservé.</li><li>`flightNumber`: (Chaîne) Numéro de vol du vol réservé.</li><li>`searchCount`: (Entier) Le nombre de fois où le statut du vol réservé a été recherché.</li></ul> |
| `agentID` | Chaîne | L’agent ou la personne chargée de la réservation, le cas échéant. |
| `aircraftID` | Chaîne | Un identifiant de l&#39;appareil. |
| `aircraftType` | Chaîne | Le type d&#39;avion. |
| `arrivalAirportCode` | Chaîne | Le code de l&#39;aéroport de la ville d&#39;arrivée. |
| `arrivalDate` | DateTime | Date d&#39;arrivée du vol réservé. |
| `cancellation` | Nombre entier | Cette valeur est capturée lorsqu’une réservation a été annulée. |
| `confirmationNumber` | Chaîne | Numéro ou identifiant de confirmation de réservation. |
| `created` | Chaîne | Cette valeur est capturée lorsqu’une réservation a été créée. |
| `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour effectuer l’achat. |
| `departureAirportCode` | Chaîne | Le code de l&#39;aéroport de la ville de départ. |
| `departureDate` | DateTime | La date de départ du vol réservé. |
| `fareClass` | Chaîne | La classe de tarif du vol réservé. |
| `flightNumber` | Chaîne | Numéro du vol réservé. |
| `length` | Nombre entier | Nombre total de jours pour la réservation. |
| `loyaltyID` | Chaîne | Identifiant du programme de fidélité ou de récompense pour le passager répertorié dans la réservation. |
| `modification` | Nombre entier | Cette valeur est capturée lorsqu’une réservation a été modifiée. |
| `modificationDate` | DateTime | Heure à laquelle la réservation a été modifiée pour la dernière fois. |
| `numberOfAdults` | Nombre entier | Nombre d’adultes associés à la réservation. |
| `numberOfChildren` | Nombre entier | Nombre d’enfants associés à la réservation. |
| `passengerID` | Chaîne | Informations sur les passagers associées à la réservation. |
| `purpose` | Chaîne | L’objet de la réservation, généralement professionnel ou personnel. |
| `salesChannel` | Chaîne | Canal de vente à partir duquel la réservation a été réservée. |
| `securityScreening` | Chaîne | Le type de contrôle de sécurité auquel le passager est soumis. |
| `status` | Chaîne | Statut de la réservation de vol. |
| `ticketNumber` | Chaîne | Numéro ou identifiant de la réservation. |
| `tripType` | Chaîne | Indique si la réservation est pour un aller simple, un aller-retour ou un voyage dans plusieurs villes. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
