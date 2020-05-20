---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentation multientité
topic: overview
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 4%

---


# Segmentation multientité

La segmentation multientité permet d’étendre les données de Profil avec des données supplémentaires basées sur des produits, des magasins ou d’autres classes non profils. Une fois connecté, les données d’autres classes deviennent disponibles comme si elles étaient natives du schéma de profil.

Pour plus d’informations sur la segmentation multientité, consultez la présentation [de la](./home.md)segmentation.

## Prise en main

Ce didacticiel nécessite une bonne compréhension des différents services Adobe Experience Platform impliqués dans l’utilisation de la segmentation. Avant de commencer ce didacticiel, consultez la documentation relative aux services suivants :

- [Profil](../profile/home.md)client en temps réel : Fournit un profil unifié pour les consommateurs en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [Adobe Experience Platform Segmentation Service](./home.md): Permet de créer des segments à partir du Profil client en temps réel.
- [Modèle de données d’expérience (XDM)](../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.

## Comment définir les relations XDM

La définition de relations avec la structure de vos schémas de modèle de données d’expérience (XDM) est une partie importante et intégrante de la création de segments.

Ce processus peut être effectué à l’aide de l’API de registre de Schéma ou de l’éditeur de Schéma. Pour un guide détaillé sur l&#39;utilisation de l&#39;API pour définir une relation entre deux schémas, consultez [le tutoriel sur la définition d&#39;une relation entre deux schémas à l&#39;aide de l&#39;API](../xdm/tutorials/relationship-api.md). Pour un guide détaillé sur l&#39;utilisation de l&#39;éditeur de Schéma pour définir une relation entre deux schémas, veuillez lire [le didacticiel sur la définition d&#39;une relation entre deux schémas à l&#39;aide de l&#39;éditeur](../xdm/tutorials/relationship-ui.md)de Schéma.

## Utilisation de la création de segments utilisant des relations XDM

Une fois que vous avez défini vos relations XDM, vous pouvez utiliser les API Profil client en temps réel pour créer un segment.

Ce processus peut être effectué à l’aide de l’API Profil client en temps réel ou du créateur de segments. Pour obtenir un guide détaillé sur l’utilisation de l’API pour créer un segment, consultez [le didacticiel sur la création d’un segment à l’aide de l’API](./tutorials/create-a-segment.md)Profil client en temps réel. Pour obtenir un guide détaillé sur l’utilisation du créateur de segments pour créer un segment, consultez [le guide](./ui/overview.md)d’utilisation du créateur de segments.

## Comment évaluer et accéder aux segments pour les segments à entités multiples

Après avoir créé un segment, vous pouvez évaluer les résultats du segment et y accéder à l’aide des API Profil client en temps réel. L’évaluation d’un segment à plusieurs entités est très similaire à l’évaluation d’un segment ordinaire.

Ce processus ne peut être effectué qu’à l’aide de l’API Profil client en temps réel. Pour obtenir un guide détaillé sur l’utilisation de l’API pour évaluer les segments et y accéder, consultez [le didacticiel sur l’évaluation et l’accès aux segments](./tutorials/evaluate-a-segment.md).