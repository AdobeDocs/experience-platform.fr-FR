---
title: Connecter MySQL à Experience Platform à l’aide de l’API Flow Service
description: Découvrez comment connecter votre base de données MySQL à Experience Platform à l’aide d’API.
exl-id: 273da568-84ed-4a3d-bfea-0f5b33f1551a
source-git-commit: b73ced639100c95f6c62be92d4796a206a688958
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 7%

---

# Connexion de [!DNL MySQL] à Experience Platform à l’aide de l’API [!DNL Flow Service]

Lisez ce guide pour savoir comment connecter votre compte [!DNL MySQL] à Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à vous connecter à [!DNL MySQL] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Lisez la [[!DNL MySQL] présentation](../../../../connectors/databases/mysql.md#prerequisites) pour plus d’informations sur l’authentification.

### Utilisation des API Experience Platform

Lisez le guide sur [Prise en main des API Experience Platform](../../../../../landing/api-guide.md) pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform.

## Connecter [!DNL MySQL] à Experience Platform sur Azure {#azure}

Pour plus d’informations sur la connexion de votre compte [!DNL MySQL] à Experience Platform sur Azure, lisez les étapes ci-dessous.

### Créer une connexion de base pour [!DNL MySQL] sur Experience Platform sur Azure {#azure-base}

Une connexion de base lie votre source à Experience Platform, stockant les détails d’authentification, le statut de connexion et un identifiant unique. Utilisez cet identifiant pour parcourir les fichiers sources et identifier les éléments spécifiques à ingérer, y compris leurs types et formats de données.

**Format d’API**

```https
POST /connections
```

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL MySQL] dans les paramètres de la requête.

>[!BEGINTABS]

>[!TAB Authentification basée sur une chaîne de connexion]

**Requête**

La requête suivante crée une connexion de base pour [!DNL MySQL] à l’aide de l’authentification par chaîne de connexion.

+++Afficher l’exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Connection String,
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.connectionString` | Chaîne de connexion [!DNL MySQL] associée à votre compte. Le modèle de chaîne de connexion [!DNL MySQL] est : `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL MySQL] : `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle connexion de base, y compris son identifiant unique (`id`).

+++Afficher l’exemple de réponse

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

+++

>[!TAB  Authentification de base ]

**Requête**

La requête suivante crée une connexion de base pour une source [!DNL MySQL] à l’aide de l’authentification de base.

+++Afficher l’exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Basic Authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "443",
              "database": "mysql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "DISABLED"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.server` | Nom ou adresse IP de la base de données [!DNL MySQL]. |
| `auth.params.database` | Nom de la base de données. |
| `auth.params.username` | Nom d’utilisateur correspondant à votre base de données. |
| `auth.params.password` | Mot de passe correspondant à votre base de données. |
| `auth.params.sslMode` | Méthode de chiffrement des données lors du transfert de données. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL MySQL] est : `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle connexion de base, y compris son identifiant unique (`id`).

+++Afficher l’exemple de réponse

```json
{
    "id": "025d4158-4113-403b-b551-e81724d3880c",
    "etag": "\"ae004437-0000-0200-0000-67ee107e0000\""
}
```

+++

>[!ENDTABS]

## Connexion de [!DNL MySQL] à Experience Platform sur Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../../../landing/multi-cloud.md).

Pour plus d’informations sur la connexion de votre compte [!DNL MySQL] à Experience Platform sur AWS, lisez les étapes ci-dessous.

### Créer une connexion de base pour [!DNL MySQL] sur Experience Platform sur AWS {#aws-base}

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL MySQL] connecter à Experience Platform sur AWS.

+++Afficher l’exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL on Experience Platform AWS",
      "description": "MySQL on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "443",
              "database": "mysql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "false"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.server` | Nom ou adresse IP de la base de données [!DNL MySQL]. |
| `auth.params.database` | Nom de la base de données. |
| `auth.params.username` | Nom d’utilisateur correspondant à votre base de données. |
| `auth.params.password` | Mot de passe correspondant à votre base de données. |
| `auth.params.sslMode` | Valeur booléenne qui contrôle l’application ou non du protocole SSL, selon la prise en charge de votre serveur. Cette configuration est définie par défaut sur `false`. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL MySQL] est : `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle connexion de base, y compris son identifiant unique (`id`).

+++Afficher l’exemple de réponse

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## Créer un flux de données pour les données [!DNL MySQL]

Maintenant que vous avez correctement connecté votre base de données [!DNL MySQL], vous pouvez [créer un flux de données et ingérer les données de votre base de données dans Experience Platform](../../collect/database-nosql.md).