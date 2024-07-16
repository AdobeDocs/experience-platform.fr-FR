---
title: Présentation de Customer.io Source
description: Découvrez comment connecter Customer.io à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur en utilisant des webhooks
badge: Version bêta
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 17%

---

# [!DNL Customer.io]

>[!NOTE]
>
>La source [!DNL Customer.io] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données à partir d’applications de diffusion en continu. [!DNL Customer.io] est compatible avec les fournisseurs de diffusion en continu.

[[!DNL Customer.io]](https://customer.io/) est une plateforme de messagerie automatisée destinée aux marketeurs qui souhaitent plus de contrôle et de flexibilité pour concevoir et envoyer des emails pilotés par les données, des notifications push, des messages in-app et des SMS.

La source [!DNL Customer.io] vous permet d’ingérer des schémas d’événement webhook pris en charge et les données d’événement associées provenant de [!DNL Customer.io] à l’aide des [[!DNL Customer.io]  webhooks de création de rapports](https://customer.io/docs/api/webhooks/).

Les schémas d’événement webhook pris en charge sont les suivants :

* Événements client
* Événements de courrier électronique
* Événements SMS
* Événements de notification push
* Événements de message in-app
* Événements de Slack
* Événements Webhook

Pour obtenir la liste des événements disponibles via les webhooks, reportez-vous à la documentation [[!DNL Customer.io] Reporting Webhook events](https://customer.io/docs/webhooks/#events) .

## Conditions préalables {#prerequisites}

Avant de pouvoir créer une connexion source [!DNL Customer.io], vous devez d’abord vous assurer que vous disposez des éléments suivants :

* Un compte [!DNL Customer.io]. Si vous n’en avez pas, lisez la [[!DNL Customer.io] page d’inscription](https://fly.customer.io/signup) pour vous enregistrer et créer votre compte.
* Une fois votre compte créé, vous devez également le faire valider. Suivez les étapes décrites sur la page [[!DNL Customer.io] Vérification de compte](https://customer.io/docs/account-verification/) pour terminer le processus.

### Configuration de [!DNL Customer.io] Webhook {#set-up-webhook}

Une fois que vous avez créé votre flux de données, vous devez configurer un webhook de création de rapports pour informer Platform des événements [!DNL Customer.io]. Les webhooks peuvent vous avertir immédiatement lorsque les attributs du client changent ou lorsque des personnes ouvrent vos messages, et envoyer ces informations à votre source [!DNL Customer.io]. Pour plus d’informations, lisez les tutoriels sur [obtention de l’URL de votre point de terminaison de diffusion en continu](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) et [configuration d’un  [!DNL Customer.io] webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Connexion de [!DNL Customer.io] à Platform {#connect-to-platform}

La documentation ci-dessous fournit des informations sur la création d’une connexion en continu [!DNL Customer.io] pour se connecter à [!DNL Platform] à l’aide d’API ou de l’interface utilisateur :

### Connecter [!DNL Customer.io] à Platform à l’aide d’API {#connect-to-platform-using-api}

* [Créez une connexion source et un flux de données pour importer les données [!DNL Customer.io] vers Platform à l’aide d’API.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Connecter [!DNL Customer.io] à Platform à l’aide de l’interface utilisateur {#connect-to-platform-using-ui}

* [Créez une connexion source et un flux de données pour importer des données  [!DNL Customer.io] vers Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
