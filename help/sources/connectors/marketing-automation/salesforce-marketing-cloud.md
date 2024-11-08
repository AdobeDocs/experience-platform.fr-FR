---
solution: Experience Platform
title: Présentation de Salesforce Marketing Cloud Source
description: Découvrez comment connecter Salesforce Marketing Cloud à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 42%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>La source [!DNL Salesforce Marketing Cloud] sera abandonnée fin mai 2025.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant de systèmes tiers d’automatisation du marketing. [!DNL Salesforce Marketing Cloud] est compatible avec les fournisseurs d’automatisation marketing.

## Conditions préalables

Avant de pouvoir connecter votre source [!DNL Salesforce Marketing Cloud] à Platform, vous devez vous assurer que les **portées d’autorisation** suivantes sont configurées sur votre combinaison [!DNL Salesforce Marketing Cloud] d’ID client et de secret client :

* `campaign_read`
* `list_and_subscribers_read`

Vous pouvez demander des portées en effectuant un appel vers la ressource `v2/userinfo` de l’API [!DNL Salesforce Marketing Cloud]. Consultez le [[!DNL Salesforce Marketing Cloud] document Portées d’autorisation d’intégration d’API](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) pour obtenir des instructions sur la demande et la comparaison des portées.

Pour plus d’informations sur les portées, y compris une liste de leurs autorisations et comportements associés, consultez ce [[!DNL Salesforce Marketing Cloud] document de l’API REST](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>L’ingestion d’objets personnalisés n’est actuellement pas prise en charge par l’intégration de la source [!DNL Salesforce Marketing Cloud].

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Connecter [!DNL Salesforce Marketing Cloud] à Platform à l’aide d’API

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Salesforce Marketing Cloud] à Platform à l’aide d’API :

* [Création d’une connexion de base de Marketing Cloud Salesforce à l’aide de l’API Flow Service](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
* [Créer un flux de données pour une source d’automatisation du marketing à l’aide de l’API Flow Service](../../tutorials/api/collect/marketing-automation.md)

## Connecter [!DNL Salesforce Marketing Cloud] à Platform à l’aide de l’interface utilisateur

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Salesforce Marketing Cloud] à Platform à l’aide de l’interface utilisateur :

* [Création d’une connexion source au Marketing Cloud Salesforce dans l’interface utilisateur](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Créer un flux de données pour une connexion à une source d’automatisation du marketing dans l’interface utilisateur](../../tutorials/ui/dataflow/marketing-automation.md)
