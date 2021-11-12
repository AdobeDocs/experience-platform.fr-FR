---
title: Classe des membres de la liste XDM Business Marketing
description: Ce document présente la classe XDM Business Marketing List Members dans le modèle de données d’expérience (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 5%

---

# [!UICONTROL Membres de la liste XDM Business Marketing] class

[!UICONTROL Membres de la liste XDM Business Marketing] est une classe XDM (Experience Data Model) standard qui décrit les membres, les personnes ou les contacts associés à une liste marketing.

![](../../images/classes/b2b/business-marketing-list-members.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si l’appartenance à une liste marketing provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `marketingListKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la liste marketing dont la personne est membre. |
| `marketingListMemberKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité d’appartenance à une liste marketing. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la personne qui est membre de la liste marketing. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de la variable `marketingListMemberID`. |
| `marketingListID` | Chaîne | Identifiant unique de la liste marketing. |
| `marketingListMemberID` | Chaîne | Identifiant unique de l’entité d’appartenance à une liste marketing. |
| `personId` | Chaîne | Identifiant unique de la personne. |

{style=&quot;table-layout:auto&quot;}

Consultez le guide sur la [relations de schéma dans l’édition B2B de la plateforme CDP en temps réel](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
