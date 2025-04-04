---
title: Présentation de SugarCRM Source
description: Découvrez comment connecter SugarCRM à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
last-substantial-update: 2023-08-23T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 28%

---

# [!DNL SugarCRM]

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’une application CRM tierce. La prise en charge des fournisseurs de gestion de la relation client inclut [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) est un système de gestion de la relation client (GRC). Les fonctionnalités d’[!DNL SugarCRM] comprennent l’automatisation de la force de vente, les campagnes marketing, le service clientèle, la collaboration, le CRM mobile, le CRM social et le reporting.

La source [!DNL SugarCRM] vous permet d’ingérer des données de comptes, de contacts et d’événements à partir des points d’entrée d’API suivants :

* [Comptes](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [Contacts](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [Événements](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)

[!DNL SugarCRM] utilise des jetons porteur comme mécanisme d’authentification pour communiquer avec les API Compte [!DNL SugarCRM] et Contact et l’API Événements [!DNL SugarCRM].

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Conditions préalables

Avant de pouvoir créer une connexion source [!DNL SugarCRM], vous devez d’abord vous assurer que vous disposez des éléments suivants :

* Un compte [!DNL SugarMarket]. Vous devez contacter votre gestionnaire de compte [!DNL SugarCRM] pour obtenir un compte [!DNL SugarMarket] valide si vous n’en avez pas déjà un.

* Nom d’utilisateur et compte API uniques distincts de tout compte utilisateur associé au processus marketing ou commercial. Cette combinaison de nom d’utilisateur et de compte unique doit disposer d’autorisations d’accès API. Pour plus d’informations sur la procédure de configuration d’un compte, consultez la documentation d’[[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro).

## Connexion de [!DNL SugarCRM Accounts & Contacts] à Experience Platform

* [Créez une connexion source pour importer  [!DNL SugarCRM Accounts & Contacts]  données dans Experience Platform à l’aide d’API](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [Créez une connexion source pour importer  [!DNL SugarCRM Accounts & Contacts]  données dans Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [Créer un flux de données pour une source CRM à l’aide de l’API Flow Service](../../tutorials/api/collect/crm.md)


## Connexion de [!DNL SugarCRM Events] à Experience Platform

* [Créez une connexion source pour importer  [!DNL SugarCRM Events]  données dans Experience Platform à l’aide d’API](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Créez une connexion source pour importer  [!DNL SugarCRM Events]  données dans Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Créer un flux de données pour une connexion source CRM dans l’interface utilisateur](../../tutorials/ui/dataflow/crm.md)
