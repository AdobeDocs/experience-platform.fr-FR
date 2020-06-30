---
keywords: Experience Platform;preview schema data;Data Science Workspace;popular topics
solution: Experience Platform
title: schémas de Prévisualisation et jeux de données
topic: Tutorial
translation-type: tm+mt
source-git-commit: 4b0f0dda97f044590f55eaf75a220f631f3313ee
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# schémas de Prévisualisation et jeux de données

Une fois le script d&#39;amorçage terminé, du didacticiel [Créer le schéma de vente au détail et le jeu de données](./create-retails-sales-dataset.md) . Les schémas de sortie et les jeux de données peuvent être affichés sur [!DNL Experience Platform]. Pour vue des schémas et des jeux de données, procédez comme suit :

1. Cliquez sur le lien **[!UICONTROL Schémas]** situé dans la colonne de navigation de gauche et recherchez le schéma d’entrée créé par le script d’amorçage. Le nom du schéma correspond à ce qui a été défini à `config.yaml` l’étape précédente. Vue les détails du schéma et sa composition en cliquant dessus.

   ![](../images/models-recipes/access-data/schema_overview.png)

2. Cliquez sur le lien **[!UICONTROL Datasets]** situé dans la colonne de navigation de gauche et ouvrez le jeu de données d&#39;entrée qui a été créé en cliquant sur le nom de la liste. Le nom du jeu de données correspond à ce qui a été défini à `config.yaml` l&#39;étape précédente.

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. Cliquez sur **[!UICONTROL Prévisualisation Dataset]** situé dans la prévisualisation supérieure droite d&#39;un sous-ensemble du jeu de données.

   ![](../images/models-recipes/access-data/preview_dataset.png)

## Étapes suivantes

Vous avez maintenant assimilé avec succès des données d’exemple Ventes au détail à [!DNL Experience Platform] l’aide du script d’amorçage fourni.

Pour continuer à travailler avec les données imbriquées :
- [Analyse de vos données à l&#39;aide de portables Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilisez les ordinateurs portables Jupyter dans [!DNL Data Science Workspace] pour accéder, explorer, visualiser et comprendre vos données.
- [compresser les fichiers source dans une recette ;](./package-source-files-recipe.md)
   - Suivez ce tutoriel pour apprendre à importer votre propre modèle dans [!DNL Data Science Workspace] en regroupant les fichiers source dans un fichier Recette important.