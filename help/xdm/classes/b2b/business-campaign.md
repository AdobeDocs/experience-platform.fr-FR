---
title: Classe de campagne commerciale XDM
description: Ce document présente la classe XDM Business Campaign dans le modèle de données d’expérience (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 6%

---

# [!UICONTROL Classe XDM Business ] Campaign

>[!NOTE]
>
>Cette classe est disponible uniquement pour les organisations qui ont accès à l’édition B2B de la plateforme de données clients en temps réel.

[!UICONTROL XDM Business ] Campaigns est une classe XDM (modèle de données d’expérience) standard qui capture les propriétés minimales requises d’une campagne d’entreprise.

![](../../images/classes/b2b/business-campaign.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de l’entité de campagne. |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système de source externe]](../../data-types/external-source-system-audit-attributes.md) | Si la campagne provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de `campaignID`. |
| `campaignDescription` | Chaîne | Description de la campagne. |
| `campaignID` | Chaîne | Identifiant unique de l’entité de campagne. |
| `campaignName` | Chaîne | Nom de la campagne. |
| `campaignType` | Chaîne | Type de campagne ou audience cible. |
