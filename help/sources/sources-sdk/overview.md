---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
solution: Experience Platform
title: Présentation du SDK des sources (version bêta)
topic-legacy: overview
description: Le SDK Sources de Adobe Experience Platform est un ensemble d’API de configuration qui vous permettent d’intégrer une source basée sur l’API REST à l’aide de l’API Flow Service pour importer vos données dans Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 3d510876cfdd8ac3045dae8df6fcf6045de2538b
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 8%

---

# Présentation du SDK des sources (version bêta)

>[!IMPORTANT]
>
>Le SDK Sources est actuellement en version bêta et votre entreprise n’y a peut-être pas encore accès. Les fonctionnalités décrites dans cette documentation peuvent faire l’objet de modifications.

Le SDK Sources de Adobe Experience Platform est un ensemble d’API de configuration qui vous permettent d’intégrer une source basée sur l’API REST à l’aide du [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) pour importer vos données dans Experience Platform.

Avec le SDK Sources, vous pouvez :

* Configurez une nouvelle source dans le catalogue de Platform, avec les fonctionnalités de création, de lecture, de mise à jour et de suppression à l’aide de la [!DNL Flow Service] API.
* Définissez les spécifications de votre source, y compris les informations relatives aux types d’authentification pris en charge et la manière dont les données de ressource sont récupérées.
* Créez une documentation destinée aux utilisateurs pour votre nouvelle source.

La documentation du SDK Sources fournit des instructions pour vous permettre d’utiliser le SDK Sources de Adobe Experience Platform pour configurer, tester et publier une intégration de source basée sur l’API REST avec Platform, et faire en sorte que votre source soit intégrée au catalogue de sources en constante augmentation.

![catalogue](./assets/catalog.png)

## Présentation des sources

Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Pour plus d’informations sur les sources et pour obtenir la liste des différentes sources actuellement prises en charge sur Platform, voir le [présentation des sources](../home.md).

## Création d’une source

Grâce au SDK Sources, vous pouvez intégrer votre propre source basée sur l’API REST et importer vos données dans Platform avec [!DNL Flow Service]. Le SDK Sources vous permet d’intégrer une nouvelle source à Platform en créant et en envoyant une nouvelle spécification de connexion via le [!DNL Flow Service] API.

Consultez le guide sur la [création d’une nouvelle spécification de connexion](./api/api-overview.md) pour plus d’informations sur la manière d’intégrer une nouvelle source à Platform.

## Document de votre source

Une fois votre source créée, reportez-vous à la section [guide de documentation](./documentation/doc-overview.md) pour obtenir des instructions sur la manière de documenter votre source via le [!DNL GitHub] ou par l’intermédiaire de votre propre éditeur de texte.

## Processus de haut niveau

Le processus étape par étape de configuration de votre source dans Experience Platform est décrit ci-dessous :

* Lisez le [Guide de l’API du SDK Sources](./api/api-overview.md);
   * Lisez le [guide de prise en main](./api/getting-started.md);
   * Suivez le tutoriel sur [création d’une nouvelle spécification de connexion](./api/create.md);
   * Suivez le tutoriel sur [mise à jour de la spécification de connexion](./api/update-connection-specs.md);
   * Suivez le tutoriel sur [Ajout de votre nouvel identifiant de spécification de connexion à une spécification de flux](./api/update-flow-specs.md)
   * [Envoyer votre nouvelle source](./api/submit.md).
* Pour une meilleure compréhension de la structure et des propriétés d’une spécification de connexion, consultez le guide sur [options de configuration du SDK Sources](./config/config.md);
   * Consultez le guide sur la [configuration de vos spécifications d’authentification](./config/authspec.md);
   * Consultez le guide sur la [configuration des spécifications source](./config/sourcespec.md);
   * Consultez le guide sur la [configuration de vos spécifications d’exploration](./config/explorespec.md);
* Pour commencer à documenter votre source, reportez-vous à la section [Présentation de la création de la documentation pour le SDK Sources](./documentation/doc-overview.md)
   * Vous pouvez utiliser [modèle de documentation sources](./documentation/template.md) pour structurer votre documentation ;
   * Consultez le guide sur la [utilisation de l’interface web GitHub](./documentation/github.md) pour savoir comment créer de la documentation à l’aide de GitHub ;
   * Consultez le guide sur la [utilisation d’un éditeur de texte](./documentation/text-editor.md) pour savoir comment créer de la documentation à l’aide de votre ordinateur local.

