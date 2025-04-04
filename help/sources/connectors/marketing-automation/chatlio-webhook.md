---
title: Présentation de Chatlio Source
description: Découvrez comment connecter Chatlio à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur en utilisant des webhooks
badge: Beta
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 7%

---

# [!DNL Chatlio]

>[!NOTE]
>
>La source [!DNL Chatlio] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données à partir d’applications de diffusion en continu. La prise en charge des fournisseurs de streaming inclut [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) est une application de chat en direct qui est entièrement intégrée à [!DNL Slack] et qui permet à plusieurs agents d’assistance d’aider simultanément un visiteur individuel du site. [!DNL Chatlio] utilise le [!DNL Chatio Zapier App] pour [!DNL Chatlio] connecter à plus de 2 000 applications et services différents.

La source [!DNL Chatlio] vous permet d’ingérer des schémas d’événement webhook pris en charge et leurs données d’événement associées à partir de [!DNL Chatlio.com] à l’aide des [[!DNL Chatlio] Webhooks](https://chatlio.com/docs/webhooks/).

Les webhooks pris en charge sont les suivants :

* Exportation des transcriptions de conversation
* Exporter des messages hors ligne
* Une nouvelle conversation a commencé
* Le visiteur n’a pas reçu de réponse à temps.
* Retour d’informations du visiteur laissé après une conversation

## Conditions préalables {#prerequisites}

Avant de pouvoir créer une connexion source [!DNL Chatlio], vous devez d’abord vous assurer que vous disposez des éléments suivants :

* Un compte [!DNL Chatlio]. Si vous n’en avez pas déjà un, visitez la [[!DNL Chatlio] page d’inscription](https://chatlio.com/app/#/signup) pour vous inscrire et créer votre compte.
* Une fois que vous avez enregistré un compte, suivez la [[!DNL Chatlio] documentation de configuration](https://chatlio.com/docs/setup/) pour terminer la configuration de votre compte.

### Configuration [!DNL Chatlio] webhook {#set-up-webhook}

Une fois le flux de données créé, vous devez configurer un webhook pour informer Experience Platform des événements [!DNL Chatlio]. Les Webhooks peuvent vous informer immédiatement lorsque les attributs du client changent ou lorsque des personnes ouvrent vos messages et envoyer ces informations à votre source de [!DNL Chatlio].

Pour plus d’informations, consultez les tutoriels sur [l’obtention de l’URL de point d’entrée de diffusion en continu](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) et [la configuration d’un  [!DNL Chatlio]  Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Connexion de [!DNL Chatlio] à Experience Platform {#connect-to-platform}

La documentation ci-dessous fournit des informations sur la création d’un connecteur de diffusion en continu [!DNL Chatlio] pour se connecter à [!DNL Experience Platform] à l’aide d’API ou de l’interface utilisateur :

### Connexion de [!DNL Chatlio] à Experience Platform à l’aide d’API {#connect-to-platform-using-api}

* [Créez une connexion source pour importer  [!DNL Chatlio]  données dans Experience Platform à l’aide d’API.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Connexion d’[!DNL Chatlio] à Experience Platform à l’aide de l’interface utilisateur {#connect-to-platform-using-ui}

* [Créer une connexion source pour importer des données  [!DNL Chatlio]  Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
