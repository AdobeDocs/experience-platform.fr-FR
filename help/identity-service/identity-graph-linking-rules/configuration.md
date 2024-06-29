---
title: Guide de configuration des règles de liaison de graphique d’identités
description: Découvrez les étapes recommandées à suivre lors de l’implémentation de vos données avec des configurations de règles de liaison de graphiques d’identités.
badge: Version bêta
source-git-commit: d8a36650b2cd3ec9683763f536ea5c2c2e27455c
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 5%

---

# Guide de configuration des règles de liaison de graphique d’identités

Lisez ce document pour obtenir un guide détaillé que vous pouvez suivre lors de l’implémentation de vos données avec Adobe Experience Platform Identity Service.

Composition détaillé :

1. [Créer les espaces de noms d’identité nécessaires](#namespace)
2. [Utilisez l’outil de simulation graphique pour vous familiariser avec l’algorithme d’optimisation des identités.](#graph-simulation)
3. [Utilisez l’outil de paramètres d’identité pour désigner vos espaces de noms uniques et configurer des classements de priorité pour vos espaces de noms.](#identity-settings)
4. [Création d’un schéma de modèle de données d’expérience (XDM)](#schema)
5. [Créer un jeu de données](#dataset)
6. [Ingestion de vos données dans Experience Platform](#ingest)

## Conditions préalables à la mise en oeuvre

Avant de commencer, vous devez vous assurer que les événements authentifiés de votre système contiennent toujours un identifiant de personne.

<!-- ## Set permissions {#set-permissions}

The first step in the implementation process for Identity Service is to ensure that your Experience Platform account is added to a role that is provisioned with the necessary permissions. Your administrator can configure permissions for your account by navigating to the Permissions UI in Adobe Experience Cloud. From there, your account must be added to a role with the following permissions:

* manage-identity-settings
* view-identity-dashboard
* view-identity-simulation

For more information on permissions, read the [permissions guide](../../access-control/abac/ui/permissions.md). -->

## Création des espaces de noms d’identité {#namespace}

Si vos données en ont besoin, vous devez d’abord créer les espaces de noms appropriés pour votre organisation. Pour savoir comment créer un espace de noms personnalisé, consultez le guide sur [création d’un espace de noms personnalisé dans l’interface utilisateur](../features/namespaces.md#create-custom-namespaces).

## Utiliser l&#39;outil de simulation graphique {#graph-simulation}

Ensuite, accédez au [outil de simulation graphique](./graph-simulation.md) dans l’espace de travail de l’interface utilisateur d’Identity Service. Vous pouvez utiliser l’outil de simulation graphique pour simuler des graphiques d’identités, créés avec différentes configurations de priorité d’espace de noms et d’espace de noms uniques.

En créant différentes configurations, vous pouvez utiliser l’outil de simulation graphique pour découvrir et mieux comprendre comment l’algorithme d’optimisation des identités et certaines configurations peuvent affecter le comportement de votre graphique.

## Configuration des paramètres d’identité {#identity-settings}

Une fois que vous avez une meilleure idée du comportement de votre graphique, accédez au [outil des paramètres d’identité](./identity-settings-ui.md) dans l’espace de travail de l’interface utilisateur d’Identity Service.

Utilisez l’outil de paramètres d’identité pour désigner vos espaces de noms uniques et configurer vos espaces de noms par ordre de priorité. Une fois que vous avez terminé d’appliquer vos paramètres, vous devez attendre au moins six heures avant de pouvoir procéder à l’ingestion des données, car au moins six heures sont nécessaires pour que les nouveaux paramètres soient reflétés dans Identity Service.

## Créer un schéma XDM {#schema}

Une fois vos espaces de noms uniques et vos priorités d’espace de noms établies, vous pouvez procéder à la configuration requise pour ingérer vos données. Tout d’abord, vous devez créer un schéma XDM. En fonction de vos données, vous devrez peut-être créer un schéma pour XDM Individual Profile et XDM ExperienceEvent.

Pour ingérer des données dans Real-time Customer Profile, vous devez vous assurer que votre schéma contient au moins un champ qui a été désigné comme identité principale. En définissant une identité principale, vous pouvez activer un schéma donné pour l’ingestion de profils.

Pour plus d’informations sur la création d’un schéma, consultez le guide sur [création d’un schéma XDM dans l’interface utilisateur](../../xdm/tutorials/create-schema-ui.md).

## Créer un jeu de données {#dataset}

Créez ensuite un jeu de données afin de fournir une structure pour les données que vous allez ingérer. Un jeu de données est une structure de stockage et de gestion pour une collection de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes). Les jeux de données fonctionnent en tandem avec les schémas. Pour ingérer des données dans Real-time Customer Profile, votre jeu de données doit être activé pour l’ingestion de Profile. Pour que votre jeu de données soit activé pour Profile, il doit référencer un schéma activé pour l’ingestion de Profile.

Pour plus d’informations sur la création d’un jeu de données, consultez la section [guide de l’interface utilisateur des jeux de données](../../catalog/datasets/user-guide.md).

## Ingestion de données {#ingest}

À ce stade, vous devriez disposer des éléments suivants :

* Autorisations nécessaires pour accéder aux fonctionnalités Identity Service.
* Espaces de noms pour vos données.
* Espaces de noms uniques désignés et priorités configurées pour vos espaces de noms.
* Au moins un schéma XDM. (En fonction de vos données et de votre cas d’utilisation spécifique, vous devrez peut-être créer des schémas d’événement de profil et d’expérience.)
* Jeu de données basé sur votre schéma.

Une fois que tous les éléments sont répertoriés ci-dessus, vous pouvez commencer à ingérer vos données dans Experience Platform. Vous pouvez procéder à l’ingestion des données de plusieurs manières différentes. Vous pouvez utiliser les services suivants pour importer vos données dans Experience Platform :

* [Ingestion par lots et par flux](../../ingestion/home.md)
* [Collecte de données dans Experience Platform](../../collection/home.md)
* [Sources Experience Platform](../../sources/home.md)

>[!TIP]
>
>Une fois vos données ingérées, la charge utile des données brutes XDM ne change pas. Il se peut que vos configurations d’identité principale s’affichent toujours dans l’interface utilisateur. Toutefois, ces configurations seront remplacées par les paramètres d’identité.

Pour tout commentaire, utilisez la variable **[!UICONTROL Commentaires Beta]** dans l’espace de travail de l’interface utilisateur d’Identity Service.