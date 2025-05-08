---
solution: Experience Platform
title: Présentation de Salesforce Marketing Cloud Source
description: Découvrez comment connecter Salesforce Marketing Cloud à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-04-29T00:00:00Z
source-git-commit: ce96dbc64845fddb40ebee709828c56d51a6c6ba
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 14%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>La source [!DNL Salesforce Marketing Cloud] sera abandonnée en janvier 2026. Une nouvelle source sera publiée plus tard cette année comme alternative. Une fois la nouvelle source publiée, vous devez planifier la migration vers la nouvelle source en créant de nouvelles connexions de compte et de nouveaux flux de données avant la fin du mois de janvier 2026.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant de systèmes d’automatisation marketing tiers. La prise en charge des fournisseurs d’automatisation marketing inclut [!DNL Salesforce Marketing Cloud].

## Prérequis

Avant de pouvoir connecter votre source de [!DNL Salesforce Marketing Cloud] à Experience Platform, vous devez vous assurer que les **portées d’autorisation** suivantes sont configurées sur votre combinaison d’identifiant client et de secret client [!DNL Salesforce Marketing Cloud] :

* `campaign_read`
* `list_and_subscribers_read`

Vous pouvez demander des portées en effectuant un appel à la ressource `v2/userinfo` de l’API [!DNL Salesforce Marketing Cloud]. Consultez le document [[!DNL Salesforce Marketing Cloud] Portées des autorisations d’intégration des API](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) pour obtenir des conseils sur la requête et la comparaison des portées.

Pour plus d’informations sur les portées, y compris une liste de leurs autorisations et comportements associés, consultez ce document [[!DNL Salesforce Marketing Cloud] API REST](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>L’ingestion d’objets personnalisés n’est actuellement pas prise en charge par l’intégration source [!DNL Salesforce Marketing Cloud].

## Liste autorisée d’adresses IP

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform. Placer sur la liste autorisée Pour plus d’informations, consultez le guide sur la [connexion des adresses IP à Experience Platform](../../ip-address-allow-list.md).

>[!WARNING]
>
>Placer sur la liste autorisée Si vous n’ajoutez pas les adresses IP nécessaires à votre, votre compte [!DNL Salesforce Marketing Cloud] ne se connectera pas à Experience Platform.

## Connexion de [!DNL Salesforce Marketing Cloud] à Experience Platform à l’aide d’API

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Salesforce Marketing Cloud] à Experience Platform à l’aide d’API :

* [Créer une connexion de base Salesforce Marketing Cloud à l’aide de l’API Flow Service](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
* [Créer un flux de données pour une source d’automatisation du marketing à l’aide de l’API Flow Service](../../tutorials/api/collect/marketing-automation.md)

## Connexion d’[!DNL Salesforce Marketing Cloud] à Experience Platform à l’aide de l’interface utilisateur

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Salesforce Marketing Cloud] à Experience Platform à l’aide de l’interface utilisateur :

* [Créer une connexion source Salesforce Marketing Cloud dans l’interface utilisateur](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Créer un flux de données pour une connexion à une source d’automatisation du marketing dans l’interface utilisateur](../../tutorials/ui/dataflow/marketing-automation.md)
