---
title: Groupe de champs du schéma de médication
description: Découvrez le groupe de champs Schéma de médicament .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: e1f53ff8-3079-4b2f-9e73-31a773907a63
TQID: https://experienceleague.adobe.com/bw0-AkUU8x2-ZyxZ7fLc2E4TZK3PGIfvcUwKPg-Rkts
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 309
ht-degree: 6%

---

# Groupe de champs de schéma [!UICONTROL Médicaments]

[!UICONTROL Médicaments] est un groupe de champs de schéma standard pour la [[!DNL Medication] classe](../../../classes/medication.md). Il fournit un `healthcareMedication` de champ de type objet unique qui capture les informations d’un médicament.

![Structure du groupe de champs](../../../images/healthcare/field-groups/medication/medication.png)

| Nom d’affichage | Propriété | Type de données | Description |
| ---|  --- | --- | --- |
| [!UICONTROL Lot] | `batch` | Objet | Détails sur un médicament emballé. Contient deux propriétés : <li>`lotNumber` : valeur de chaîne pour l’identifiant attribué au lot.</li> <li>`expirationDate` : valeur DateTime indiquant le moment d’expiration du lot.</li> |
| [!UICONTROL Code] | `code` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Le code qui identifie ce médicament. |
| [!UICONTROL Définition] | `definition` | [[!UICONTROL Référence]](../data-types/reference.md) | La définition du médicament. |
| [!UICONTROL Forme De Dose] | `doseForm` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Décrit la forme posologique du médicament, comme des comprimés ou des gélules. |
| [!UICONTROL Identifiant] | `identifier` | Tableau d’[[!UICONTROL identifiant]](../data-types/identifier.md) | Identifiant du médicament. |
| [!UICONTROL Ingrédient] | `ingredient` | Tableau d’objets | Décrit les informations sur les ingrédients du médicament. Pour plus d’informations, consultez la [section ci-dessous](#ingredient). |
| [!UICONTROL Titulaire De L’Autorisation De Mise Sur Le Marché] | `marketingAuthorizationHolder` | [[!UICONTROL Référence]](../data-types/reference.md) | L&#39;organisation qui a l&#39;autorisation de commercialiser le médicament. |
| [!UICONTROL Volume total] | `totalVolume` | [[!UICONTROL Quantité]](../data-types/quantity.md) | La quantité de produit fournie dans le médicament lorsque le code du produit ne déduit pas la taille de l’emballage. |
| [!UICONTROL Statut] | `status` | Chaîne | Le statut du médicament. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `active` </li> <li> `inactive` </li> <li> `entered-in-error` </li> |

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.schema.json)

## `ingredient` {#ingredient}

`ingredient` est fourni sous la forme d’un tableau d’objets . La structure de chaque objet est décrite ci-dessous.

![structure des ingrédients](../../../images/healthcare/field-groups/medication/ingredient.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Poste] | `item` | [[!UICONTROL Référence codable]](../data-types/codeable-reference.md) | L&#39;ingrédient décrit. |
| [!UICONTROL Concept codable de la force] | `strengthCodeableConcept` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Quantité de l’ingrédient présent, exprimée dans une terminologie définie par le système. |
| [!UICONTROL Quantité de résistance] | `strengthQuantity` | [[!UICONTROL Quantité]](../data-types/quantity.md) | Quantité de l’ingrédient présent. |
| [!UICONTROL Rapport de résistance] | `strengthRatio` | [[!UICONTROL Rapport]](../data-types/ratio.md) | Rapport de l’ingrédient présent. |
| [!UICONTROL Est actif] | `isActive` | Booléen | Indique si l&#39;ingrédient est actif. |
