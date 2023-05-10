---
title: Classe de liste XDM Business Marketing
description: Ce document présente la classe XDM Business Marketing List dans Experience Data Model (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 5%

---

# [!UICONTROL Liste XDM Business Marketing] class

>[!IMPORTANT]
>
>Cette classe est destinée aux organisations ayant accès à [Adobe Real-time Customer Data Platform version B2B](../../../rtcdp/b2b-overview.md). Vous devez avoir accès à Real-Time CDP B2B Edition pour que cette classe puisse participer à la [Profil client en temps réel](../../../profile/home.md).

[!UICONTROL Liste XDM Business Marketing] est une classe XDM (Experience Data Model) standard qui capture les propriétés minimales requises d’une liste marketing. Les listes marketing vous permettent de classer par priorité les clients prospects les plus susceptibles d’acheter votre produit.

![Structure de la classe XDM Business Marketing List telle qu’elle apparaît dans l’interface utilisateur](../../images/classes/b2b/business-marketing-list.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si la liste marketing provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `marketingListKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité de liste marketing. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de la variable `marketingListID`. |
| `isDeleted` | Booléen | Indique si cette entité de liste marketing a été supprimée dans Marketo Engage.<br><br>Lors de l’utilisation de la variable [Connecteur source Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), les enregistrements supprimés dans Marketo sont automatiquement répercutés dans Real-time Customer Profile. Cependant, les enregistrements relatifs à ces profils peuvent toujours persister dans le lac de données. En définissant `isDeleted` to `true`, vous pouvez utiliser ce champ pour filtrer les enregistrements qui ont été supprimés de vos sources lors de l’interrogation du lac de données. |
| `marketingListDescription` | Chaîne | Description de la liste marketing. |
| `marketingListID` | Chaîne | Identifiant unique de l’entité de liste marketing. |
| `marketingListName` | Chaîne | Nom de la liste marketing. |

{style="table-layout:auto"}

Consultez le guide sur la [relations de schéma dans Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
