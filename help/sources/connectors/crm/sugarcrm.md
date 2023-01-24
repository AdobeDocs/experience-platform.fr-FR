---
title: Présentation de la source SugarCRM
description: Découvrez comment connecter SugarCRM à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
source-git-commit: 666767d45ca24f1c3fbbc0265d5f5c26a904e4b2
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 43%

---

# (version bêta) [!DNL SugarCRM]

>[!NOTE]
>
>La source [!DNL SugarCRM] est en version Beta. Voir la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données à partir d’une application CRM tierce. La prise en charge des fournisseurs de gestion de la relation client inclut [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) est un système de gestion de la relation client (CRM). [!DNL SugarCRM]Les fonctionnalités de comprennent l’automatisation des forces de vente, les campagnes marketing, l’assistance clientèle, la collaboration, la gestion de la relation client mobile, la gestion de la relation client (CRM) des réseaux sociaux et la création de rapports.

Le [!DNL SugarCRM] source vous permet d’ingérer des données de comptes, de contacts et d’événements à partir des points de terminaison d’API suivants :

* [Comptes](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [Contacts](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [Événements](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)


[!DNL SugarCRM] utilise des jetons au porteur comme mécanisme d’authentification pour communiquer avec le [!DNL SugarCRM] API de compte et de contact et [!DNL SugarCRM] API d’événements.

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Conditions préalables

Avant de pouvoir créer un [!DNL SugarCRM] connexion source, vous devez d’abord vous assurer que vous disposez des éléments suivants :

* A [!DNL SugarMarket] compte . Vous devez contacter votre [!DNL SugarCRM] gestionnaire de compte pour obtenir un [!DNL SugarMarket] si vous n’en avez pas déjà un.

* Nom d’utilisateur et compte d’API uniques, séparés de tout compte d’utilisateur associé au processus marketing ou de vente. Cette combinaison unique de nom d’utilisateur et de compte doit disposer d’autorisations d’accès API. Pour plus d’informations sur le processus de configuration d’un compte, consultez la page [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro) documentation.

## Connecter [!DNL SugarCRM Accounts & Contacts] à Platform

* [Créez une connexion source pour importer [!DNL SugarCRM Accounts & Contacts] les données dans Platform à l’aide d’API](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [Créer une connexion source à importer [!DNL SugarCRM Accounts & Contacts] données vers Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [Créer un flux de données pour une source CRM à l’aide de l’API Flow Service](../../tutorials/api/collect/crm.md)


## Connecter [!DNL SugarCRM Events] à Platform

* [Créez une connexion source pour importer [!DNL SugarCRM Events] les données dans Platform à l’aide d’API](../../tutorials/api/create/crm/sugarcrm-events.md).
* [Créer une connexion source à importer [!DNL SugarCRM Events] données vers Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Créer un flux de données pour une connexion source CRM dans l’interface utilisateur](../../tutorials/ui/dataflow/crm.md)
