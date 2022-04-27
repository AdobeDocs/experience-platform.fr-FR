---
title: Classe de campagne commerciale XDM
description: Ce document présente la classe XDM Business Campaign dans le modèle de données d’expérience (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: 0084492ed467c5996a94c5c55a79c9faf8f5046e
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 8%

---

# [!UICONTROL Campagne commerciale XDM] class

>[!IMPORTANT]
>
>Cette classe est destinée aux organisations ayant accès à [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Pour que cette classe puisse participer à , vous devez avoir accès à l’édition B2B de la plateforme CDP en temps réel . [Real-time Customer Profile](../../../profile/home.md).

[!UICONTROL Campagne commerciale XDM] est une classe XDM (Experience Data Model) standard qui capture les propriétés minimales requises d’une campagne d’entreprise.

![Structure de la classe XDM Business Campaign telle qu’elle apparaît dans l’interface utilisateur](../../images/classes/b2b/business-campaign.png)

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

Pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform, consultez le guide sur [relations de schéma dans l’édition B2B de la plateforme CDP en temps réel](../../tutorials/relationship-b2b.md)

Pour les champs supplémentaires compatibles avec cette classe, voir la référence du groupe de champs pour [[!UICONTROL Détails des campagnes commerciales XDM]](../../field-groups/b2b-campaign/details.md).
