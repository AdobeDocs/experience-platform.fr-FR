---
keywords: Experience Platform ; accueil ; rubriques populaires ; Marketo Engage ; marketing à engager ; Marketo ; mappage
solution: Experience Platform
title: Mappage de champs pour la source du Marketo Engage
topic-legacy: overview
description: Les tableaux ci-dessous contiennent les mappages entre les champs des jeux de données Marketo et les champs XDM correspondants.
exl-id: 2b217bba-2748-4d6f-85ac-5f64d5e99d49
translation-type: tm+mt
source-git-commit: 8f03b2e8a10d57fcae77dedecdce0e0176ba04fd
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 3%

---

# (bêta) [!DNL Marketo Engage] mappages de champs

>[!IMPORTANT]
>
>La source [!DNL Marketo Engage] est actuellement en version bêta. Ses fonctionnalités et la documentation peuvent être modifiées.

Les tableaux ci-dessous contiennent les mappages entre les champs des neuf jeux de données [!DNL Marketo] et les champs correspondants du modèle de données d’expérience (XDM).

## Activités {#activities}

| Jeu de données source | Champ de cible XDM | Notes |
| -------------- | ---------------- | ----- |
| `_id` | `_id` |
| `personID` | `personID` | Identité Principal |
| `eventType` | `eventType` |
| `timeStamp` | `timestamp` |
| `web.webPageDetails._marketo.URL` | `web.webPageDetails._marketo.URL` |
| `environment.browserDetails.userAgent` | `environment.browserDetails.userAgent` |
| `environment.ipV4` | `environment.ipV4` |
| `search.keywords` | `search.keywords` |
| `search.searchEngine` | `search.searchEngine` |
| `web.webPageDetails.webPageID` | `web.webPageDetails.webPageID` |
| `web.webPageDetails.name` | `web.webPageDetails.name` |
| `web.webPageDetails.isPersonalizedURL` | `web.webPageDetails.isPersonalizedURL` |
| `web.webPageDetails.queryParameters` | `web.webPageDetails.queryParameters` |
| `web.webReferrer.URL` | `web.webReferrer.URL` |
| `listOperations.listID` | `listOperations.listID` |
| `opportunityEvent.isPrimary` | `opportunityEvent.isPrimary` |
| `opportunityEvent.opportunityID` | `opportunityEvent.opportunityID` |
| `opportunityEvent.role` | `opportunityEvent.role` |
| `leadOperation.newLead.createdDate` | `leadOperation.newLead.createdDate` |
| `leadOperation.newLead.formName` | `leadOperation.newLead.formName` |
| `leadOperation.newLead.leadSource` | `leadOperation.newLead.leadSource` |
| `leadOperation.newLead.listName` | `leadOperation.newLead.listName` |
| `leadOperation.newLead.sfdcType` | `leadOperation.newLead.sfdcType` |
| `leadOperation.newLead.sourceType` | `leadOperation.newLead.sourceType` |
| `leadOperation.convertLead.assignTo` | `leadOperation.convertLead.assignTo` |
| `leadOperation.convertLead.convertedStatus` | `leadOperation.convertLead.convertedStatus` |
| `leadOperation.convertLead.isSentNotificationEmail` | `leadOperation.convertLead.isSentNotificationEmail` |
| `directMarketing.mailingID` | `directMarketing.mailingID` |
| `directMarketing.mailingName` | `directMarketing.mailingName` |
| `directMarketing.testVariantID` | `directMarketing.testVariantID` |
| `directMarketing.testVariantName` | `directMarketing.testVariantName` |
| `directMarketing.emailBouncedCode` | `directMarketing.emailBouncedCode` |
| `directMarketing.emailBouncedDetails` | `directMarketing.emailBouncedDetails` |
| `directMarketing.email` | `directMarketing.email` |
| `device.isMobileDevice` | `device.isMobileDevice` |
| `device.model` | `device.model` |
| `environment.operatingSystem` | `environment.operatingSystem` |
| `directMarketing.linkURL` | `directMarketing.linkURL` |
| `web.webInteraction.linkID` | `web.webInteraction.linkID` |
| `web.fillOutForm.webFormID` | `web.fillOutForm.webFormID` |
| `web.fillOutForm.webFormName` | `web.fillOutForm.webFormName` |
| `web.webInteraction.linkURL` | `web.webInteraction.linkURL` |
| `leadOperation.changeScore.changeValue` | `leadOperation.changeScore.changeValue` |
| `leadOperation.changeScore.newValue` | `leadOperation.changeScore.newValue` |
| `leadOperation.changeScore.oldValue` | `leadOperation.changeScore.oldValue` |
| `leadOperation.changeScore.priority` | `leadOperation.changeScore.priority` |
| `leadOperation.changeScore.reason` | `leadOperation.changeScore.reason` |
| `leadOperation.changeScore.relativeScore` | `leadOperation.changeScore.relativeScore` |
| `leadOperation.changeScore.relativeUrgency` | `leadOperation.changeScore.relativeUrgency` |
| `leadOperation.changeScore.scoreAttributeID` | `leadOperation.changeScore.scoreAttributeID` |
| `leadOperation.changeScore.scoreAttributeName` | `leadOperation.changeScore.scoreAttributeName` |
| `leadOperation.changeScore.urgency` | `leadOperation.changeScore.urgency` |
| `opportunityEvent.dataValueChanges.attributeName` | `opportunityEvent.dataValueChanges.attributeName` |
| `opportunityEvent.dataValueChanges.newValue` | `opportunityEvent.dataValueChanges.newValue` |
| `opportunityEvent.dataValueChanges.oldValue` | `opportunityEvent.dataValueChanges.oldValue` |
| `opportunityEvent.opportunityID` | `opportunityEvent.opportunityID` |
| `leadOperation.campaignProgression.campaignID` | `leadOperation.campaignProgression.campaignID` |
| `leadOperation.campaignProgression.isAcquiredBy` | `leadOperation.campaignProgression.isAcquiredBy` |
| `leadOperation.campaignProgression.isSuccessful` | `leadOperation.campaignProgression.isSuccessful` |
| `leadOperation.campaignProgression.newStatusID` | `leadOperation.campaignProgression.newStatusID` |
| `leadOperation.campaignProgression.newStatusName` | `leadOperation.campaignProgression.newStatusName` |
| `leadOperation.campaignProgression.oldStatusID` | `leadOperation.campaignProgression.oldStatusID` |
| `leadOperation.campaignProgression.oldStatusName` | `leadOperation.campaignProgression.oldStatusName` |
| `leadOperation.campaignProgression.reason` | `leadOperation.campaignProgression.reason` |

{style=&quot;table-layout:auto&quot;}

## Programmes {#programs}

| Jeu de données source | Champ de cible XDM | Notes |
| -------------- | ---------------- | ----- |
| `id` | `campaignID` | Identité Principal |
| `sfdcId` | `extSourceSystemAudit.externalID` | Identité Secondaire |
| `name` | `campaignName` |
| `description` | `campaignDescription` |
| `type` | `campaignType` |
| `status` | `campaignStatus` |
| `channel` | `channelName` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `cost` | `actualCost.amount` |
| `parentProgramId` | `parentCampaignID` |
| `integrationPartner` | `integrationPartnerName` |
| `startDate` | `campaignStartDate` |
| `endDate` | `campaignEndDate` |

{style=&quot;table-layout:auto&quot;}

## Membres de programme {#program-memberships}

| Jeu de données source | Champ de cible XDM | Notes |
| -------------- | ---------------- | ----- |
| `id` | `campaignMemberID` | Identité Principal |
| `programId` | `campaignID` | Relation |
| `leadId` | `personID` | Relation |
| `acquiredByCampaignID` | `acquiredByCampaignID` |
| `reachedSuccess` | `hasReachedSuccess` |
| `isExhausted` | `isExhausted` |
| `statusName` | `memberStatus` |
| `statusReason` | `memberStatusReason` |
| `membershipDate` | `membershipDate` |
| `nurtureCadence` | `nurtureCadence` |
| `trackName` | `nurtureTrackName` |
| `webinarUrl` | `webinarConfirmationUrl` |
| `registrationCode` | `webinarRegistrationID` |
| `reachedSuccessDate` | `reachedSuccessDate` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## Sociétés {#companies}

| Jeu de données source | Champ de cible XDM | Notes |
| -------------- | ---------------- | ----- |
| `id` | `accountID` | Identité Principal |
| `mktoCdpExternalId` | `extSourceSystemAudit.externalID` | Identité Secondaire |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `billingCity` | `accountBillingAddress.city` |
| `billingCountry` | `accountBillingAddress.country` |
| `billingPostalCode` | `accountBillingAddress.postalCode` |
| `billingState` | `accountBillingAddress.state` |
| `billingStreet` | `accountBillingAddress.street1` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `website` | `accountOrganization.website` |
| `mainPhone` | `accountPhone.number` |
| `company` | `accountName` |
| `companyNotes` | `accountDescription` |
| `site` | `accountSite` |
| `mktoCdpParentOrgId` | `accountParentID` |

{style=&quot;table-layout:auto&quot;}

## Listes statiques {#static-lists}

| Jeu de données source | Champ de cible XDM | Notes |
| -------------- | ---------------- | ----- |
| `id` | `marketingListID` | Identité Principal |
| `name` | `marketingListName` |
| `description` | `marketingListDescription` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## Abonnements à la liste statique {#static-list-memnberships}

| Jeu de données source | Champ de cible XDM | Notes |
| -------------- | ---------------- | ----- |
| `staticListMemberID` | `marketingListMemberID` | Identité Principal |
| `staticListID` | `marketingListID` | Relation |
| `personID` | `personID` | Relation |
| `createdAt` | `extSourceSystemAudit.createdDate` |

{style=&quot;table-layout:auto&quot;}

## Comptes nommés {#named-accounts}

>[!IMPORTANT]
>
>Le jeu de données des comptes nommés n&#39;est nécessaire qu&#39;avec la fonction marketing basée sur les comptes (ABM) Marketo. Si vous n&#39;utilisez pas ABM, vous n&#39;avez pas besoin de configurer des mappages pour des comptes nommés.

| Jeu de données source | Champ de cible XDM | Notes |
| -------------- | ---------------- | ----- |
| `id` | `accountID` | Identité Principal |
| `crmGuid` | `extSourceSystemAudit.externalID` | Identité Secondaire |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `city` | `accountBillingAddress.city` |
| `country` | `accountBillingAddress.country` |
| `state` | `accountBillingAddress.state` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `logoUrl` | `accountOrganization.logoUrl` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `name` | `accountName` |
| `parentAccountId` | `accountParentID` |
| `sourceType` | `accountSourceType` |

{style=&quot;table-layout:auto&quot;}

## Opportunités {#opportunities}

| Jeu de données source | Champ de cible XDM | Notes |
| -------------- | ---------------- | ----- |
| `id` | `opportunityID` | Identité Principal |
| `externalOpportunityId` | `extSourceSystemAudit.externalID` | Identité Secondaire |
| `mktoCdpAccountOrgId` | `accountID` | Relation |
| `description` | `opportunityDescription` |
| `name` | `opportunityName` |
| `stage` | `opportunityStage` |
| `type` | `opportunityType` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `expectedRevenue` | `expectedRevenue.amount` |
| `amount` | `opportunityAmount.amount` |
| `closeDate` | `expectedCloseDate` |
| `fiscalQuarter` | `fiscalQuarter` |
| `fiscalYear` | `fiscalYear` |
| `forecastCategory` | `forecastCategory` |
| `forecastCategoryName` | `forecastCategoryName` |
| `isClosed` | `isClosed` |
| `isWon` | `isWon` |
| `quantity` | `opportunityQuantity` |
| `probability` | `probabilityPercentage` |
| `mktoCdpSourceCampaignId` | `campaignID` | Recommandé uniquement si vous utilisez l’intégration Salesforce. |
| `lastActivityDate` | `lastActivityDate` |
| `leadSource` | `leadSource` |
| `nextStep` | `nextStep` |

{style=&quot;table-layout:auto&quot;}

## Rôles de contact d&#39;opportunité {#opportunity-contact-roles}

| Jeu de données source | Champ de cible XDM | Notes |
| -------------- | ---------------- | ----- |
| `id` | `opportunityPersonID` | Identité Principal |
| `mktoCdpSfdcId` | `extSourceSystemAudit.externalID` | Identité Secondaire |
| `mktoCdpOpptyId` | `opportunityID` | Relation |
| `leadId` | `personID` | Relation |
| `role` | `personRole` |
| `isPrimary` | `isPrimary` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## Personnes {#persons}

Dans le tableau de bord [!DNL Profiles] de l&#39;interface utilisateur de la plate-forme, si la valeur de l&#39;assemblage d&#39;ID dans la stratégie de fusion que vous avez utilisée pour naviguer est définie sur `None`, la fenêtre des identités liées n&#39;affichera que l&#39;attribut d&#39;identité Principal.

Pour pallier ce problème, vous pouvez mettre à jour le champ d’assemblage d’ID de `None` en `Private graph` afin d’afficher toutes les identités liées à un [!DNL Profile]. Vous pouvez également créer une nouvelle stratégie de fusion ou utiliser une autre stratégie de fusion qui contient une valeur d&#39;assemblage d&#39;ID définie sur `Private graph`. Si vous choisissez de créer une nouvelle stratégie de fusion ou d&#39;utiliser une autre stratégie de fusion, vous devez vous assurer que la stratégie contient le même type de schéma que celui utilisé pour le jeu de correspondances [!DNL Marketo] Personnes. Pour plus d&#39;informations, consultez le [guide de l&#39;interface utilisateur des stratégies de fusion](../../../../profile/ui/merge-policies.md).

| Jeu de données source | Champ de cible XDM | Notes |
| -------------- | ---------------- | ----- |
| `id` | `personID` | Identité Principal |
| `emailSuspended` | `b2b.personOptInOut._channels.email` |
| `emailSuspendedAt` | `b2b.personOptInOut.optOutDetails.email.optOutDate` |
| `emailSuspendedCause` | `b2b.personOptInOut.optOutDetails.email.optOutReason` |
| `contactCompany` | `b2b.accountID` |
| `marketingSuspended` | `b2b.isMarketingSuspended` |
| `marketingSuspendedCause` | `b2b.marketingSuspendedCause` |
| `leadScore` | `b2b.personScore` |
| `leadSource` | `b2b.personSource` |
| `leadStatus` | `b2b.personStatus` |
| `personType` | `b2b.personType` |
| `leadPartitionId` | `b2b.personGroupID` |
| `mktoCdpCnvContactPersonId` | `b2b.convertedContactID` |
| `mktoCdpIsConverted` | `b2b.isConverted` |
| `mktoCdpConvertedDate` | `b2b.convertedDate` |
| `sfdcLeadId` | `extSourceSystemAudit.externalID` | Identité Secondaire |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `title` | `extendedWorkDetails.jobTitle` |
| `fax` | `faxPhone.number` |
| `mobilePhone` | `mobilePhone.number` |
| `firstName` | `person.name.firstName` |
| `lastName` | `person.name.lastName` |
| `middleName` | `person.name.middleName` |
| `salutation` | `person.name.courtesyTitle` |
| `dateOfBirth` | `person.birthDate` |
| `city` | `workAddress.city` |
| `country` | `workAddress.country` |
| `postalCode` | `workAddress.postalCode` |
| `state` | `workAddress.state` |
| `address` | `workAddress.street1` |
| `phone` | `workPhone.number` |
| `company` | `organizations` |
| `leadScore` | `personComponents.personScore` |
| `leadSource` | `personComponents.personSource` |
| `leadStatus` | `personComponents.personStatus` |
| `personType` | `personComponents.personType` |
| `leadPartitionId` | `personComponents.personGroupID` |
| `mktoCdpCnvContactPersonId` | `personComponents.sourceConvertedContactID` |
| `contactCompany` | `personComponents.sourceAccountID` |
| `sfdcContactId` | `personComponents.sourceExternalID` | Recommandé uniquement si vous utilisez l’intégration Salesforce. |
| `id` | `personComponents.sourcePersonID` |
| `email` | `personComponents.workEmail.address` |
| `email` | `workEmail.address` |
| `to_object('ECID',arrays_to_objects('id',explode(ecids)))` | `identityMap` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>Le champ source `to_object('ECID',arrays_to_objects('id',explode(ecids)))` est un champ calculé qui doit être ajouté à l&#39;aide de l&#39;option [!UICONTROL Ajouter champ calculé] dans l&#39;interface utilisateur de la plate-forme. Pour plus d&#39;informations, consultez le didacticiel sur l&#39;[ajout de champs calculés](../../../../ingestion/tutorials/map-a-csv-file.md).

## Étapes suivantes

En lisant ce document, vous obtenez des informations sur la relation de mappage entre vos jeux de données [!DNL Marketo] et leurs champs XDM correspondants. Consultez le didacticiel sur [la création d&#39;une  [!DNL Marketo] connexion source](../../../tutorials/ui/create/adobe-applications/marketo.md) pour terminer votre flux de données [!DNL Marketo].
