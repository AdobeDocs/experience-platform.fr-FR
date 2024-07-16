---
title: Création d’une connexion de base Microsoft SQL Server à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Microsoft SQL Server à l’aide de l’API Flow Service.
exl-id: 00455a61-c8c1-42f4-a962-fc16f7370cbd
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 61%

---

# Créez une connexion de base SQL Server [!DNL Microsoft] à l’aide de l’API [!DNL Flow Service]

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Lisez ce tutoriel pour découvrir comment créer une connexion de base pour [!DNL Microsoft SQL Server] à l’aide de l’ [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL Microsoft SQL Server] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises {#gather-required-credentials}

Pour vous connecter à [!DNL Microsoft SQL Server], vous devez fournir la propriété de connexion suivante :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| `connectionString` | Chaîne de connexion associée à votre compte [!DNL Microsoft SQL Server]. Le modèle de chaîne de connexion varie selon que vous utilisez le nom de serveur ou d’instance pour votre source de données :<ul><li>Chaîne de connexion utilisant le nom du serveur : `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Chaîne de connexion utilisant le nom de l’instance :`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’ID de spécification de connexion pour [!DNL Microsoft SQL Server] est `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

Pour plus d&#39;informations sur l&#39;obtention d&#39;une chaîne de connexion, consultez ce [[!DNL Microsoft SQL Server] document](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Microsoft SQL Server] dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Microsoft SQL Server] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for sql-server",
      "description": "Base connection for sql-server",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword"
          }
      },
      "connectionSpec": {
          "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
          "version": "1.0"
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.connectionString` | Chaîne de connexion associée à votre compte [!DNL Microsoft SQL Server]. Lisez la section sur la [collecte des informations d’identification requises](#gather-required-credentials) pour plus d’informations. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL Microsoft SQL Server] est : `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer votre base de données dans le tutoriel suivant.

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base [!DNL Microsoft SQL Server] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de base de données dans Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/database-nosql.md)