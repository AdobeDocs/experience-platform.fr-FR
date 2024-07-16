---
keywords: Experience Platform;données web luma;Data Science Workspace;rubriques les plus consultées;recettes;données de démonstration;données web de démonstration;données luma
solution: Experience Platform
title: Création de jeux de données et de schémas web Luma
type: Tutorial
description: Ce tutoriel vous fournit les prérequis et les ressources requis pour le modèle de propension aux démonstrations Luma.
exl-id: a791e532-1116-4407-b745-fd6c2ac0d8f7
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# Création de schémas et de jeux de données de modèle de propension Luma

Ce tutoriel vous fournit les prérequis et les ressources requis pour tous les autres tutoriels [!DNL Adobe Experience Platform] [!DNL Data Science Workspace]. Une fois l’opération terminée, vous et votre organisation aurez accès aux schémas et jeux de données suivants.

**Schémas :**

- Schéma de données web Luma
- Schéma des résultats de la notation du modèle de propension

**Jeux de données :**

- Jeu de données web Luma
- Jeu de données de formation du modèle de propension
- Jeu de données de notation du modèle de propension
- Jeu de données de notation des modèles de propension

## Téléchargement des ressources {#assets}

Le tutoriel suivant utilise un modèle personnalisé de propension à l’achat de Luma. Avant de poursuivre, [téléchargez le dossier compressé de ressources](https://experienceleague.adobe.com/docs/platform-learn/assets/DSW-course-sample-assets.zip) requis. Ce dossier contient :

- notebook de modèle de propension à l’achat
- notebook utilisé pour ingérer des données dans un jeu de données de formation et de notation (un sous-ensemble des données web Luma).
- Fichier de démonstration JSON contenant les données web de 730 000 utilisateurs Luma
- Notebook facultatif Python 3 EDA (analyse de données exploratoire) qui peut être utilisé pour aider à comprendre les données web et le modèle.

>[!NOTE]
>
> Vous pouvez utiliser votre propre schéma et vos propres données pour n’importe quel tutoriel. Cependant, le modèle de démonstration fourni dans les ressources ne fonctionne pas à moins qu’il ne fournisse les fichiers de configuration et le fichier d’exigences appropriés. Ce modèle de propension aux démonstrations a été conçu pour fonctionner avec les données web de Luma.

### Créer le schéma de données web Luma et ingérer les données

Pour créer un modèle, vous devez disposer d’un jeu de données dans Platform qui est utilisé pour entraîner et noter votre modèle. Le tutoriel vidéo suivant du [cours Data Science Workspace](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2021.1.dsw&amp;lang=fr) vous guide tout au long de la création du schéma Luma et de l’ingestion des données utilisées par le modèle de propension à l’achat.

>[!VIDEO](https://video.tv.adobe.com/v/333312)

### Création des jeux de données de formation, de notation et de notation

Pour exécuter le notebook du créateur de recettes ou utiliser l’API pour former et noter un modèle, vous devez spécifier le ou les jeux de données et le ou les schémas utilisés pour la formation/notation. Le tutoriel vidéo suivant vous guide tout au long des étapes nécessaires pour configurer les jeux de données de formation, de notation et de notation, ainsi que le schéma de résultats de notation utilisé dans le modèle de propension à l’achat de Luma.

>[!VIDEO](https://video.tv.adobe.com/v/333426)

## Étapes suivantes

En suivant ce tutoriel, vous avez créé avec succès les schémas et les jeux de données requis pour le modèle de propension Luma. Vous êtes maintenant prêt à passer au tutoriel suivant et à créer le modèle à l’aide du tutoriel [notebook de créateur de recettes](../jupyterlab/create-a-model.md).

De plus, vous pouvez explorer les données à l’aide du notebook d’analyse des données exploratoires (EDA) fourni. Ce notebook peut être utilisé pour aider à comprendre les modèles dans les données Luma, vérifier l’intégrité des données et résumer les données pertinentes pour le modèle de propension prédictive. Pour en savoir plus sur l’analyse des données exploratoires, consultez la [documentation EDA](../jupyterlab/eda-notebook.md).
