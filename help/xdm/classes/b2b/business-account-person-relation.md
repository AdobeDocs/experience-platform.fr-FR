---
title: Classe de relation de personne de compte professionnel XDM
description: Ce document présente la classe XDM Business Account Person Relation dans le modèle de données d’expérience (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 5%

---

# [!UICONTROL Relation avec la personne du compte d’entreprise XDM] class

[!UICONTROL Relation avec la personne du compte d’entreprise XDM] est une classe XDM (Experience Data Model) standard qui capture les propriétés minimales requises d’une personne associée à un compte d’entreprise.

![](../../images/classes/b2b/business-account-person-relation.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite du compte dans la relation entre le compte et la personne. |
| `accountPersonKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité de relation compte-personne. |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si la relation compte-personne provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la personne dans la relation compte-personne. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte des autres champs d’ID capturés par la classe . |
| `accountID` | Chaîne | Identifiant unique du compte dans la relation compte-personne. |
| `accountPersonID` | Chaîne | Identifiant unique de l’entité de relation compte-personne. |
| `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour la relation entre le compte et la personne. |
| `isActive` | Booléen | Indique si la relation entre le compte et la personne est principale. |
| `isDirect` | Booléen | Indique s’il s’agit d’une relation directe entre le compte et la personne. |
| `isPrimary` | Booléen | Indique si la personne est le contact Principal sur ce compte. |
| `personID` | Chaîne | Identifiant unique de la personne dans la relation compte-personne. |
| `personRole` | Chaîne | Le rôle de la personne dans la relation entre le compte et la personne. |
| `relationEndDate` | DateTime | Date à laquelle la relation entre le compte et la personne s’est terminée. |
| `relationStartDate` | DateTime | Date à laquelle la relation entre le compte et la personne a commencé. |

{style=&quot;table-layout:auto&quot;}

Consultez le guide sur la [relations de schéma dans l’édition B2B de la plateforme CDP en temps réel](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
