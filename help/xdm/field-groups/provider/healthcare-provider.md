---
title: Groupe de champs du schéma du fournisseur de soins de santé
description: Découvrez le groupe de champs du schéma Fournisseur de soins de santé .
exl-id: e39b4082-4b66-47b3-a8e2-951d8a96f742
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 3%

---

# Groupe de champs de schéma [!UICONTROL Fournisseur de soins de santé]

[!UICONTROL Healthcare Provider] est un groupe de champs de schéma standard pour la [[!UICONTROL classe Provider]](../../classes/provider.md). Il fournit un champ de type objet unique `healthcareProvider` qui capture les propriétés liées à un professionnel de la santé individuel ou à une organisation d’établissements de santé autorisée à fournir des services de diagnostic et de traitement de santé.

![](../../images/field-groups/healthcare-provider.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `addressDetails` | Tableau d’objets | Répertorie les détails de l’adresse du fournisseur. Chaque objet comprend les propriétés suivantes : <ul><li>`address` : ([[!UICONTROL Adresse postale]](../../data-types/postal-address.md)) : adresse postale du fournisseur.</li><li>`addressType` : (chaîne). Type d’adresse, indiquant où le fournisseur fournit des services.</li></ul> |
| `emailAddress` | [[!UICONTROL Adresse électronique]](../../data-types/email-address.md) | Adresse électronique du fournisseur. |
| `fax` | [[!UICONTROL Numéro de téléphone]](../../data-types/phone-number.md) | Numéro de fax du fournisseur. |
| `phoneNumber` | [[!UICONTROL Numéro de téléphone]](../../data-types/phone-number.md) | Numéro de téléphone du fournisseur. |
| `qualifications` | Tableau d’objets | Répertorie les certifications, les licences ou la formation relatives à la prestation de soins. Chaque objet comprend les propriétés suivantes : <ul><li>`issuer` : ([[!UICONTROL Détails du compte]](../../data-types/account-details.md)) : organisation qui réglemente et émet la qualification.</li><li>`activePeriod` : (entier) année jusqu’à laquelle la qualification est valide.</li><li>`code` : (chaîne). Représentation codée de la qualification.</li></ul> |
| `classification` | Chaîne | Classification du fournisseur de services en fonction de la classe ou de la catégorie (par exemple, soins aux patients, soins non patients, etc.). |
| `isActive` | Booléen | Indique si le fournisseur est actif. |
| `languages` | Tableau de chaînes | Liste des langues sous lesquelles le fournisseur effectue des opérations. |
| `practiceGroupName` | Chaîne | Nom du groupe d’exercices pour le fournisseur de services. |
| `practiceGroupType` | Chaîne | Type de groupe d’exercices pour le fournisseur de services. |
| `practiceType` | Chaîne | Type d’entraînement du prestataire. |
| `specialties` | Tableau de chaînes | Une liste de spécialités proposées par ce prestataire. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
