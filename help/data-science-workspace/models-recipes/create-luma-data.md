---
keywords: Experience Platform;données web luma;Workspace de science des données;rubriques populaires;recettes;données de démonstration;données web de démonstration;données luma
solution: Experience Platform
title: Créer des schémas web et des jeux de données Luma
type: Tutorial
description: Ce tutoriel vous présente les prérequis et les ressources nécessaires au modèle de propension de démonstration de Luma.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: 219305a71c70a5bbec2fad591c166761e3aaa9ee
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# Créer des schémas et des jeux de données de modèle de propension Luma

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

Ce tutoriel vous présente les prérequis et les ressources nécessaires à tous les autres tutoriels [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] . Une fois l’opération terminée, les schémas et jeux de données suivants seront disponibles pour vous et votre organisation.

**Schémas:**

- Schéma de données web Luma
- Schéma des résultats du score du modèle de propension

**Jeux de données:**

- Jeu de données web Luma
- Jeu de données d’entraînement du modèle de propension
- Jeu de données de score du modèle de propension
- Jeu de données de résultats de score du modèle de propension

## Téléchargement des ressources {#assets}

Le tutoriel suivant utilise un modèle personnalisé de propension à l’achat de Luma . Avant de poursuivre, [téléchargez les ressources requises](../assets/DSW-course-sample-assets.7z) le dossier zip. Ce dossier contient les éléments suivants :

- Le notebook de modèle de propension à l’achat
- Un notebook utilisé pour ingérer des données dans un jeu de données d’entraînement et de notation (un sous-ensemble des données web de Luma)
- Un fichier JSON de démonstration contenant les données web de 730 000 utilisateurs de Luma.
- Un notebook Python 3 EDA (analyse exploratoire des données) facultatif qui peut être utilisé pour aider à comprendre les données et le modèle web.

>[!NOTE]
>
> Vous pouvez utiliser votre propre schéma et vos propres données pour l’un des tutoriels. Cependant, le modèle de démonstration fourni dans les ressources ne fonctionne pas, sauf s’il est fourni avec les fichiers de configuration et de configuration requis appropriés. Ce modèle de propension de démonstration a été conçu pour fonctionner avec les données web de Luma.

### Créer le schéma de données web Luma et ingérer les données

Pour créer un modèle, vous devez disposer d’un jeu de données dans Experience Platform utilisé pour entraîner et noter votre modèle. Le tutoriel vidéo suivant du [cours Workspace de science des données](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw&lang=fr) vous guide tout au long de la création du schéma Luma et de l’ingestion des données utilisées par le modèle de propension à l’achat.

>[!VIDEO](https://video.tv.adobe.com/v/3447156?captions=fre_fr)

### Créez les jeux de données de résultats d’entraînement, de notation et de notation

Pour exécuter le notebook du créateur de recettes ou utiliser l’API pour entraîner et noter un modèle, vous devez spécifier le ou les jeux de données et le ou les schémas utilisés pour l’entraînement/la notation. Le tutoriel vidéo suivant vous guide tout au long de la configuration des jeux de données de résultats d’entraînement, de notation et de notation, ainsi que du schéma de résultats de notation utilisé dans le modèle de propension aux achats de Luma.

>[!VIDEO](https://video.tv.adobe.com/v/3447423?captions=fre_fr)

## Étapes suivantes

En suivant ce tutoriel, vous avez créé les schémas et les jeux de données requis pour le modèle de propension de Luma. Vous êtes maintenant prêt à passer au tutoriel suivant et à créer le modèle à l’aide du tutoriel [notebook du créateur de recettes](../jupyterlab/create-a-model.md).

De plus, vous pouvez explorer les données à l’aide du notebook d’analyse exploratoire des données (AED) fourni. Ce notebook peut être utilisé pour aider à comprendre les modèles dans les données Luma, vérifier l’intégrité des données et résumer les données pertinentes pour le modèle de propension prédictif. Pour en savoir plus sur l’analyse exploratoire des données, consultez la documentation [AED](../jupyterlab/eda-notebook.md).
