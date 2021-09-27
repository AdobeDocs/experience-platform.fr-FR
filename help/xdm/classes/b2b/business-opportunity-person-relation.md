---
title: Classe de relation d’une personne avec une opportunité commerciale XDM
description: Ce document présente la classe XDM Business Opportunity Person Relation dans Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 4%

---

# [!UICONTROL Classe de ] relation de personne avec les opportunités commerciales XDM

>[!NOTE]
>
>Cette classe est disponible uniquement pour les organisations qui ont accès à l’édition B2B de la plateforme de données clients en temps réel.

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
