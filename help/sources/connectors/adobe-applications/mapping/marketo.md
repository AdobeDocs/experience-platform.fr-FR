---
keywords: Experience Platform;accueil;rubriques les plus consultées;Marketo Engage;marketo engage;Marketo;mappage
solution: Experience Platform
title: Mapper des champs pour la source Marketo Engage
description: Les tableaux ci-dessous contiennent les mappages entre les champs des jeux de données Marketo et les champs XDM correspondants.
exl-id: 2b217bba-2748-4d6f-85ac-5f64d5e99d49
source-git-commit: 3b21d952da603b519c9919b08467cd5c6091f235
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 41%

---

# Mappages de champs [!DNL Marketo Engage] {#marketo-engage-field-mappings}

Les tableaux ci-dessous contiennent les mappages entre les champs des neuf jeux de données [!DNL Marketo] et leurs champs de modèle de données d’expérience (XDM) correspondants.

>[!TIP]
>
>Tous les jeux de données [!DNL Marketo], sauf `Activities`, prennent désormais `isDeleted` en charge. Vos flux de données existants incluront automatiquement `isDeleted`, mais n’ingèreront que l’indicateur pour les données nouvellement ingérées. Si vous souhaitez appliquer l’indicateur à toutes vos données historiques, vous devez arrêter vos flux de données existants et les recréer avec le nouveau mappage. Notez que si vous supprimez `isDeleted`, vous n’aurez plus accès à la fonctionnalité. Il est essentiel que le mappage soit conservé une fois qu’il est automatiquement renseigné.

## Activités {#activities}

La source [!DNL Marketo] prend désormais en charge les activités standards supplémentaires. Pour utiliser des activités standards, vous devez mettre à jour votre schéma à l’aide de l’[utilitaire de génération automatique de schéma](../marketo/marketo-namespaces.md), car si vous créez de nouveaux flux de données `activities` sans mettre à jour votre schéma, les modèles de mappage échouent, car les nouveaux champs cibles ne seront pas présents dans votre schéma. Si vous choisissez de ne pas mettre à jour votre schéma, vous pouvez toujours créer un nouveau flux de données et ignorer les erreurs. Toutefois, les champs nouveaux ou mis à jour ne seront pas ingérés dans Experience Platform.

Lisez la documentation relative à la [classe d’événement d’expérience XDM](../../../../xdm/classes/experienceevent.md) pour plus d’informations sur la classe XDM et le ou les groupes de champs XDM.

>[!NOTE]
>
>Le champ source `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` est un champ calculé qui doit être ajouté à l’aide de l’option **[!UICONTROL Ajouter un champ calculé]** dans l’interface utilisateur d’Experience Platform. Pour plus d’informations, consultez le tutoriel sur [l’ajout de champs calculés](../../../../data-prep/ui/mapping.md#calculated-fields) .

| Champ source Marketo | Identifiant du type d’activité | Jeu de données source | Champ cible XDM | Notes |
| -------------------- | ---------------- | -------------- | ---------------- | ----- |
| `_id` |  | `_id` | `_id` |  |
|  |  | `"Marketo"` | `personKey.sourceType` |  |
|  |  | `"${MUNCHKIN_ID}"` | `personKey.sourceInstanceID` | MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `leadId` |  | `personID` | `personKey.sourceID` |  |
|  |  | `concat(personID,"@${MUNCHKIN_ID}.Marketo")` | `personKey.sourceKey` | Identité principale. MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `activityTypeId` |  | `eventType` | `eventType` |  |
| <ul><li>Si le <code>activityTypeId</code> correspond à 1, 2, 3, 9, 10 ou 11 → marque <code>productBy</code> comme <strong>soi</strong>.</li><li>Si le <code>activityTypeId</code> marque de → 6, 7, 8, 12, 21, 22, 24, 25, 27, 32, 34, 35, 36, 46, 101, 104, 110, 113, 114 ou 115 <code>produite par</code> comme <strong>système</strong>.</li><li>Pour toutes les autres valeurs, → marquez <code>productBy</code> comme <strong>soi</strong>.</li></ul> |  | `producedBy` | `producedBy` |  |
| `activityDate` |  | `timestamp` | `timestamp` |  |
| `attributes.Webpage URL` |  | `web.webPageDetails.URL` | `web.webPageDetails.URL` |  |
| `attributes.User Agent` |  | `environment.browserDetails.userAgent` | `environment.browserDetails.userAgent` |  |
| `attributes.Client IP Address` |  | `environment.ipV4` | `environment.ipV4` |  |
| `attributes.Search Query` |  | `search.keywords` | `search.keywords` |  |
| `attributes.Search Engine` |  | `search.searchEngine` | `search.searchEngine` |  |
| `primaryAttributeValue when activityTypeId = 1` | 1 | `web.webPageDetails.webPageID` | `web.webPageDetails.webPageID` |  |
| `primaryAttributeValue when activityTypeId = 1` | 1 | `web.webPageDetails.name` | `web.webPageDetails.name` |  |
| `attributes.Personalized URL` | 1 | `web.webPageDetails.isPersonalizedURL` | `web.webPageDetails.isPersonalizedURL` |  |
| `attributes.Query Parameters` | 1 | `web.webPageDetails.queryParameters` | `web.webPageDetails.queryParameters` |  |
| `attributes.Referrer URL` |  | `web.webReferrer.URL` | `web.webReferrer.URL` |  |
| `primaryAttributeValueId when activityTypeId in (24, 25)` | 24, 25 | `iif(${listOperations\.listID} != null && ${listOperations\.listID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", ${listOperations\.listID}, "sourceKey", concat(${listOperations\.listID},"@${MUNCHKIN_ID}.Marketo")), null)` | `listOperations.listKey` |  |
| `attributes.Is Primary` | 34 35 36 | `opportunityEvent.isPrimary` | `opportunityEvent.isPrimary` |  |
| primaryAttributeValueId lorsque activityTypeId dans (34, 35, 36) | 34, 35, 36 | `iif(${opportunityEvent\.opportunityID} != null && ${opportunityEvent\.opportunityID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${opportunityEvent\.opportunityID}, "sourceKey", concat(${opportunityEvent\.opportunityID},"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityEvent.opportunityKey` |  |
| `attributes.Role` | 34, 35, 36 | `opportunityEvent.role` | `opportunityEvent.role` |  |
| `attributes.Created Date` |  | `leadOperation.newLead.createdDate` | `leadOperation.newLead.createdDate` |  |
| `attributes.Form Name` |  | `leadOperation.newLead.formName` | `leadOperation.newLead.formName` |  |
| `attributes.Lead Source` |  | `leadOperation.newLead.leadSource` | `leadOperation.newLead.leadSource` |  |
| `attributes.List Name` |  | `leadOperation.newLead.listName` | `leadOperation.newLead.listName` |  |
| `attributes.SFDC Type` |  | `leadOperation.newLead.sfdcType` | `leadOperation.newLead.sfdcType` |  |
| `attributes.Source Type` |  | `leadOperation.newLead.sourceType` | `leadOperation.newLead.sourceType` |  |
| primaryAttributeValue lorsque activityTypeId = 21 | 21 | `leadOperation.convertLead.assignTo` | `leadOperation.convertLead.assignTo` |  |
| `attributes.Converted Status` | 21 | `leadOperation.convertLead.convertedStatus` | `leadOperation.convertLead.convertedStatus` |  |
| `attributes.Send Notification Email` | 21 | `leadOperation.convertLead.isSentNotificationEmail` | `leadOperation.convertLead.isSentNotificationEmail` |  |
| primaryAttributeValueId lorsque activityTypeId dans (7, 8, 9, 10, 11, 27) | 7, 8, 9, 10, 11, 27 | `iif(${directMarketing\\.mailingID} != null && ${directMarketing\\.mailingID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${directMarketing\\.mailingID}, \"sourceKey\", concat(${directMarketing\\.mailingID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `directMarketing.mailingKey` |  |
| primaryAttributeValueId lorsque activityTypeId dans (7, 8, 9, 10, 11, 27) | 7, 8, 9, 10, 11, 27 | `directMarketing.mailingName` | `directMarketing.mailingName` |  |
|  |  | `directMarketing.testVariantName` | `directMarketing.testVariantName` |  |
| `attributes.Test Variant` |  | `directMarketing.testVariantID` | `directMarketing.testVariantID` |  |
| `attributes.Subcategory` <ul><li><strong>activityTypeId = 8</strong><ul><li>1099 → BLOQUÉ</li><li>1 003 → DE SPAM BLOQUÉS SUR SOURCE</li><li>1004 → DE SPAM BLOQUÉ SUR LE MESSAGE</li><li>ADRESSE E-MAIL → 2003 NON VALIDE</li><li>ERREUR D&#39;ADRESSE E-MAIL → 2001</li><li>* → RAISON INCONNUE DU REBOND</li></ul></li><li><strong>activityTypeId = 27</strong><ul><li>3999 → MESSAGE NON ACCEPTÉ</li><li>BOÎTE PLEINE 3001 →</li><li>DÉLAI D’EXPIRATION DE → 3004</li><li>4003 → ÉCHEC DU DNS</li><li>4002 → MESSAGE TROP GRAND</li><li>4006 → VIOLATION DE POLITIQUE</li><li>4999 → DÉFAILLANCE TRANSITOIRE</li><li>9999 → MAUVAISE RÉPONSE REÇUE</li><li>* → RAISON INCONNUE DU SOFT BOUNCE</li></ul></li></ul> | 8, 27 | `directMarketing.emailBouncedCode` | `directMarketing.emailBouncedCode` |  |
| `attributes.Details` |  | `directMarketing.emailBouncedDetails` | `directMarketing.emailBouncedDetails` |  |
| `attributes.Email` |  | `directMarketing.email` | `directMarketing.email` |  |
| `attributes.Is Mobile Device` |  | `device.isMobileDevice` | `device.isMobileDevice` |  |
| `attributes.device` |  | `device.model` | `device.model` |  |
| `attributes.Platform` |  | `environment.operatingSystem` | `environment.operatingSystem` |  |
| `attributes.Link` |  | `directMarketing.linkURL` | `directMarketing.linkURL` |  |
| primaryAttributeValueId lorsque activityTypeId = 3 else attributes.Link ID | 3 | `iif(${web\\.webInteraction\\.linkID} != null && ${web\\.webInteraction\\.linkID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${web\\.webInteraction\\.linkID}, \"sourceKey\", concat(${web\\.webInteraction\\.linkID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `web.webInteraction.webInteractionKey` |  |
| primaryAttributeValueId lorsque activityTypeId = 2 autres attributs.Webform ID | 2 | `iif(${web\\.fillOutForm\\.webFormID} != null && ${web\\.fillOutForm\\.webFormID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${web\\.fillOutForm\\.webFormID}, \"sourceKey\", concat(${web\\.fillOutForm\\.webFormID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `web.fillOutForm.webFormKey` |  |
| primaryAttributeValueId lorsque activityTypeId = 2 else null | 2 | `web.fillOutForm.webFormName` | `web.fillOutForm.webFormName` |  |
| primaryAttributeValueId lorsque activityTypeId = 3 else attributes.Link | 3 | `web.webInteraction.linkURL` | `web.webInteraction.linkURL` |  |
| `attributes.Change Value` | 22 | `leadOperation.changeScore.changeValue` | `leadOperation.changeScore.changeValue` |  |
| `attributes.New Value` | 22 | `leadOperation.changeScore.newValue` | `leadOperation.changeScore.newValue` |  |
| `attributes.Old Value` | 22 | `leadOperation.changeScore.oldValue` | `leadOperation.changeScore.oldValue` |  |
| `attributes.Priority` | 22 | `leadOperation.changeScore.priority` | `leadOperation.changeScore.priority` |  |
| `attributes.Reason` | 22 | `leadOperation.changeScore.reason` | `leadOperation.changeScore.reason` |  |
| `attributes.Relative Score` | 22 | `leadOperation.changeScore.relativeScore` | `leadOperation.changeScore.relativeScore` |  |
| `attributes.Relative Urgency` | 22 | `leadOperation.changeScore.relativeUrgency` | `leadOperation.changeScore.relativeUrgency` |  |
| primaryAttributeValueId lorsque activityTypeId = 22 | 22 | `iif(${leadOperation\.changeScore\.scoreAttributeID} != null && ${leadOperation\.changeScore\.scoreAttributeID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeScore\.scoreAttributeID}, "sourceKey", concat(${leadOperation\.changeScore\.scoreAttributeID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeScore.scoreAttributeKey` |  |
| primaryAttributeValueId lorsque activityTypeId = 22 | 22 | `leadOperation.changeScore.scoreAttributeName` | `leadOperation.changeScore.scoreAttributeName` |  |
| `attributes.Urgency` | 22 | `leadOperation.changeScore.urgency` | `leadOperation.changeScore.urgency` |  |
| `attributes.Data Value Changes` |  | `json_to_object(${opportunityEvent\.dataValueChanges})` | `opportunityEvent.dataValueChanges` |  |
| primaryAttributeValueId lorsque activityTypeId = 104 | 104 | `iif(${leadOperation\.campaignProgression\.campaignID} != null && ${leadOperation\.campaignProgression\.campaignID} != "" , to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", ${leadOperation\.campaignProgression\.campaignID}, "sourceKey", concat(${leadOperation\.campaignProgression\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.campaignProgression.campaignKey` |  |
| `attributes.Acquired By` | 104 | `leadOperation.campaignProgression.isAcquiredBy` | `leadOperation.campaignProgression.isAcquiredBy` |  |
| `attributes.Success` | 104 | `leadOperation.campaignProgression.isSuccessful` | `leadOperation.campaignProgression.isSuccessful` |  |
| `attributes.New Status ID` | 104 | `leadOperation.campaignProgression.newStatusID` | `leadOperation.campaignProgression.newStatusID` |  |
| `attributes.New Status` | 104 | `leadOperation.campaignProgression.newStatusName` | `leadOperation.campaignProgression.newStatusName` |  |
| `attributes.Old Status ID` | 104 | `leadOperation.campaignProgression.oldStatusID` | `leadOperation.campaignProgression.oldStatusID` |  |
| `attributes.Old Status` | 104 | `leadOperation.campaignProgression.oldStatusName` | `leadOperation.campaignProgression.oldStatusName` |  |
| `attributes.Reason` | 104 | `leadOperation.campaignProgression.reason` | `leadOperation.campaignProgression.reason` |  |
| `attributes.Date` | 46 | `leadOperation.interestingMoment.date` | `leadOperation.interestingMoment.date` |  |
| `attributes.Description` | 46 | `leadOperation.interestingMoment.description` | `leadOperation.interestingMoment.description` |  |
| `attributes.Source` | 46 | `leadOperation.interestingMoment.source` | `leadOperation.interestingMoment.source` |  |
| primaryAttributeValue lorsque activityTypeId = 46 | 46 | `leadOperation.interestingMoment.type` | `leadOperation.interestingMoment.type` |  |
| primaryAttributeValueId lorsque activityTypeId = 110 | 110 | `iif(${leadOperation\\.callWebhook\\.webhookID} != null && ${leadOperation\\.callWebhook\\.webhookID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.callWebhook\\.webhookID}, \"sourceKey\", concat(${leadOperation\\.callWebhook\\.webhookID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.callWebhook.webhookKey` |  |
| primaryAttributeValueId lorsque activityTypeId = 110 | 110 | `leadOperation.callWebhook.webhookName` | `leadOperation.callWebhook.webhookName` |  |
| `attributes.Error Type` | 110 | `leadOperation.callWebhook.responseCode` | `leadOperation.callWebhook.responseCode` |  |
| primaryAttributeValueId lorsque activityTypeId = 115 | 115 | `iif(${leadOperation\\.changeCampaignCadence\\.campaignID} != null && ${leadOperation\\.changeCampaignCadence\\.campaignID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.changeCampaignCadence\\.campaignID}, \"sourceKey\", concat(${leadOperation\\.changeCampaignCadence\\.campaignID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.changeCampaignCadence.campaignKey` |  |
| `attributes.New Nurture Cadence` | 115 | `leadOperation.changeCampaignCadence.newCadence` | `leadOperation.changeCampaignCadence.newCadence` |  |
| `attributes.Previous Nurture Cadence` | 115 | `leadOperation.changeCampaignCadence.previousCadence` | `leadOperation.changeCampaignCadence.previousCadence` |  |
| primaryAttributeValueId lorsque activityTypeId = 114 | 113 | `iif(${leadOperation\.addToCampaign\.campaignID} != null && ${leadOperation\.addToCampaign\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.campaignID}, "sourceKey", concat(${leadOperation\.addToCampaign\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.campaignKey` |  |
| `attributes.Track ID` | 113 | `iif(${leadOperation\.addToCampaign\.streamID} != null && ${leadOperation\.addToCampaign\.streamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.streamID}, "sourceKey", concat(${leadOperation\.addToCampaign\.streamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.streamKey` |  |
| `attributes.Stream Name` | 113 | `leadOperation.addToCampaign.streamName` | `leadOperation.addToCampaign.streamName` |  |
| primaryAttributeValueId lorsque activityTypeId = 115 | 115 | `iif(${leadOperation\.changeCampaignStream\.campaignID} != null && ${leadOperation\.changeCampaignStream\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.campaignID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.campaignKey` |  |
| `attributes.New Track ID` | 115 | `iif(${leadOperation\.changeCampaignStream\.newStreamID} != null && ${leadOperation\.changeCampaignStream\.newStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.newStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.newStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.newStreamKey` |  |
| `attributes.New Track Name` | 115 | `leadOperation.changeCampaignStream.newStreamName` | `leadOperation.changeCampaignStream.newStreamName` |  |
| `attributes.Previous Track ID` | 115 | `iif(${leadOperation\.changeCampaignStream\.previousStreamID} != null && ${leadOperation\.changeCampaignStream\.previousStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.previousStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.previousStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.previousStreamKey` |  |
| `attributes.Previous Stream Name` | 115 | `leadOperation.changeCampaignStream.previousStreamName` | `leadOperation.changeCampaignStream.previousStreamName` |  |
| primaryAttributeValueId lorsque activityTypeId = 101 | 101 | `iif(${leadOperation\.changeRevenueStage\.modelID} != null && ${leadOperation\.changeRevenueStage\.modelID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.modelID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.modelID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.modelKey` |  |
| primaryAttributeValueId lorsque activityTypeId = 101 | 101 | `leadOperation.changeRevenueStage.modelName` | `leadOperation.changeRevenueStage.modelName` |  |
| `attributes.New Stage ID` | 101 | `iif(${leadOperation\.changeRevenueStage\.newStageID} != null && ${leadOperation\.changeRevenueStage\.newStageID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.newStageID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.newStageID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.newStageKey` |  |
| `attributes.New Stage` | 101 | `leadOperation.changeRevenueStage.newStageName` | `leadOperation.changeRevenueStage.newStageName` |  |
| `attributes.Old Stage ID` | 101 | `iif(${leadOperation\\.changeRevenueStage\\.previousStageID} != null && ${leadOperation\\.changeRevenueStage\\.previousStageID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${leadOperation\\.changeRevenueStage\\.previousStageID}, \"sourceKey\", concat(${leadOperation\\.changeRevenueStage\\.previousStageID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.changeRevenueStage.previousStageKey` |  |
| `attributes.Old Stage` | 101 | `leadOperation.changeRevenueStage.previousStageName` | `leadOperation.changeRevenueStage.previousStageName` |  |
| `attributes.Reason` | 101 | `leadOperation.changeRevenueStage.reason` | `leadOperation.changeRevenueStage.reason` |  |
| `attributes.Merge IDs` lorsque activityTypeId = 32 | 32 | `json_to_object(${leadOperation\.mergeLeads\.mergeIDs})` | `leadOperation.mergeLeads.sourceKeys` |  |
| `attributes.Master Updated` | 32 | `leadOperation.mergeLeads.targetUpdated` | `leadOperation.mergeLeads.targetUpdated` |  |
| `attributes.Merged in Sales` | 32 | `leadOperation.mergeLeads.mergedInCRM` | `leadOperation.mergeLeads.mergedInCRM` |  |
| `attributes.Merge Source` | 32 | `leadOperation.mergeLeads.mergeSource` | `leadOperation.mergeLeads.mergeSource` |  |
| primaryAttributeValueId lorsque activityTypeId = 6 | 6 | `iif(${directMarketing\.emailSent\.mailingID} != null && ${directMarketing\.emailSent\.mailingID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${directMarketing\.emailSent\.mailingID}, "sourceKey", concat(${directMarketing\.emailSent\.mailingID},"@${MUNCHKIN_ID}.Marketo")), null)` | `directMarketing.emailSent.mailingKey` |  |
| primaryAttributeValueId lorsque activityTypeId = 6 | 6 | `directMarketing.emailSent.mailingName` | `directMarketing.emailSent.mailingName` |  |
| `attributes.Test Variant` | 6 | `directMarketing.emailSent.testVariantID` | `directMarketing.emailSent.testVariantID` |  |
| Note - dérivée de la valeur des actifs secondaires |  | `directMarketing.emailSent.testVariantName` | `directMarketing.emailSent.testVariantName` |  |
| `attributes.Campaign Run ID` | 6 | `directMarketing.emailSent.automationRunID` | `directMarketing.emailSent.automationRunID` |  |
|  |  | `directMarketing.automationRunID` | `directMarketing.automationRunID` |  |

{style="table-layout:auto"}

## Programmes {#programs}

Lisez la [présentation de XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign.md) pour plus d’informations sur la classe XDM. Pour plus d’informations sur les groupes de champs XDM, consultez le guide [groupe de champs de schéma des détails Business Campaign](../../../../xdm/field-groups/b2b-campaign/details.md).

>[!NOTE]
>
>Pour les types de balises personnalisés, accédez aux schémas et créez des groupes de champs. Ajoutez ensuite tous les noms de champ supplémentaires requis pour mapper les champs source aux champs XDM de destination.

| Jeu de données source | Champ cible XDM | Notes |
| -------------- | --------------- | ----- |
| `"${MUNCHKIN_ID}"` | `campaignKey.sourceInstanceID` | MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `"Marketo"` | `campaignKey.sourceType` |  |
| `channel` | `channelName` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignKey.sourceKey` | Identité du Principal. MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `cost` | `actualCost.amount` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `description` | `campaignDescription` |  |
| `endDate` | `campaignEndDate` |  |
| `id` | `campaignKey.sourceID` |  |
| `iif(parentProgramId != null && parentProgramId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", parentProgramId, "sourceKey", concat(parentProgramId,"@${MUNCHKIN_ID}.Marketo")), null)` | `parentCampaignKey` |  |
| `iif(sfdcId != null && sfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", sfdcId, "sourceKey", concat(sfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` est une identité Secondaire. CRM_TYPE et CRM_ORG_ID seront remplacés dans le cadre de l’API Explorer |
| `integrationPartner` | `integrationPartnerName` |  |
| `marketoIsDeleted` | `isDeleted` |  |
| `name` | `campaignName` |  |
| `startDate` | `campaignStartDate` |  |
| `status` | `campaignStatus` |  |
| `type` | `campaignType` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `webinarHistorySyncDate` | `webinarHistorySyncDate` |  |
| `webinarHistorySyncStatus` | `webinarHistorySyncStatus` |  |
| `webinarSessionDescription` | `webinarSessionDescription` |  |
| `webinarSessionName` | `webinarSessionName` |  |

{style="table-layout:auto"}

## Abonnements au programme {#program-memberships}

Lisez la [présentation des membres XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign-members.md) pour plus d’informations sur la classe XDM. Pour plus d’informations sur les groupes de champs XDM, consultez le guide [Groupe de champs de schéma des détails des membres XDM Business Campaign](../../../../xdm/field-groups/b2b-campaign-members/details.md).

| Jeu de données source | Champ cible XDM | Notes |
| -------------- | --------------- | ----- |
| `"Marketo"` | `campaignMemberKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `campaignMemberKey.sourceInstanceID` | MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `id` | `campaignMemberKey.sourceID` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignMemberKey.sourceKey` | Identité du Principal. MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `iif(programId != null && programId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", programId, "sourceKey", concat(programId,"@${MUNCHKIN_ID}.Marketo")), null)` | `campaignKey` | Relation |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relation |
| `iif(acquiredByCampaignID != null && acquiredByCampaignID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", acquiredByCampaignID, "sourceKey", concat(acquiredByCampaignID,"@${MUNCHKIN_ID}.Marketo")), null)` | `acquiredByCampaignKey` |  |
| `reachedSuccess` | `hasReachedSuccess` |  |
| `isExhausted` | `isExhausted` |  |
| `statusName` | `memberStatus` |  |
| `statusReason` | `memberStatusReason` |  |
| `membershipDate` | `membershipDate` |  |
| `nurtureCadence` | `nurtureCadence` |  |
| `trackName` | `nurtureTrackName` |  |
| `webinarUrl` | `webinarConfirmationUrl` |  |
| `registrationCode` | `webinarRegistrationID` |  |
| `reachedSuccessDate` | `reachedSuccessDate` |  |
| `iif(sfdc.crmId != null && sfdc.crmId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", sfdc.crmId, "sourceKey", concat(sfdc.crmId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` est une identité Secondaire. CRM_TYPE et CRM_ORG_ID seront remplacés dans le cadre de l’API Explorer |
| `sfdc.lastStatus` | `lastStatus` |  |
| `sfdc.hasResponded` | `hasResponded` |  |
| `sfdc.firstRespondedDate` | `firstRespondedDate` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## Sociétés {#companies}

Lisez la [présentation des comptes professionnels XDM](../../../../xdm/classes/b2b/business-account.md) pour plus d’informations sur la classe XDM.

| Jeu de données source | Champ cible XDM | Notes |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` | |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `concat(id, ".mkto_org")` | `accountKey.sourceID` | |
| `concat(id, ".mkto_org@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | Identité du Principal. MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| <ul><li><code>iif(mktoCdpExternalId != null &amp;&amp; mktoCdpExternalId != «  », to_object(« sourceType », « ${CRM_TYPE} », « sourceInstanceID », « ${CRM_ORG_ID} », « sourceID », mktoCdpExternalId, « sourceKey », concat(mktoCdpExternalId, »@${CRM_ORG_ID}.${CRM_TYPE} »), nul)</code></li><li><code>iif(msftCdpExternalId != null &amp;&amp; msftCdpExternalId != «  », to_object(« sourceType », « ${CRM_TYPE} », « sourceInstanceID », « ${CRM_ORG_ID} », « sourceID », msftCdpExternalId, « sourceKey », concat(msftCdpExternalId, »@${CRM_ORG_ID}.${CRM_TYPE} »), nul)</code></li></ul> | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` est une identité Secondaire. CRM_ORG_ID et CRM_TYPE seront remplacés dans le cadre de l’API Explorer |
| `createdAt` | `extSourceSystemAudit.createdDate` | |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` | |
| `billingCity` | `accountBillingAddress.city` | |
| `billingCountry` | `accountBillingAddress.country` | |
| `billingPostalCode` | `accountBillingAddress.postalCode` | |
| `billingState` | `accountBillingAddress.state` | |
| `billingStreet` | `accountBillingAddress.street1` | |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` | |
| `sicCode` | `accountOrganization.SICCode` | |
| `industry` | `accountOrganization.industry` | |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` | |
| `website` | `accountOrganization.website` | |
| `mainPhone` | `accountPhone.number` | |
| `company` | `accountName` | |
| `companyNotes` | `accountDescription` | |
| `site` | `accountSite` | |
| `iif(mktoCdpParentOrgId != null && mktoCdpParentOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(mktoCdpParentOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpParentOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` | |
| `marketoIsDeleted` | `isDeleted` | |

{style="table-layout:auto"}

## Listes statiques {#static-lists}

Lisez la [présentation de la liste XDM Business Marketing](../../../../xdm/classes/b2b/business-marketing-list.md) pour plus d’informations sur la classe XDM.

| Jeu de données source | Champ cible XDM | Notes |
| -------------- | --------------- | ----- |
| `"Marketo"` | `marketingListKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `marketingListKey.sourceInstanceID` | MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `id` | `marketingListKey.sourceID` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `marketingListKey.sourceKey` | Identité du Principal. MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `name` | `marketingListName` |  |
| `description` | `marketingListDescription` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## Abonnements à des listes statiques {#static-list-memberships}

Lisez la [Présentation des membres de la liste XDM Business Marketing](../../../../xdm/classes/b2b/business-marketing-list-members.md) pour plus d’informations sur la classe XDM.

| Jeu de données source | Champ cible XDM | Notes |
| -------------- | --------------- | ----- |
| `"Marketo"` | `marketingListMemberKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `marketingListMemberKey.sourceInstanceID` | MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `staticListMemberID` | `marketingListMemberKey.sourceID` |  |
| `concat(staticListMemberID,"@${MUNCHKIN_ID}.Marketo")` | `marketingListMemberKey.sourceKey` | Identité du Principal. MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `iif(staticListID != null && staticListID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", staticListID, "sourceKey", concat(staticListID,"@${MUNCHKIN_ID}.Marketo")), null)` | `marketingListKey` | Relation |
| `iif(personID != null && personID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", personID, "sourceKey", concat(personID,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relation |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## Comptes désignés {#named-accounts}

>[!IMPORTANT]
>
>Le jeu de données de comptes désignés n’est nécessaire qu’avec la fonctionnalité Account-based marketing (ABM) de Marketo. Si vous n’utilisez pas ABM, vous n’avez pas besoin de configurer des mappages pour les comptes désignés.

Lisez la [Présentation des comptes professionnels XDM](../../../../xdm/classes/b2b/business-account.md) pour plus d’informations sur la classe XDM.

| Jeu de données source | Champ cible XDM | Notes |
| -------------- | --------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `concat(id, ".mkto_acct")` | `accountKey.sourceID` |  |
| `concat(id, ".mkto_acct@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | Identité du Principal. MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `iif(crmGuid != null && crmGuid != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", crmGuid, "sourceKey", concat(crmGuid,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` est une identité Secondaire. CRM_TYPE et CRM_ORG_ID seront remplacés dans le cadre de l’API Explorer |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `city` | `accountBillingAddress.city` |  |
| `country` | `accountBillingAddress.country` |  |
| `state` | `accountBillingAddress.state` |  |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |  |
| `sicCode` | `accountOrganization.SICCode` |  |
| `industry` | `accountOrganization.industry` |  |
| `logoUrl` | `accountOrganization.logoUrl` |  |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |  |
| `name` | `accountName` |  |
| `iif(parentAccountId != null && parentAccountId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(parentAccountId, ".mkto_acct"), "sourceKey", concat(parentAccountId, ".mkto_acct@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` |  |
| `sourceType` | `accountSourceType` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## Opportunités {#opportunities}

Lisez la [Présentation des opportunités commerciales XDM](../../../../xdm/classes/b2b/business-opportunity.md) pour plus d’informations sur la classe XDM.

| Jeu de données source | Champ cible XDM | Notes |
| -------------- | --------------- | ----- |
| `"Marketo"` | `opportunityKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `opportunityKey.sourceInstanceID` | MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `id` | `opportunityKey.sourceID` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityKey.sourceKey` | Identité du Principal. MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `iif(externalOpportunityId != null && externalOpportunityId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", externalOpportunityId, "sourceKey", concat(externalOpportunityId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` est une identité Secondaire. CRM_TYPE et CRM_ORG_ID seront remplacés dans le cadre de l’API Explorer |
| `iif(mktoCdpAccountOrgId != null && mktoCdpAccountOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(mktoCdpAccountOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpAccountOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountKey` | Relation |
| `description` | `opportunityDescription` |  |
| `name` | `opportunityName` |  |
| `stage` | `opportunityStage` |  |
| `type` | `opportunityType` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `expectedRevenue` | `expectedRevenue.amount` |  |
| `amount` | `opportunityAmount.amount` |  |
| `closeDate` | `expectedCloseDate` |  |
| `fiscalQuarter` | `fiscalQuarter` |  |
| `fiscalYear` | `fiscalYear` |  |
| `forecastCategory` | `forecastCategory` |  |
| `forecastCategoryName` | `forecastCategoryName` |  |
| `isClosed` | `isClosed` |  |
| `isWon` | `isWon` |  |
| `quantity` | `opportunityQuantity` |  |
| `probability` | `probabilityPercentage` |  |
| `iif(mktoCdpSourceCampaignId != null && mktoCdpSourceCampaignId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpSourceCampaignId, "sourceKey", concat(mktoCdpSourceCampaignId,"@${MUNCHKIN_ID}.Marketo")), null)` | `campaignKey` | Pour les clients avec intégration de Salesforce uniquement |
| `lastActivityDate` | `lastActivityDate` |  |
| `leadSource` | `leadSource` |  |
| `nextStep` | `nextStep` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## Rôles de contact d’opportunité {#opportunity-contact-roles}

Lisez la [Présentation de la relation Personne-opportunité commerciale XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) pour plus d’informations sur la classe XDM.

| Jeu de données source | Champ cible XDM | Notes |
| -------------- | --------------- | ----- |
| `"${MUNCHKIN_ID}"` | `opportunityPersonKey.sourceInstanceID` | MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `"Marketo"` | `opportunityPersonKey.sourceType` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityPersonKey.sourceKey` | Identité du Principal. MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `id` | `opportunityPersonKey.sourceID` |  |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relation |
| `iif(mktoCdpOpptyId != null && mktoCdpOpptyId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpOpptyId, "sourceKey", concat(mktoCdpOpptyId,"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityKey` | Relation |
| `iif(mktoCdpSfdcId != null && mktoCdpSfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", mktoCdpSfdcId, "sourceKey", concat(mktoCdpSfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` est une identité Secondaire. CRM_TYPE et CRM_ORG_ID seront remplacés dans le cadre de l’API Explorer |
| `isPrimary` | `isPrimary` |  |
| `marketoIsDeleted` | `isDeleted` |  |
| `role` | `personRole` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |

{style="table-layout:auto"}

## Personnes {#persons}

Lisez la [Présentation du Profil individuel XDM](../../../../xdm/classes/individual-profile.md) pour plus d’informations sur la classe XDM. Pour plus d’informations sur les groupes de champs XDM, consultez les guides [Groupe de champs de schéma Détails professionnels XDM](../../../../xdm/field-groups/profile/business-person-details.md) et [Groupe de champs de schéma Composants professionnels XDM](../../../../xdm/field-groups/profile/business-person-components.md).

| Champ source | Champ XDM cible | Notes |
|---|---|---|
| `"${MUNCHKIN_ID}"` | `b2b.personKey.sourceInstanceID` | MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `"Marketo"` | `b2b.personKey.sourceType` | |
| `address` | `workAddress.street1` | |
| `city` | `workAddress.city` | |
| `company` | `organizations` | |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `b2b.personKey.sourceKey` | Identité du Principal. MUNCHKIN_ID sera remplacé dans le cadre de l’API Explorer |
| `country` | `workAddress.country` | |
| `createdAt` | `extSourceSystemAudit.createdDate` | |
| `dateOfBirth` | `person.birthDate` | |
| `email` | `personComponents.workEmail.address` | |
| `email` | `workEmail.address` | |
| `fax` | `faxPhone.number` | |
| `firstName` | `person.name.firstName` | |
| `id` | `b2b.personKey.sourceID` | |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `b2b.accountKey` | |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourceAccountKey` | |
| <ul><li><code>iif(decode(sfdcType, « Contact », sfdcContactId, « Lead », sfdcLeadId , null) != null, to_object(« sourceType », « ${CRM_TYPE} », « sourceInstanceID », « ${CRM_ORG_ID} »,« sourceID », decode(sfdcType, « Contact », sfdcContactId, « Lead », sfdcLeadId , null), « sourceKey », concat(decode(sfdcType, « Contact », sfdcContactId, « Lead », sfdcLeadId , null), »@${CRM_ORG_ID}.${CRM_TYPE} »), nul)</code></li><li><code>iif(decode(msftType, « Contact », msftContactId, « Lead », msftLeadId , null) != null, to_object(« sourceType », « ${CRM_TYPE} », « sourceInstanceID », « ${CRM_ORG_ID} »,« sourceID », decode(msftType, « Contact », msftContactId, « Lead », msftLeadId , null), « sourceKey », concat(decode(msftType, « Contact », msftContactId, « Lead », msftLeadId , null), »@${CRM_ORG_ID}.${CRM_TYPE} »), nul)</code></li></ul> | `personComponents.sourceExternalKey` | |
| <ul><li><code>iif(decode(sfdcType, « Contact », sfdcContactId, « Lead », sfdcLeadId , null) != null, to_object(« sourceType », « ${CRM_TYPE} », « sourceInstanceID », « ${CRM_ORG_ID} »,« sourceID », decode(sfdcType, « Contact », sfdcContactId, « Lead », sfdcLeadId , null), « sourceKey », concat(decode(sfdcType, « Contact », sfdcContactId, « Lead », sfdcLeadId , null), »@${CRM_ORG_ID}.${CRM_TYPE} »), nul)</code></li><li><code>iif(decode(msftType, « Contact », msftContactId, « Lead », msftLeadId , null) != null, to_object(« sourceType », « ${CRM_TYPE} », « sourceInstanceID », « ${CRM_ORG_ID} »,« sourceID », decode(msftType, « Contact », msftContactId, « Lead », msftLeadId , null), « sourceKey », concat(decode(msftType, « Contact », msftContactId, « Lead », msftLeadId , null), »@${CRM_ORG_ID}.${CRM_TYPE} »), nul)</code></li></ul> | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` est une identité secondaire |
| `iif(ecids != null, to_object('ECID',arrays_to_objects('id',explode(ecids))), null)` | `identityMap` | Ceci est un champ calculé |
| `iif(id != null && id != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", id, "sourceKey", concat(id,"@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourcePersonKey` | |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpCnvContactPersonId, "sourceKey", concat(mktoCdpCnvContactPersonId,"@${MUNCHKIN_ID}.Marketo")), null)` | `b2b.convertedContactKey` | Ceci est un champ calculé |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpCnvContactPersonId, "sourceKey", concat(mktoCdpCnvContactPersonId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourceConvertedContactKey` | Ceci est un champ calculé |
| `iif(unsubscribed == 'true', 'n', 'y' )` | `consents.marketing.email.val` | Si le désabonnement est vrai (c’est-à-dire que la valeur = 1), définissez consentements.marketing.email.val sur « n ». Si le désabonnement a la valeur false (c’est-à-dire la valeur = 0), définissez consentements.marketing.email.val sur null. |
| `iif(unsubscribedReason != null && unsubscribedReason != "", substr(unsubscribedReason, 0, 100), null)` | `consents.marketing.email.reason` | |
| `lastName` | `person.name.lastName` | |
| `leadPartitionId` | `b2b.personGroupID` | |
| `leadPartitionId` | `personComponents.personGroupID` | |
| `leadScore` | `b2b.personScore` | |
| `leadScore` | `personComponents.personScore` | |
| `leadSource` | `b2b.personSource` | |
| `leadSource` | `personComponents.personSource` | |
| `leadStatus` | `b2b.personStatus` | |
| `leadStatus` | `personComponents.personStatus` | |
| `marketingSuspended` | `b2b.isMarketingSuspended` | |
| `marketingSuspendedCause` | `b2b.marketingSuspendedCause` | |
| `marketoIsDeleted` | `isDeleted` | |
| `middleName` | `person.name.middleName` | |
| `mktoCdpConvertedDate` | `b2b.convertedDate` | |
| `mktoCdpIsConverted` | `b2b.isConverted` | |
| `mobilePhone` | `mobilePhone.number` | |
| `personType` | `b2b.personType` | |
| `personType` | `personComponents.personType` | |
| `phone` | `workPhone.number` | |
| `postalCode` | `workAddress.postalCode` | |
| `salutation` | `person.name.courtesyTitle` | |
| `state` | `workAddress.state` | |
| `title` | `extendedWorkDetails.jobTitle` | |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` | |

{style="table-layout:auto"}

## Étapes suivantes

En lisant ce document, vous avez obtenu des informations sur la relation de mappage entre vos jeux de données [!DNL Marketo] et leurs champs XDM correspondants. Voir le tutoriel sur la [création d’une  [!DNL Marketo] connexion source](../../../tutorials/ui/create/adobe-applications/marketo.md) pour terminer vos flux de données [!DNL Marketo].