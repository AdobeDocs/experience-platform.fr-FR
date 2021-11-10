---
keywords: Experience Platform;accueil;rubriques populaires;REST générique;repos générique
solution: Experience Platform
title: Présentation générique du connecteur source de l’API REST
topic-legacy: overview
description: Découvrez comment connecter l’API REST générique à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
source-git-commit: 0c7bb3d6f0a1bc4154bff0e4d79cc4c3c0b0ab71
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 8%

---

# (version bêta) [!DNL Generic REST API]

>[!NOTE]
>
>Le [!DNL Generic REST API] La source est en version bêta. Voir [Présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs bêta-étiquetés.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

Platform prend en charge l’ingestion de données à partir d’applications de protocoles, y compris [!DNL Generic REST API].

Le [!DNL Generic REST API] source vous permet d’importer dans Platform des données provenant d’applications REST. [!DNL Generic REST API] prend en charge l’authentification de base et l’authentification basée sur le code d’actualisation OAuth 2.

## LISTE AUTORISÉE d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou des performances peuvent se produire lors de l’utilisation de sources. Voir [LISTE AUTORISÉE d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

La documentation ci-dessous fournit des informations sur la connexion à un [!DNL Generic REST API] source vers Platform à l’aide des API.

## Connexion [!DNL Generic REST API] to [!DNL Platform] utilisation des API

- [Créer une connexion de base d’API REST générique à l’aide de l’API Flow Service](../../tutorials/api/create/protocols/generic-rest.md)
- [Explorer la structure de données et le contenu d’une source de protocoles à l’aide de l’API Flow Service](../../tutorials/api/explore/protocols.md)
- [Création d’un flux de données pour une source de protocoles à l’aide de l’API Flow Service](../../tutorials/api/collect/protocols.md)