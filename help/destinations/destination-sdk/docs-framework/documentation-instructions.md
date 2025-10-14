---
title: Documenter votre destination dans Adobe Experience Platform
description: Cette section contient des instructions détaillées pour créer une page de documentation pour votre destination dans Adobe Experience Platform.
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 8%

---

# Documenter votre destination dans Adobe Experience Platform

>[!IMPORTANT]
>
>Le processus documenté ici n’est nécessaire que pour les partenaires qui envoient des destinations productisées (publiques). Si vous créez une destination privée à des fins personnelles, il n’est pas nécessaire de créer et de publier de la documentation pour cette destination.

## Vue d’ensemble {#overview}

Bienvenue à Adobe Experience Platform, super de vous avoir ici !
La documentation de votre destination est la dernière étape avant qu’elle ne puisse être définie dans Adobe Experience Platform.

Cette section de documentation comprend :

* Cette section contient des instructions détaillées pour vous permettre de créer une page de documentation pour votre nouvelle destination.
* Un modèle à remplir pour votre destination ;
* [Instructions générales sur l’utilisation de Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=fr) ;
* [Instructions spécifiques pour la saveur Adobe Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=fr#custom-markdown-extensions) (la saveur Adobe Markdown est très similaire à Markdown standard).
* Une [&#x200B; page de bonnes pratiques](./authoring-best-practices.md) pour vous aider à créer une page de documentation pour votre page de destination, qui respecte les normes de qualité de la documentation Experience Platform.

## Conditions préalables {#prerequisites}

Pour créer la documentation de votre destination conformément aux instructions de cet article, les éléments suivants sont nécessaires :

* **Compte GitHub**. Inscrivez-vous à [GitHub](https://github.com/) si vous n’avez pas encore de compte.
* **GitHub Desktop**. Si vous choisissez de [créer la documentation dans votre environnement local](./work-in-local-environment.md), vous devez utiliser [GitHub Desktop](https://desktop.github.com/).
* Votre intégration à Adobe doit être dans une phase de test avec votre destination déployée dans un environnement d’évaluation dans Adobe Experience Platform.

## Instructions de haut niveau pour créer de la documentation pour votre destination dans Adobe Experience Platform {#high-level-instructions}

À un niveau élevé, pour créer de la documentation pour votre destination, vous devez [créer un double](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=fr#fork-the-repository) du référentiel de documentation Adobe Experience Platform et modifier le [modèle de documentation fourni](./self-service-template.md) dans une nouvelle branche. Utilisez le modèle fourni par l’Adobe pour créer une page de destination. Ouvrez une requête de tirage (PR) lorsque vous êtes prêt. Les instructions pour ce faire sont décrites plus loin dans la section [Procédure de création de votre nouvelle page de destination](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/fr-FR/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## Modèle de documentation {#documentation-template}

Pour vous aider à créer votre page de documentation, Adobe a prérempli un [modèle de documentation](./self-service-template.md) pour vous. Vous trouverez ci-dessous des instructions pour modifier le modèle et ouvrir une requête d’extraction. L’équipe de documentation de l’Adobe examinera et publiera la documentation relative à votre nouvelle destination.

[Téléchargez le modèle ici](../assets/docs-framework/yourdestination-template.zip) et décompressez le fichier pour extraire le fichier `yourdestination.md`.

Vous trouverez ci-dessous des instructions sur l’utilisation du modèle pour créer votre page de documentation.

## Procédure de création d’une page de destination {#steps-to-create-docs-page}

Vous pouvez utiliser l’interface web GitHub ou votre environnement local pour créer de la documentation pour votre nouvelle destination dans Adobe Experience Platform. Recherchez des instructions pour les deux options dans les liens ci-dessous :

* [Utiliser l’interface web GitHub pour créer une page de documentation de destination](./use-github-interface-to-create-documentation.md)
* [Utiliser un éditeur de texte dans votre environnement local pour créer une page de documentation de destination](./work-in-local-environment.md)

## Bonnes pratiques {#best-practices}

Passez en revue les [bonnes pratiques de création](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) avant et pendant que vous créez la page de documentation de destination. Veillez également à lire les [conseils d’écriture pour la documentation d’Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=fr) pour obtenir des conseils d’écriture que l’équipe de documentation d’Adobe utilise lors de la création de la documentation.