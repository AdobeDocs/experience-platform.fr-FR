---
title: Classe de campagne commerciale XDM
description: Ce document présente la classe XDM Business Campaign dans le modèle de données d’expérience (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 7%

---

# [!UICONTROL Campagne commerciale XDM] class

[!UICONTROL Campagne commerciale XDM] est une classe XDM (Experience Data Model) standard qui capture les propriétés minimales requises d’une campagne d’entreprise.

![](../../images/classes/b2b/business-campaign.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité de campagne. |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si la campagne provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de la variable `campaignID`. |
| `campaignDescription` | Chaîne | Description de la campagne. |
| `campaignID` | Chaîne | Identifiant unique de l’entité de campagne. |
| `campaignName` | Chaîne | Nom de la campagne. |
| `campaignType` | Chaîne | Type de campagne ou audience cible. |

{style=&quot;table-layout:auto&quot;}

Consultez le guide sur la [relations de schéma dans l’édition B2B de la plateforme CDP en temps réel](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
