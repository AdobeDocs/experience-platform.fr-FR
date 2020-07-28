---
keywords: Experience Platform;preview schema data;Data Science Workspace;popular topics
solution: Experience Platform
title: Prévisualisation des schémas et des jeux de données
topic: Tutorial
translation-type: tm+mt
source-git-commit: 4b0f0dda97f044590f55eaf75a220f631f3313ee
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 77%

---


# Prévisualisation des schémas et des jeux de données

Une fois le script de bootstrap du tutoriel [Création du schéma et du jeu de données de ventes au détail](./create-retails-sales-dataset.md) terminé avec succès. Vous pouvez afficher les schémas et les jeux de données de sortie sur [!DNL Experience Platform]. Pour afficher les schémas et les jeux de données, suivez les étapes ci-dessous :

1. Cliquez sur le lien **[!UICONTROL Schémas]** situé dans la colonne de navigation de gauche et repérez le schéma d’entrée créé par le script de bootstrap. Le nom du schéma correspondra à ce qui a été défini dans `config.yaml` à l’étape précédente. Affichez les détails du schéma et sa composition en cliquant dessus.

   ![](../images/models-recipes/access-data/schema_overview.png)

2. Cliquez sur le lien **[!UICONTROL Jeux de données]** situé dans la colonne de navigation de gauche et ouvrez le jeu de données d’entrée créé en cliquant sur le nom de l’offre. Le nom du jeu de données correspondra à ce qui a été défini dans `config.yaml` à l’étape précédente.

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. Cliquer sur **[!UICONTROL Prévisualiser le jeu de données]** en haut à droite affiche un aperçu du sous-ensemble du jeu de données.

   ![](../images/models-recipes/access-data/preview_dataset.png)

## Étapes suivantes

You have now successfully ingested Retail Sales sample data into [!DNL Experience Platform] using the provided bootstrap script.

Pour continuer à travailler sur les données ingérées, procédez de la façon suivante :
- [Analysez vos données à l’aide des notebooks Jupyter](../jupyterlab/analyze-your-data.md)
   - Use Jupyter notebooks in [!DNL Data Science Workspace] to access, explore, visualize, and understand your data.
- [Regroupez les fichiers source dans une recette](./package-source-files-recipe.md)
   - Follow this tutorial to learn how to bring your own Model into [!DNL Data Science Workspace] by packaging source files in an importable Recipe file.