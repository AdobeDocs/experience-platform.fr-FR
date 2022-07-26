---
title: Groupe de champs du schéma des médicaments pour le secteur de la santé
description: Ce document présente un aperçu du groupe de champs Schéma des médicaments pour les soins de santé .
source-git-commit: 3b0c85eb5184dd116b1013e617cf528080fa0656
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 12%

---

# [!UICONTROL Médicaments de santé] groupe de champs de schéma

[!UICONTROL Médicaments de santé] est un groupe de champs de schéma standard pour la variable [[!UICONTROL Médicaments] class](../../classes/medication.md). Il fournit un champ de type objet unique. `medication` qui capture des détails tels que le nom de la marque, le numéro de lot et la quantité.

![](../../images/field-groups/healthcare-medication.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `ingredients` | Tableau d’objets | Répertorie les ingrédients présents dans le médicament. Chaque objet comprend les propriétés suivantes : <ul><li>`isActive`: (booléen) Indique si cet ingrédient est toujours activement utilisé dans ce médicament.</li><li>`name`: (Chaîne) Nom de l’ingrédient.</li><li>`quantity`: (Chaîne) La quantité de l’ingrédient présent dans le médicament.</li></ul> |
| `brandName` | Chaîne | Nom de la marque du médicament. |
| `codes` | Tableau de chaînes | Une liste de codes qui identifient ce médicament. |
| `dosageUnitNumber` | Double | Numéro de l’unité de dosage du médicament. |
| `dosageUnitOfMeasurement` | Chaîne | Unité de mesure du nombre de doses. |
| `expiryDate` | DateTime | Date d’expiration du traitement. |
| `genericName` | Chaîne | Nom générique du médicament. |
| `lotNumber` | Chaîne | Identifiant unique du lot du médicament. |
| `manufacturerName` | Chaîne | Nom du fabricant du médicament. |
| `quantity` | Double | La quantité de médicament dans le paquet. |
| `status` | Chaîne | Un état général indiquant si le médicament ou le médicament est principal ou non. |
| `volume` | Double | Le volume du médicament. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous à la section [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
