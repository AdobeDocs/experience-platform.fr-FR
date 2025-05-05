---
title: Classe de liste XDM Business Marketing
description: Découvrez la classe XDM Business Marketing List dans Experience Data Model (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 3%

---

# [!UICONTROL Classe XDM Business Marketing List]

>[!IMPORTANT]
>
>Cette classe est conçue pour être utilisée par les organisations ayant accès à [Adobe Real-Time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Vous devez avoir accès à l’édition B2B de Real-Time CDP pour que cette classe puisse participer à [Real-time Customer Profile](../../../profile/home.md).

[!UICONTROL XDM Business Marketing List] est une classe de modèle de données d’expérience (XDM) standard qui capture les propriétés minimales requises d’une liste marketing. Les listes marketing vous permettent de classer par priorité les clients prospects les plus susceptibles d’acheter votre produit.

![Structure de la classe XDM Business Marketing List telle qu’elle apparaît dans l’interface utilisateur](../../images/classes/b2b/business-marketing-list.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL &#x200B; Attributs d’audit système Source externes]](../../data-types/external-source-system-audit-attributes.md) | Si la liste marketing provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `marketingListKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité de liste marketing. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de `marketingListID`. |
| `isDeleted` | Booléen | Indique si cette entité de liste marketing a été supprimée dans Marketo Engage.<br><br>Lors de l’utilisation du [connecteur source Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tous les enregistrements supprimés dans Marketo sont automatiquement répercutés dans Real-time Customer Profile. Cependant, les enregistrements relatifs à ces profils peuvent toujours persister dans le lac de données. En définissant `isDeleted` sur `true`, vous pouvez utiliser le champ pour filtrer les enregistrements qui ont été supprimés de vos sources lors de l’interrogation du lac de données. |
| `marketingListDescription` | Chaîne | Description de la liste marketing. |
| `marketingListID` | Chaîne | Identifiant unique de l’entité de liste marketing. |
| `marketingListName` | Chaîne | Nom de la liste marketing. |

{style="table-layout:auto"}

Consultez le guide sur les [relations de schéma dans Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe est liée conceptuellement aux autres classes B2B et comment établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
