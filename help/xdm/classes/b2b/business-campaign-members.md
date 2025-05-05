---
title: Classe des membres XDM Business Campaign
description: Découvrez la classe XDM Business Campaign Members dans Experience Data Model (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 2%

---

# [!UICONTROL Classe XDM Business Campaign Members]

>[!IMPORTANT]
>
>Cette classe est conçue pour être utilisée par les organisations ayant accès à [Adobe Real-Time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Vous devez avoir accès à l’édition B2B de Real-Time CDP pour que cette classe puisse participer à [Real-time Customer Profile](../../../profile/home.md).

[!UICONTROL XDM Business Campaign Members] est une classe de modèle de données d’expérience (XDM) standard qui décrit un contact ou un prospect associé à une campagne commerciale.

![Structure de la classe XDM Business Campaign Members telle qu’elle apparaît dans l’interface utilisateur](../../images/classes/b2b/business-campaign-members.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la campagne associée. |
| `campaignMemberKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité d’appartenance à une campagne. |
| `extSourceSystemAudit` | [[!UICONTROL &#x200B; Attributs d’audit système Source externes]](../../data-types/external-source-system-audit-attributes.md) | Si l’adhésion à la campagne provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la personne qui est membre de la campagne associée. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de `campaignMemberID`. |

{style="table-layout:auto"}

Pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment établir ces relations dans l’interface utilisateur de Adobe Experience Platform, consultez le guide sur les [relations de schéma dans Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Pour plus d’informations sur les champs compatibles avec cette classe, reportez-vous à la référence du groupe de champs pour les [[!UICONTROL détails des membres XDM Business Campaign]](../../field-groups/b2b-campaign-members/details.md).
