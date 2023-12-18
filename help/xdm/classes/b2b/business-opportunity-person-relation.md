---
title: Classe de relation d’une personne avec une opportunité commerciale XDM
description: Découvrez la classe XDM Business Opportunity Person Relation dans Experience Data Model (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 3%

---

# [!UICONTROL Relation de personne avec les opportunités commerciales XDM] class

>[!IMPORTANT]
>
>Cette classe est destinée aux organisations ayant accès à [Adobe Real-time Customer Data Platform version B2B](../../../rtcdp/b2b-overview.md). Vous devez avoir accès à Real-Time CDP B2B Edition pour que cette classe puisse participer à la [Profil client en temps réel](../../../profile/home.md).

[!UICONTROL Relation de personne avec les opportunités commerciales XDM] est une classe XDM (Experience Data Model) standard qui capture les propriétés minimales requises d’une personne associée à une opportunité commerciale.

![Structure de la classe XDM Business Opportunity Person telle qu’elle apparaît dans l’interface utilisateur](../../images/classes/b2b/business-opportunity-person-relation.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si la relation homme-entreprise provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `opportunityKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’opportunité dans la relation opportunité-personne. |
| `opportunityPersonKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité de relation opportunité-personne. |
| `personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la personne dans la relation opportunité-personne. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte des autres champs d’ID capturés par la classe . |
| `isDeleted` | Booléen | Indique si cette entité de liste marketing a été supprimée dans Marketo Engage.<br><br>Lors de l’utilisation de la variable [Connecteur source Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tous les enregistrements supprimés dans Marketo sont automatiquement répercutés dans Real-time Customer Profile. Cependant, les enregistrements relatifs à ces profils peuvent toujours persister dans le lac de données. En définissant `isDeleted` to `true`, vous pouvez utiliser ce champ pour filtrer les enregistrements qui ont été supprimés de vos sources lors de l’interrogation du lac de données. |
| `isPrimary` | Booléen | Indique si la personne est le premier contact pour cette opportunité. |
| `opportunityID` | Chaîne | Identifiant unique de l’opportunité dans la relation opportunité-personne. |
| `opportunityPersonID` | Chaîne | Identifiant unique de l’entité de relation opportunité-personne |
| `personID` | Chaîne | Identifiant unique de la personne dans la relation opportunité-personne. |
| `personRole` | Chaîne | Le rôle de la personne dans la relation opportunité-personne. |

{style="table-layout:auto"}

Consultez le guide sur la [relations de schéma dans Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
