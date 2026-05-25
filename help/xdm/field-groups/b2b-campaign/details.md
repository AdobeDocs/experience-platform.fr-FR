---
title: Groupe de champs de schéma des détails de XDM Business Campaign
description: Découvrez le groupe de champs de schéma Détails de XDM Business Campaign .
exl-id: 3ef6c0b9-cba1-449e-8868-46446c00465f
TQID: https://experienceleague.adobe.com/Nla70G3CZQeV-wnghG7ZZDTVTl9Pa0oNQJaxYjAdpJU
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 330
ht-degree: 1%

---

# [!UICONTROL XDM Business Campaign Details] groupe de champs de schéma

[!UICONTROL XDM Business Campaign Details] est un groupe de champs de schéma standard pour la classe [[!UICONTROL XDM Business Campaign]](../../classes/b2b/business-campaign.md) qui recueille des informations détaillées sur une campagne commerciale.

![&#x200B; Structure du groupe de champs Détails de XDM Business Campaign, telle qu’elle apparaît dans l’interface utilisateur](../../images/field-groups/b2b/business-campaign-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL Currency]](../../data-types/currency.md) | Représente le coût réel de la campagne commerciale. |
| `budgetedCost` | [[!UICONTROL Currency]](../../data-types/currency.md) | Représente le coût budgété de la campagne commerciale. |
| `expectedRevenue` | [[!UICONTROL Currency]](../../data-types/currency.md) | Représente le chiffre d’affaires que la campagne commerciale est censée générer. |
| `parentCampaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Identifiant composite d’une campagne parent, le cas échéant. |
| `campaignEndDate` | [!UICONTROL DateTime] | Date et heure ISO 8601 indiquant la date de fin de la campagne. |
| `campaignProgressionName` | [!UICONTROL String] | Nom de la progression de la campagne. |
| `campaignStartDate` | [!UICONTROL DateTime] | Date et heure ISO 8601 du début de la campagne ou du début à venir. |
| `campaignStatus` | [!UICONTROL String] | Statut actuel de la campagne. |
| `channelName` | [!UICONTROL String] | Nom du canal associé à cette campagne. |
| `expectedResponse` | [!UICONTROL String] | Réponse attendue pour la campagne. |
| `integrationPartnerName` | [!UICONTROL String] | Nom du partenaire qui a été intégré à cette campagne. |
| `isActive` | [!UICONTROL Boolean] | Indique si cette campagne est active. |
| `isDeleted` | [!UICONTROL Boolean] | Indique si cette campagne a été supprimée dans Marketo Engage.<br><br>Lors de l’utilisation du connecteur source [Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tous les enregistrements supprimés dans Marketo sont automatiquement répercutés dans le profil client en temps réel. Cependant, les enregistrements relatifs à ces profils peuvent toujours persister dans le lac de données. En définissant `isDeleted` sur `true`, vous pouvez utiliser le champ pour filtrer les enregistrements qui ont été supprimés de vos sources lors de l’interrogation du lac de données. |
| `lastActivityDate` | [!UICONTROL DateTime] | Horodatage ISO 8601 de la dernière activité associée à la campagne. |
| `timeZone` | [!UICONTROL String] | Fuseau horaire dans lequel opère la campagne. |
| `timeZoneDelivery` | [!UICONTROL String] | Fuseau horaire de diffusion dans lequel opère la campagne. |
| `timeZoneName` | [!UICONTROL String] | Nom du fuseau horaire dans lequel la campagne opère. |
| `webinarHistorySyncDate` | [!UICONTROL DateTime] | Horodatage ISO 8601 de la dernière synchronisation de l’historique du webinaire pour cette campagne. |
| `webinarHistorySyncStatus` | [!UICONTROL String] | Statut de la synchronisation de l’historique du webinaire pour cette campagne. |
| `webinarSessionDescription` | [!UICONTROL String] | Description de la session de webinaire associée à cette campagne. |
| `webinarSessionName` | [!UICONTROL String] | Nom de la session de webinaire associée à cette campagne. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
