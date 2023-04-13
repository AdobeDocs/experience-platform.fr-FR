---
title: Présentation de la source Customer.io
description: Découvrez comment connecter Customer.io à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur en utilisant des webhooks
badge: Version bêta
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 16%

---

# [!DNL Customer.io]

>[!NOTE]
>
>La source [!DNL Customer.io] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données à partir d’applications de diffusion en continu. La prise en charge des fournisseurs de diffusion en continu inclut [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) est une plateforme de messagerie automatisée destinée aux marketeurs qui souhaitent plus de contrôle et de flexibilité pour concevoir et envoyer des emails pilotés par les données, des notifications push, des messages in-app et des SMS.

Le [!DNL Customer.io] source vous permet d’ingérer les schémas d’événement webhook pris en charge et leurs données d’événement associées à partir de [!DNL Customer.io] en utilisant la variable [[!DNL Customer.io] Webhooks de création de rapports](https://customer.io/docs/api/webhooks/).

Les schémas d’événement webhook pris en charge sont les suivants :

* Événements client
* Événements de courrier électronique
* Événements SMS
* Événements de notification push
* Événements de message in-app
* Événements de Slack
* Événements Webhook

Pour obtenir la liste des événements disponibles via des webhooks, reportez-vous à la section [[!DNL Customer.io] Reporting d’événements Webhook](https://customer.io/docs/webhooks/#events) documentation.

## Conditions préalables {#prerequisites}

Avant de pouvoir créer un [!DNL Customer.io] connexion source, vous devez d’abord vous assurer que vous disposez des éléments suivants :

* A [!DNL Customer.io] compte . Si vous n’en avez pas, lisez la variable [[!DNL Customer.io] page d’inscription](https://fly.customer.io/signup) pour enregistrer et créer votre compte.
* Une fois votre compte créé, vous devez également le faire valider. Suivez les étapes décrites dans la section [[!DNL Customer.io] Vérification de compte](https://customer.io/docs/account-verification/) pour terminer le processus.

### Configuration [!DNL Customer.io] Webhook {#set-up-webhook}

Une fois que vous avez créé votre flux de données, vous devez configurer un webhook de création de rapports pour informer Platform sur [!DNL Customer.io] événements . Les webhooks peuvent vous avertir immédiatement lorsque les attributs du client changent ou lorsque des personnes ouvrent vos messages, et envoyer ces informations à vos [!DNL Customer.io] source. Pour plus d’informations, consultez les tutoriels sur [obtention de l’URL de point de terminaison de diffusion en continu](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) et [configuration d’un [!DNL Customer.io] Webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Connexion [!DNL Customer.io] vers Platform {#connect-to-platform}

La documentation ci-dessous fournit des informations sur la création d’un [!DNL Customer.io] connexion en continu à [!DNL Platform] à l’aide des API ou de l’interface utilisateur :

### Connecter [!DNL Customer.io] à Platform à l’aide d’API {#connect-to-platform-using-api}

* [Créer une connexion source et un flux de données à importer [!DNL Customer.io] données vers Platform à l’aide d’API.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Connecter [!DNL Customer.io] à Platform à l’aide de l’interface utilisateur {#connect-to-platform-using-ui}

* [Créer une connexion source et un flux de données à importer [!DNL Customer.io] données vers Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
