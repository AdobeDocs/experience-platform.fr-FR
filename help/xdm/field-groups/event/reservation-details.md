---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;ExperienceEvent;champs;schémas;schémas;conception de schéma;groupe de champs;groupe de champs;réservation;détails de réservation;;page d’accueil;schéma;schéma;schéma;schéma;schéma;groupe de champs;groupe de champs;groupe de réservation;détails de réservation
title: Groupe de champs de schéma Détails de la réservation
description: Ce document présente un aperçu du groupe de champs de schéma Détails de la réservation.
exl-id: 06f9ee37-9879-4db2-af68-9336366f7521
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 6%

---

# [!UICONTROL Groupe de champs ] Détails de la réservation

[!UICONTROL Réservation ] Détail d’un groupe de champs de schéma standard pour la  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) classe afin de capturer des informations concernant une réservation, notamment la longueur, la modification, le statut remboursable et le nombre de pièces.

Le groupe de champs fournit un champ de type objet unique, `reservations`. Les propriétés contenues dans cet objet sont expliquées ci-dessous.

![Structure des détails de la réservation](../../images/field-groups/reservation-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `nonRefundableAmount` | [Devise](../../data-types/currency.md) | Montant du prix de réservation qui est marqué comme non remboursable. |
| `transaction` | [Transaction](../../data-types/transaction.md) | Décrit la transaction de devise pour la réservation. |
| `id` | Chaîne | Identifiant unique de la réservation. |
| `cancellation` | Entier | Cette valeur est capturée lorsqu’une réservation a été annulée. |
| `confirmationNumber` | Chaîne | Numéro ou identifiant de confirmation de la réservation. |
| `created` | Entier | Cette valeur est capturée lorsque la réservation a été créée. |
| `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour effectuer l’achat. |
| `endDate` | DateTime | Date de fin d’abandon, de retour ou d’extraction pour la réservation. |
| `length` | Entier | Nombre total de jours pour la réservation. |
| `modification` | Entier | Cette valeur est capturée lorsqu’une réservation a été modifiée. |
| `modificationDate` | DateTime | Heure à laquelle la réservation a été modifiée pour la dernière fois. |
| `numberOfAdults` | Entier | Nombre d’adultes associés à la réservation. |
| `numberOfChildren` | Entier | Nombre d’enfants associés à la réservation. |
| `purpose` | Chaîne | L’objet de la réservation, généralement professionnel ou personnel. |
| `startDate` | DateTime | Date de démarrage, de sortie ou d’archivage de la réservation. |
| `triptype` | Chaîne | Indique si la réservation est pour un aller simple, un aller-retour ou un voyage dans plusieurs villes. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## Groupes de champs de réservation spécifiques au secteur

Il existe plusieurs autres groupes de champs standard qui étendent le schéma [!UICONTROL Détails de la réservation] pour les cas d’utilisation spécifiques au secteur. Pour plus d’informations, consultez la documentation suivante :

* [[!UICONTROL Définition de la réservation]](./dining-reservation.md)
* [[!UICONTROL Réservation en vol]](./flight-reservation.md)
* [[!UICONTROL Réservation logement]](./lodging-reservation.md)
