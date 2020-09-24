---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Schémas et descripteurs XDM
topic: tutorial
type: Tutorial
description: La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. Le modèle de données d’expérience (XDM), optimisé par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client. Les schémas sont la manière standard de décrire les données dans Experience Platform. Ils permettent à toutes les données conformes aux schémas d’être réutilisables sans conflit au sein d’une organisation et même d’être partagées entre plusieurs organisations.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 60%

---


# Utilisation de schémas [!DNL Experience Data Model] (XDM) et de descripteurs de relation

La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. [!DNL Experience Data Model] (XDM), piloté par l’Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client. Schemas are the standard way of describing data in [!DNL Experience Platform], allowing all data that conforms to schemas to be reusable without conflicts across an organization and even to be sharable between multiple organizations. Pour en savoir plus sur les schémas XDM, commencez par lire la [présentation du système XDM](../xdm/home.md).

## Création d’un schéma à l’aide du registre des schémas

Le registre des schémas fournit une interface utilisateur et une API RESTful à partir desquelles vous pouvez afficher et gérer toutes les ressources de la bibliothèque des schémas d’Adobe Experience Platform. The Schema Library contains resources made available to you by Adobe, [!DNL Experience Platform] partners, and vendors whose applications you use, as well as resources that you define and save to the Schema Registry. Pour apprendre à créer des schémas pour votre organisation, suivez les tutoriels portant sur la [création d’un schéma à l’aide de l’API Schema Registry](../xdm/tutorials/create-schema-api.md) ou sur la [création d’un schéma à l’aide de l’interface utilisateur de l’éditeur de schémas](../xdm/tutorials/create-schema-ui.md).

## Définition d’une relation entre deux schémas

Comprendre les relations entre vos clients et leurs interactions avec votre marque sur divers canaux est un aspect important d’Adobe Experience Platform. Defining these relationships within the structure of your [!DNL Experience Data Model] (XDM) schemas allows you to gain complex insights into your customer data. Ces descripteurs de relation peuvent être définis à l’aide de l’API Schema Registry et de l’interface utilisateur de l’éditeur de schémas. Pour plus d’informations, reportez-vous aux tutoriels portant sur la définition des relations entre deux schémas [à l’aide de l’API](../xdm/tutorials/relationship-api.md) ou [de l’interface utilisateur](../xdm/tutorials/relationship-ui.md).

## Création d’un schéma ad hoc

In specific circumstances, it may be necessary to create an [!DNL Experience Data Model] (XDM) schema with fields that are namespaced for usage only by a single dataset. On parle alors de schéma « ad hoc ». Ad-hoc schemas are used in various [data ingestion](../ingestion/home.md) workflows for [!DNL Experience Platform], including ingesting CSV files and creating certain kinds of [source connections](../sources/home.md). Creating an ad-hoc schema is done using the Schema Registry API and is intended to be used in conjunction with other [!DNL Experience Platform] tutorials that require creating an ad-hoc schema as part of their workflow. Pour commencer à créer un schéma ad hoc, consultez le tutoriel portant sur la [création d’un schéma ad hoc à l’aide de l’API](../xdm/tutorials/ad-hoc.md).

## Étapes suivantes

Une fois que vous avez défini des schémas pour votre organisation, vous pouvez commencer à créer des jeux de données dans lesquels les données peuvent être ingérées. Pour commencer, consultez la documentation suivante :

* [Présentation des jeux de données](../catalog/datasets/overview.md)
* [Présentation de Data Ingestion](../ingestion/home.md)