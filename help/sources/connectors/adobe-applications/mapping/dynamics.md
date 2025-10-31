---
title: Champs de mappage Microsoft Dynamics
description: Les tableaux ci-dessous contiennent les mappages entre les champs source Microsoft Dynamics et leurs champs XDM correspondants.
exl-id: 32f51761-5de3-4192-8f23-c1412ca12c08
source-git-commit: 83a249daddbee1ec264b6e505517325c76ac9b09
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 41%

---

# Mappages de champs [!DNL Microsoft Dynamics]

Les tableaux ci-dessous contiennent les mappages entre les champs source [!DNL Microsoft Dynamics] et leurs champs Modèle de données d’expérience (XDM) correspondants.

## Contacts {#contacts}

| Champ source | Champ XDM cible | Notes |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |  |
| `address1_city` | `workAddress.city` |  |
| `address1_country` | `workAddress.country` |  |
| `address1_county` | `workAddress.stateProvince` |  |
| `address1_latitude` | `workAddress._schema.latitude` |  |
| `address1_line1` | `workAddress.street1` |  |
| `address1_line2` | `workAddress.street2` |  |
| `address1_line3` | `workAddress.street3` |  |
| `address1_longitude` | `workAddress._schema.longitude` |  |
| `address1_postalcode` | `workAddress.postalCode` |  |
| `address1_postofficebox` | `workAddress.postOfficeBox` |  |
| `address1_stateorprovince` | `workAddress.state` |  |
| `assistantname` | `extendedWorkDetails.assistantDetails.name.fullName` |  |
| `assistantphone` | `extendedWorkDetails.assistantDetails.phone.number` |  |
| `birthdate` | `person.birthDate` |  |
| `"Dynamics"` | `b2b.personKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `contactid` | `b2b.personKey.sourceID` |  |
| `concat(contactid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | Identité principale. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `iif(contactid != null && contactid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", contactid, "sourceKey", concat(contactid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |  |
| `department` | `extendedWorkDetails.departments` |  |
| `fullname` | `person.name.fullName` |  |
| `suffix` | `person.name.suffix` |  |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey", concat(parentcustomerid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourceAccountKey` |  |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey",  concat(parentcustomerid, "@${CRM_ORG_ID}.Dynamics")), null)` | `b2b.accountKey` |  |
| `createdon` | `extSourceSystemAudit.createdDate` |  |
| `emailaddress1` | `workEmail.address` | Identifiant Secondaire. |
| `emailaddress2` | `personalEmail.address` |  |
| `emailaddress1` | `personComponents.workEmail.address` |  |
| `firstname` | `person.name.firstName` |  |
| `fullname` | `person.name.fullName` |  |
| `lastname` | `person.name.lastName` |  |
| `jobtitle` | `extendedWorkDetails.jobTitle` |  |
| `middlename` | `person.name.middleName` |  |
| `mobilephone` | `mobilePhone.number` |  |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `salutation` | `person.name.courtesyTitle` |  |
| `telephone1` | `workPhone.number` |  |

{style="table-layout:auto"}

## Prospects {#leads}

| Champ source | Champ XDM cible | Remarques |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |  |
| `address1_city` | `workAddress.city` |  |
| `address1_country` | `workAddress.country` |  |
| `address1_county` | `workAddress.stateProvince` |  |
| `address1_latitude` | `workAddress._schema.latitude` |  |
| `address1_line1` | `workAddress.street1` |  |
| `address1_line2` | `workAddress.street2` |  |
| `address1_line3` | `workAddress.street3` |  |
| `address1_longitude` | `workAddress._schema.longitude` |  |
| `address1_postalcode` | `workAddress.postalCode` |  |
| `address1_postofficebox` | `workAddress.postOfficeBox` |  |
| `address1_stateorprovince` | `workAddress.state` |  |
| `telephone1` | `workPhone.number` |  |
| `mobilephone` | `mobilePhone.number` |  |
| `createdon` | `extSourceSystemAudit.createdDate` |  |
| `emailaddress1` | `workEmail.address` | identifiant Secondaire |
| `emailaddress2` | `personalEmail.address` |  |
| `emailaddress1` | `personComponents.workEmail.address` |  |
| `fax` | `faxPhone.number` |  |
| `firstname` | `person.name.firstName` |  |
| `fullname` | `person.name.fullName` |  |
| `jobtitle` | `extendedWorkDetails.jobTitle` |  |
| `lastname` | `person.name.lastName` |  |
| `"Dynamics"` | `b2b.personKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `leadid` | `b2b.personKey.sourceID` |  |
| `concat(leadid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | Identité principale. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `iif(leadid != null && leadid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", leadid, "sourceKey", concat(leadid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |  |
| `middlename` | `person.name.middleName` |  |
| `mobilephone` | `mobilePhone.number` |  |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `salutation` | `person.name.courtesyTitle` |  |

{style="table-layout:auto"}

## Comptes {#accounts}

| Champ source | Champ XDM cible | Notes |
| --- | --- | --- |
| `"Dynamics"` | `accountKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `accountKey.sourceInstanceID` | La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `accountid` | `accountKey.sourceID` | Identité principale. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `accountnumber` | `accountNumber` |  |
| `accountratingcode` | `accountOrganization.rating` |  |
| `address1_addressid` | `accountPhysicalAddress._id` |  |
| `address1_city` | `accountPhysicalAddress.city` |  |
| `address1_country` | `accountPhysicalAddress.country` |  |
| `address1_county` | `accountPhysicalAddress.region` |  |
| `address1_latitude` | `accountPhysicalAddress._schema.latitude` |  |
| `address1_line1` | `accountPhysicalAddress.street1` |  |
| `address1_line2` | `accountPhysicalAddress.street2` |  |
| `address1_line3` | `accountPhysicalAddress.street3` |  |
| `address1_longitude` | `accountPhysicalAddress._schema.longitude` |  |
| `address1_name` | `accountPhysicalAddress.label` |  |
| `address1_postalcode` | `accountPhysicalAddress.postalCode` |  |
| `address1_postofficebox` | `accountPhysicalAddress.postOfficeBox` |  |
| `address1_stateorprovince` | `accountPhysicalAddress.state` |  |
| `createdon` | `extSourceSystemAudit.createdDate` |  |
| `description` | `accountDescription` |  |
| `fax` | `accountFax.number` |  |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `name` | `accountName` |  |
| `numberofemployees` | `accountOrganization.numberOfEmployees` |  |
| `revenue` | `accountOrganization.annualRevenue.amount` |  |
| `sic` | `accountOrganization.SICCode` |  |
| `telephone1` | `accountPhone.number` |  |
| `tickersymbol` | `accountOrganization.tickerSymbol` |  |
| `websiteurl` | `accountOrganization.website` |  |
| `concat(accountid,"@${CRM_ORG_ID}.Dynamics")` | `accountKey.sourceKey` |  |

{style="table-layout:auto"}

## Opportunités {#opportunities}

| Champ source | Champ XDM cible | Notes |
| --- | --- | --- |
| `name` | `opportunityName` |  |
| `"Dynamics"` | `opportunityKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` | La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `iif(parentaccountid != null && parentaccountid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", parentaccountid, "sourceKey", concat(parentaccountid, "@${CRM_ORG_ID}.Dynamics")), null)` | `accountKey` |  |
| `actualclosedate` | `actualCloseDate` |  |
| `actualvalue` | `opportunityAmount.amount` |  |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `campaignKey` |  |
| `closeprobability` | `probabilityPercentage` |  |
| `createdon` | `extSourceSystemAudit.createdDate` |  |
| `description` | `opportunityDescription` |  |
| `estimatedclosedate` | `expectedCloseDate` |  |
| `estimatedvalue` | `expectedRevenue.amount` |  |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `opportunityid` | `opportunityKey.sourceID` |  |
| `concat(opportunityid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityKey.sourceKey` | Identité principale. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `salesstage` | `opportunityStage` |  |
| `stepname` | `nextStep` |  |

{style="table-layout:auto"}

## Rôles de contact d’opportunité {#opportunity-contact-roles}

| Champ source | Champ XDM cible | Notes |
| --- | --- | --- |
| `"Dynamics"` | `opportunityPersonKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `opportunityPersonKey.sourceInstanceID` | La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `connectionid` | `opportunityPersonKey.sourceID` |  |
| `concat(connectionid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityPersonKey.sourceKey` | Identité principale. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `createdon` | `extSourceSystemAudit.createdDate` |  |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `iif(record1id != null && record1id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record1id, "sourceKey", concat(record1id,"@${CRM_ORG_ID}.Dynamics")), null)` | `opportunityKey` |  |
| `iif(record2id != null && record2id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record2id, "sourceKey", concat(record2id,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |  |
| `connectionrole1.name` | `personRole` |  |
| `record1objecttypecode` | *Un groupe de champs personnalisé doit être défini en tant que schéma cible.* Pour plus d’informations, consultez la section annexe pour savoir comment [mapper un champ source de type liste de sélection à un schéma XDM cible](#picklist-type-fields). | Pour obtenir la liste des valeurs et des libellés possibles pour le champ source de `record1objecttypecode`, consultez ce [[!DNL Microsoft Dynamics] document de référence des entités de connexion](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record1objecttypecode-options). |
| `record2objecttypecode` | *Un groupe de champs personnalisé doit être défini en tant que schéma cible.* Pour plus d’informations, consultez la section annexe pour savoir comment [mapper un champ source de type liste de sélection à un schéma XDM cible](#picklist-type-fields). | Pour obtenir la liste des valeurs et des libellés possibles pour le champ source de `record2objecttypecode`, consultez ce [[!DNL Microsoft Dynamics] document de référence des entités de connexion](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record2objecttypecode-options). |

{style="table-layout:auto"}

## Campagnes {#campaigns}

| Champ source | Champ XDM cible | Notes |
| --- | --- | --- |
| `campaignid` | `campaignKey.sourceID` |  |
| `"${CRM_ORG_ID}"` | `campaignKey.sourceInstanceID` | La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `concat(campaignid,"@${CRM_ORG_ID}.Dynamics")` | `campaignKey.sourceKey` | Identité principale. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `"Dynamics"` | `campaignKey.sourceType` |  |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `extSourceSystemAudit.externalKey` | Le champ `extSourceSystemAudit.externalKey` est l’identité secondaire. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `createdon` | `extSourceSystemAudit.createdDate` |  |
| `modifiedby` | `extSourceSystemAudit.lastUpdatedBy` |  |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `description` | `campaignDescription` |  |
| `name` | `campaignName` |  |
| `totalactualcost` | `actualCost.amount` |  |
| `budgetedcost` | `budgetedCost.amount` |  |
| `expectedrevenue` | `expectedRevenue.amount` |  |
| `actualend` | `campaignEndDate` |  |
| `actualstart` | `campaignStartDate` |  |
| `expectedresponse` | `expectedResponse` |  |
| `utcconversiontimezonecode` | `timeZone` |  |
| `utcconversiontimezonecode` | `timezoneName` |  |

{style="table-layout:auto"}

## Liste marketing {#marketing-list}

| Champ source | Champ XDM cible | Notes |
| --- | --- | --- |
| `"Dynamics"` | `marketingListKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `marketingListKey.sourceInstanceID` | La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `description` | `marketingListDescription` |  |
| `listname` | `marketingListName` |  |
| `listid` | `marketingListKey.sourceID` |  |
| `concat(listid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListKey.sourceKey` | Identité principale. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `createdon` | `extSourceSystemAudit.createdDate` |  |

{style="table-layout:auto"}

## Personnes membres de la liste marketing {#marketing-list-members}

| Champ source | Champ XDM cible | Notes |
| --- | --- | --- |
| `"Dynamics"` | `marketingListMemberKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `marketingListMemberKey.sourceInstanceID` | La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `iif(entityid != null && entityid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", entityid, "sourceKey", concat(entityid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |
| `listmemberid` | `marketingListMemberKey.sourceID` |  |
| `concat(listmemberid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListMemberKey.sourceKey` | Identité principale. La valeur de `"${CRM_ORG_ID}"` sera automatiquement remplacée. |
| `iif(listid != null && listid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", listid, "sourceKey", concat(listid,"@${CRM_ORG_ID}.Dynamics")), null)` | `marketingListKey` |  |
| `createdon` | `extSourceSystemAudit.createdDate` |  |

{style="table-layout:auto"}

## Annexe

Les sections ci-dessous fournissent des informations supplémentaires que vous pouvez utiliser lors de la configuration des mappages B2B pour votre source [!DNL Microsoft] Dynamics.

### Champs de type Liste à sélection {#picklist-type-fields}

Vous pouvez utiliser des [champs calculés](../../../../data-prep/ui/mapping.md#calculated-fields) pour mapper un champ source de type liste de sélection de [!DNL Microsoft Dynamics] à un champ XDM cible.

Par exemple, le champ `genderCode` comprend deux options :

| Valeur | Libellé |
| --- | --- |
| 1 | `male` |
| 2 | `female` |

Vous pouvez utiliser les options suivantes pour mapper le champ source `genderCode` à `person.gender` champ cible :

#### Utiliser un opérateur logique

| Champ source | Champ XDM cible |
| --- | --- |
| `decode(genderCode, "1", "male", "2", "female", "default")` | `person.gender` |

Dans ce scénario, la valeur correspond à la clé, si celle-ci se trouve dans les options, ou `default`, si `default` est présente et que la clé est introuvable. La valeur correspond à `null` si les options sont `null` ou s’il n’existe aucune `default` et que la clé est introuvable.

#### Utiliser un champ calculé

| Champ source | Champ XDM cible |
| --- | --- |
| `iif(gendercode.equals("1"),"male",iif(gendercode.equals("2"),"female",null))` | `person.gender` |

>[!TIP]
>
>Une itération imbriquée de l’opération ci-dessus serait similaire à : `iif(condition, iif(cond1, tv1, fv1), iif(cond2, tv2, fv2))`.

Pour plus d’informations, consultez le document [ sur les opérateurs logiques dans  [!DNL Data Prep]](../../../../data-prep/functions.md##logical-operators)
