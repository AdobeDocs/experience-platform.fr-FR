---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;réservation;vol;
title: Groupe de champs de schéma de réservation de vol
description: Découvrez le groupe de champs du schéma de réservation de vols.
exl-id: df4bb525-c2d3-4e1d-921f-903142a570ac
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 10%

---

# Groupe de champs de schéma [!UICONTROL Flight Reserve]

[!UICONTROL Flight Reserve] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilisée pour capturer des informations concernant une réservation de vol.

Le groupe de champs est une extension du groupe de champs [!UICONTROL Détails de la réservation] et contient tous les mêmes champs sous un seul champ de type objet, `reservations`. Outre ces champs génériques, la [!UICONTROL réservation de vol] comprend également un tableau `flightReservations`. Ce tableau d’objets est utilisé pour décrire une ou plusieurs réservations avec des propriétés propres au transport aérien.

>[!NOTE]
>
>Ce document couvre les détails du tableau `flightReservations`. Pour plus d’informations sur les autres champs fournis sous l’objet `reservations`, reportez-vous à la [[!UICONTROL référence du groupe de champs  Détails de la réservation]](./reservation-details.md).

![Structure de réservation de vol](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` est un tableau d’objets qui représente une liste de réservations de vols. Si un événement de réservation implique des réservations pour plusieurs vols de correspondance lors d’un voyage, par exemple, ces réservations peuvent être répertoriées comme des objets individuels sous `flightReservations` pour un seul événement.

La structure de chaque objet fourni sous `flightReservations` est fournie ci-dessous.

![Structure de flightReserve](../../images/field-groups/flight-reservation/flightReservations.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `flightCheckIn` | Objet | Capture les détails de l’enregistrement en vol. L’objet comprend les propriétés suivantes :<ul><li>`arrivalAirportCode` : (chaîne) code de l’aéroport de la ville d’arrivée.</li><li>`boardingGroup` : (chaîne). Indicateur spécifique de la compagnie aérienne de la commande d’embarquement.</li><li>`checkInMethod` : (chaîne). Méthode utilisée pour l’archivage, par exemple : compteur, en ligne, kiosque ou libre-service.</li><li>`checkedBags` : (nombre entier) nombre de sacs vérifiés pour le vol.</li><li>`checkedPassengers` : (nombre entier) nombre de passagers enregistrés pour le vol, s’il existe plusieurs passagers pour le même numéro de réservation.</li><li>`confirmationNumber` : (chaîne). Numéro ou identifiant de confirmation de réservation.</li><li>`departureAirportCode` : (chaîne) code de l’aéroport de la ville de départ.</li><li>`flightNumber` : (chaîne) numéro du vol pour le vol réservé.</li></ul> |
| `flightStatusSearch` | Objet | Capture les détails renvoyés lors de la recherche du statut du vol. L’objet comprend les propriétés suivantes :<ul><li>`arrivalAirportCode` : (chaîne) code de l’aéroport de la ville d’arrivée.</li><li>`boardingGroup` : (chaîne). Indicateur spécifique de la compagnie aérienne de la commande d’embarquement.</li><li>`departureAirportCode` : (chaîne) code de l’aéroport de la ville de départ.</li><li>`departureDate` : (DateTime) Date de départ du vol réservé.</li><li>`flightNumber` : (chaîne) numéro du vol pour le vol réservé.</li><li>`searchCount` : (nombre entier) nombre de fois où l’état du vol réservé a été recherché.</li></ul> |
| `agentID` | Chaîne | L’agent ou la personne chargée de la réservation, le cas échéant. |
| `aircraftID` | Chaîne | Un identifiant de l&#39;appareil. |
| `aircraftType` | Chaîne | Le type d&#39;avion. |
| `arrivalAirportCode` | Chaîne | Le code de l&#39;aéroport de la ville d&#39;arrivée. |
| `arrivalDate` | DateTime | Date d’arrivée du vol en cours de réservation. |
| `cancellation` | Nombre entier | Cette valeur est capturée lorsqu’une réservation a été annulée. |
| `confirmationNumber` | Chaîne | Numéro ou identifiant de confirmation de réservation. |
| `created` | Chaîne | Cette valeur est capturée lorsqu’une réservation a été créée. |
| `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour effectuer l’achat. |
| `departureAirportCode` | Chaîne | Le code de l&#39;aéroport de la ville de départ. |
| `departureDate` | DateTime | Date de départ du vol en cours de réservation. |
| `fareClass` | Chaîne | Classe tarifaire du vol en cours de réservation. |
| `flightNumber` | Chaîne | Numéro du vol réservé. |
| `length` | Nombre entier | Nombre total de jours pour la réservation. |
| `loyaltyID` | Chaîne | Identifiant du programme de fidélité ou de récompense pour le passager répertorié dans la réservation. |
| `modification` | Nombre entier | Cette valeur est capturée lorsqu’une réservation a été modifiée. |
| `modificationDate` | DateTime | Heure de la dernière modification de la réservation. |
| `numberOfAdults` | Nombre entier | Nombre d’adultes associés à la réservation. |
| `numberOfChildren` | Nombre entier | Nombre d’enfants associés à la réservation. |
| `passengerID` | Chaîne | Informations sur le passager associées à la réservation. |
| `purpose` | Chaîne | L’objet de la réservation, généralement professionnel ou personnel. |
| `salesChannel` | Chaîne | Canal de vente à partir duquel la réservation a été réservée. |
| `securityScreening` | Chaîne | Le type de contrôle de sécurité auquel le passager est soumis. |
| `status` | Chaîne | Statut de la réservation de vol. |
| `ticketNumber` | Chaîne | Numéro ou identifiant de la réservation. |
| `tripType` | Chaîne | Indique si la réservation est pour un aller simple, un aller-retour ou un voyage dans plusieurs villes. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
