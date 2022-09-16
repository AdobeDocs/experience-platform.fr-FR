---
keywords: Experience Platform;prévisualiser les données de schéma;Data Science Workspace;rubriques les plus consultées
solution: Experience Platform
title: Aperçu du schéma et du jeu de données de ventes au détail
topic-legacy: tutorial
type: Tutorial
description: Le document suivant décrit la prévisualisation des schémas et des jeux de données sur Adobe Experience Platform.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 25%

---

# Aperçu du schéma et du jeu de données des ventes au détail

Une fois le script de bootstrap du fichier [jeu de données et schéma de ventes au détail](./create-retails-sales-dataset.md) tutoriel . Vous pouvez afficher les schémas et les jeux de données de sortie sur [!DNL Experience Platform]. Pour afficher les schémas et les jeux de données, suivez les étapes ci-dessous :

Sélectionnez la **[!UICONTROL Schémas]** dans le volet de navigation de gauche et recherchez le schéma d’entrée créé par le script bootstrap. Le nom du schéma correspondra à ce qui a été défini dans `config.yaml` à l’étape précédente. Affichez les détails du schéma et sa composition en cliquant dessus.

![](../images/models-recipes/access-data/schema.PNG)

Sélectionnez la **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche, puis ouvrez le jeu de données d’entrée qui a été créé en sélectionnant le nom du jeu de données. Le nom du jeu de données correspond à ce qui a été défini dans `config.yaml` de l’étape précédente.

![](../images/models-recipes/access-data/dataset.PNG)

Sélectionner **[!UICONTROL Aperçu du jeu de données]** situé en haut à droite pour prévisualiser un sous-ensemble du jeu de données.

![](../images/models-recipes/access-data/preview.PNG)

## Étapes suivantes

Vous avez maintenant ingéré avec succès des données d’exemple de ventes au détail dans [!DNL Experience Platform] à l’aide du script de bootstrap fourni.

Pour continuer à travailler sur les données ingérées, procédez de la façon suivante :
- [Analyse de vos données à l’aide des notebooks Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilisation des notebooks Jupyter dans [!DNL Data Science Workspace] pour accéder à vos données, les explorer, les visualiser et les comprendre.
- [Regroupez les fichiers source dans une recette](./package-source-files-recipe.md)
   - Suivez ce tutoriel pour apprendre à importer votre propre modèle dans [!DNL Data Science Workspace] en regroupant les fichiers source dans un fichier Recette pouvant être importé.
