---
title: Groupe de champs du schéma des médicaments pour le secteur de la santé
description: Découvrez le groupe de champs Schéma des médicaments pour les soins de santé .
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 7%

---

# Groupe de champs [!UICONTROL Médicaments de santé] du schéma

[!UICONTROL Healthcare médication] est un groupe de champs de schéma standard pour la [[!UICONTROL classe Medication]](../../classes/medication.md). Il fournit un champ de type objet unique `medication` qui capture des détails tels que le nom de la marque, le numéro de lot et la quantité.

![](../../images/field-groups/healthcare-medication.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `ingredients` | Tableau d’objets | Répertorie les ingrédients présents dans le médicament. Chaque objet comprend les propriétés suivantes : <ul><li>`isActive` : (booléen). Indique si cet ingrédient est toujours activement utilisé dans ce médicament.</li><li>`name` : (chaîne). Nom de l’ingrédient.</li><li>`quantity` : (chaîne). La quantité de l’ingrédient présent dans le médicament.</li></ul> |
| `brandName` | Chaîne | Nom de la marque du médicament. |
| `codes` | Tableau de chaînes | Une liste de codes qui identifient ce médicament. |
| `dosageUnitNumber` | Double | Numéro de l’unité de dosage du médicament. |
| `dosageUnitOfMeasurement` | Chaîne | Unité de mesure du nombre de doses. |
| `expiryDate` | DateTime | Date d’expiration du traitement. |
| `genericName` | Chaîne | Nom générique du médicament. |
| `lotNumber` | Chaîne | Identifiant unique du lot du médicament. |
| `manufacturerName` | Chaîne | Nom du fabricant du médicament. |
| `quantity` | Double | La quantité de médicament dans le paquet. |
| `status` | Chaîne | État général indiquant si le médicament ou le médicament est actif ou non. |
| `volume` | Double | Le volume du médicament. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
