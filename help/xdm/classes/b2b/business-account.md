---
title: Classe de compte professionnel XDM
description: Ce document présente la classe XDM Business Account dans le modèle de données d’expérience (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: 50e5fe8573d828f88867ed33fe86e974c85de60a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 6%

---

# [!UICONTROL Compte d’entreprise XDM] class

>[!IMPORTANT]
>
>Cette classe est destinée aux organisations ayant accès à [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Pour que cette classe puisse participer à , vous devez avoir accès à l’édition B2B de la plateforme CDP en temps réel . [Real-time Customer Profile](../../../profile/home.md).

[!UICONTROL Compte d’entreprise XDM] est une classe XDM (Experience Data Model) standard qui capture les propriétés minimales requises d’un compte d’entreprise.

![Structure de la classe XDM Business Account telle qu’elle apparaît dans l’interface utilisateur](../../images/classes/b2b/business-account.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité de compte. |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si le compte provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de la variable `accountKey` identifiant. |
| `isDeleted` | Booléen | Indique si cette entité de compte a été supprimée dans Marketo Engage.<br><br>Lors de l’utilisation de la variable [Connecteur source Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tous les enregistrements supprimés dans Marketo sont automatiquement répercutés dans Real-time Customer Profile. Cependant, les enregistrements relatifs à ces profils peuvent toujours persister dans le lac de données. En définissant `isDeleted` to `true`, vous pouvez utiliser ce champ pour filtrer les enregistrements qui ont été supprimés de vos sources lors de l’interrogation du lac de données. |

{style=&quot;table-layout:auto&quot;}

Consultez le guide sur la [relations de schéma dans l’édition B2B de la plateforme CDP en temps réel](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe correspond conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
