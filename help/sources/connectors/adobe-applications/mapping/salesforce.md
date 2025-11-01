---
title: Champs de mappage Salesforce
description: Les tableaux ci-dessous contiennent les mappages entre les champs source Salesforce et leurs champs XDM correspondants.
exl-id: 33ee76f2-0495-4acd-a862-c942c0fa3177
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 100%

---

# Mappages de champs [!DNL Salesforce]

Les tableaux ci-dessous contiennent les mappages entre les champs source [!DNL Salesforce] et leurs champs Modèle de données d’expérience (XDM) correspondants.

## Contact {#contact}

Lisez la [Présentation du Profil individuel XDM](../../../../xdm/classes/individual-profile.md) pour plus d’informations sur la classe XDM. Pour plus d’informations sur les groupes de champs XDM, consultez les guides [Groupe de champs de schéma Détails professionnels XDM](../../../../xdm/field-groups/profile/business-person-details.md) et [Groupe de champs de schéma Composants professionnels XDM](../../../../xdm/field-groups/profile/business-person-components.md).

| Champ source | Chemin du champ XDM cible | Notes |
| --- | --- | --- |
| `AccountId` | `b2b.accountKey.sourceID` |  |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `b2b.accountKey` |  |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", AccountId, "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personComponents.sourceAccountKey` |  |
| `"Salesforce"` | `b2b.personKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `b2b.personKey.sourceKey` | Identité principale. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `AssistantName` | `extendedWorkDetails.assistantDetails.name.fullName` |  |
| `AssistantPhone` | `extendedWorkDetails.assistantDetails.phone.number` |  |
| `Birthdate` | `person.birthDate` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `Department` | `extendedWorkDetails.departments` |  |
| `Email` | `workEmail.address` | Identité secondaire. |
| `Email` | `personComponents.workEmail.address` |  |
| `Fax` | `faxPhone.number` |  |
| `FirstName` | `person.name.firstName` |  |
| `HomePhone` | `homePhone.number` |  |
| `isDeleted` | `isDeleted` |  |
| `Id` | `b2b.personKey.sourceID` |  |
| `"Salesforce"` | `personComponents.sourcePersonKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `personComponents.sourcePersonKey.sourceInstanceID` |  |
| `Id` | `personComponents.sourcePersonKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `personComponents.sourcePersonKey.sourceKey` |  |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `LastName` | `person.name.lastName` |  |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |  |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |  |
| `LeadSource` | `b2b.personSource` |  |
| `LeadSource` | `personComponents.personSource` |  |
| `MailingCity` | `workAddress.city` |  |
| `MailingCountry` | `workAddress.country` |  |
| `MailingLatitude` | `workAddress._schema.latitude` |  |
| `MailingLongitude` | `workAddress._schema.longitude` |  |
| `MailingPostalCode` | `workAddress.postalCode` |  |
| `MailingState` | `workAddress.state` |  |
| `MailingStreet` | `workAddress.street1` |  |
| `MobilePhone` | `mobilePhone.number` |  |
| `Name` | `person.name.fullName` |  |
| `OtherCity` | `otherAddress.city` |  |
| `OtherCountry` | `otherAddress.country` |  |
| `OtherLatitude` | `otherAddress._schema.latitude` |  |
| `OtherLongitude` | `otherAddress._schema.longitude` |  |
| `OtherPhone` | `otherPhone.number` |  |
| `OtherPostalCode` | `otherAddress.postalCode` |  |
| `OtherState` | `otherAddress.state` |  |
| `OtherStreet` | `otherAddress.street1` |  |
| `Phone` | `workPhone.number` |  |
| `ReportsToId` | `extendedWorkDetails.reportsToID` |  |
| `Salutation` | `person.name.courtesyTitle` |  |
| `Title` | `extendedWorkDetails.jobTitle` |  |
| `"Contact"` | `b2b.personType` |  |

{style="table-layout:auto"}

## Prospect {#lead}

Lisez la [Présentation du Profil individuel XDM](../../../../xdm/classes/individual-profile.md) pour plus d’informations sur la classe XDM. Pour plus d’informations sur les groupes de champs XDM, consultez les guides [Groupe de champs de schéma Détails professionnels XDM](../../../../xdm/field-groups/profile/business-person-details.md) et [Groupe de champs de schéma Composants professionnels XDM](../../../../xdm/field-groups/profile/business-person-components.md).

| Champ source | Chemin du champ XDM cible | Notes |
| --- | --- | --- |
| `City` | `workAddress.city` |  |
| `ConvertedDate` | `b2b.convertedDate` |  |
| `Country` | `workAddress.country` |  |
| `Email` | `workEmail.address` | Identité secondaire. |
| `Email` | `personComponents.workEmail.address` |  |
| `Fax` | `faxPhone.number` |  |
| `FirstName` | `person.name.firstName` |  |
| `IsConverted` | `b2b.isConverted` |  |
| `isDeleted` | `isDeleted` |  |
| `"Salesforce"` | `b2b.personKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` |  |
| `Id` | `b2b.personKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `b2b.personKey.sourceKey` | Identité principale. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `"Salesforce"` | `personComponents.sourcePersonKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `personComponents.sourcePersonKey.sourceInstanceID` |  |
| `Id` | `personComponents.sourcePersonKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `personComponents.sourcePersonKey.sourceKey` |  |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `LastName` | `person.name.lastName` |  |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |  |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |  |
| `LeadSource` | `b2b.personSource` |  |
| `LeadSource` | `personComponents.personSource` |  |
| `Latitude` | `workAddress._schema.latitude` |  |
| `Longitude` | `workAddress._schema.longitude` |  |
| `Name` | `person.name.fullName` |  |
| `PostalCode` | `workAddress.postalCode` |  |
| `Salutation` | `person.name.courtesyTitle` |  |
| `State` | `workAddress.state` |  |
| `Status` | `b2b.personStatus` |  |
| `Status` | `personComponents.personStatus` |  |
| `Street` | `workAddress.street1` |  |
| `Title` | `extendedWorkDetails.jobTitle` |  |
| `Suffix` | `person.name.suffix` |  |
| `Company` | `b2b.companyName` |  |
| `Website` | `b2b.companyWebsite` |  |
| `ConvertedContactId` | `b2b.convertedContactKey.sourceID` |  |
| `iif(ConvertedContactId != null && ConvertedContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ConvertedContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `b2b.convertedContactKey` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `"Lead"` | `b2b.personType` |  |
| `iif(ConvertedContactId != null && ConvertedContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", ConvertedContactId, "sourceKey", concat(ConvertedContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personComponents.sourceConvertedContactKey` |  |

{style="table-layout:auto"}

## Compte {#account}

Lisez la [Présentation des détails du compte professionnel XDM](../../../../xdm/classes/b2b/business-account.md) pour plus d’informations sur la classe XDM.

| Champ source | Chemin du champ XDM cible | Notes |
| --- | --- | --- |
| `"Salesforce"` | `accountKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `accountKey.sourceInstanceID` | La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `AccountNumber` | `accountNumber` |  |
| `AccountSource` | `accountSourceType` |  |
| `AnnualRevenue` | `accountOrganization.annualRevenue.amount` |  |
| `BillingCity` | `accountBillingAddress.city` |  |
| `BillingCountry` | `accountBillingAddress.country` |  |
| `BillingLatitude` | `accountBillingAddress._schema.latitude` |  |
| `BillingLongitude` | `accountBillingAddress._schema.longitude` |  |
| `BillingPostalCode` | `accountBillingAddress.postalCode` |  |
| `BillingState` | `accountBillingAddress.state` |  |
| `BillingStreet` | `accountBillingAddress.street1` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `Description` | `accountDescription` |  |
| `DunsNumber` | `accountOrganization.DUNSNumber` | Fonctionnalité data.com |
| `Fax` | `accountFax.number` |  |
| `isDeleted` | `isDeleted` |  |
| `Id` | `accountKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `accountKey.sourceKey` | Identité principale. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `Industry` | `accountOrganization.industry` |  |
| `Jigsaw` | `accountOrganization.jigsaw` |  |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |  |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |  |
| `NaicsCode` | `accountOrganization.NAICSCode` | Fonctionnalité data.com |
| `NaicsDesc` | `accountOrganization.NAICSDescription` | Fonctionnalité data.com |
| `Name` | `accountName` |  |
| `NumberOfEmployees` | `accountOrganization.numberOfEmployees` |  |
| `Ownership` | `accountOwnership` |  |
| `ParentId` | `accountParentKey.sourceID` |  |
| `iif(ParentId != null && ParentId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ParentId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountParentKey` |  |
| `Phone` | `accountPhone.number` |  |
| `ShippingCity` | `accountShippingAddress.city` |  |
| `ShippingCountry` | `accountShippingAddress.country` |  |
| `ShippingLatitude` | `accountShippingAddress._schema.latitude` |  |
| `ShippingLongitude` | `accountShippingAddress._schema.longitude` |  |
| `ShippingPostalCode` | `accountShippingAddress.postalCode` |  |
| `ShippingState` | `accountShippingAddress.state` |  |
| `ShippingStreet` | `accountShippingAddress.street1` |  |
| `Sic` | `accountOrganization.SICCode` |  |
| `SicDesc` | `accountOrganization.SICDescription` |  |
| `Site` | `accountSite` |  |
| `TickerSymbol` | `accountOrganization.tickerSymbol` |  |
| `Tradestyle` | `accountTradeStyle` | Fonctionnalité data.com |
| `Type` | `accountType` |  |
| `Website` | `accountOrganization.website` |  |

{style="table-layout:auto"}

## Opportunité {#opportunity}

Lisez la [Présentation des opportunités commerciales XDM](../../../../xdm/classes/b2b/business-opportunity.md) pour plus d’informations sur la classe XDM.

| Champ source | Chemin du champ XDM cible | Notes |
| --- | --- | --- |
| `"Salesforce"` | `opportunityKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` | La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `opportunityKey.sourceKey` | Identité principale. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `AccountId` | `accountKey.sourceID` |  |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountKey` | Relation. |
| `Amount` | `opportunityAmount.amount` |  |
| `CampaignId` | `campaignKey.sourceID` |  |
| `iif(CampaignId != null && CampaignId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(CampaignId,"@${CRM_ORG_ID}.Salesforce")), null)` | `campaignKey` |  |
| `CloseDate` | `expectedCloseDate` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `Description` | `opportunityDescription` |  |
| `ExpectedRevenue` | `expectedRevenue.amount` |  |
| `FiscalQuarter` | `fiscalQuarter` |  |
| `FiscalYear` | `fiscalYear` |  |
| `ForecastCategory` | `forecastCategory` |  |
| `ForecastCategoryName` | `forecastCategoryName` |  |
| `Id` | `opportunityKey.sourceID` |  |
| `IsClosed` | `isClosed` |  |
| `isDeleted` | `isDeleted` |  |
| `IsWon` | `isWon` |  |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |  |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |  |
| `LeadSource` | `leadSource` |  |
| `Name` | `opportunityName` |  |
| `NextStep` | `nextStep` |  |
| `Probability` | `probabilityPercentage` |  |
| `StageName` | `opportunityStage` |  |
| `TotalOpportunityQuantity` | `opportunityQuantity` |  |
| `Type` | `opportunityType` |  |
| `CurrencyIsoCode` | `opportunityAmount.currencyCode` |  |

{style="table-layout:auto"}

## Rôle de contact d’opportunité {#opportunity-contact-role}

Lisez la [Présentation de la classe de relation entre la personne et l’opportunité commerciale XDM](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) pour plus d’informations sur la classe XDM.

| Champ source | Chemin du champ XDM cible | Notes |
| --- | --- | --- |
| `"Salesforce"` | `opportunityPersonKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `opportunityPersonKey.sourceInstanceID` | La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `"Salesforce"` | `personKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `personKey.sourceInstanceID` |  |
| `ContactId` | `personKey.sourceID` |  |
| `concat(ContactId,"@${CRM_ORG_ID}.Salesforce")` | `personKey.sourceKey` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `Id` | `opportunityPersonKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `opportunityPersonKey.sourceKey` | Identité principale. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `isDeleted` | `isDeleted` |  |
| `IsPrimary` | `isPrimary` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `"Salesforce"` | `opportunityKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` |  |
| `OpportunityId` | `opportunityKey.sourceID` |  |
| `concat(OpportunityId,"@${CRM_ORG_ID}.Salesforce")` | `opportunityKey.sourceKey` |  |
| `Role` | `personRole` |  |

{style="table-layout:auto"}

## Campaign {#campaign}

Lisez la [Présentation de la classe XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign.md) pour plus d’informations sur la classe XDM. Pour plus d’informations sur les groupes de champs XDM, consultez le guide [Groupe de champs de schéma des détails de XDM Business Campaign](../../../../xdm/field-groups/b2b-campaign/details.md).

| Champ source | Chemin du champ XDM cible | Notes |
| --- | --- | --- |
| `"Salesforce"` | `campaignKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `campaignKey.sourceInstanceID` | La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `isDeleted` | `isDeleted` |  |
| `Id` | `campaignKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `campaignKey.sourceKey` | Identité principale. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `Name` | `campaignName` |  |
| `ParentId` | `parentCampaignKey.sourceID` |  |
| `iif(ParentId != null && ParentId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ParentId,"@${CRM_ORG_ID}.Salesforce")), null)` | `parentCampaignKey` |  |
| `Type` | `campaignType` |  |
| `Status` | `campaignStatus` |  |
| `StartDate` | `campaignStartDate` |  |
| `EndDate` | `campaignEndDate` |  |
| `ExpectedRevenue` | `expectedRevenue.amount` |  |
| `BudgetedCost` | `budgetedCost.amount` |  |
| `ActualCost` | `actualCost.amount` |  |
| `ExpectedResponse` | `expectedResponse` |  |
| `IsActive` | `isActive` |  |
| `Description` | `campaignDescription` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |  |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |  |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |  |
| `CurrencyIsoCode` | `actualCost.currencyCode` |  |

## Membre de Campaign {#campaign-member}

Lisez la [Présentation des membres de XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign-members.md) pour plus d’informations sur la classe XDM. Pour plus d’informations sur les groupes de champs XDM, consultez le document [Groupe de champs du schéma Détails du membre de la campagne commerciale XDM](../../../../xdm/field-groups/b2b-campaign/details.md).

| Champ source | Chemin du champ XDM cible | Notes |
| --- | --- | --- |
| `"Salesforce"` | `campaignMemberKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `campaignMemberKey.sourceInstanceID` | La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `isDeleted` | `isDeleted` |  |
| `Id` | `campaignMemberKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `campaignMemberKey.sourceKey` | Identité principale. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `"Salesforce"` | `campaignKey.sourceType` |  |
| `${CRM_ORG_ID}` | `campaignKey.sourceInstanceID` |  |
| `CampaignId` | `campaignKey.sourceID` |  |
| `concat(CampaignId,"@${CRM_ORG_ID}.Salesforce")` | `campaignKey.sourceKey` |  |
| `"Salesforce"` | `personKey.sourceType` |  |
| `${CRM_ORG_ID}` | `personKey.sourceInstanceID` |  |
| `LeadOrContactId` | `personKey.sourceID` |  |
| `concat(LeadOrContactId,"@${CRM_ORG_ID}.Salesforce")` | `personKey.sourceKey` |  |
| `Status` | `memberStatus` |  |
| `HasResponded` | `hasResponded` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `FirstRespondedDate` | `firstRespondedDate` |  |
| `Type` | `b2b.personType` |  |

## Relation de contact de compte {#account-contact-relation}

Lisez la documentation sur la [Classe de relation entre la personne et le compte professionnel XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) pour plus d’informations sur la classe XDM.

| Champ source | Chemin du champ XDM cible | Notes |
| --- | --- | --- |
| `AccountId` | `accountKey.sourceID` |  |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountKey` |  |
| `ContactId` | `personKey.sourceID` |  |
| `iif(ContactId != null && ContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personKey` |  |
| `CreatedById` | `extSourceSystemAudit.createdBy` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `EndDate` | `relationEndDate` |  |
| `IsDeleted` | `isDeleted` |  |
| `Id` | `accountPersonKey.sourceID` |  |
| `"Salesforce"` | `accountPersonKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `accountPersonKey.sourceInstanceID` |  |
| `concat(Id, "@${CRM_ORG_ID}.Salesforce")` | `accountPersonKey.sourceKey` | Identité principale. |
| `IsActive` | `IsActive` |  |
| `IsDirect` | `IsDirect` |  |
| `LastModifiedById` | `extSourceSystemAudit.lastUpdatedBy` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `explode(Roles,";")` | `personRoles[]` |  |
| `StartDate` | `relationStartDate` |  |

## Étapes suivantes

En lisant ce document, vous avez reçu des informations sur la relation de mappage entre les champs source [!DNL Salesforce] et leurs champs XDM correspondants. Pour plus d’informations, consultez la documentation sur la [création d’une connexion source  [!DNL Salesforce] ](../../../connectors/crm/salesforce.md).
