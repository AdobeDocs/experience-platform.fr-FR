---
title: Classe des membres de la liste XDM Business Marketing
description: Ce document présente la classe XDM Business Marketing List Members dans le modèle de données d’expérience (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 4%

---

# [!UICONTROL Classe ] Membres de la liste XDM Business Marketing

>[!NOTE]
>
>Cette classe est disponible uniquement pour les organisations qui ont accès à l’édition B2B de la plateforme de données clients en temps réel.

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
