---
title: Classe de compte professionnel XDM
description: Ce document présente la classe XDM Business Account dans le modèle de données d’expérience (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 9%

---

# [!UICONTROL Classe de ] compte commercial XDM (bêta)

>[!IMPORTANT]
>
>Cette classe est disponible dans le cadre de la plateforme de données clients en temps réel de l’édition B2B, actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

[!UICONTROL XDM Business ] Account est une classe XDM (Experience Data Model) standard qui capture les propriétés minimales requises d’un compte d’entreprise.

![](../../images/classes/b2b/business-account.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité de compte. |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si le compte provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de `accountID`. |
| `accountID` | Chaîne | Identifiant unique de l’entité de compte. |

{style=&quot;table-layout:auto&quot;}

Consultez le guide sur les [relations de schéma dans l’édition B2B de la plateforme des données clients en temps réel](../../tutorials/relationship-b2b.md) pour découvrir comment cette classe est liée conceptuellement aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
