---
title: Documenter votre destination dans Adobe Experience Platform
description: Cette section contient des instructions détaillées pour la création d’une page de documentation pour la destination dans Adobe Experience Platform
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 7%

---

# Documenter la destination dans [!DNL Adobe Experience Platform]

>[!IMPORTANT]
>
>Le processus documenté ici n’est nécessaire que pour les partenaires qui soumettent des destinations standardisées (publiques). Si vous créez une destination privée destinée à votre propre usage, vous n’avez pas besoin de créer et de publier de la documentation pour la destination.

## Vue d’ensemble {#overview}

Bienvenue à [!DNL Adobe Experience Platform], ravi de vous compter parmi nous !
La documentation de la destination est la dernière étape avant qu’elle puisse être mise en ligne dans [!DNL Adobe Experience Platform].

Cette section de documentation comprend les éléments suivants :

* Cette section contient des instructions détaillées pour créer une page de documentation pour votre nouvelle destination.
* un modèle à remplir pour votre destination ;
* [Instructions générales sur l’utilisation de Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=fr);
* [Instructions spécifiques pour la version Markdown d’Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=fr#custom-markdown-extensions) (la version Markdown d’Adobe est très similaire à la version standard de Markdown).
* Une [page des bonnes pratiques](./authoring-best-practices.md) pour vous aider à créer une page de documentation pour la page de destination, qui répond aux normes de qualité de la documentation Experience Platform.

## Conditions préalables {#prerequisites}

Pour créer de la documentation pour la destination conformément aux instructions de cet article, les éléments suivants sont nécessaires :

* **Compte GitHub**. Inscrivez-vous à [GitHub](https://github.com/) si vous ne disposez pas encore d’un compte.
* **Bureau GitHub**. Si vous choisissez de [créer la documentation dans votre environnement local](./work-in-local-environment.md), vous devez utiliser [Bureau GitHub](https://desktop.github.com/).
* Votre intégration à Adobe doit être en phase de test, avec votre destination déployée dans un environnement d’évaluation en [!DNL Adobe Experience Platform].

## Instructions générales pour créer de la documentation pour la destination dans [!DNL Adobe Experience Platform] {#high-level-instructions}

À un niveau élevé, pour créer de la documentation pour la destination, vous devez [créer un branchement](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=fr#fork-the-repository) du référentiel de documentation [!DNL Adobe Experience Platform] et modifier le [modèle de documentation fourni](./self-service-template.md) dans une nouvelle branche. Utilisez le modèle fourni par Adobe pour créer une page de destination. Ouvrez une requête de tirage (PR) lorsque vous êtes prêt. Pour ce faire, reportez-vous aux instructions ci-dessous, dans la section [Procédure de création de votre page de destination](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/fr-FR/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## Modèle de documentation {#documentation-template}

Pour vous aider à créer votre page de documentation, Adobe a prérempli un [&#x200B; modèle de documentation &#x200B;](./self-service-template.md). Plus bas, vous trouverez des instructions sur la modification du modèle et l’ouverture d’une requête d’extraction. L’équipe de documentation d’Adobe examinera et publiera la documentation de votre nouvelle destination.

[Téléchargez le modèle ici](../assets/docs-framework/yourdestination-template.zip) puis décompressez le fichier pour extraire le fichier `yourdestination.md`.

Vous trouverez ci-dessous des instructions sur l’utilisation du modèle pour créer votre page de documentation.

## Étapes de création de votre page de destination {#steps-to-create-docs-page}

Vous pouvez utiliser l’interface web GitHub ou votre environnement local pour créer la documentation de votre nouvelle destination dans [!DNL Adobe Experience Platform]. Recherchez des instructions pour les deux options dans les liens ci-dessous :

* [Utiliser l’interface web GitHub pour créer une page de documentation de destination](./use-github-interface-to-create-documentation.md)
* [Utiliser un éditeur de texte dans votre environnement local pour créer une page de documentation de destination](./work-in-local-environment.md)

## Bonnes pratiques {#best-practices}

Consultez les [&#x200B; bonnes pratiques de création &#x200B;](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) avant et pendant la création de la page de documentation de destination. Veillez également à lire le [guide de rédaction pour la documentation Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=fr) pour obtenir d’autres conseils de rédaction que l’équipe de documentation Adobe utilise lors de la création de documentation.