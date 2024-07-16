---
title: Groupe de champs de schéma d’actions de carte
description: Découvrez le groupe de champs de schéma Actions carte .
exl-id: 49851544-9118-4b73-b1d1-4cf49b3f1dee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 24%

---

# [!UICONTROL Groupe de champs de schéma Actions de carte]

[!UICONTROL Actions de carte] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Le groupe de champs fournit un champ `personalFinances.cardActions` unique à un schéma, qui capture les détails d’une action de carte comme le type de carte, l’état d’activation et l’état de verrouillage.

![](../../images/field-groups/card-actions.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `cardActivated` | Nombre entier | Effectue le suivi lorsque la carte a bien été activée. |
| `cardActivationStart` | Nombre entier | Effectue le suivi lorsque le processus d’activation des cartes a été démarré. |
| `cardCancelled` | Nombre entier | Indique à quel moment une carte a été annulée. |
| `cardControlsLocked` | Nombre entier | Effectue un suivi lorsque les commandes d’une carte ont été verrouillées. |
| `cardControlsUnlocked` | Nombre entier | Effectue un suivi lorsque les commandes d’une carte ont été déverrouillées. |
| `cardID` | Chaîne | Identifiant de la carte en cours d’activation. Cette valeur peut être différente du numéro de carte. |
| `cardLocked` | Nombre entier | Indique à quel moment une carte a été verrouillée. |
| `cardOrderNew` | Nombre entier | Indique à quel moment une carte a été demandée. |
| `cardOrderType` | Chaîne | Type de commande de carte associé à un événement de commande de carte. |
| `cardType` | Chaîne | Type de carte. |
| `cardUnlocked` | Nombre entier | Indique à quel moment une carte a été déverrouillée. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
