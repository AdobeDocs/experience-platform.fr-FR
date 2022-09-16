---
keywords: Experience Platform;guide de développement;Data Science Workspace;rubriques les plus consultées;apprentissage automatique en temps réel ;
solution: Experience Platform
title: Présentation de l’apprentissage automatique en temps réel
topic-legacy: Overview
description: L’apprentissage automatique en temps réel peut considérablement améliorer la pertinence de votre contenu d’expérience numérique pour vos utilisateurs finaux. Pour ce faire, vous pouvez tirer parti de l’inférencement en temps réel et de l’apprentissage continu sur Experience Edge.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 5%

---

# Présentation de l’apprentissage automatique en temps réel (Alpha)

>[!IMPORTANT]
>
>L’apprentissage automatique en temps réel n’est pas encore disponible pour tous les utilisateurs. Cette fonctionnalité est en version alpha et est encore en cours de test. Ce document peut faire l’objet de modifications.

L’apprentissage automatique en temps réel peut considérablement améliorer la pertinence de votre contenu d’expérience numérique pour vos utilisateurs finaux. Cela est rendu possible en tirant parti de l’infériorité en temps réel et de l’apprentissage continu sur la variable [!DNL Experience Edge].

Combinaison de calcul transparent sur le Hub et la variable [!DNL Edge] réduit considérablement la latence traditionnellement impliquée dans l’alimentation d’expériences hyper-personnalisées qui sont à la fois pertinentes et réactives. Par conséquent, l’apprentissage automatique en temps réel fournit des inférences avec une latence incroyablement faible pour la prise de décision synchrone. Par exemple, le rendu du contenu d’une page web personnalisée ou l’affichage d’une offre ou d’une remise pour réduire l’attrition et augmenter les conversions sur une boutique web.

## Architecture d’apprentissage automatique en temps réel {#architecture}

Les diagrammes suivants fournissent un aperçu de l’architecture d’apprentissage automatique en temps réel. Actuellement, alpha a une version plus simplifiée.

![couche alpha](../images/rtml/alpha-arch.png)

![Présentation simplifiée](../images/rtml/end-to-end-arch.png)

## Workflow d’apprentissage automatique en temps réel

Le workflow suivant décrit les étapes et les résultats typiques de la création et de l’utilisation d’un modèle d’apprentissage automatique en temps réel.

### Ingestion et préparation des données

Les données sont ingérées et transformées avec la variable [!DNL Experience Data Model] (XDM) sur Adobe Experience Platform. Ces données sont utilisées pour la formation des modèles. Pour en savoir plus sur XDM, consultez la [présentation de XDM](../../xdm/home.md).

### Création

Créez un modèle d’apprentissage automatique en temps réel à partir de zéro ou incorporez-le en tant que modèle ONNX sérialisé préentraîné dans les notebooks Adobe Experience Platform Jupyter.

### Déploiement

Déployez votre modèle sur [!DNL Experience Edge] Création d’un service d’apprentissage automatique en temps réel dans le [!UICONTROL Galerie de services] à l’aide du point de terminaison de l’API de prédiction.

### Inférence   

Utilisez le point d’entrée de l’API REST de prédiction pour générer des insights d’apprentissage automatique en temps réel.

### Diffusion

Les marketeurs peuvent ensuite définir des segments et des règles qui mappent les scores d’apprentissage automatique en temps réel aux expériences à l’aide d’Adobe Target. Cela permet aux visiteurs du site web de votre marque d’afficher en temps réel la même expérience hyper-personnalisée sur la même page ou la page suivante.

## Fonctionnalités actuelles

L’apprentissage automatique en temps réel est actuellement en version alpha. Les fonctionnalités décrites ci-dessous peuvent être modifiées à mesure que d’autres fonctionnalités et noeuds sont disponibles.

>[!NOTE]
>
> Limites Alpha :
> - Actuellement, seuls les modèles basés sur ONNX sont pris en charge.
> - Les fonctions utilisées dans les noeuds ne peuvent pas être sérialisées. Par exemple, une fonction lambda utilisée dans un noeud Pandas.
> - Il y a 20 secondes de sommeil après [!DNL Edge] Le déploiement est effectué manuellement.
> - Pour un apprentissage profond, vos données doivent être envoyées de manière à ce que, lors de la `df.values` est appelée , elle renvoie un tableau acceptable par votre modèle DL. En effet, le noeud de notation de modèle ONNX utilise `df.values` et envoie la sortie à noter par rapport au modèle.



### Fonctionnalités:

|  | Alpha (mai) |
| --- | --- |
| **Fonctionnalités** | - Utilisation du modèle de notebook RTML, création, test et déploiement d’un modèle d’apprentissage automatique personnalisé. <br> - Prise en charge de l’importation de modèles d’apprentissage automatique pré-entraînés. <br> - SDK d’apprentissage automatique en temps réel. <br> - Ensemble de noeuds de création de départ. <br> - Déployé sur Adobe Experience Platform Hub. |
| **Disponibilité** | Amérique du Nord |
| **Noeuds de création** | - Pandas <br> - ScikitLearn <br> - ONNXNode <br> - Partage <br> - ModelUpload <br> - OneHotEncoder |
| **Temps d’exécution de notation** | ONNX |

## Étapes suivantes

Vous pouvez commencer par suivre le [guide de prise en main](./getting-started.md). Ce guide vous guide tout au long des étapes nécessaires à la configuration de toutes les conditions préalables requises pour créer un modèle d’apprentissage automatique en temps réel.
