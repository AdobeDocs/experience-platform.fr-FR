---
title: Connecter Snowflake à Experience Platform à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à Snowflake à l’aide de l’API Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 0476c42924bf0163380e650141fad8e50b98d4cf
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 18%

---

# Connexion de [!DNL Snowflake] à Experience Platform à l’aide de l’API [!DNL Flow Service]

>[!IMPORTANT]
>
>La source [!DNL Snowflake] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Lisez ce guide pour savoir comment connecter votre compte source [!DNL Snowflake] à Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

La section suivante fournit des informations supplémentaires que vous devez connaître pour réussir à vous connecter à [!DNL Snowflake] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Lisez la [[!DNL Snowflake] présentation](../../../../connectors/databases/snowflake.md#prerequisites) pour plus d’informations sur l’authentification.

## Connecter [!DNL Snowflake] à Experience Platform sur Azure {#azure}

>[!WARNING]
>
>L’authentification de base (ou authentification par clé de compte) de la source [!DNL Snowflake] sera abandonnée en novembre 2025. Vous devez passer à l’authentification par paire de clés pour continuer à utiliser la source et à ingérer des données de votre base de données vers Experience Platform. Pour plus d’informations sur l’obsolescence, consultez le [[!DNL Snowflake] guide des bonnes pratiques sur la réduction des risques liés à la compromission des informations d’identification](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/).

Pour plus d’informations sur la connexion de votre source [!DNL Snowflake] à Experience Platform sur Azure, lisez les étapes ci-dessous.

>[!NOTE]
>
>Vous devez définir l’indicateur de `PREVENT_UNLOAD_TO_INLINE_URL` sur `FALSE` pour permettre le déchargement des données de votre base de données [!DNL Snowflake] vers Experience Platform.

### Créer une connexion de base pour [!DNL Snowflake] sur Experience Platform sur Azure {#azure-base}

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Snowflake] dans le corps de la requête.

**Format d’API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB ConnectionString]

+++Requête

La requête suivante permet de créer une connexion de base pour [!DNL Snowflake] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion utilisée pour la connexion à votre instance [!DNL Snowflake]. Le modèle de chaîne de connexion pour [!DNL Snowflake] est `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Snowflake] : `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Réponse

Une réponse réussie renvoie la nouvelle connexion, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


>[!TAB Authentification par paire de clés avec clé privée chiffrée]

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "privateKeyPassphrase": "abcd1234",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.account` | Nom de votre compte [!DNL Snowflake]. |
| `auth.params.username` | Nom d’utilisateur associé à votre compte [!DNL Snowflake]. |
| `auth.params.database` | Base de données [!DNL Snowflake] à partir de laquelle les données seront extraites. |
| `auth.params.privateKey` | La clé privée chiffrée [!DNL Base64-]encodée) de votre compte [!DNL Snowflake]. |
| `auth.params.privateKeyPassphrase` | Phrase secrète correspondant à votre clé privée. |
| `auth.params.warehouse` | Entrepôt de [!DNL Snowflake] utilisé. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Snowflake] : `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Réponse

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`).

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!TAB Authentification par paire de clés avec clé privée non chiffrée]

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with unencrypted private key",
      "description": "Snowflake base connection with unencrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.account` | Nom de votre compte [!DNL Snowflake]. |
| `auth.params.username` | Nom d’utilisateur associé à votre compte [!DNL Snowflake]. |
| `auth.params.database` | Base de données [!DNL Snowflake] à partir de laquelle les données seront extraites. |
| `auth.params.privateKey` | La clé privée [!DNL Base64-]encodée et non chiffrée de votre compte [!DNL Snowflake]. |
| `auth.params.warehouse` | Entrepôt de [!DNL Snowflake] utilisé. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Snowflake] : `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Réponse

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`).

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

## Connexion de [!DNL Snowflake] à Experience Platform sur Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../../../landing/multi-cloud.md).

Pour plus d’informations sur la connexion de votre source [!DNL Snowflake] à Experience Platform sur AWS, lisez les étapes ci-dessous.

### Créer une connexion de base pour [!DNL Snowflake] sur Experience Platform dans AWS {#aws-base}

**Format d’API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB  Authentification de base ]

La requête suivante crée une connexion de base pour [!DNL Snowflake] d’ingérer des données vers Experience Platform sur AWS :

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection for Experience Platform on AWS",
      "description": "Snowflake base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme.snowflakecomputing.com",
              "port": "443",
              "username": "acme-cj123",
              "password": "{PASSWORD}",
              "database": "ACME_DB",
              "warehouse": "COMPUTE_WH",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.host` | URL hôte à laquelle votre compte [!DNL Snowflake] se connecte. |
| `auth.params.port` | Numéro de port utilisé par [!DNL Snowflake] lors de la connexion à un serveur via Internet. |
| `auth.params.username` | Nom d’utilisateur associé à votre compte [!DNL Snowflake]. |
| `auth.params.database` | Base de données [!DNL Snowflake] à partir de laquelle les données seront extraites. |
| `auth.params.password` | Mot de passe associé à votre compte [!DNL Snowflake]. |
| `auth.params.warehouse` | Entrepôt de [!DNL Snowflake] utilisé. |
| `auth.params.schema` | Nom du schéma associé à votre base de données [!DNL Snowflake]. Vous devez vous assurer que l’utilisateur auquel vous souhaitez accorder l’accès à la base de données a également accès à ce schéma. |

+++

+++Réponse

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`).

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++

>[!TAB Authentification par paire de clés avec clé privée non chiffrée]

+++Requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with unencrypted private key",
      "description": "Snowflake base connection with unencrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.account` | Nom de votre compte [!DNL Snowflake]. |
| `auth.params.username` | Nom d’utilisateur associé à votre compte [!DNL Snowflake]. |
| `auth.params.database` | Base de données [!DNL Snowflake] à partir de laquelle les données seront extraites. |
| `auth.params.privateKey` | La clé privée [!DNL Base64-]encodée et non chiffrée de votre compte [!DNL Snowflake]. |
| `auth.params.warehouse` | Entrepôt de [!DNL Snowflake] utilisé. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Snowflake] : `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++


+++Réponse

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`).

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++

>[!ENDTABS]

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Snowflake] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer les données de la base de données dans Experience Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/database-nosql.md)
