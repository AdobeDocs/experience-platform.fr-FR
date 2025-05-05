---
title: Classe de campagne commerciale XDM
description: Découvrez la classe XDM Business Campaign dans Experience Data Model (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---

# [!UICONTROL Classe XDM Business Campaign]

>[!IMPORTANT]
>
>Cette classe est conçue pour être utilisée par les organisations ayant accès à [Adobe Real-Time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Vous devez avoir accès à l’édition B2B de Real-Time CDP pour que cette classe puisse participer à [Real-time Customer Profile](../../../profile/home.md).

[!UICONTROL XDM Business Campaign] est une classe XDM (Experience Data Model) standard qui capture les propriétés minimales requises d’une campagne commerciale.

![Structure de la classe XDM Business Campaign telle qu’elle apparaît dans l’interface utilisateur](../../images/classes/b2b/business-campaign.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité de campagne. |
| `extSourceSystemAudit` | [[!UICONTROL &#x200B; Attributs d’audit système Source externes]](../../data-types/external-source-system-audit-attributes.md) | Si la campagne provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de `campaignID`. |
| `campaignDescription` | Chaîne | Description de la campagne. |
| `campaignID` | Chaîne | Identifiant unique de l’entité de campagne. |
| `campaignName` | Chaîne | Nom de la campagne. |
| `campaignType` | Chaîne | Type de campagne ou audience cible. |

{style="table-layout:auto"}

Pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment établir ces relations dans l’interface utilisateur de Adobe Experience Platform, consultez le guide sur les [relations de schéma dans Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Pour plus d’informations sur les champs compatibles avec cette classe, reportez-vous à la référence du groupe de champs pour les [[!UICONTROL détails XDM Business Campaign]](../../field-groups/b2b-campaign/details.md).
