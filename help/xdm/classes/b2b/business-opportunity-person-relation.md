---
title: Classe de relation d’une personne avec une opportunité commerciale XDM
description: Ce document présente la classe XDM Business Opportunity Person Relation dans Experience Data Model (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 3%

---

# [!UICONTROL Classe de ] relation de personne avec les opportunités commerciales XDM

>[!NOTE]
>
>Cette classe est uniquement disponible pour les organisations qui ont accès à la plateforme de données clients en temps réel de l’édition B2B.

[!UICONTROL XDM Business Opportunity Persson ] Relationship est une classe XDM standard qui capture les propriétés minimales requises d’une personne associée à une opportunité commerciale.

![](../../images/classes/b2b/business-opportunity-person-relation.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si la relation homme-entreprise provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `opportunityKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’opportunité dans la relation opportunité-personne. |
| `opportunityPersonKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité de relation opportunité-personne. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la personne dans la relation opportunité-personne. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte des autres champs d’ID capturés par la classe . |
| `opportunityID` | Chaîne | Identifiant unique de l’opportunité dans la relation opportunité-personne. |
| `opportunityPersonID` | Chaîne | Identifiant unique de l’entité de relation opportunité-personne |
| `isPrimary` | Booléen | Indique si la personne est le contact Principal pour cette opportunité. |
| `personID` | Chaîne | Identifiant unique de la personne dans la relation opportunité-personne. |
| `personRole` | Chaîne | Le rôle de la personne dans la relation opportunité-personne. |

Consultez le guide sur les [relations de schéma dans l’édition B2B de la plateforme des données clients en temps réel](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe est liée conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
