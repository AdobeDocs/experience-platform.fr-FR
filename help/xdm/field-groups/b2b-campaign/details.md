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
source-git-commit: 74579d9ca311b241313a3d89b564f217cd3476c7
workflow-type: tm+mt
source-wordcount: 370
ht-degree: 6%

---

# [!UICONTROL Détails XDM Business Campaign] groupe de champs de schéma

[!UICONTROL Détails de XDM Business Campaign] est un groupe de champs de schéma standard pour la classe [[!UICONTROL XDM Business Campaign]](../../classes/b2b/business-campaign.md), qui recueille les informations détaillées sur une campagne commerciale.

![&#x200B; Structure du groupe de champs Détails de XDM Business Campaign, telle qu’elle apparaît dans l’interface utilisateur](../../images/field-groups/b2b/business-campaign-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL Devise]](../../data-types/currency.md) | Représente le coût réel de la campagne commerciale. |
| `budgetedCost` | [[!UICONTROL Devise]](../../data-types/currency.md) | Représente le coût budgété de la campagne commerciale. |
| `expectedRevenue` | [[!UICONTROL Devise]](../../data-types/currency.md) | Représente le chiffre d’affaires que la campagne commerciale est censée générer. |
| `parentCampaignKey` | Source B2B[&#128279;](../../data-types/b2b-source.md) | Identifiant composite d’une campagne parent, le cas échéant. |
| `campaignEndDate` | [!UICONTROL DateHeure] | Horodatage [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) (`yyyy-MM-dd'T'HH:mm:ssXXX`) du moment où la campagne s’est terminée ou se terminera. |
| `campaignProgressionName` | [!UICONTROL Chaîne] | Nom de la progression de la campagne. |
| `campaignStartDate` | [!UICONTROL DateHeure] | Horodatage ISO 8601 (`yyyy-MM-dd'T'HH:mm:ssXXX`) du moment où la campagne a démarré ou démarrera. |
| `campaignStatus` | [!UICONTROL Chaîne] | Statut actuel de la campagne. |
| `channelName` | [!UICONTROL Chaîne] | Nom du canal associé à cette campagne. |
| `expectedResponse` | [!UICONTROL Chaîne] | Réponse attendue pour la campagne. |
| `integrationPartnerName` | [!UICONTROL Chaîne] | Nom du partenaire qui a été intégré à cette campagne. |
| `isActive` | [!UICONTROL booléen] | Indique si cette campagne est active. |
| `isDeleted` | [!UICONTROL booléen] | Indique si cette campagne a été supprimée dans Marketo Engage.<br><br>Lors de l’utilisation du connecteur source [Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tous les enregistrements supprimés dans Marketo sont automatiquement répercutés dans le profil client en temps réel. Cependant, les enregistrements relatifs à ces profils peuvent toujours persister dans le lac de données. En définissant `isDeleted` sur `true`, vous pouvez utiliser le champ pour filtrer les enregistrements qui ont été supprimés de vos sources lors de l’interrogation du lac de données. |
| `lastActivityDate` | [!UICONTROL DateHeure] | Horodatage ISO 8601 (`yyyy-MM-dd'T'HH:mm:ssXXX`) de la dernière activité associée à la campagne. |
| `timeZone` | [!UICONTROL Chaîne] | Fuseau horaire dans lequel opère la campagne. |
| `timeZoneDelivery` | [!UICONTROL Chaîne] | Fuseau horaire de diffusion dans lequel opère la campagne. |
| `timeZoneName` | [!UICONTROL Chaîne] | Nom du fuseau horaire dans lequel la campagne opère. |
| `webinarHistorySyncDate` | [!UICONTROL DateHeure] | Horodatage ISO 8601 (`yyyy-MM-dd'T'HH:mm:ssXXX`) de la dernière synchronisation de l’historique du webinaire pour cette campagne. |
| `webinarHistorySyncStatus` | [!UICONTROL Chaîne] | Statut de la synchronisation de l’historique du webinaire pour cette campagne. |
| `webinarSessionDescription` | [!UICONTROL Chaîne] | Description de la session de webinaire associée à cette campagne. |
| `webinarSessionName` | [!UICONTROL Chaîne] | Nom de la session de webinaire associée à cette campagne. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
