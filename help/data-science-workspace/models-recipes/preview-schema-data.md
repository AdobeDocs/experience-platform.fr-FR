---
keywords: Experience Platform ; données de schéma de prévisualisation ; Espace de travail des sciences de données ; sujets populaires
solution: Experience Platform
title: Prévisualisation du Schéma de vente au détail et du jeu de données
topic: tutorial
type: Tutorial
description: Le document suivant décrit la prévisualisation des schémas et des jeux de données sur Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 62%

---


# Prévisualisation du schéma de vente au détail et du jeu de données

Une fois le script de bootstrap du tutoriel [Création du schéma et du jeu de données de ventes au détail](./create-retails-sales-dataset.md) terminé avec succès. Vous pouvez afficher les schémas et les jeux de données de sortie sur [!DNL Experience Platform]. Pour afficher les schémas et les jeux de données, suivez les étapes ci-dessous :

1. Cliquez sur le lien **[!UICONTROL Schémas]** situé dans la colonne de navigation de gauche et repérez le schéma d’entrée créé par le script de bootstrap. Le nom du schéma correspondra à ce qui a été défini dans `config.yaml` à l’étape précédente. Affichez les détails du schéma et sa composition en cliquant dessus.

   ![](../images/models-recipes/access-data/schema_overview.png)

2. Cliquez sur le lien **[!UICONTROL Jeux de données]** situé dans la colonne de navigation de gauche et ouvrez le jeu de données d’entrée créé en cliquant sur le nom de l’offre. Le nom du jeu de données correspondra à ce qui a été défini dans `config.yaml` à l’étape précédente.

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. Cliquer sur **[!UICONTROL Prévisualiser le jeu de données]** en haut à droite affiche un aperçu du sous-ensemble du jeu de données.

   ![](../images/models-recipes/access-data/preview_dataset.png)

## Étapes suivantes

Vous avez maintenant saisi avec succès des données d&#39;exemple Ventes au détail dans [!DNL Experience Platform] à l&#39;aide du script d&#39;amorçage fourni.

Pour continuer à travailler sur les données ingérées, procédez de la façon suivante :
- [Analyse de vos données à l’aide des ordinateurs portables Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilisez les portables Jupyter dans [!DNL Data Science Workspace] pour accéder, explorer, visualiser et comprendre vos données.
- [Regroupez les fichiers source dans une recette](./package-source-files-recipe.md)
   - Suivez ce tutoriel pour apprendre à importer votre propre modèle dans [!DNL Data Science Workspace] en regroupant les fichiers source dans un fichier Recette important.