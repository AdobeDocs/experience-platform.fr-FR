---
keywords: Experience Platform ; données de schéma de prévisualisation ; Espace de travail des sciences de données ; sujets populaires
solution: Experience Platform
title: Prévisualisation du Schéma de vente au détail et du jeu de données
topic: tutorial
type: Tutorial
description: Le document suivant décrit la prévisualisation des schémas et des jeux de données sur Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 5129a75071af680bc54a7f60bb89ce32d3216d09
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 25%

---


# Prévisualisation du schéma de vente au détail et du jeu de données

Une fois le script d&#39;amorçage terminé, suivez le didacticiel [schéma de vente au détail et jeu de données](./create-retails-sales-dataset.md). Vous pouvez afficher les schémas et les jeux de données de sortie sur [!DNL Experience Platform]. Pour afficher les schémas et les jeux de données, suivez les étapes ci-dessous :

Sélectionnez l&#39;onglet **[!UICONTROL Schémas]** situé dans le volet de navigation de gauche et recherchez le schéma d&#39;entrée créé par le script d&#39;amorçage. Le nom du schéma correspondra à ce qui a été défini dans `config.yaml` à l’étape précédente. Affichez les détails du schéma et sa composition en cliquant dessus.

![](../images/models-recipes/access-data/schema.PNG)

Sélectionnez l&#39;onglet **[!UICONTROL Datasets]** situé dans le volet de navigation de gauche et ouvrez le jeu de données d&#39;entrée qui a été créé en sélectionnant le nom du jeu de données. Le nom du jeu de données correspond à ce qui a été défini dans `config.yaml` à l&#39;étape précédente.

![](../images/models-recipes/access-data/dataset.PNG)

Sélectionnez **[!UICONTROL Prévisualisation Dataset]** situé en haut à droite de la prévisualisation d&#39;un sous-ensemble du jeu de données.

![](../images/models-recipes/access-data/preview.PNG)

## Étapes suivantes

Vous avez maintenant saisi avec succès des données d&#39;exemple Ventes au détail dans [!DNL Experience Platform] à l&#39;aide du script d&#39;amorçage fourni.

Pour continuer à travailler sur les données ingérées, procédez de la façon suivante :
- [Analyse de vos données à l’aide des ordinateurs portables Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilisez les portables Jupyter dans [!DNL Data Science Workspace] pour accéder, explorer, visualiser et comprendre vos données.
- [Regroupez les fichiers source dans une recette](./package-source-files-recipe.md)
   - Suivez ce tutoriel pour apprendre à importer votre propre modèle dans [!DNL Data Science Workspace] en regroupant les fichiers source dans un fichier Recette important.