---
title: Classe de campagne commerciale XDM
description: Découvrez la classe XDM Business Campaign dans Experience Data Model (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---

# [!UICONTROL Campagne commerciale XDM] class

>[!IMPORTANT]
>
>Cette classe est destinée aux organisations ayant accès à [Adobe Real-time Customer Data Platform version B2B](../../../rtcdp/b2b-overview.md). Vous devez avoir accès à Real-Time CDP B2B Edition pour que cette classe puisse participer à la [Profil client en temps réel](../../../profile/home.md).

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

{style="table-layout:auto"}

Pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform, consultez le guide sur [relations de schéma dans Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Pour les champs supplémentaires compatibles avec cette classe, voir la référence du groupe de champs pour [[!UICONTROL Détails des campagnes commerciales XDM]](../../field-groups/b2b-campaign/details.md).
