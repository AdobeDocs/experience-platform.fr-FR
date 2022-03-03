---
title: Groupe de champs de schéma Détails de la requête entre guillemets
description: Ce document présente un aperçu du groupe de champs Détails de la demande de devis .
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 8%

---

# [!UICONTROL Détails de la demande de devis] groupe de champs de schéma

[!UICONTROL Détails de la demande de devis] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Le groupe de champs fournit une `quotes` vers un schéma, qui capture les détails du processus de demande pour différents types de devis, y compris les polices d’assurance, les soins de santé, les commandes de fabrication et les commandes high-tech.

![](../../images/field-groups/quote-request-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `discount` | [[!UICONTROL Devise]](../../data-types/currency.md) | Montant de remise d’un devis présenté à un visiteur. |
| `premium` | [[!UICONTROL Devise]](../../data-types/currency.md) | Montant des primes d’un devis présenté à un visiteur. |
| `location` | [!UICONTROL Chaîne] | Code postal utilisé pour rechercher des détaillants près de l’emplacement du visiteur. |
| `requestID` | [!UICONTROL Chaîne] | Identifiant unique de la requête de devis. |
| `selectedRetailer` | [!UICONTROL Chaîne] | Le détaillant sélectionné pour la demande de devis, le cas échéant. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous à la section [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
