---
title: Groupe de champs de schéma des médicaments de santé
description: Découvrez le groupe de champs Schéma des médicaments pour les soins de santé .
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
TQID: https://experienceleague.adobe.com/u3yvWq3IDCt5sqCD2xGMtagNhm9wFVE5HhB35PUf9TE
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 208
ht-degree: 12%

---

# [!UICONTROL Médicaments pour la santé] groupe de champs de schéma

[!UICONTROL Médicaments] est un groupe de champs de schéma standard pour la classe [[!UICONTROL Médicaments]](../../classes/medication.md). Il fournit un `medication` de champ de type objet unique qui recueille les informations telles que le nom de la marque, le numéro de lot et la quantité.

![](../../images/field-groups/healthcare-medication.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `ingredients` | Tableau d’objets | Dresse la liste des ingrédients présents dans le médicament. Chaque objet comprend les propriétés suivantes : <ul><li>`isActive` : (booléen) Indique si cet ingrédient est encore utilisé activement dans ce médicament.</li><li>`name` : (chaîne). Nom de l’ingrédient.</li><li>`quantity` : (Chaîne) La quantité de l&#39;ingrédient présent dans le médicament.</li></ul> |
| `brandName` | Chaîne | Nom de marque du médicament. |
| `codes` | Tableau de chaînes | Une liste de codes qui identifient ce médicament. |
| `dosageUnitNumber` | Double | Numéro d’unité de dosage du médicament. |
| `dosageUnitOfMeasurement` | Chaîne | Unité de mesure du nombre de doses. |
| `expiryDate` | DateTime | Date de péremption du médicament. |
| `genericName` | Chaîne | Nom générique du médicament. |
| `lotNumber` | Chaîne | Identifiant unique du lot du médicament. |
| `manufacturerName` | Chaîne | Le nom du fabricant du médicament. |
| `quantity` | Double | La quantité de médicament dans l’emballage. |
| `status` | Chaîne | État général indiquant si le médicament est actif ou non. |
| `volume` | Double | Le volume du médicament. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
