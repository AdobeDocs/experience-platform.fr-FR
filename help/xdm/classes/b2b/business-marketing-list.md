---
title: Classe de liste XDM Business Marketing
description: Ce document présente la classe XDM Business Marketing List dans Experience Data Model (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 5%

---

# [!UICONTROL Liste XDM Business Marketing] class

[!UICONTROL Liste XDM Business Marketing] est une classe XDM (Experience Data Model) standard qui capture les propriétés minimales requises d’une liste marketing. Les listes marketing vous permettent de classer par priorité les clients prospects les plus susceptibles d’acheter votre produit.

![](../../images/classes/b2b/business-marketing-list.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si la liste marketing provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `marketingListKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité de liste marketing. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de la variable `marketingListID`. |
| `marketingListDescription` | Chaîne | Description de la liste marketing. |
| `marketingListID` | Chaîne | Identifiant unique de l’entité de liste marketing. |
| `marketingListName` | Chaîne | Nom de la liste marketing. |

{style=&quot;table-layout:auto&quot;}

Consultez le guide sur la [relations de schéma dans l’édition B2B de la plateforme CDP en temps réel](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
