---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;ExperienceEvent;champs;schémas;Schémas;Conception de schéma;groupe de champs;groupe de champs;réservation;détails de réservation;
title: Groupe de champs de schéma des détails de la réservation
description: Découvrez le groupe de champs de schéma Détails de la réservation.
exl-id: 06f9ee37-9879-4db2-af68-9336366f7521
TQID: https://experienceleague.adobe.com/N1FtdebvPbxQaTHOLf5h2zWt2AAMr2X2GAUjZKqQCrY
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 350
ht-degree: 7%

---

# [!UICONTROL Détails de la réservation] groupe de champs de schéma

[!UICONTROL Détails de la réservation] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilisé pour capturer des informations concernant une réservation, notamment la durée, la modification, le statut de remboursement et le nombre de chambres.

Le groupe de champs fournit un seul champ de type objet, `reservations`. Les propriétés contenues dans cet objet sont expliquées ci-dessous.

![Structure des détails de la réservation](../../images/field-groups/reservation-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `nonRefundableAmount` | [Devise](../../data-types/currency.md) | Montant du prix de la réservation marqué comme non remboursable. |
| `transaction` | [ Transaction ](../../data-types/transaction.md) | Décrit la transaction de devise pour la réservation. |
| `id` | Chaîne | Identifiant unique de la réservation. |
| `cancellation` | Entier | Cette valeur est capturée lorsqu’une réservation a été annulée. |
| `confirmationNumber` | Chaîne | Numéro ou identifiant de confirmation de la réservation. |
| `created` | Entier | Cette valeur est capturée lorsque la réservation a été créée. |
| `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour effectuer l’achat. |
| `endDate` | DateTime | Date de fin de la restitution, du retour ou du départ pour la réservation. |
| `length` | Entier | Nombre total de jours pour la réservation. |
| `modification` | Entier | Cette valeur est capturée lorsqu’une réservation a été modifiée. |
| `modificationDate` | DateTime | Heure à laquelle la réservation a été modifiée pour la dernière fois. |
| `numberOfAdults` | Entier | Nombre d’adultes associés à la réservation. |
| `numberOfChildren` | Entier | Nombre d’enfants associés à la réservation. |
| `purpose` | Chaîne | L’objectif de la réservation, généralement professionnel ou personnel. |
| `startDate` | DateTime | Date de début de prise en charge, de départ ou d’enregistrement de la réservation. |
| `triptype` | Chaîne | Indique si la réservation concerne un aller simple, un aller-retour ou un voyage multi-villes. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## Groupes de champs de réservation spécifiques au secteur

Il existe plusieurs autres groupes de champs standard qui étendent le schéma [!UICONTROL  Détails de la réservation ] pour des cas d’utilisation spécifiques au secteur. Pour plus d’informations, consultez la documentation suivante :

* [[!UICONTROL Réservation de restaurant]](./dining-reservation.md)
* [[!UICONTROL Réservation de vol]](./flight-reservation.md)
* [[!UICONTROL Réservation de logement]](./lodging-reservation.md)
