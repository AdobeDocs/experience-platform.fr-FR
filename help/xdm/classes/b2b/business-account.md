---
title: Classe de compte professionnel XDM
description: Ce document présente la classe XDM Business Account dans le modèle de données d’expérience (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 5%

---

# [!UICONTROL Compte d’entreprise XDM] class

>[!IMPORTANT]
>
>Cette classe est destinée aux organisations ayant accès à [Adobe Real-time Customer Data Platform version B2B](../../../rtcdp/b2b-overview.md). Vous devez avoir accès à Real-Time CDP B2B Edition pour que cette classe puisse participer à la [Profil client en temps réel](../../../profile/home.md).

[!UICONTROL Compte d’entreprise XDM] est une classe XDM (Experience Data Model) standard qui capture les propriétés minimales requises d’un compte d’entreprise.

![Structure de la classe XDM Business Account telle qu’elle apparaît dans l’interface utilisateur](../../images/classes/b2b/business-account.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité de compte. |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si le compte provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de la variable `accountKey` identifiant. |
| `isDeleted` | Booléen | Indique si cette entité de compte a été supprimée dans Marketo Engage.<br><br>Lors de l’utilisation de la variable [Connecteur source Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), les enregistrements supprimés dans Marketo sont automatiquement répercutés dans Real-time Customer Profile. Cependant, les enregistrements relatifs à ces profils peuvent toujours persister dans le lac de données. En définissant `isDeleted` to `true`, vous pouvez utiliser ce champ pour filtrer les enregistrements qui ont été supprimés de vos sources lors de l’interrogation du lac de données. |

{style="table-layout:auto"}

Consultez le guide sur la [relations de schéma dans Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
