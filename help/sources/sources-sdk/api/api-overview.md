---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Guide de l’API des sources en libre-service (SDK par lots)
description: Ce document présente le processus de création d’une source, y compris les étapes de récupération, d’écriture et d’envoi d’une nouvelle spécification de connexion à l’aide de l’API Flow Service.
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 8%

---

# Guide de l’API des sources en libre-service (SDK par lots)

Ce document présente le processus de création d’une source, y compris les étapes d’écriture et d’envoi d’une nouvelle spécification de connexion à l’aide de l’API [[!DNL Flow Service] ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] est utilisé pour collecter et centraliser les données client provenant de diverses sources dans Experience Platform. Le service fournit une interface utilisateur et une API RESTful qui vous permettent de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent d’authentifier vos systèmes tiers, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

L’API [!DNL Flow Service] fournit plusieurs points d’entrée vous permettant de gérer par programmation les spécifications de connexion et de flux pour une nouvelle source que vous intégrez par le biais de sources en libre-service (SDK par lots).

## Créer une spécification de connexion

La première étape de la configuration d’une nouvelle source consiste à créer une spécification de connexion.

Les spécifications de connexion renvoient les propriétés du connecteur d’une source. Ils incluent des spécifications d’authentification liées à la création des connexions de base et source, ainsi qu’un identifiant de spécification de connexion fixe attribué à une source particulière. Les spécifications de connexion sont indépendantes du client et de l’organisation. Une spécification de connexion type contient des informations de base sur une source donnée, ainsi que trois sections distinctes : `authSpec`, `sourceSpec` et `exploreSpec`.

Pour obtenir des instructions détaillées, consultez le guide sur la [création d’une spécification de connexion](./create.md). Pour plus d’informations sur les propriétés et les valeurs utilisées pour une spécification de connexion, y compris des détails sur la configuration des spécifications d’authentification, de source et d’exploration, voir le document [Options de configuration](../config/config.md).

## Mettre à jour les spécifications de flux

Une fois que vous avez créé une spécification de connexion, vous devez ajouter la spécification de flux `RestStorageToAEP` pour permettre à votre source de créer un flux de données.

Les spécifications de flux contiennent des informations qui définissent un flux, y compris les identifiants de connexion source et cible pris en charge, les spécifications de transformation qui doivent être appliquées aux données et les paramètres de planification requis pour générer un flux.

Pour obtenir des instructions détaillées, consultez le guide sur la [mise à jour des spécifications de flux](./update-flow-specs.md).

## Mettre à jour votre spécification de connexion

Vous pouvez mettre à jour votre spécification de connexion en effectuant une requête PUT à l’API [!DNL Flow Service]. Pour plus d’informations, consultez le guide sur la [mise à jour des spécifications de connexion](./update-connection-specs.md).

## Envoyer votre source

Pour envoyer votre source en vue de son intégration à Experience Platform, vous devez d’abord exécuter l’ensemble du workflow de l’API [!DNL Flow Service] pour les sources afin de vous assurer que votre source fonctionne correctement. Si votre source s’exécute correctement, vous pouvez continuer et contacter votre représentant Adobe pour vérification et promotion. Pour plus d’informations, consultez le guide sur le [test et envoi de votre source](./submit.md)

## Étapes suivantes

Pour commencer à utiliser l’API [!DNL Flow Service] et créer une source par le biais de sources en libre-service (SDK par lots), lisez le guide [prise en main](./getting-started.md) puis sélectionnez l’un des guides des points d’entrée pour savoir comment utiliser des points d’entrée spécifiques.
