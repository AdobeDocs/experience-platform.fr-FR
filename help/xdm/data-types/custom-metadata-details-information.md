---
title: Type de données Détails sur les métadonnées personnalisées
description: Découvrez le type de données XDM (Custom Metadata Details) Information Experience Data Model (XDM) .
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 11%

---

# [!UICONTROL Informations détaillées sur les métadonnées personnalisées] type de données

[!UICONTROL Informations détaillées sur les métadonnées personnalisées] est un type de données XDM (Experience Data Model) standard qui définit une structure pour le stockage de métadonnées personnalisées. Utilisez la variable [!UICONTROL Informations détaillées sur les métadonnées personnalisées] type de données pour capturer des détails tels que le nom et la valeur des métadonnées personnalisées associées au contenu ou aux interactions.

![Schéma du type de données Informations sur les métadonnées personnalisées .](../images/data-types/custom-metadata-details-information.png)

| Nom d’affichage | Propriété | Type de données | Description |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Nom du champ de métadonnées personnalisé] | `name` | chaîne | Nom du champ personnalisé. |
| [!UICONTROL Valeur du champ de métadonnées personnalisé] | `value` | chaîne | La valeur du champ personnalisé. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/custommetadatadetails.schema.json)
