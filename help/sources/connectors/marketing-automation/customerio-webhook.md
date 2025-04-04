---
title: Présentation de Customer.io Source
description: Découvrez comment connecter Customer.io à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur en utilisant des webhooks
badge: Beta
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 6%

---

# [!DNL Customer.io]

>[!NOTE]
>
>La source [!DNL Customer.io] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’applications de diffusion en continu. La prise en charge des fournisseurs de streaming inclut [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) est une plateforme de messagerie automatisée destinée aux marketeurs qui souhaitent plus de contrôle et de flexibilité pour concevoir et envoyer des e-mails pilotés par les données, des notifications push, des messages in-app et des SMS.

La source [!DNL Customer.io] vous permet d’ingérer des schémas d’événement webhook pris en charge et leurs données d’événement associées à partir de [!DNL Customer.io] à l’aide des [[!DNL Customer.io] Webhooks de création de rapports](https://customer.io/docs/api/webhooks/).

Les schémas d’événement webhook pris en charge sont les suivants :

* Événements client
* Événements d’e-mail
* Événements SMS
* Événements de notification push
* Événements De Message In-App
* Événements Slack
* Événements Webhook

Pour obtenir la liste des événements disponibles par le biais de webhooks, reportez-vous à la documentation [[!DNL Customer.io] Reporting des événements Webhook](https://customer.io/docs/webhooks/#events).

## Conditions préalables {#prerequisites}

Avant de pouvoir créer une connexion source [!DNL Customer.io], vous devez d’abord vous assurer que vous disposez des éléments suivants :

* Un compte [!DNL Customer.io]. Si vous n’en avez pas, lisez la [[!DNL Customer.io] page d’inscription](https://fly.customer.io/signup) pour vous inscrire et créer votre compte.
* Après avoir créé votre compte, vous devrez également le faire valider. Suivez les étapes décrites sur la page [[!DNL Customer.io] Vérification du compte](https://customer.io/docs/account-verification/) pour terminer le processus.

### Configurer [!DNL Customer.io] Webhook {#set-up-webhook}

Une fois votre flux de données créé, vous devez configurer un Webhook de création de rapports pour informer Experience Platform des événements [!DNL Customer.io]. Les Webhooks peuvent vous avertir immédiatement lorsque les attributs du client changent ou lorsque des personnes ouvrent vos messages et envoyer ces informations à votre source de [!DNL Customer.io]. Pour plus d’informations, consultez les tutoriels sur [l’obtention de l’URL de point d’entrée de diffusion en continu](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) et [la configuration d’un  [!DNL Customer.io]  Webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Connexion de [!DNL Customer.io] à Experience Platform {#connect-to-platform}

La documentation ci-dessous fournit des informations sur la création d’une connexion en continu [!DNL Customer.io] pour se connecter à [!DNL Experience Platform] à l’aide d’API ou de l’interface utilisateur :

### Connexion de [!DNL Customer.io] à Experience Platform à l’aide d’API {#connect-to-platform-using-api}

* [Créez une connexion source et un flux de données pour importer  [!DNL Customer.io]  données dans Experience Platform à l’aide d’API.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Connexion d’[!DNL Customer.io] à Experience Platform à l’aide de l’interface utilisateur {#connect-to-platform-using-ui}

* [Créer une connexion source et un flux de données pour importer des données  [!DNL Customer.io]  Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
