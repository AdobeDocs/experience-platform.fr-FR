---
title: Groupe de champs de schéma des détails de campagne commerciale XDM
description: Ce document présente un aperçu du groupe de champs Détails de la campagne XDM Business.
exl-id: 3ef6c0b9-cba1-449e-8868-46446c00465f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 6%

---

# [!UICONTROL Détails des campagnes commerciales XDM] groupe de champs de schéma

[!UICONTROL Détails des campagnes commerciales XDM] est un groupe de champs de schéma standard pour la variable [[!UICONTROL Campagne commerciale XDM] class](../../classes/b2b/business-campaign.md), qui capture des informations détaillées sur une campagne d’entreprise.

![Structure du groupe de champs Détails de la campagne XDM tel qu’il apparaît dans l’interface utilisateur](../../images/field-groups/b2b/business-campaign-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL Devise]](../../data-types/currency.md) | Représente le coût réel de la campagne commerciale. |
| `budgetedCost` | [[!UICONTROL Devise]](../../data-types/currency.md) | Représente le coût budgété de la campagne commerciale. |
| `expectedRevenue` | [[!UICONTROL Devise]](../../data-types/currency.md) | Représente les recettes que la campagne commerciale doit générer. |
| `parentCampaignKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | L’identifiant composite d’une campagne parente, le cas échéant. |
| `campaignEndDate` | [!UICONTROL DateTime] | Horodatage ISO 8601 de la fin ou de la fin de la campagne. |
| `campaignProgressionName` | [!UICONTROL Chaîne] | Nom de la progression de la campagne. |
| `campaignStartDate` | [!UICONTROL DateTime] | Horodatage ISO 8601 du début ou du début de la campagne. |
| `campaignStatus` | [!UICONTROL Chaîne] | État actuel de la campagne. |
| `channelName` | [!UICONTROL Chaîne] | Nom du canal associé à cette campagne. |
| `expectedResponse` | [!UICONTROL Chaîne] | Réponse attendue pour la campagne. |
| `integrationPartnerName` | [!UICONTROL Chaîne] | Nom du partenaire qui a intégré cette campagne. |
| `isActive` | [!UICONTROL Booléen] | Indique si cette campagne est principale. |
| `isDeleted` | [!UICONTROL Booléen] | Indique si cette campagne a été supprimée dans Marketo Engage.<br><br>Lors de l’utilisation de la variable [Connecteur source Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), les enregistrements supprimés dans Marketo sont automatiquement répercutés dans Real-time Customer Profile. Cependant, les enregistrements relatifs à ces profils peuvent toujours persister dans le lac de données. En définissant `isDeleted` to `true`, vous pouvez utiliser ce champ pour filtrer les enregistrements qui ont été supprimés de vos sources lors de l’interrogation du lac de données. |
| `lastActivityDate` | [!UICONTROL DateTime] | Horodatage ISO 8601 de la dernière activité associée à la campagne. |
| `timeZone` | [!UICONTROL Chaîne] | Fuseau horaire dans lequel la campagne fonctionne. |
| `timeZoneDelivery` | [!UICONTROL Chaîne] | Fuseau horaire de la diffusion dans laquelle la campagne fonctionne. |
| `timeZoneName` | [!UICONTROL Chaîne] | Nom du fuseau horaire dans lequel la campagne fonctionne. |
| `webinarHistorySyncDate` | [!UICONTROL DateTime] | Horodatage ISO 8601 de la dernière synchronisation de l’historique des webinaires pour cette campagne. |
| `webinarHistorySyncStatus` | [!UICONTROL Chaîne] | État de la synchronisation de l’historique des webinaires pour cette campagne. |
| `webinarSessionDescription` | [!UICONTROL Chaîne] | Description de la session de webinaire associée à cette campagne. |
| `webinarSessionName` | [!UICONTROL Chaîne] | Nom de la session de webinaire associée à cette campagne. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous à la section [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
