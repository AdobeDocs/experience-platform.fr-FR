---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
solution: Experience Platform
title: Présentation Des Sources En Libre-Service (SDK Par Lots)
description: Les sources en libre-service Adobe Experience Platform (SDK par lots) sont un ensemble d’API de configuration qui vous permettent d’intégrer une source basée sur l’API REST à l’aide de l’API Flow Service pour importer vos données dans Experience Platform.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 7%

---

# Présentation des sources en libre-service (SDK par lots)

Les sources en libre-service Adobe Experience Platform (SDK par lots) sont un framework qui vous permet d’intégrer une source basée sur l’API REST au catalogue de sources Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Sources en libre-service (Batch SDK) fournit un ensemble d’API de configuration pour créer votre propre source et importer vos données par lot dans Experience Platform.

Avec les sources en libre-service (SDK par lots), vous pouvez :

* Configurez et intégrez une nouvelle source au catalogue Experience Platform à l’aide de l’API [!DNL Flow Service].
* Définissez des spécifications pour votre source, y compris des informations relatives aux types d’authentification pris en charge et à la manière dont les données de ressource sont récupérées.
* Créer une documentation destinée aux utilisateurs pour votre nouvelle source.

La documentation sur les sources en libre-service fournit des instructions pour configurer, tester et publier une intégration source basée sur l’API REST avec Experience Platform, et pour que votre source fasse partie du catalogue de sources en constante évolution.

![catalogue](./assets/catalog.png)

## Comprendre les sources

Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services d’Experience Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Pour plus d’informations sur les sources et pour afficher la liste des différentes sources actuellement prises en charge sur Experience Platform, consultez la [présentation des sources](../home.md).

## Création d’une source

Grâce aux sources en libre-service, vous pouvez intégrer votre propre source basée sur l’API REST et importer vos données dans Experience Platform avec [!DNL Flow Service]. Vous pouvez intégrer une source au catalogue de sources Experience Platform en créant, en configurant et en envoyant une nouvelle spécification de connexion via l’API [!DNL Flow Service].

Consultez le guide sur la [création d’une spécification de connexion](./api/api-overview.md) pour plus d’informations sur l’intégration d’une nouvelle source à Experience Platform.

## Documenter votre source

Une fois votre source créée, consultez le [guide de documentation](./documentation/doc-overview.md) pour obtenir des instructions sur la manière de la documenter via l’interface web [!DNL GitHub] ou votre propre éditeur de texte.

## Aperçu général de la configuration

Le processus détaillé de configuration de votre source dans Experience Platform est décrit ci-dessous :

* Lisez le [ Guide de l’API des sources en libre-service (SDK par lots)](./api/api-overview.md).
   * Lisez le [ guide de prise en main ](./api/getting-started.md).
   * Suivez le tutoriel sur la [création d’une spécification de connexion](./api/create.md).
   * Suivez le tutoriel sur la [mise à jour de la spécification de connexion](./api/update-connection-specs.md).
   * Suivez le tutoriel sur [l’ajout de votre nouvel identifiant de spécification de connexion à une spécification de flux](./api/update-flow-specs.md)
   * [Envoyez votre nouvelle source](./api/submit.md).
* Pour mieux comprendre la structure et les propriétés d’une spécification de connexion, consultez le guide sur [ Options de configuration pour les sources en libre-service (SDK par lots)](./config/config.md).
   * Lisez le guide sur [la configuration de vos spécifications d’authentification](./config/authspec.md) pour mieux comprendre les différents types d’authentification que vous pouvez utiliser pour votre source.
   * Lisez le guide sur [la configuration des spécifications de votre source](./config/sourcespec.md) pour plus d’informations sur les différents types de pagination, les formats de planification et les schémas personnalisés qui peuvent être configurés pour votre source.
   * Lisez le guide sur la [configuration des spécifications d’exploration](./config/explorespec.md) pour plus d’informations sur la définition des paramètres requis pour explorer et inspecter les objets contenus dans votre source.
* Pour commencer à documenter votre source, lisez la [présentation de la création de documentation pour les sources en libre-service](./documentation/doc-overview.md)
   * Vous pouvez utiliser ce [modèle de documentation de l’API sources](./documentation/template.md) pour structurer votre documentation d’API.
   * Vous pouvez utiliser ce [modèle de documentation de l’interface utilisateur des sources](./documentation/ui-template.md) pour structurer votre documentation de l’interface utilisateur.
   * Consultez le guide sur [à l’aide de l’interface web GitHub](./documentation/github.md) pour savoir comment créer de la documentation à l’aide de GitHub.
   * Pour savoir comment créer de la documentation à l’aide de votre ordinateur local[&#128279;](./documentation/text-editor.md) consultez le guide sur à l’aide d’un éditeur de texte.
