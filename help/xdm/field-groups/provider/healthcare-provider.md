---
title: Groupe de champs du schéma du fournisseur de soins de santé
description: Ce document présente le groupe de champs Schéma du fournisseur de soins de santé.
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 10%

---

# [!UICONTROL Fournisseur de soins de santé] groupe de champs de schéma

[!UICONTROL Fournisseur de soins de santé] est un groupe de champs de schéma standard pour la variable [[!UICONTROL Fournisseur] class](../../classes/provider.md). Il fournit un champ de type objet unique. `healthcareProvider` qui capture les propriétés liées à un professionnel de la santé ou à un organisme d’établissements de santé autorisé à fournir des services de diagnostic et de traitement de santé.

![](../../images/field-groups/healthcare-provider.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `addressDetails` | Tableau d’objets | Répertorie les détails de l’adresse du fournisseur. Chaque objet comprend les propriétés suivantes : <ul><li>`address`: ([[!UICONTROL Adresse postale]](../../data-types/postal-address.md)) : Adresse postale du fournisseur.</li><li>`addressType`: (Chaîne) Type d’adresse, indiquant où le fournisseur fournit des services.</li></ul> |
| `emailAddress` | [[!UICONTROL Adresse e-mail]](../../data-types/email-address.md) | Adresse électronique du fournisseur. |
| `fax` | [[!UICONTROL Numéro de téléphone]](../../data-types/phone-number.md) | Numéro de fax du fournisseur. |
| `phoneNumber` | [[!UICONTROL Numéro de téléphone]](../../data-types/phone-number.md) | Numéro de téléphone du fournisseur. |
| `qualifications` | Tableau d’objets | Répertorie les certifications, les licences ou la formation relatives à la prestation de soins. Chaque objet comprend les propriétés suivantes : <ul><li>`issuer`: ([[!UICONTROL Détails du compte]](../../data-types/account-details.md)) : L’organisation qui réglemente et publie la qualification.</li><li>`activePeriod`: (Entier) Année jusqu’à laquelle la qualification est valide.</li><li>`code`: (Chaîne) Représentation codée de la qualification.</li></ul> |
| `classification` | Chaîne | Classification du fournisseur de services en fonction de la classe ou de la catégorie (par exemple, soins aux patients, soins non patients, etc.). |
| `isActive` | Booléen | Indique si le fournisseur est principal. |
| `languages` | Tableau de chaînes | Liste des langues sous lesquelles le fournisseur effectue des opérations. |
| `practiceGroupName` | Chaîne | Nom du groupe d’exercices pour le fournisseur de services. |
| `practiceGroupType` | Chaîne | Type de groupe d’exercices pour le prestataire. |
| `practiceType` | Chaîne | Type d’entraînement du prestataire. |
| `specialties` | Tableau de chaînes | Une liste de spécialités proposées par ce prestataire. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous à la section [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
