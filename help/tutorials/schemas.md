---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: schémas et descripteurs XDM
topic: tutorial
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---


# Utilisation de schémas de modèle de données d’expérience (XDM) et de descripteurs de relation

La normalisation et l’interopérabilité sont des concepts clés d’Adobe Experience Platform. Le modèle de données d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client. Les Schémas sont la manière standard de décrire les données dans la plateforme d’expérience, ce qui permet à toutes les données conformes aux schémas d’être réutilisables sans conflit au sein d’une organisation et même d’être partagées entre plusieurs organisations. Pour en savoir plus sur les schémas XDM, début en lisant la présentation [du système](../xdm/home.md)XDM.

## Création d’un schéma à l’aide du registre des Schémas

Le registre des Schémas fournit une interface utilisateur et une API RESTful à partir de laquelle vous pouvez vue et gérer toutes les ressources de la bibliothèque de Schémas de la plate-forme Adobe Experience Platform. La bibliothèque de Schémas contient les ressources mises à votre disposition par Adobe, les partenaires de la plateforme d’expérience et les fournisseurs dont vous utilisez les applications, ainsi que les ressources que vous définissez et enregistrez dans le registre des Schémas. Pour savoir comment créer des schémas pour votre organisation, suivez les didacticiels de [création d&#39;un schéma à l&#39;aide de l&#39;API](../xdm/tutorials/create-schema-api.md) de registre de Schéma ou de [création d&#39;un schéma à l&#39;aide de l&#39;interface](../xdm/tutorials/create-schema-ui.md)utilisateur de l&#39;éditeur de Schémas.

## Définir une relation entre deux schémas

La capacité de comprendre les relations entre vos clients et leurs interactions avec votre marque sur différents canaux est un élément important d’Adobe Experience Platform. La définition de ces relations au sein de la structure de vos schémas de modèle de données d’expérience (XDM) vous permet d’obtenir des informations complexes sur vos données client. Ces descripteurs de relation peuvent être définis à l’aide de l’API de registre de Schéma et de l’interface utilisateur de l’éditeur de Schéma. Pour plus d’informations, voir les didacticiels de définition de relations entre deux schémas [à l’aide de l’API](../xdm/tutorials/relationship-api.md) ou [à l’aide de l’interface utilisateur](../xdm/tutorials/relationship-ui.md).

## Création d’un schéma ad hoc

Dans des circonstances spécifiques, il peut être nécessaire de créer un schéma de modèle de données d’expérience (XDM) avec des champs dont l’espacement des noms n’est utilisé que par un seul jeu de données. On parle alors de schéma &quot;ad hoc&quot;. Les schémas ad hoc sont utilisés dans divers workflows d’assimilation [de](../ingestion/home.md) données pour la plate-forme d’expérience, y compris l’assimilation de fichiers CSV et la création de certains types de connexions [](../sources/home.md)source. La création d’un schéma ad hoc s’effectue à l’aide de l’API Schéma Registry et est destinée à être utilisée conjointement avec d’autres didacticiels de la plateforme d’expérience qui nécessitent la création d’un schéma ad hoc dans le cadre de leur processus. Pour commencer à créer un schéma ad hoc, consultez le didacticiel de [création d’un schéma ad hoc à l’aide de l’API](../xdm/tutorials/ad-hoc.md).

## Étapes suivantes

Une fois que vous avez défini des schémas pour votre organisation, vous pouvez commencer à créer des jeux de données dans lesquels les données peuvent être ingérées. Pour commencer, consultez la documentation suivante :

* [Présentation des jeux de données](../catalog/datasets/overview.md)
* [Présentation de l&#39;insertion de données](../ingestion/home.md)