---
title: Documenter votre Source (Streaming SDK)
description: La dernière étape avant que votre nouvelle source puisse être mise en ligne dans Adobe Experience Platform consiste à documenter votre nouvelle source.
exl-id: 65ca7a4d-3e02-4f54-bf07-ea2c92b8dbf1
badge: Beta
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 2%

---

# Documenter votre source (SDK de streaming)

>[!NOTE]
>
>La diffusion en continu de SDK par les sources en libre-service est en version bêta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

La dernière étape avant que votre nouvelle source puisse être mise en ligne dans Adobe Experience Platform consiste à documenter votre nouvelle source.

Ce guide de documentation comprend :

* Tutoriel que vous pouvez suivre pour créer une page de documentation pour votre nouvelle source ;
* Un modèle de documentation à remplir pour votre nouvelle source ;
* [Instructions sur la façon d’utiliser Markdown pour rédiger la documentation technique](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=fr)
* [Instructions pour comprendre la version Adobe Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=fr#custom-markdown-extensions).

## Conditions préalables

Les éléments suivants sont requis avant de commencer à documenter votre nouvelle source :

* **Un compte utilisateur GitHub valide** : si vous ne disposez pas d’un compte GitHub existant, vous devez en créer un via la page d’inscription [GitHub](https://github.com/) ;
* **Accès à GitHub Desktop** : vous devez utiliser l’application [GitHub Desktop](https://desktop.github.com/) afin de créer votre documentation source dans votre environnement local ;
* Votre intégration à Adobe doit être en phase de test, avec votre source déployée dans un environnement d’évaluation dans Experience Platform.

## Instructions générales pour créer de la documentation pour votre source dans Experience Platform

À un niveau élevé, pour créer de la documentation pour votre source, vous devez créer un formulaire du référentiel de documentation Experience Platform et modifier le modèle de documentation fourni dans une nouvelle branche. Utilisez le modèle fourni par Adobe pour créer une page source et ouvrir une requête de tirage (PR) lorsque vous êtes prêt(e). Pour ce faire, reportez-vous aux instructions ci-dessous, dans la procédure de création de votre page source.

## Modèle de documentation

Vous pouvez utiliser un modèle de documentation [API](streaming-template-api.md) prérempli ou le modèle de documentation [UI](streaming-template-ui.md) pour créer de la documentation pour votre source. Plus bas, vous trouverez des instructions sur la modification du modèle et l’ouverture d’une requête d’extraction. La documentation envoyée pour votre nouvelle source sera examinée et publiée par l’équipe de documentation d’Adobe.

Vous pouvez également télécharger les modèles de documentation ci-dessous :

* [Modèle de documentation de l’API](../assets/streaming/streaming-template-api.zip)
* [Modèle de documentation de l’interface utilisateur](../assets/streaming/streaming-template-ui.zip)

## Créer votre page source

Vous pouvez utiliser l’interface web GitHub ou votre environnement local pour créer la documentation de votre nouvelle source dans Experience Platform. Recherchez des instructions pour les deux options dans les liens ci-dessous :

* [Utiliser l’interface web GitHub pour créer une page de documentation source](../documentation/github.md)
* [Utiliser un éditeur de texte dans votre environnement local pour créer une page de documentation source](../documentation/text-editor.md)
