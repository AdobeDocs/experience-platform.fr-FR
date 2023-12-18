---
title: Type de données de catégorie
description: Découvrez le type de données du modèle de données d’expérience (XDM) de données de catégorie.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 9%

---

# [!UICONTROL Données de catégorie] type de données

[!UICONTROL Données de catégorie] est un type de données XDM (Experience Data Model) standard qui décrit les informations liées à la catégorie d’un produit.

![Diagramme du type de données Catégorie .](../images/data-types/category-data.png)

| Nom d’affichage | Propriété | Type de données | Description |
|-----------------|--------------------|-----------|------------------------------------------|
| [!UICONTROL Identifiant de catégorie] | `categoryID` | chaîne | Identifiant de la catégorie du produit. |
| [!UICONTROL Nom de catégorie] | `categoryName` | chaîne | Nom de la catégorie du produit. |
| [!UICONTROL Chemin de la catégorie] | `categoryPath` | chaîne | Chemin d’accès de la catégorie du produit. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/categorydata.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/categorydata.schema.json)
