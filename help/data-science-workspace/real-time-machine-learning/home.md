---
keywords: Experience Platform;guide de développement;Espace de travail de science des données;rubriques les plus consultées;machine learning en temps réel;
solution: Experience Platform
title: Vue d’ensemble du machine learning en temps réel
description: Le machine learning en temps réel peut considérablement améliorer la pertinence de votre contenu d’expérience digitale pour vos utilisateurs finaux. Pour ce faire, vous pouvez tirer parti des référencements en temps réel et de l’apprentissage continu sur l’Edge Network Experience Platform.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 93%

---

# Vue d’ensemble du machine learning en temps réel (version alpha)

>[!IMPORTANT]
>
>Le machine learning en temps réel n’est pas encore disponible pour tous les utilisateurs et utilisatrices. Cette fonctionnalité est en version alpha et est encore en cours de test. Ce document est sujet à modification.

Le machine learning en temps réel peut considérablement améliorer la pertinence de votre contenu d’expérience digitale pour vos utilisateurs finaux. Ce résultat est obtenu par l’utilisation de l’inférence en temps réel et de l’apprentissage continu sur [!DNL Experience Platform Edge Network].

Une combinaison de calcul transparent sur le hub et [!DNL Edge] réduit considérablement la latence généralement liée à la fourniture d’expériences hyper-personnalisées qui sont à la fois pertinentes et réactives. Le machine learning en temps réel fournit donc des inférences avec une latence incroyablement faible pour une prise de décision synchrone. Il peut s’agir, par exemple, d’effectuer le rendu du contenu d’une page web personnalisée ou de faire apparaître une offre ou une remise pour réduire le taux d’attrition et augmenter les conversions sur une boutique en ligne.

## Architecture du machine learning en temps réel {#architecture}

Les diagrammes ci-après donnent un aperçu de l’architecture du machine learning en temps réel. Actuellement, la version alpha possède une version plus simplifiée.

![architecture alpha](../images/rtml/alpha-arch.png)

![Vue d’ensemble simplifiée](../images/rtml/end-to-end-arch.png)

## Workflow du machine learning en temps réel

Le workflow ci-après décrit les étapes et les résultats classiques de la création et de l’utilisation d’un modèle de machine learning en temps réel.

### Ingestion et préparations des données

Les données sont ingérées et transformées avec [!DNL Experience Data Model] (XDM) sur Adobe Experience Platform. Ces données sont utilisées pour l’apprentissage des modèles. Pour en savoir plus sur XDM, consultez la [présentation de XDM](../../xdm/home.md).

### Création

Créez entièrement un modèle de machine learning en temps réel ou incorporez-le en tant que modèle ONNX sérialisé préentraîné dans les notebooks Jupyter Adobe Experience Platform.

### Déploiement

Déployez votre modèle sur le [!DNL Edge Network] pour créer un service d’apprentissage automatique en temps réel dans la [!UICONTROL Galerie de services] à l’aide du point de terminaison de l’API de prédiction.

### Inférence   

Utilisez le point d’entrée de l’API REST Prediction pour générer des informations de machine learning en temps réel.

### Diffusion

Les spécialistes marketing peuvent ensuite définir des segments et des règles qui mappent les scores de machine learning en temps réel aux expériences à l’aide d’Adobe Target. Les visiteurs et visiteuses du site web de votre marque peuvent ainsi afficher en temps réel une expérience hyper-personnalisée sur la même page ou la page suivante.

## Fonctionnalités actuelles

Le machine learning en temps réel est actuellement en version alpha. Les fonctionnalités décrites ci-dessous sont susceptibles d’être modifiées au fur et à mesure que d’autres fonctionnalités et nœuds sont disponibles.

>[!NOTE]
>
> Limites de la version alpha :
> - Actuellement, seuls les modèles basés sur ONNX sont pris en charge.
> - Les fonctions utilisées dans les nœuds ne peuvent pas être sérialisées. Par exemple, une fonction lambda utilisée dans un nœud Pandas.
> - Il y a une mise en veille de 20 secondes après le déploiement manuel d’[!DNL Edge].
> - Pour le deep learning, vos données doivent être envoyées de manière à ce que, quand `df.values` est appelé, il renvoie un tableau acceptable par votre modèle DL. En effet, le nœud de notation du modèle ONNX utilise `df.values` et envoie la sortie pour noter le modèle.


### Fonctionnalités :

| | Version alpha (mai) |
| --- | --- |
| **Fonctionnalités** | - En utilisant le modèle de notebook RTML, créez, testez et déployez un modèle de machine learning personnalisé. <br> - Prise en charge de l’importation de modèles de machine learning préentraînés. <br> - SDK Real-time Machine Learning. <br> - Ensemble de démarrage de nœuds de création. <br> - Déployé sur le hub Adobe Experience Platform. |
| **Disponibilité** | Amérique du Nord |
| **Nœuds de création** | - Pandas <br> - ScikitLearn <br> - ONNXNode <br> - Split <br> - ModelUpload <br> - OneHotEncoder |
| **Temps d’exécution de la notation** | ONNX |

## Étapes suivantes

Vous pouvez commencer par suivre le [guide de prise en main](./getting-started.md). Ce guide vous explique comment mettre en place tous les prérequis nécessaire pour créer un modèle de machine learning en temps réel.
