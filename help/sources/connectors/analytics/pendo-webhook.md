---
title: Présentation de Pendo Source
description: Découvrez comment connecter Pendo à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur en utilisant des webhooks.
badge: Beta
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
TQID: https://experienceleague.adobe.com/K3ehdkUA-4pw7qaiCKD2jb-el-DXptmbGWLDhIZnT7c
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 394
ht-degree: 13%

---

# [!DNL Pendo]

>[!NOTE]
>
>La source [!DNL Pendo] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’une application d’analyse tierce. La prise en charge des fournisseurs d’analyses inclut [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) est une application d’analyse de produits conçue pour aider les éditeurs de logiciels à développer des produits qui interagissent avec les clients. L’application permet aux concepteurs de logiciels d’intégrer leurs produits à un large éventail d’outils qui peuvent aboutir à une meilleure expérience du produit pour les utilisateurs et à de nouvelles informations pour l’équipe produit.

La source [!DNL Pendo] vous permet d’ingérer des schémas d’événement webhook pris en charge et leurs données d’événement associées à partir de [!DNL Pendo.io] à l’aide des [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). La source [!DNL Pendo] fonctionne avec les Webhooks d’URL [!DNL Pendo].

Les webhooks pris en charge sont les suivants :

* [Guide](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) affiché
* [Sondage](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) affiché/envoyé
* [Net Promoter Score](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) affiché/envoyé

## Conditions préalables {#prerequisites}

Avant de pouvoir créer une connexion source [!DNL Pendo], vous devez d’abord vous assurer que vous disposez des éléments suivants :

Un compte [!DNL Pendo]. Si vous n’en avez pas encore, consultez la page [[!DNL Pendo] inscription](https://app.pendo.io/register) pour vous enregistrer et créer votre compte.

### Configurer [!DNL Pendo] Webhook {#set-up-webhook}

Une fois le flux de données créé, vous devez configurer un webhook pour informer Experience Platform des événements [!DNL Pendo]. [!DNL Pendo] Les Webhooks peuvent envoyer des notifications en temps réel à d’autres services lorsque certains événements se produisent et envoyer ces informations à votre source d’[!DNL Pendo]. Pour plus d’informations, consultez les tutoriels sur [l’obtention de l’URL de point d’entrée de diffusion en continu](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) et [la configuration d’un  [!DNL Pendo]  Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Connexion de [!DNL Pendo] à Experience Platform {#connect-to-platform}

La documentation ci-dessous fournit des informations sur la création d’un connecteur de diffusion en continu [!DNL Pendo] pour se connecter à [!DNL Experience Platform] à l’aide d’API ou de l’interface utilisateur :

### Connexion de [!DNL Pendo] à Experience Platform à l’aide d’API {#connect-to-platform-using-api}

* [Créez une connexion source pour importer  [!DNL Pendo]  données dans Experience Platform à l’aide d’API.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Connexion d’[!DNL Pendo] à Experience Platform à l’aide de l’interface utilisateur {#connect-to-platform-using-ui}

* [Créer une connexion source pour importer des données  [!DNL Pendo]  Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/analytics/pendo-webhook.md)
