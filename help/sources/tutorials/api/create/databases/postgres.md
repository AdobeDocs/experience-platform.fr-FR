---
title: Connecter PostgreSQL à Experience Platform à l’aide de l’API Flow Service
description: Découvrez comment connecter votre base  [!DNL PostgreSQL]  données à Experience Platform à l’aide d’API.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 18%

---

# Connexion de [!DNL PostgreSQL] à Experience Platform à l’aide de l’API [!DNL Flow Service]

Lisez ce guide pour savoir comment connecter votre base de données [!DNL PostgreSQL] à Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à vous connecter à [!DNL PostgreSQL] à l’aide de l’API [!DNL Flow Service].

### Utilisation des API Experience Platform

Lisez le guide sur [Prise en main des API Experience Platform](../../../../../landing/api-guide.md) pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform.

### Collecter les informations d’identification requises

Lisez la [[!DNL PostgreSQL] présentation](../../../../connectors/databases/postgres.md) pour plus d’informations sur l’authentification.

### Activer le chiffrement SSL pour votre chaîne de connexion

Vous pouvez activer le chiffrement SSL pour votre chaîne de connexion [!DNL PostgreSQL] en ajoutant votre chaîne de connexion avec les propriétés suivantes :

| Propriété | Description | Exemple |
| --- | --- | --- |
| `EncryptionMethod` | Permet d’activer le chiffrement SSL sur vos données [!DNL PostgreSQL]. | <uL><li>`EncryptionMethod=0`(Désactivé)</li><li>`EncryptionMethod=1`(Activé)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Valide le certificat envoyé par votre base de données [!DNL PostgreSQL] lorsque la `EncryptionMethod` est appliquée. | <uL><li>`ValidationServerCertificate=0`(Désactivé)</li><li>`ValidationServerCertificate=1`(Activé)</li></ul> |

Voici un exemple de chaîne de connexion [!DNL PostgreSQL] ajoutée avec le chiffrement SSL : `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## Connecter [!DNL PostgreSQL] à Experience Platform sur Azure {#azure}

Lisez les étapes ci-dessous pour savoir comment connecter votre compte [!DNL PostgreSQL] à Experience Platform sur Azure.

### Créer une connexion de base {#azure-base}

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL PostgreSQL] dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Authentification par clé de compte]

**Requête**

La requête suivante crée une connexion de base pour [!DNL PostgreSQL] à l’aide de l’authentification par clé de compte :

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via connection string",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| ------------- | --------------- |
| `auth.params.connectionString` | Chaîne de connexion associée à votre compte [!DNL PostgreSQL]. Le modèle de chaîne de connexion [!DNL PostgreSQL] est : `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Identifiants de spécification de connexion [!DNL PostgreSQL] : `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion de base.

+++Afficher l’exemple de réponse

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

+++

>[!TAB  Authentification de base ]

**Requête**

La requête suivante crée une connexion de base pour [!DNL PostgreSQL] à l’aide de l’authentification de base :

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "3306",
              "database": "postgresql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "Allow"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| ---| --- |
| `auth.params.server` | Nom ou adresse IP de la base de données [!DNL PostgreSQL]. |
| `auth.params.port` | Numéro de port du serveur de base de données. |
| `auth.params.database` | Nom de la base de données [!DNL PostgreSQL]. |
| `auth.params.username` | Nom d’utilisateur associé à l’authentification de la base de données [!DNL PostgreSQL]. |
| `auth.params.password` | Mot de passe associé à l’authentification de la base de données [!DNL PostgreSQL]. |
| `auth.params.sslMode` | Méthode de chiffrement des données lors du transfert de données. Les valeurs disponibles sont les suivantes : `Disable`, `Allow`, `Prefer`, `Verify Ca` et `Verify Full`. |
| `connectionSpec.id` | Identifiants de spécification de connexion [!DNL PostgreSQL] : `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion de base.

+++Afficher l’exemple de réponse

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

>[!ENDTABS]

## Connexion de [!DNL PostgreSQL] à Experience Platform sur Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../../../landing/multi-cloud.md).

Pour plus d’informations sur la connexion de votre base de données [!DNL PostgreSQL] à Experience Platform sur AWS, lisez les étapes ci-dessous.

### Créer une connexion de base {#aws-base}

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` lors de la fourniture des informations d’identification d’authentification [!DNL PostgreSQL] dans le cadre des paramètres de requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL PostgreSQL] connecter à Experience Platform sur AWS.

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "3306",
              "database": "postgresql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "false"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| ---| --- |
| `auth.params.server` | Nom ou adresse IP de la base de données [!DNL PostgreSQL]. |
| `auth.params.port` | Numéro de port du serveur de base de données. |
| `auth.params.database` | Nom de la base de données [!DNL PostgreSQL]. |
| `auth.params.username` | Nom d’utilisateur associé à l’authentification de la base de données [!DNL PostgreSQL]. |
| `auth.params.password` | Mot de passe associé à l’authentification de la base de données [!DNL PostgreSQL]. |
| `sslMode` | Valeur booléenne qui contrôle l’application ou non du protocole SSL, selon la prise en charge de votre serveur. Cette configuration est définie par défaut sur `false`. |
| `connectionSpec.id` | Identifiants de spécification de connexion [!DNL PostgreSQL] : `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion de base.

+++Afficher l’exemple de réponse

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

## Étapes suivantes

Maintenant que vous avez créé une connexion entre votre base de données [!DNL PostgreSQL] et Experience Platform, vous pouvez passer aux étapes suivantes et importer vos données [!DNL PostgreSQL] dans Experience Platform. Pour plus d’informations, consultez la documentation suivante :

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer les données de la base de données dans Experience Platform à l’aide de l’API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)
