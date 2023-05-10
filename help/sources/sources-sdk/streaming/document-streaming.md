---
title: Document Your Source (SDK de diffusion)
description: La dernière étape avant que votre nouvelle source puisse être mise en ligne dans Adobe Experience Platform consiste à documenter votre nouvelle source.
hide: true
hidefromtoc: true
exl-id: 65ca7a4d-3e02-4f54-bf07-ea2c92b8dbf1
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---

# Documenter votre source (SDK de streaming)

La dernière étape avant de pouvoir définir votre nouvelle source en direct dans Adobe Experience Platform consiste à documenter votre nouvelle source.

Ce guide de documentation comprend :

* Un tutoriel que vous pouvez suivre pour créer une page de documentation pour votre nouvelle source ;
* un modèle de documentation à remplir pour votre nouvelle source ;
* [Instructions sur l’utilisation de Markdown pour la rédaction de documentation technique](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en);
* [Instructions sur la compréhension de la saveur Adobe Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions).

## Conditions préalables

Les éléments suivants sont requis pour pouvoir commencer à documenter votre nouvelle source :

* **Un compte utilisateur GitHub valide**: Si vous ne disposez pas d’un compte GitHub existant, vous devez en créer un via la variable [Page d’inscription GitHub](https://github.com/);
* **Accès à GitHub Desktop**: Vous devez utiliser la variable [Application de bureau GitHub](https://desktop.github.com/) afin de créer votre documentation source dans votre environnement local ;
* Votre intégration à Adobe doit être dans une phase de test avec votre source déployée dans un environnement d’évaluation de Platform.

## Instructions générales pour créer la documentation de votre source dans Platform

À un niveau élevé, pour créer de la documentation pour votre source, vous devez créer un branchement du référentiel de documentation de Platform et modifier le modèle de documentation fourni dans une nouvelle branche. Utilisez le modèle fourni par l’Adobe pour créer une page source et ouvrir une requête de tirage (PR) lorsque vous êtes prêt. Les instructions à suivre pour ce faire sont présentées ci-dessous, dans les étapes de création de votre page source.

## Modèle de documentation

Vous pouvez utiliser un champ prérempli [Modèle de documentation d’API](streaming-template-api.md) ou le [Modèle de documentation de l’interface utilisateur](streaming-template-ui.md) pour faciliter la création de la documentation pour votre source. Vous trouverez ci-dessous des instructions sur la manière de modifier le modèle et d’ouvrir une requête d’extraction. La documentation envoyée pour votre nouvelle source sera révisée et publiée par l’équipe de documentation d’Adobe.

Vous pouvez également télécharger les modèles de documentation ci-dessous :

* [Modèle de documentation d’API](../assets/streaming/streaming-template-api.zip)
* [Modèle de documentation de l’interface utilisateur](../assets/streaming/streaming-template-ui.zip)

## Créer une page source

Vous pouvez utiliser l’interface web GitHub ou votre environnement local pour créer de la documentation pour votre nouvelle source dans Platform. Recherchez des instructions pour les deux options dans les liens ci-dessous :

* [Utilisation de l’interface web GitHub pour créer une page de documentation source](../documentation/github.md)
* [Utilisation d’un éditeur de texte dans votre environnement local pour créer une page de documentation source](../documentation/text-editor.md)
