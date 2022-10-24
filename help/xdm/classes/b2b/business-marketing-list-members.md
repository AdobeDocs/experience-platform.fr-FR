---
title: Classe des membres de la liste XDM Business Marketing
description: Ce document présente la classe XDM Business Marketing List Members dans le modèle de données d’expérience (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 7%

---

# [!UICONTROL Membres de la liste XDM Business Marketing] class

>[!IMPORTANT]
>
>Cette classe est destinée aux organisations ayant accès à [Adobe Real-time Customer Data Platform version B2B](../../../rtcdp/b2b-overview.md). Vous devez avoir accès à Real-Time CDP B2B Edition pour que cette classe puisse participer à la [Real-time Customer Profile](../../../profile/home.md).

[!UICONTROL Membres de la liste XDM Business Marketing] est une classe XDM (Experience Data Model) standard qui décrit les membres, les personnes ou les contacts associés à une liste marketing.

![Structure de la classe XDM Business Marketing List Members telle qu’elle apparaît dans l’interface utilisateur](../../images/classes/b2b/business-marketing-list-members.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si l’appartenance à une liste marketing provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `marketingListKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la liste marketing dont la personne est membre. |
| `marketingListMemberKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité d’appartenance à une liste marketing. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la personne qui est membre de la liste marketing. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de la variable `marketingListMemberID`. |
| `isDeleted` | Booléen | Indique si cette entité membre de liste marketing a été supprimée dans Marketo Engage.<br><br>Lors de l’utilisation de la variable [Connecteur source Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tous les enregistrements supprimés dans Marketo sont automatiquement répercutés dans Real-time Customer Profile. Cependant, les enregistrements relatifs à ces profils peuvent toujours persister dans le lac de données. En définissant `isDeleted` to `true`, vous pouvez utiliser ce champ pour filtrer les enregistrements qui ont été supprimés de vos sources lors de l’interrogation du lac de données. |
| `marketingListID` | Chaîne | Identifiant unique de la liste marketing. |
| `marketingListMemberID` | Chaîne | Identifiant unique de l’entité d’appartenance à une liste marketing. |
| `personId` | Chaîne | Identifiant unique de la personne. |

{style=&quot;table-layout:auto&quot;}

Consultez le guide sur la [relations de schéma dans Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
