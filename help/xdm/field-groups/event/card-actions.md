---
title: Groupe de champs de schéma d’actions de carte
description: Ce document présente un aperçu du groupe de champs de schéma Actions carte .
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 9%

---

# [!UICONTROL Actions de carte] groupe de champs de schéma

[!UICONTROL Actions de carte] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Le groupe de champs fournit une `personalFinances.cardActions` à un schéma, qui capture les détails d’une action de carte, tels que le type de carte, l’état d’activation et l’état de verrouillage.

![](../../images/field-groups/card-actions.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `cardActivated` | Nombre entier | Effectue le suivi lorsque la carte a bien été activée. |
| `cardActivationStart` | Nombre entier | Effectue le suivi lorsque le processus d’activation des cartes a été démarré. |
| `cardCancelled` | Nombre entier | Effectue le suivi lorsqu’une carte a été annulée. |
| `cardControlsLocked` | Nombre entier | Effectue un suivi lorsque les commandes d’une carte ont été verrouillées. |
| `cardControlsUnlocked` | Nombre entier | Effectue un suivi lorsque les commandes d’une carte ont été déverrouillées. |
| `cardID` | Chaîne | Identifiant de la carte en cours d’activation. Cette valeur peut être différente du numéro de carte. |
| `cardLocked` | Nombre entier | Effectue le suivi lorsqu’une carte a été verrouillée. |
| `cardOrderNew` | Nombre entier | Effectue le suivi lorsqu’une carte a été demandée. |
| `cardOrderType` | Chaîne | Type de commande de carte associé à un événement de commande de carte. |
| `cardType` | Chaîne | Type de carte. |
| `cardUnlocked` | Nombre entier | Effectue le suivi lorsqu’une carte a été déverrouillée. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous à la section [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
