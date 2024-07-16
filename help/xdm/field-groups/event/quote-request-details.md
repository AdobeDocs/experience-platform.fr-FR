---
title: Groupe de champs de schéma Détails de la requête entre guillemets
description: Découvrez le groupe de champs Détails de la demande de devis .
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---

# [!UICONTROL Détails de la demande de devis] groupe de champs de schéma

[!UICONTROL Détails de la requête entre guillemets] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Le groupe de champs fournit un seul objet `quotes` à un schéma, qui capture les détails du processus de demande pour différents types de devis, y compris les polices d’assurance, les soins de santé, les commandes de fabrication et les commandes high-tech.

![](../../images/field-groups/quote-request-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `discount` | [[!UICONTROL Devise]](../../data-types/currency.md) | Montant de remise d’un devis présenté à un visiteur. |
| `premium` | [[!UICONTROL Devise]](../../data-types/currency.md) | Montant des primes d’un devis présenté à un visiteur. |
| `location` | [!UICONTROL Chaîne] | Code postal utilisé pour rechercher des détaillants près de l’emplacement du visiteur. |
| `requestID` | [!UICONTROL Chaîne] | Identifiant unique de la requête de devis. |
| `selectedRetailer` | [!UICONTROL Chaîne] | Le détaillant sélectionné pour la demande de devis, le cas échéant. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
