---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentation d’entités multiples
topic: overview
translation-type: tm+mt
source-git-commit: 7110be2654e55ea411580f8c9e2e92bb52badab5
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 93%

---


# Segmentation d’entités multiples

La segmentation d’entités multiples est la capacité à élargir les données de profil grâce à des données supplémentaires basées sur les produits, les magasins et d’autres classes hors profil. Une fois connectées, les données des classes supplémentaires deviennent disponibles comme si elles étaient des données natives du schéma Profile.

Pour en savoir plus sur la segmentation multientité, veuillez continuer à lire la documentation et compléter votre apprentissage en regardant la vidéo ci-dessous ou en explorant la présentation [de la](./home.md)segmentation.]

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## Prise en main

Ce tutoriel nécessite une compréhension pratique des divers services Adobe Experience Platform impliqués dans l’utilisation de la segmentation. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [Real-time Customer Profile](../profile/home.md) : fournit un profil de consommateur en temps réel unifié sur base des données agrégées provenant de plusieurs sources.
- [Adobe Experience Platform Segmentation Service](./home.md) : vous permet de créer des segments depuis Real-time Customer Profile.
- [Modèle de données d’expérience (XDM)](../xdm/home.md) : cadre normalisé selon lequel Experience Platform organise les données d’expérience client.

## Définition des relations XDM

La définition des relations avec la structure de vos schémas de modèle de données d’expérience (XDM) est une partie importante et intégrante de la création de segments.

Ce processus peut être réalisé soit à l’aide de l’API Schema Registry, soit à l’aide de l’éditeur de schémas. Vous trouverez un guide détaillé sur l’utilisation de l’API pour définir une relation entre deux schémas dans [le tutoriel sur la définition d’une relation entre deux schémas à l’aide de l’API](../xdm/tutorials/relationship-api.md). Vous trouverez un guide détaillé sur l’utilisation de l’éditeur de schémas pour définir une relation entre deux schémas dans [le tutoriel sur la définition d’une relation entre deux schémas à l’aide de l’éditeur de schémas](../xdm/tutorials/relationship-ui.md).

## Création de segments à l’aide de relations XDM

Une fois que vous avez défini vos relations XDM, vous pouvez utiliser les API Real-time Customer Profile pour créer un segment.

Ce processus peut être réalisé à l’aide de l’API Real-time Customer Profile ou du créateur de segments. Pour obtenir un guide détaillé sur l’utilisation de l’API pour créer un segment, consultez [le tutoriel sur la création d’un segment à l’aide de l’API Real-time Customer Profile](./tutorials/create-a-segment.md). Pour obtenir un guide détaillé sur l’utilisation du créateur de segments pour créer un segment, consultez [le guide d’utilisation du créateur de segments](./ui/overview.md).

## Évaluation et accès aux segments pour les segments d’entités multiples

Après avoir créé un segment, vous pouvez évaluer les résultats du segment et y accéder à l’aide des API Real-time Customer Profile. L’évaluation d’un segment d’entités multiples est très similaire à celle d’un segment standard.

Ce processus ne peut être réalisé qu’en utilisant l’API Real-time Customer Profile. Vous trouverez un guide détaillé sur l’utilisation de l’API pour évaluer les segments et y accéder dans [le tutoriel sur l’évaluation et l’accès aux segments](./tutorials/evaluate-a-segment.md).