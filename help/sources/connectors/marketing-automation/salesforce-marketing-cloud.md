---
keywords: Experience Platform;accueil;rubriques les plus consultées;Salesforce marketing cloud;Marketing Cloud Salesforce;automatisation du marketing
solution: Experience Platform
title: Présentation de la source de Marketing Cloud Salesforce
topic-legacy: overview
description: Découvrez comment connecter le Marketing Cloud Salesforce à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
source-git-commit: 6876ad592e4924dc884568899662dfa9c8eecc62
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 13%

---

# (version bêta) [!DNL Salesforce Marketing Cloud]

>[!NOTE]
>
>Le [!DNL Salesforce Marketing Cloud] La source est en version bêta. Voir [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

[!DNL Experience Platform] prend en charge l’ingestion de données provenant de systèmes tiers d’automatisation du marketing. La prise en charge des fournisseurs d’automatisation marketing inclut [!DNL Salesforce Marketing Cloud].

## Conditions préalables

Avant de pouvoir connecter votre [!DNL Salesforce Marketing Cloud] source vers Platform, vous devez vous assurer que : **portées d’autorisation** sont configurés pour [!DNL Salesforce Marketing Cloud] combinaison client ID et client secret :

* `campaign_read`
* `list_and_subscribers_read`

Vous pouvez demander des portées en effectuant un appel à la fonction `v2/userinfo` de la ressource [!DNL Salesforce Marketing Cloud] API. Voir [[!DNL Salesforce Marketing Cloud] Document Portées d’autorisation d’intégration d’API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html) pour savoir comment demander et comparer des portées.

Pour plus d’informations sur les portées, y compris une liste de leurs autorisations et comportements associés, voir ceci [[!DNL Salesforce Marketing Cloud] Document de l’API REST](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html).

## LISTE AUTORISÉE d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou des performances peuvent se produire lors de l’utilisation de sources. Voir [LISTE AUTORISÉE d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Connexion [!DNL Salesforce Marketing Cloud] vers Platform à l’aide d’API

La documentation ci-dessous fournit des informations sur la connexion. [!DNL Salesforce Marketing Cloud] vers Platform à l’aide d’API :

* [Création d’une connexion de base de Marketing Cloud Salesforce à l’aide de l’API Flow Service](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Explorer la structure et le contenu des données d’une source d’automatisation marketing à l’aide de l’API Flow Service](../../tutorials/api/explore/marketing-automation.md)
* [Création d’un flux de données pour une source d’automatisation marketing à l’aide de l’API Flow Service](../../tutorials/api/collect/marketing-automation.md)

## Connexion [!DNL Salesforce Marketing Cloud] vers Platform à l’aide de l’interface utilisateur

La documentation ci-dessous fournit des informations sur la connexion. [!DNL Salesforce Marketing Cloud] vers Platform à l’aide de l’interface utilisateur :

* [Création d’une connexion source de Marketing Cloud Salesforce dans l’interface utilisateur](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Création d’un flux de données pour une connexion à la source d’automatisation marketing dans l’interface utilisateur](../../tutorials/ui/dataflow/marketing-automation.md)
