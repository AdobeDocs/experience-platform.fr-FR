---
title: Classe des membres de la liste XDM Business Marketing
description: Ce document présente la classe XDM Business Marketing List Members dans le modèle de données d’expérience (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 7%

---

# [!UICONTROL Classe ] Membres de la liste XDM Business Marketing (bêta)

>[!IMPORTANT]
>
>Cette classe est disponible dans le cadre de la plateforme de données clients en temps réel de l’édition B2B, actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

[!UICONTROL L’] appartenance à une liste XDM de marketing constitue une classe XDM (Experience Data Model) standard qui décrit les membres, les personnes ou les contacts associés à une liste marketing.

![](../../images/classes/b2b/business-marketing-list-members.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si l’appartenance à une liste marketing provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `marketingListKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la liste marketing dont la personne est membre. |
| `marketingListMemberKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité d’appartenance à une liste marketing. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la personne qui est membre de la liste marketing. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de `marketingListMemberID`. |
| `marketingListID` | Chaîne | Identifiant unique de la liste marketing. |
| `marketingListMemberID` | Chaîne | Identifiant unique de l’entité d’appartenance à une liste marketing. |
| `personId` | Chaîne | Identifiant unique de la personne. |

{style=&quot;table-layout:auto&quot;}

Consultez le guide sur les [relations de schéma dans l’édition B2B de la plateforme des données clients en temps réel](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe est liée conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
