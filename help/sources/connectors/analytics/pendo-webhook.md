---
title: Présentation de la source Pendo
description: Découvrez comment connecter Pendo à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur en utilisant des webhooks
badge: Version Beta
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 20%

---

# [!DNL Pendo]

>[!NOTE]
>
>La source [!DNL Pendo] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données à partir d’une application d’analyse tierce. La prise en charge des fournisseurs d’analyses inclut [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) est une application product-analytics conçue pour aider les sociétés de logiciels à développer des produits qui interagissent avec leurs clients. L’application permet aux développeurs de logiciels d’incorporer leurs produits à un large éventail d’outils qui peuvent à la fois offrir une meilleure expérience produit aux utilisateurs et de nouvelles informations pour l’équipe produit.

La variable [!DNL Pendo] source vous permet d’ingérer les schémas d’événement webhook pris en charge et leurs données d’événement associées à partir de [!DNL Pendo.io] en utilisant la variable [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). La variable [!DNL Pendo] source fonctionne avec [!DNL Pendo] Les webhooks d’URL.

Les webhooks pris en charge sont les suivants :

* [Guide](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) Affiché
* [Sondage](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) Affiché/Envoyé
* [Score du Net Promoteur](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) Affiché/Envoyé

## Conditions préalables {#prerequisites}

Avant de pouvoir créer un [!DNL Pendo] connexion source, vous devez d’abord vous assurer que vous disposez des éléments suivants :

A [!DNL Pendo] compte . Si vous n’en avez pas déjà un, la fonction [[!DNL Pendo] register](https://app.pendo.io/register) pour enregistrer et créer votre compte.

### Configuration [!DNL Pendo] Webhook {#set-up-webhook}

Une fois que vous avez créé votre flux de données, vous devez configurer un webhook pour informer Platform sur [!DNL Pendo] événements . [!DNL Pendo] Les webhooks peuvent envoyer des notifications en temps réel à d’autres services lorsque certains événements se produisent, puis envoyer ces informations à vos [!DNL Pendo] source. Pour plus d’informations, consultez les tutoriels sur [obtention de l’URL de point de terminaison de diffusion en continu](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) et [configuration d’un [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Connexion [!DNL Pendo] vers Platform {#connect-to-platform}

La documentation ci-dessous fournit des informations sur la création d’un [!DNL Pendo] connecteur de diffusion en continu pour se connecter à [!DNL Platform] à l’aide des API ou de l’interface utilisateur :

### Connecter [!DNL Pendo] à Platform à l’aide d’API {#connect-to-platform-using-api}

* [Créez une connexion source pour importer [!DNL Pendo] les données dans Platform à l’aide d’API.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Connecter [!DNL Pendo] à Platform à l’aide de l’interface utilisateur {#connect-to-platform-using-ui}

* [Créer une connexion source à importer [!DNL Pendo] données vers Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/analytics/pendo-webhook.md)
