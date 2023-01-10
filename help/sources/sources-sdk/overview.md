---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
solution: Experience Platform
title: Présentation des sources en libre-service (SDK par lots)
description: Les sources en libre-service Adobe Experience Platform (SDK par lots) sont un ensemble d’API de configuration qui vous permettent d’intégrer une source basée sur l’API REST à l’aide de l’API Flow Service pour importer vos données dans Experience Platform.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 8%

---

# Présentation des sources en libre-service (SDK par lots)

Les sources en libre-service Adobe Experience Platform (SDK par lots) sont une structure qui vous permet d’intégrer une source basée sur l’API REST au catalogue des sources Experience Platform à l’aide du [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Les sources en libre-service (SDK par lots) fournissent un ensemble d’API de configuration pour créer votre propre source et importer vos données de lot dans Experience Platform.

Avec les sources en libre-service (SDK par lots), vous pouvez :

* Configurez et intégrez une nouvelle source au catalogue de l’Experience Platform à l’aide du [!DNL Flow Service] API.
* Définissez les spécifications de votre source, y compris les informations relatives aux types d’authentification pris en charge et la manière dont les données de ressource sont récupérées.
* Créer une documentation destinée aux utilisateurs pour votre nouvelle source.

La documentation des sources en libre-service fournit des instructions pour configurer, tester et publier une intégration de source basée sur l’API REST avec Experience Platform et faire en sorte que votre source soit intégrée au catalogue de sources en constante augmentation.

![catalogue](./assets/catalog.png)

## Présentation des sources

Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide de services Experience Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Pour plus d’informations sur les sources et pour obtenir la liste des différentes sources actuellement prises en charge par Experience Platform, voir la section [présentation des sources](../home.md).

## Création d’une source

Grâce aux sources en libre-service, vous pouvez intégrer votre propre source basée sur l’API REST et importer vos données dans Experience Platform avec [!DNL Flow Service]. Vous pouvez intégrer une source au catalogue de sources Experience Platform en créant, en configurant et en envoyant une nouvelle spécification de connexion via le [!DNL Flow Service] API.

Consultez le guide sur la [création d’une nouvelle spécification de connexion](./api/api-overview.md) pour plus d’informations sur l’intégration d’une nouvelle source à Experience Platform.

## Document de votre source

Une fois votre source créée, reportez-vous à la section [guide de documentation](./documentation/doc-overview.md) pour obtenir des instructions sur la manière de documenter votre source via le [!DNL GitHub] ou par l’intermédiaire de votre propre éditeur de texte.

## Aperçu général de la configuration

Le processus étape par étape de configuration de votre source dans Experience Platform est décrit ci-dessous :

* Lisez le [Guide de l’API des sources en libre-service (SDK par lots)](./api/api-overview.md).
   * Lisez le [guide de prise en main](./api/getting-started.md).
   * Suivez le tutoriel sur [création d’une nouvelle spécification de connexion](./api/create.md).
   * Suivez le tutoriel sur [mise à jour de la spécification de connexion](./api/update-connection-specs.md).
   * Suivez le tutoriel sur [Ajout de votre nouvel identifiant de spécification de connexion à une spécification de flux](./api/update-flow-specs.md)
   * [Envoyer votre nouvelle source](./api/submit.md).
* Pour une meilleure compréhension de la structure et des propriétés d’une spécification de connexion, consultez le guide sur [options de configuration pour les sources en libre-service (SDK par lots)](./config/config.md).
   * Lisez le guide sur [configuration de vos spécifications d’authentification](./config/authspec.md) pour mieux comprendre les différents types d’authentification que vous pouvez utiliser pour votre source.
   * Lisez le guide sur [configuration des spécifications source](./config/sourcespec.md) pour plus d’informations sur les différents types de pagination, les formats de planification et les schémas personnalisés qui peuvent être configurés pour votre source.
   * Lisez le guide sur [configuration de vos spécifications d’exploration](./config/explorespec.md) pour plus d’informations sur la manière de définir les paramètres requis pour l’exploration et l’inspection des objets contenus dans votre source.
* Pour commencer à documenter votre source, lisez le [Présentation de la création de documentation pour les sources en libre-service](./documentation/doc-overview.md)
   * Vous pouvez utiliser [modèle de documentation de l’API sources](./documentation/template.md) pour structurer la documentation de votre API.
   * Vous pouvez utiliser [modèle de documentation de l’interface utilisateur de sources](./documentation/ui-template.md) pour structurer la documentation de votre interface utilisateur.
   * Consultez le guide sur la [utilisation de l’interface web GitHub](./documentation/github.md) pour savoir comment créer de la documentation à l’aide de GitHub.
   * Consultez le guide sur la [utilisation d’un éditeur de texte](./documentation/text-editor.md) pour savoir comment créer de la documentation à l’aide de votre ordinateur local.
