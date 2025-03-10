---
title: Type de données du canal
description: Découvrez le type de données Modèle de données d’expérience de publication (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 56eda38b-a7f7-40da-af08-73cfe9db0c7e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 6%

---

# Type de données [!UICONTROL Dosage]

[!UICONTROL Dosage] est un type de données standard du modèle de données d’expérience (XDM) qui décrit comment le médicament est/a été pris ou doit être pris. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données du canal](../../../images/healthcare/data-types/dosage/dosage.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Instructions supplémentaires] | `additionalInstruction` | Tableau de [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Instructions ou avertissements supplémentaires pour le patient. |
| [!UICONTROL Selon Les Besoins Pour] | `asNeededFor` | Tableau de [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Décrit le problème pour lequel les médicaments doivent être pris en fonction des besoins. |
| [!UICONTROL Dose Et Taux] | `doseAndRate` | Tableau d’objets | La quantité de médicaments administrés, à administrer ou la quantité typique à administrer. Pour plus d’informations, consultez la [section ci-dessous](#dose-and-rate) . |
| [!UICONTROL Nombre max. de points par administration] | `maxDosePerAdministration` | [[!UICONTROL Quantité simple]](../data-types/simple-quantity.md) | La limite supérieure des médicaments par administration. |
| [!UICONTROL Dose max. par durée de vie] | `maxDosePerLifetime` | [[!UICONTROL Quantité simple]](../data-types/simple-quantity.md) | La limite supérieure des médicaments par vie du patient. |
| [!UICONTROL Dose max. par période] | `maxDosePerPeriod` | Tableau de [[!UICONTROL Ratio]](../data-types/ratio.md) | La limite supérieure du traitement par unité de temps. |
| [!UICONTROL Méthode] | `method` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | La technique pour administrer les médicaments. |
| [!UICONTROL Route] | `route` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Comment le médicament doit entrer dans le corps. |
| [!UICONTROL Body Site] | `site` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Le site du corps pour administrer le médicament. |
| [!UICONTROL Minutage] | `timing` | [[!UICONTROL Minutage]](../data-types/timing.md) | Quand les médicaments devraient être administrés. |
| [!UICONTROL Selon Les Besoins] | `asNeeded` | Booléen | Indicateur pour savoir si le médicament doit être pris selon les besoins. |
| [!UICONTROL Instructions sur le patient] | `patientInstruction` | Chaîne | Les instructions en termes d&#39;être compris par le patient ou le consommateur. |
| [!UICONTROL Séquence] | `Integer` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | L’ordre des instructions de dosage. |
| [!UICONTROL Texte] | `text` | Chaîne | Planifiez les instructions de dosage du texte. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.schema.json)

## `doseAndRate` {#dose-and-rate}

`doseAndRate` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![dose et structure de taux](../../../images/healthcare/data-types/dosage/dose-and-rate.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Dose Quantity] | `doseQuantity` | [[!UICONTROL Quantité simple]](../data-types/simple-quantity.md) | La quantité de médicaments par dose. |
| [!UICONTROL Dose Range] | `doseRange` | [[!UICONTROL Plage]](../data-types/range.md) | La quantité de médicaments par dose. |
| [!UICONTROL Quantité de taux] | `rateQuantity` | [[!UICONTROL Quantité simple]](../data-types/simple-quantity.md) | La quantité de médicaments par unité de temps. |
| [!UICONTROL Plage de taux] | `rateRange` | [[!UICONTROL Plage]](../data-types/range.md) | La quantité de médicaments par unité de temps. |
| [!UICONTROL Ratio de taux] | `rateRatio` | [[!UICONTROL Ratio]](../data-types/ratio.md) | La quantité de médicaments par unité de temps. |
| [!UICONTROL Type] | `type` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Le type de dose ou de taux spécifié. |
