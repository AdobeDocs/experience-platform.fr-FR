---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Présentation de l'apprentissage automatique en temps réel
topic: Overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 5%

---


# Présentation de l&#39;apprentissage automatique en temps réel (Alpha)

>[!IMPORTANT]
>
>L&#39;apprentissage automatique en temps réel n&#39;est pas encore disponible pour tous les utilisateurs. Cette fonction est en alpha et est encore en cours de test. Ce document est sujet à changement.

L&#39;apprentissage automatique en temps réel peut considérablement améliorer la pertinence de votre contenu d&#39;expérience numérique pour vos utilisateurs finaux. Cela est rendu possible grâce à l&#39;utilisation d&#39;un processus de référencement en temps réel et à l&#39;apprentissage continu sur le [!DNL Experience Edge]marché.

La combinaison d’un calcul transparent sur le Hub et sur le Hub [!DNL Edge] réduit considérablement la latence traditionnellement impliquée dans l’activation d’expériences hyper-personnalisées à la fois pertinentes et réactives. Par conséquent, l&#39;apprentissage automatique en temps réel fournit des inférences avec une latence incroyablement faible pour la prise de décision synchrone. Par exemple, le rendu du contenu d’une page Web personnalisée ou l’apparition d’une offre ou d’une remise afin de réduire le taux de fréquentation et d’augmenter les conversions sur un site Web de stockage.

## Architecture d&#39;apprentissage automatique en temps réel {#architecture}

Les diagrammes suivants donnent un aperçu de l&#39;architecture d&#39;apprentissage automatique en temps réel. Actuellement, alpha a une version plus simplifiée.

![arche alpha](../images/rtml/alpha-arch.png)

![Présentation simplifiée](../images/rtml/end-to-end-arch.png)

## Flux de travaux d&#39;apprentissage automatique en temps réel

Le processus suivant décrit les étapes et les résultats typiques de la création et de l&#39;utilisation d&#39;un modèle d&#39;apprentissage automatique en temps réel.

### Extraction de données et préparations

Les données sont ingérées et transformées avec le [!DNL Experience Data Model] (XDM) sur Adobe Experience Platform. Ces données sont utilisées pour la formation aux modèles. Pour en savoir plus sur XDM, consultez la [présentation de XDM](../../xdm/home.md).

### Création

Créez un modèle d&#39;apprentissage automatique en temps réel en le rédigeant à partir de zéro ou en l&#39;incorporant comme modèle ONNX sérialisé préformé dans les portables Adobe Experience Platform Jupyter.

### Déploiement

Déployez votre modèle pour [!DNL Experience Edge] créer un service d’apprentissage automatique en temps réel dans la Galerie [!UICONTROL de] services à l’aide du point de terminaison de l’API de prédiction.

### Inférence   

Utilisez le point de terminaison de l’API REST de prédiction pour générer des statistiques d’apprentissage automatique en temps réel.

### Diffusion

Les marketeurs peuvent ensuite définir des segments et des règles qui associent les scores d’apprentissage automatique en temps réel aux expériences à l’aide de Adobe Target. Cela permet aux visiteurs du site Web de votre marque de bénéficier en temps réel d’une même expérience hyper-personnalisée ou d’une page suivante.

## Fonctionnalité actuelle

L&#39;apprentissage automatique en temps réel est actuellement en alpha. Les fonctionnalités décrites ci-dessous peuvent être modifiées à mesure que davantage de fonctions et de noeuds sont disponibles.

>[!NOTE]
>
> Limites Alpha :
> - Actuellement, seuls les modèles ONNX sont pris en charge.
> - Les fonctions utilisées dans les noeuds ne peuvent pas être sérialisées. Par exemple, une fonction lambda utilisée dans un noeud Pandas.
> - 20 secondes de sommeil s’écoulent après [!DNL Edge] le déploiement manuel.
> - Pour un apprentissage approfondi, vos données doivent être envoyées de telle sorte que, lorsqu&#39; `df.values` elles sont appelées, elles retournent un tableau acceptable par votre modèle DL. Cela est dû au fait que le noeud de notation du modèle ONNX utilise `df.values` et envoie la sortie pour marquer par rapport au modèle.



### Fonctionnalités:

|  | Alpha (mai) |
| --- | --- |
| **Fonctionnalités** | - Utilisation du modèle de bloc-notes RTML, création, test et déploiement d&#39;un modèle d&#39;apprentissage automatique personnalisé. <br> - Appui à l&#39;importation de modèles d&#39;apprentissage automatique préformés. <br> - SDK d&#39;apprentissage automatique en temps réel. <br> - Ensemble de noeuds de création de départ. <br> - Déployé sur Adobe Experience Platform Hub. |
| **Disponibilité** | Amérique du Nord |
| **Noeuds de création** | - Pandas <br> - ScikitLearn <br> - ONNXNode <br> - Split <br> - ModelUpload <br> - OneHotEncoder |
| **Score des durées d’exécution** | ONNX |

## Étapes suivantes

Vous pouvez commencer par suivre le [guide de prise en main](./getting-started.md). Ce guide vous guide tout au long de la configuration de toutes les conditions préalables requises pour créer un modèle d’apprentissage automatique en temps réel.

