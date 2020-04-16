---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' et descripteurs XDM'
topic: tutorial
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac

---


# Utilisation des  de modèle de données d’expérience (XDM) et des descripteurs de relation

La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. Le modèle de données d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des  pour la gestion de l’expérience client. Les  de sont la manière standard de décrire les données dans la plateforme d’expérience, permettant à toutes les données conformes au d’être réutilisables sans conflit au sein d’une organisation et même d’être partagées entre plusieurs organisations. Pour en savoir plus sur les  XDM, en lisant la présentation [du système](../xdm/home.md)XDM.

## Création d’un  à l’aide du registre 

Le Registre des  de fournit une interface utilisateur et une API RESTful à partir de laquelle vous pouvez et gérer toutes les ressources de la bibliothèque de  de la plateforme d’expérience Adobe. La bibliothèque de  de contient les ressources mises à votre disposition par Adobe, les partenaires de la plate-forme d’expérience et les fournisseurs dont vous utilisez les applications, ainsi que les ressources que vous définissez et enregistrez dans le registre  de. Pour savoir comment créer des  de pour votre organisation, suivez les didacticiels de [création d&#39;un à l&#39;aide de l&#39;API](../xdm/tutorials/create-schema-api.md) de registre de l&#39; [](../xdm/tutorials/create-schema-ui.md)d&#39;origine ou de lacréation d&#39;un à l&#39;aide de l&#39;interfaceutilisateur de l&#39;éditeur de.

## Définir une relation entre deux 

La capacité de comprendre les relations entre vos clients et leurs interactions avec votre marque dans divers  de est un élément important d’Adobe Experience Platform. La définition de ces relations au sein de la structure de votre de modèle de données d’expérience (XDM) vous permet d’obtenir des informations complexes sur vos données client. Ces descripteurs de relation peuvent être définis à l’aide de l’API de Registre  et de l’interface utilisateur de l’éditeur de  de. Pour plus d’informations, reportez-vous aux didacticiels de définition des relations entre deux  [à l’aide de l’API](../xdm/tutorials/relationship-api.md) ou [de l’interface utilisateur](../xdm/tutorials/relationship-ui.md).

## Création d’un  ad hoc

Dans des circonstances spécifiques, il peut être nécessaire de créer un de modèle de données d’expérience (XDM) avec des champs dont l’espace de noms n’est utilisé que par un seul jeu de données. On parle alors de  &quot;ad hoc&quot;. Les  ad hoc sont utilisées dans divers d’assimilation [de](../ingestion/home.md) données pour la plateforme d’expérience, notamment l’assimilation de fichiers CSV et la création de certains types de connexions [](../sources/home.md)source. La création d’un  de ad hoc s’effectue à l’aide de l’API de registre et est destinée à être utilisée en association avec d’autres didacticiels de la plateforme d’expérience qui nécessitent la création d’unjournal ad hoc dans le cadre de leur processus. Pour commencer à créer un  de ad hoc, consultez le didacticiel relatif à la [création d’un  ad hoc à l’aide de l’API](../xdm/tutorials/ad-hoc.md).

## Étapes suivantes

Une fois que vous avez défini des  pour votre organisation, vous pouvez commencer à créer des jeux de données dans lesquels les données peuvent être assimilées. Pour commencer, consultez la documentation suivante :

* [Présentation des jeux de données](../catalog/datasets/overview.md)
* [Présentation de l&#39;insertion de données](../ingestion/home.md)