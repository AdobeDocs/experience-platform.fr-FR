---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Schémas et descripteurs XDM
topic-legacy: tutorial
type: Tutorial
description: La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. Le modèle de données d’expérience (XDM), optimisé par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client. Les schémas sont la manière standard de décrire les données dans Experience Platform. Ils permettent à toutes les données conformes aux schémas d’être réutilisables sans conflit au sein d’une organisation et même d’être partagées entre plusieurs organisations.
exl-id: 1cdc45d7-57ca-4a2d-99a4-9a8cd885a511
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 59%

---

# Utilisation de schémas [!DNL Experience Data Model] (XDM) et de descripteurs de relation

La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. [!DNL Experience Data Model] (XDM), piloté par l’Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client. Les schémas sont la manière standard de décrire les données dans [!DNL Experience Platform], ce qui permet à toutes les données conformes aux schémas d&#39;être réutilisables sans conflit au sein d&#39;une organisation et même d&#39;être partagées entre plusieurs organisations. Pour en savoir plus sur les schémas XDM, commencez par lire la [présentation du système XDM](../xdm/home.md).

## Création d’un schéma à l’aide du registre des schémas

Le registre des schémas fournit une interface utilisateur et une API RESTful à partir desquelles vous pouvez afficher et gérer toutes les ressources de la bibliothèque des schémas d’Adobe Experience Platform. La bibliothèque de Schémas contient des ressources mises à votre disposition par Adobe, [!DNL Experience Platform] partenaires et fournisseurs dont vous utilisez les applications, ainsi que des ressources que vous définissez et enregistrez dans le registre des Schémas. Pour apprendre à créer des schémas pour votre organisation, suivez les tutoriels portant sur la [création d’un schéma à l’aide de l’API Schema Registry](../xdm/tutorials/create-schema-api.md) ou sur la [création d’un schéma à l’aide de l’interface utilisateur de l’éditeur de schémas](../xdm/tutorials/create-schema-ui.md).

## Définition d’une relation entre deux schémas

Comprendre les relations entre vos clients et leurs interactions avec votre marque sur divers canaux est un aspect important d’Adobe Experience Platform. La définition de ces relations au sein de la structure de vos schémas [!DNL Experience Data Model] (XDM) vous permet d’obtenir des informations complexes sur vos données client. Ces descripteurs de relation peuvent être définis à l’aide de l’API Schema Registry et de l’interface utilisateur de l’éditeur de schémas. Pour plus d’informations, reportez-vous aux tutoriels portant sur la définition des relations entre deux schémas [à l’aide de l’API](../xdm/tutorials/relationship-api.md) ou [de l’interface utilisateur](../xdm/tutorials/relationship-ui.md).

## Création d’un schéma ad hoc

Dans des circonstances spécifiques, il peut être nécessaire de créer un schéma [!DNL Experience Data Model] (XDM) avec des champs qui sont espacés de noms pour une utilisation uniquement par un seul jeu de données. On parle alors de schéma « ad hoc ». Les schémas ad hoc sont utilisés dans divers workflows [d&#39;assimilation de données](../ingestion/home.md) pour [!DNL Experience Platform], y compris l&#39;assimilation de fichiers CSV et la création de certains types de [connexions source](../sources/home.md). La création d’un schéma ad hoc s’effectue à l’aide de l’API Schéma Registry et doit être utilisée conjointement avec d’autres [!DNL Experience Platform] didacticiels qui nécessitent la création d’un schéma ad hoc dans le cadre de leur processus. Pour commencer à créer un schéma ad hoc, consultez le tutoriel portant sur la [création d’un schéma ad hoc à l’aide de l’API](../xdm/tutorials/ad-hoc.md).

## Étapes suivantes

Une fois que vous avez défini des schémas pour votre organisation, vous pouvez commencer à créer des jeux de données dans lesquels les données peuvent être ingérées. Pour commencer, consultez la documentation suivante :

* [Présentation des jeux de données](../catalog/datasets/overview.md)
* [Présentation de Data Ingestion](../ingestion/home.md)
