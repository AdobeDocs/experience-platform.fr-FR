---
title: Classe d’opportunités commerciales XDM
description: Ce document présente la classe XDM Business Opportunity dans Experience Data Model (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 5%

---

# [!UICONTROL Classe ] d’opportunités commerciales XDM

>[!NOTE]
>
>Cette classe est uniquement disponible pour les organisations qui ont accès à la plateforme de données clients en temps réel de l’édition B2B.

[!UICONTROL XDM Business ] Opportunity est une classe XDM standard qui capture les propriétés minimales requises d’une opportunité commerciale.

![](../../images/classes/b2b/business-opportunity.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite du compte auquel cette opportunité est associée. |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si l’opportunité provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `opportunityKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité d’opportunité. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de `opportunityID`. |
| `accountID` | Chaîne | Identifiant unique du compte auquel cette opportunité est associée. |
| `opportunityDescription` | Chaîne | Description de l’opportunité. |
| `opportunityID` | Chaîne | Identifiant unique de l’entité d’opportunité. |
| `opportunityName` | Chaîne | Nom de l’opportunité. |
| `opportunityStage` | Chaîne | L’étape de vente de l’opportunité. |
| `opportunityType` | Chaîne | Le type d’opportunité. |

Consultez le guide sur les [relations de schéma dans l’édition B2B de la plateforme des données clients en temps réel](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe est liée conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
