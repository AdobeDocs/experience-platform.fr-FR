---
title: Classe de liste XDM Business Marketing
description: Ce document présente la classe XDM Business Marketing List dans Experience Data Model (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 4%

---

# [!UICONTROL Classe de ] liste XDM Business Marketing

>[!NOTE]
>
>Cette classe est uniquement disponible pour les organisations qui ont accès à la plateforme de données clients en temps réel de l’édition B2B.

[!UICONTROL XDM Business Marketing ] List est une classe XDM (modèle de données d’expérience) standard qui capture les propriétés minimales requises d’une liste marketing. Les listes marketing vous permettent de classer par priorité les clients prospects les plus susceptibles d’acheter votre produit.

![](../../images/classes/b2b/business-marketing-list.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si la liste marketing provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `marketingListKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité de liste marketing. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de `marketingListID`. |
| `marketingListDescription` | Chaîne | Description de la liste marketing. |
| `marketingListID` | Chaîne | Identifiant unique de l’entité de liste marketing. |
| `marketingListName` | Chaîne | Nom de la liste marketing. |

Consultez le guide sur les [relations de schéma dans l’édition B2B de la plateforme des données clients en temps réel](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe est liée conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
