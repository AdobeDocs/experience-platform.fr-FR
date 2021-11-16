---
title: Classe des membres XDM Business Campaign
description: Ce document présente la classe XDM Business Campaign Members dans le modèle de données d’expérience (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 4%

---

# [!UICONTROL Membres de XDM Business Campaign] class

>[!IMPORTANT]
>
>Cette classe est destinée aux organisations ayant accès à [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Pour que cette classe puisse participer à , vous devez avoir accès à l’édition B2B de la plateforme CDP en temps réel . [Real-time Customer Profile](../../../profile/home.md).

[!UICONTROL Membres de XDM Business Campaign] est une classe XDM (Experience Data Model) standard qui décrit un contact ou un prospect associé à une campagne commerciale.

![](../../images/classes/b2b/business-campaign-members.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la campagne associée. |
| `campaignMemberKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité d’appartenance à une campagne. |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si l’adhésion à la campagne provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la personne qui est membre de la campagne associée. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de la variable `campaignMemberID`. |
| `campaignID` | Chaîne | Identifiant unique de la campagne associée. |
| `campaignMemberID` | Chaîne | Identifiant unique de l’entité d’appartenance à une campagne. |
| `personId` | Chaîne | Identifiant unique de la personne qui est membre de la campagne associée. |

{style=&quot;table-layout:auto&quot;}

Consultez le guide sur la [relations de schéma dans l’édition B2B de la plateforme CDP en temps réel](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
