---
title: Classe d’opportunités commerciales XDM
description: Ce document présente la classe XDM Business Opportunity dans Experience Data Model (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 5%

---

# [!UICONTROL Opportunités commerciales XDM] class

>[!IMPORTANT]
>
>Cette classe est destinée aux organisations ayant accès à [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Pour que cette classe puisse participer à , vous devez avoir accès à l’édition B2B de la plateforme CDP en temps réel . [Real-time Customer Profile](../../../profile/home.md).

[!UICONTROL Opportunités commerciales XDM] est une classe XDM (Experience Data Model) standard qui capture les propriétés minimales requises d’une opportunité commerciale.

![](../../images/classes/b2b/business-opportunity.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite du compte auquel cette opportunité est associée. |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si l’opportunité provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `opportunityKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité d’opportunité. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de la variable `opportunityID`. |
| `accountID` | Chaîne | Identifiant unique du compte auquel cette opportunité est associée. |
| `opportunityDescription` | Chaîne | Description de l’opportunité. |
| `opportunityID` | Chaîne | Identifiant unique de l’entité d’opportunité. |
| `opportunityName` | Chaîne | Nom de l’opportunité. |
| `opportunityStage` | Chaîne | L’étape de vente de l’opportunité. |
| `opportunityType` | Chaîne | Le type d’opportunité. |

{style=&quot;table-layout:auto&quot;}

Consultez le guide sur la [relations de schéma dans l’édition B2B de la plateforme CDP en temps réel](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
