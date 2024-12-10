---
title: Groupe de champs du schéma de médicaments
description: Découvrez le groupe de champs Schéma de médicament .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e1f53ff8-3079-4b2f-9e73-31a773907a63
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 7%

---

# Groupe de champs de schéma [!UICONTROL Medication]

[!UICONTROL Medication] est un groupe de champs de schéma standard pour la [[!DNL Medication] classe](../../../classes/medication.md). Il fournit un seul champ de type objet `healthcareMedication` qui capture les informations d’un médicament.

![Structure de groupe de champs](../../../images/healthcare/field-groups/medication/medication.png)

| Nom d’affichage | Propriété | Type de données | Description |
| ---|  --- | --- | --- |
| [!UICONTROL Lot] | `batch` | Objet | Détails sur un médicament emballé. Contient deux propriétés : <li>`lotNumber` : valeur de chaîne de l’identifiant affecté au lot.</li> <li>`expirationDate` : valeur DateTime pour laquelle le lot arrivera à expiration.</li> |
| [!UICONTROL Code] | `code` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Le code qui identifie ce médicament. |
| [!UICONTROL Définition] | `definition` | [[!UICONTROL Référence]](../data-types/reference.md) | La définition du médicament. |
| [!UICONTROL Dose Form] | `doseForm` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Décrit la forme de la dose du médicament, comme les comprimés ou les capsules. |
| [!UICONTROL Identifiant] | `identifier` | Tableau de [[!UICONTROL Identifiant]](../data-types/identifier.md) | Identifiant du médicament. |
| [!UICONTROL Ingrédient] | `ingredient` | Tableau d’objets | Décrit les informations sur les ingrédients du médicament. Pour plus d’informations, consultez la [section ci-dessous](#ingredient) . |
| [!UICONTROL Holder d’autorisation marketing] | `marketingAuthorizationHolder` | [[!UICONTROL Référence]](../data-types/reference.md) | L’organisation qui a l’autorisation de commercialiser le médicament. |
| [!UICONTROL Volume total] | `totalVolume` | [[!UICONTROL Quantity]](../data-types/quantity.md) | La quantité de produit fournie dans le médicament lorsque le code de produit ne déduit pas la taille du paquet. |
| [!UICONTROL Statut] | `status` | Chaîne | Le statut du médicament. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `active` </li> <li> `inactive` </li> <li> `entered-in-error` </li> |

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.schema.json)

## `ingredient` {#ingredient}

`ingredient` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![structure d’ingrédient](../../../images/healthcare/field-groups/medication/ingredient.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Item] | `item` | [[!UICONTROL Référence codeable]](../data-types/codeable-reference.md) | L’ingrédient en cours de description. |
| [!UICONTROL Force Concept Codeable] | `strengthCodeableConcept` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | La quantité de l’ingrédient présent, exprimée dans une terminologie définie par le système. |
| [!UICONTROL Force Quantité] | `strengthQuantity` | [[!UICONTROL Quantity]](../data-types/quantity.md) | La quantité de l’ingrédient présent. |
| [!UICONTROL Ratio de force] | `strengthRatio` | [[!UICONTROL Ratio]](../data-types/ratio.md) | Le ratio de l’ingrédient présent. |
| [!UICONTROL Est Actif] | `isActive` | Booléen | Indique si l’ingrédient est actif. |
