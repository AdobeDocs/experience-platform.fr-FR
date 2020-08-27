---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segments;Segments
solution: Experience Platform
title: Segmentation d’entités multiples
topic: overview
description: La segmentation d’entités multiples est la capacité à élargir les données de profil grâce à des données supplémentaires basées sur les produits, les magasins et d’autres classes hors profil. Une fois connectées, les données des classes supplémentaires deviennent disponibles comme si elles étaient des données natives du schéma Profile.
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 38%

---


# Segmentation d’entités multiples

Multi-entity segmentation is the ability to extend [!DNL Profile] data with additional data based on products, stores, or other non-profile classes. Once connected, data from additional classes becomes available as if they were native to the [!DNL Profile] schema.

Pour en savoir plus sur la segmentation multientité, veuillez continuer à lire la documentation et compléter votre apprentissage en regardant la vidéo ci-dessous ou en explorant la présentation [de la](./home.md)segmentation.

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## Prise en main

Ce tutoriel nécessite une compréhension pratique des divers services Adobe Experience Platform impliqués dans l’utilisation de la segmentation. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[ !Profil client en temps réel DNL]](../profile/home.md): Fournit un profil unifié pour les consommateurs en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [Adobe Experience Platform Segmentation Service](./home.md) : vous permet de créer des segments depuis Real-time Customer Profile.
- [[ ! Modèle de données d’expérience DNL (XDM)]](../xdm/home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience client.

## Définition des relations XDM

Defining relationships with the structure of your [!DNL Experience Data Model] (XDM) schemas is an important and integral part of segment creation.

This process can be done either using the [!DNL Schema Registry] API or the [!DNL Schema Editor]. Vous trouverez un guide détaillé sur l’utilisation de l’API pour définir une relation entre deux schémas dans [le tutoriel sur la définition d’une relation entre deux schémas à l’aide de l’API](../xdm/tutorials/relationship-api.md). For a detailed guide on using the [!DNL Schema Editor] to define a relationship between two schemas, please read [the tutorial on defining a relationship between two schemas using the Schema Editor](../xdm/tutorials/relationship-ui.md).

## Comment créer des segments qui utilisent des relations XDM

Once you have defined your XDM relationships, you can use the [!DNL Segmentation Service] API to build a segment.

This process can be done either using the [!DNL Segmentation] API or the [!DNL Segment Builder] user interface. For a detailed guide on using the API to build a segment, please read [the tutorial on creating a segment using the Segmentation API](./tutorials/create-a-segment.md). Pour obtenir un guide détaillé sur l’utilisation du créateur de segments pour créer un segment, consultez [le guide d’utilisation du créateur de segments](./ui/overview.md).

## Évaluation et accès aux segments pour les segments d’entités multiples

After creating a segment, you can evaluate and access the segment results using the [!DNL Segmentation Service] API. L’évaluation d’un segment d’entités multiples est très similaire à celle d’un segment standard.

This process can only be done using the [!DNL Segmentation Service] API. For a detailed guide on using the API to evaluate and access segments, please read the tutorial on [evaluating and accessing segments](./tutorials/evaluate-a-segment.md).