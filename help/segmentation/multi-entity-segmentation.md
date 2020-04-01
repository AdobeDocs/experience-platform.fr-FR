---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentation multientité
topic: overview
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Segmentation multientité

La segmentation multientité permet d’étendre les données  avec des données supplémentaires basées sur des produits, des magasins ou d’autres classes  non. Une fois connecté, les données d’autres classes deviennent disponibles comme si elles étaient natives du  .

Pour plus d’informations sur la segmentation multi-entités, consultez la présentation [de la](./home.md)segmentation.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans l’utilisation de la segmentation. Avant de commencer ce didacticiel, veuillez consulter la documentation des services suivants :

- [](../profile/home.md)du client en temps réel : Fournit un de consommateurs unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [Adobe Experience Platform Segmentation Service](./home.md): Permet de créer des segments à partir des  de clients en temps réel.
- [Modèle de données d’expérience (XDM)](../xdm/home.md): Cadre normalisé selon lequel la plateforme organise les données d’expérience client.

## Comment définir les relations XDM

La définition de relations avec la structure de votre  de modèle de données d’expérience (XDM) est une partie importante et intégrale de la création de segments.

Ce processus peut être effectué à l’aide de l’API de Registre  ou de l’éditeur de  de. Pour un guide détaillé sur l&#39;utilisation de l&#39;API pour définir une relation entre deux  de, veuillez lire [le didacticiel sur la définition d&#39;une relation entre deux  de à l&#39;aide de l&#39;API](../xdm/tutorials/relationship-api.md). Pour obtenir un guide détaillé sur l’utilisation de l’éditeur de  pour définir une relation entre deux  de, veuillez lire [le didacticiel sur la définition d’une relation entre deux  à l’aide de l’éditeur](../xdm/tutorials/relationship-ui.md)de.

## Utilisation de la création de segments utilisant des relations XDM

Une fois que vous avez défini vos relations XDM, vous pouvez utiliser les API de client en temps réel pour créer un segment.

Ce processus peut être effectué à l’aide de l’API  client en temps réel ou du créateur de segments. Pour obtenir un guide détaillé sur l’utilisation de l’API pour créer un segment, consultez [le didacticiel sur la création d’un segment à l’aide de l’API](./tutorials/create-a-segment.md)de  du client en temps réel. Pour obtenir un guide détaillé sur l’utilisation du créateur de segments pour créer un segment, consultez [le guide](./ui/overview.md)d’utilisation du créateur de segments.

## Comment évaluer et accéder aux segments pour les segments à entités multiples

Après avoir créé un segment, vous pouvez évaluer les résultats du segment et y accéder à l’aide des API de client en temps réel. L’évaluation d’un segment à plusieurs entités est très similaire à l’évaluation d’un segment ordinaire.

Ce processus ne peut être effectué qu’à l’aide de l’API  client en temps réel. Pour obtenir un guide détaillé sur l’utilisation de l’API pour évaluer les segments et y accéder, consultez [le didacticiel sur l’évaluation et l’accès aux segments](./tutorials/evaluate-a-segment.md).