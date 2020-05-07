---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Présentation de l'apprentissage automatique en temps réel
topic: Overview
translation-type: tm+mt
source-git-commit: ab8b000bec0ae30c695582f57c40105b7ca1f22f
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 2%

---


# Présentation de l&#39;apprentissage automatique en temps réel

>[!IMPORTANT]
>L&#39;apprentissage automatique en temps réel n&#39;est pas encore disponible pour tous les utilisateurs. Cette fonction est en alpha et est encore en cours de test. Ce document est sujet à changement.

La structure d’apprentissage automatique en temps réel d’Adobe Experience Platform vous permet d’utiliser l’apprentissage automatique pour offrir aux utilisateurs finaux les meilleures expériences au bon moment dans les canaux appropriés avec une période de moins de deux secondes.

## Avantages

L&#39;apprentissage automatique en temps réel peut considérablement améliorer la pertinence de votre contenu d&#39;expérience numérique pour vos utilisateurs finaux. Cela est rendu possible en tirant parti des référencements en temps réel et de l’apprentissage continu sur le bord de l’expérience.

La combinaison d’un calcul transparent à la fois sur le concentrateur et sur le bord réduit considérablement la latence traditionnellement impliquée dans l’alimentation d’expériences hyper-personnalisées à la fois pertinentes et réactives. Par conséquent, l&#39;apprentissage automatique en temps réel fournit des inférences avec une latence incroyablement faible pour la prise de décision synchrone. Par exemple, le rendu du contenu d’une page Web personnalisée ou l’apparition d’une offre ou d’une remise afin de réduire le taux de fréquentation et d’augmenter les conversions sur un site Web de stockage.

## Architecture d&#39;apprentissage automatique en temps réel

Le diagramme suivant présente un aperçu de l&#39;architecture d&#39;apprentissage automatique en temps réel.

![Présentation simplifiée](../images/rtml/simple-overview.png)

## Flux de travaux d’apprentissage automatique en temps réel (Alpha)

Le processus suivant décrit les étapes et les résultats typiques de la création et de l&#39;utilisation d&#39;un modèle d&#39;apprentissage automatique en temps réel.

### Extraction de données et préparations

Les données sont ingérées et transformées avec le modèle de données d’expérience (XDM) sur la plate-forme Adobe Experience Platform. Ces données sont utilisées pour la formation aux modèles. Pour en savoir plus sur XDM, consultez la présentation [de](../../xdm/home.md)XDM.

### Création  

Créez un modèle d’apprentissage automatique en temps réel en le rédigeant à partir de zéro ou en l’incorporant sous la forme d’un modèle ONNX sérialisé et préformé dans les portables Jupyter d’Adobe Experience Platform.

### Déploiement

Déployez votre modèle sur Experience Edge pour créer un service d’apprentissage automatique en temps réel dans la Galerie de services à l’aide du point de terminaison de l’API de prédiction.

### Inférence   

Utilisez le point de terminaison de l’API REST de prédiction pour générer des statistiques d’apprentissage automatique en temps réel.

### Diffusion

Les marketeurs peuvent ensuite définir des segments et des règles qui associent les scores d’apprentissage automatique en temps réel aux expériences à l’aide d’Adobe Cible. Cela permet aux visiteurs du site Web de votre marque de bénéficier en temps réel d’une même expérience hyper-personnalisée ou d’une page suivante (moins de 100 ms).

## Plan de développement

L&#39;apprentissage automatique en temps réel est actuellement en phase Alpha. Le tableau ci-dessous présente quelques-unes des fonctionnalités et mises à jour qui devraient être publiées dans la prochaine version bêta.

<table>
    <th></th>
    <th>Alpha (mai)</th>
    <th>Bêta</th>
    <tr>
        <td>
            <strong>Fonctionnalités</strong>
        </td>
        <td>
            <li>Data Science Workspace vous permet d’apporter votre propre modèle et auteur via l’intégration du lanceur de blocs-notes.</li>
            <li>Jeu de départ d’opérateurs de création.</li>
            <li>Déploiement sur le concentrateur</li>
            <li>Scikit Learn based Models.</li>
        </td>
        <td>
            <li>Intégration de l’interface utilisateur de la Galerie de services Data Science Workspace.</li>
            <li>Enrichissez automatiquement le Profil client en temps réel avec des résultats inférence.</li>
            <li>Modèles d'apprentissage profonds.</li>
            <li>Ensemble étendu d’opérateurs de création, y compris les opérateurs personnalisés.</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Disponibilité</strong>
        </td>
        <td>
            Amérique du Nord
        </td>
        <td>
            <li>Amérique du Nord</li>
            <li>Europe et Moyen-Orient (EMEA)</li>
            <li>Asie-Pacifique (APAC)</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Création  </strong>
        </td>
        <td>
            <li>Prise en charge de Python</li>
            <li>SDK d’apprentissage automatique en temps réel</li>
            <li>Noeuds de création Python : Pandas, ScikitLearn, ONNXNode, Split, ModelUpload, OneHotEncoder.</li>
        </td>
        <td>
            <li>Prise en charge de Tensorflow.</li>
            <li>Autres noeuds de création Python : Lecteur de Profil client en temps réel, Ecrivain de Profil client en temps réel, Nombreuses baies, XDM2Frame, Frame2XDM. </li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Score des durées d’exécution</strong>
        </td>
        <td>
            ONNX
        </td>
        <td>
            ONNX
        </td>
    </tr>
</table>

## Étapes suivantes

Vous pouvez commencer par suivre le guide de [prise en main](./getting-started.md) . Ce guide vous guide tout au long de la configuration de toutes les conditions préalables requises pour créer un modèle d’apprentissage automatique en temps réel.

