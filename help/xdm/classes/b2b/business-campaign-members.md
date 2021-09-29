---
title: Classe des membres XDM Business Campaign
description: Ce document présente la classe XDM Business Campaign Members dans le modèle de données d’expérience (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 8%

---

# [!UICONTROL Classe ] membres XDM Business Campaign (bêta)

>[!IMPORTANT]
>
>Cette classe est disponible dans le cadre de la plateforme de données clients en temps réel de l’édition B2B, actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

[!UICONTROL L’] appartenance à une campagne XDM est une classe XDM (Experience Data Model) standard qui décrit un contact ou un prospect associé à une campagne commerciale.

![](../../images/classes/b2b/business-campaign-members.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la campagne associée. |
| `campaignMemberKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité d’appartenance à une campagne. |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si l’adhésion à la campagne provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la personne qui est membre de la campagne associée. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de `campaignMemberID`. |
| `campaignID` | Chaîne | Identifiant unique de la campagne associée. |
| `campaignMemberID` | Chaîne | Identifiant unique de l’entité d’appartenance à une campagne. |
| `personId` | Chaîne | Identifiant unique de la personne qui est membre de la campagne associée. |

{style=&quot;table-layout:auto&quot;}

Consultez le guide sur les [relations de schéma dans l’édition B2B de la plateforme des données clients en temps réel](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe est liée conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
