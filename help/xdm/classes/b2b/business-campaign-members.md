---
title: Classe des membres XDM Business Campaign
description: Ce document présente la classe XDM Business Campaign Members dans le modèle de données d’expérience (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 8%

---

# [!UICONTROL Membres de XDM Business Campaign] class

>[!IMPORTANT]
>
>Cette classe est destinée aux organisations ayant accès à [Adobe Real-time Customer Data Platform version B2B](../../../rtcdp/b2b-overview.md). Vous devez avoir accès à Real-Time CDP B2B Edition pour que cette classe puisse participer à la [Real-time Customer Profile](../../../profile/home.md).

[!UICONTROL Membres de XDM Business Campaign] est une classe XDM (Experience Data Model) standard qui décrit un contact ou un prospect associé à une campagne commerciale.

![Structure de la classe XDM Business Campaign Members telle qu’elle apparaît dans l’interface utilisateur](../../images/classes/b2b/business-campaign-members.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la campagne associée. |
| `campaignMemberKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité d’appartenance à une campagne. |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si l’adhésion à la campagne provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la personne qui est membre de la campagne associée. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de la variable `campaignMemberID`. |

{style=&quot;table-layout:auto&quot;}

Pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform, consultez le guide sur [relations de schéma dans Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Pour les champs supplémentaires compatibles avec cette classe, voir la référence du groupe de champs pour [[!UICONTROL Détails des membres XDM Business Campaign]](../../field-groups/b2b-campaign-members/details.md).
