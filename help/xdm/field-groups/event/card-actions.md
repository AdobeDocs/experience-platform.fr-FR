---
title: Groupe de champs de schéma Actions de carte
description: Découvrez le groupe de champs de schéma Actions de carte .
exl-id: 49851544-9118-4b73-b1d1-4cf49b3f1dee
TQID: https://experienceleague.adobe.com/yEkB4QzAstJgzhhroOYGcURFJFbdpS55WOp-I2NeNXI
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 185
ht-degree: 8%

---

# [!UICONTROL Card Actions] groupe de champs de schéma

[!UICONTROL Card Actions] groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Le groupe de champs fournit un champ de `personalFinances.cardActions` unique à un schéma, qui capture les détails d’une action de carte, tels que le type de carte, le statut d’activation et le statut de verrouillage.

![](../../images/field-groups/card-actions.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `cardActivated` | Entier | Indique à quel moment la carte a été activée. |
| `cardActivationStart` | Entier | Indique à quel moment le processus d’activation de la carte a commencé. |
| `cardCancelled` | Entier | Indique quand une carte a été annulée. |
| `cardControlsLocked` | Entier | Indique à quel moment les commandes d’une carte ont été verrouillées. |
| `cardControlsUnlocked` | Entier | Indique à quel moment les contrôles d’une carte ont été déverrouillés. |
| `cardID` | Chaîne | Identifiant de la carte en cours d’activation. Cette valeur peut être différente du numéro de carte. |
| `cardLocked` | Entier | Indique à quel moment une carte a été verrouillée. |
| `cardOrderNew` | Entier | Indique à quel moment une carte a été demandée. |
| `cardOrderType` | Chaîne | Type de commande de carte associé à un événement de commande de carte. |
| `cardType` | Chaîne | Type de carte. |
| `cardUnlocked` | Entier | Indique à quel moment une carte a été déverrouillée. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
