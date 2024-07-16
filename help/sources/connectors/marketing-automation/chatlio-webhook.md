---
title: Présentation de Chatlio Source
description: Découvrez comment connecter Chatlio à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur en utilisant des webhooks
badge: Version bêta
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 18%

---

# [!DNL Chatlio]

>[!NOTE]
>
>La source [!DNL Chatlio] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données à partir d’applications de diffusion en continu. [!DNL Chatlio] est compatible avec les fournisseurs de diffusion en continu.

[[!DNL Chatlio]](https://chatlio.com/) est une application de chat en direct qui est entièrement intégrée à [!DNL Slack] et qui facilite l’utilisation de plusieurs agents de support pour aider simultanément un visiteur individuel du site. [!DNL Chatlio] utilise le [!DNL Chatio Zapier App] pour se connecter à [!DNL Chatlio] avec plus de 2 000 applications et services différents.

La source [!DNL Chatlio] vous permet d’ingérer les schémas d’événement webhook pris en charge et les données d’événement associées provenant de [!DNL Chatlio.com] à l’aide des [[!DNL Chatlio]  webhooks](https://chatlio.com/docs/webhooks/).

Les webhooks pris en charge sont les suivants :

* Exporter des transcriptions de conversation
* Exporter des messages hors ligne
* Une nouvelle conversation a commencé
* Le visiteur n’a pas reçu de réponse à temps
* Commentaires du visiteur après une conversation

## Conditions préalables {#prerequisites}

Avant de pouvoir créer une connexion source [!DNL Chatlio], vous devez d’abord vous assurer que vous disposez des éléments suivants :

* Un compte [!DNL Chatlio]. Si vous n’en avez pas déjà un, rendez-vous sur la [[!DNL Chatlio] page d’inscription](https://chatlio.com/app/#/signup) pour vous enregistrer et créer votre compte.
* Après avoir enregistré un compte, suivez la [[!DNL Chatlio] documentation de configuration](https://chatlio.com/docs/setup/) pour terminer la configuration de votre compte.

### Configuration de [!DNL Chatlio] webhook {#set-up-webhook}

Une fois que vous avez créé votre flux de données, vous devez configurer un webhook pour informer Platform des événements [!DNL Chatlio]. Les webhooks peuvent vous avertir immédiatement lorsque les attributs du client changent ou lorsque des personnes ouvrent vos messages et envoient ces informations à votre source [!DNL Chatlio].

Pour plus d’informations, lisez les tutoriels sur [obtention de l’URL de votre point de terminaison de diffusion en continu](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) et [configuration d’un  [!DNL Chatlio] webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Connecter [!DNL Chatlio] à Platform {#connect-to-platform}

La documentation ci-dessous fournit des informations sur la création d’un connecteur de diffusion en continu [!DNL Chatlio] pour se connecter à [!DNL Platform] à l’aide d’API ou de l’interface utilisateur :

### Connecter [!DNL Chatlio] à Platform à l’aide d’API {#connect-to-platform-using-api}

* [Créez une connexion source pour importer des données [!DNL Chatlio] vers Platform à l’aide d’API.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Connecter [!DNL Chatlio] à Platform à l’aide de l’interface utilisateur {#connect-to-platform-using-ui}

* [Créez une connexion source pour importer des données [!DNL Chatlio] vers Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
