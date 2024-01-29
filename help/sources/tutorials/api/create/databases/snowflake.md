---
title: Création d’une connexion de base de Snowflake à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à Snowflake à l’aide de l’API Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 25%

---

# Créez une connexion de base à [!DNL Snowflake] à l’aide de l’API [!DNL Flow Service].

>[!IMPORTANT]
>
>La variable [!DNL Snowflake] source est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-time Customer Data Platform Ultimate.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Suivez le tutoriel suivant pour savoir comment créer une connexion de base pour [!DNL Snowflake] en utilisant la variable [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../../../landing/api-guide.md).

La section suivante fournit des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL Snowflake] en utilisant la variable [!DNL Flow Service] API.

### Collecter les informations d’identification requises

Vous devez fournir des valeurs pour les propriétés d’identification suivantes afin d’authentifier votre [!DNL Snowflake] source.

>[!BEGINTABS]

>[!TAB Authentification par clé de compte]

| Informations d’identification | Description |
| ---------- | ----------- |
| `account` | Un nom de compte identifie de manière unique un compte au sein de votre organisation. Dans ce cas, vous devez identifier de manière unique un compte parmi différents [!DNL Snowflake] organisations. Pour ce faire, vous devez ajouter le nom de votre organisation en préfixe sur le nom du compte. Par exemple :`orgname-account_name` Pour plus d’informations sur les noms de compte, consultez la section [!DNL Snowflake] documentation sur [identificateurs de compte](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | La variable [!DNL Snowflake] l’entrepôt gère le processus d’exécution des requêtes de l’application. Chaque [!DNL Snowflake] L’entrepôt est indépendant l’un de l’autre et doit être accessible individuellement lors de l’importation de données vers Platform. |
| `database` | La variable [!DNL Snowflake] La base de données contient les données que vous souhaitez importer dans Platform. |
| `username` | Nom d’utilisateur de la variable [!DNL Snowflake] compte . |
| `password` | Le mot de passe du [!DNL Snowflake] compte utilisateur. |
| `role` | Le rôle de contrôle d’accès par défaut à utiliser dans la variable [!DNL Snowflake] session. Le rôle doit être un rôle existant qui a déjà été attribué à l’utilisateur spécifié. Le rôle par défaut est `PUBLIC`. |
| `connectionString` | Chaîne de connexion utilisée pour se connecter à votre [!DNL Snowflake] instance. Le modèle de chaîne de connexion pour [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Authentification par paire de clés]

Pour utiliser l’authentification par paire de clés, vous devez générer une paire de clés RSA 2 048 bits, puis fournir les valeurs suivantes lors de la création d’un compte pour votre [!DNL Snowflake] source.

| Informations d’identification | Description |
| --- | --- |
| `account` | Un nom de compte identifie de manière unique un compte au sein de votre organisation. Dans ce cas, vous devez identifier de manière unique un compte parmi différents [!DNL Snowflake] organisations. Pour ce faire, vous devez ajouter le nom de votre organisation en préfixe sur le nom du compte. Par exemple :`orgname-account_name` Pour plus d’informations sur les noms de compte, consultez la section [!DNL Snowflake] documentation sur [identificateurs de compte](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Le nom d’utilisateur de votre [!DNL Snowflake] compte . |
| `privateKey` | La variable [!DNL Base64-]clé privée codée de votre [!DNL Snowflake] compte . Vous pouvez générer des clés privées chiffrées ou non chiffrées. Si vous utilisez une clé privée chiffrée, vous devez également fournir un mot de passe de clé privée lors de l’authentification par rapport à un Experience Platform. |
| `privateKeyPassphrase` | La phrase secrète de clé privée est une couche supplémentaire de sécurité que vous devez utiliser lors de l’authentification avec une clé privée chiffrée. Vous n’êtes pas tenu de fournir la phrase secrète si vous utilisez une clé privée non chiffrée. |
| `database` | La variable [!DNL Snowflake] base de données contenant les données que vous souhaitez ingérer à Experience Platform. |
| `warehouse` | La variable [!DNL Snowflake] l’entrepôt gère le processus d’exécution des requêtes de l’application. Chaque [!DNL Snowflake] l’entrepôt est indépendant l’un de l’autre et doit être accessible individuellement lors de la transmission de données à Experience Platform. |

Pour plus d’informations sur ces valeurs, reportez-vous au [[!DNL Snowflake] guide d’authentification de paire de clés](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>Vous devez définir la variable `PREVENT_UNLOAD_TO_INLINE_URL` indicateur pour `FALSE` pour permettre le déchargement des données de votre [!DNL Snowflake] base de données vers Experience Platform.

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au `/connections` point de terminaison lors de la fourniture de [!DNL Snowflake] informations d’identification d’authentification dans le corps de la requête.

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
| `auth.params.connectionString` | Chaîne de connexion utilisée pour se connecter à votre [!DNL Snowflake] instance. Le modèle de chaîne de connexion pour [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | La variable [!DNL Snowflake] identifiant de spécification de connexion : `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Réponse

Une réponse réussie renvoie la connexion nouvellement créée, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

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
| `auth.params.account` | Le nom de votre [!DNL Snowflake] compte . |
| `auth.params.username` | Le nom d’utilisateur associé à votre [!DNL Snowflake] compte . |
| `auth.params.database` | La variable [!DNL Snowflake] à partir de laquelle les données seront extraites. |
| `auth.params.privateKey` | La variable [!DNL Base64-]clé privée chiffrée de votre [!DNL Snowflake] compte . |
| `auth.params.privateKeyPassphrase` | La phrase secrète qui correspond à votre clé privée. |
| `auth.params.warehouse` | La variable [!DNL Snowflake] entrepôt utilisé. |
| `connectionSpec.id` | La variable [!DNL Snowflake] identifiant de spécification de connexion : `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Réponse

Une réponse réussie renvoie la connexion nouvellement créée, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

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
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
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
| `auth.params.account` | Le nom de votre [!DNL Snowflake] compte . |
| `auth.params.username` | Le nom d’utilisateur associé à votre [!DNL Snowflake] compte . |
| `auth.params.database` | La variable [!DNL Snowflake] à partir de laquelle les données seront extraites. |
| `auth.params.privateKey` | La variable [!DNL Base64-]clé privée non chiffrée de votre [!DNL Snowflake] compte . |
| `auth.params.warehouse` | La variable [!DNL Snowflake] entrepôt utilisé. |
| `connectionSpec.id` | La variable [!DNL Snowflake] identifiant de spécification de connexion : `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Réponse

Une réponse réussie renvoie la connexion nouvellement créée, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Snowflake] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de base de données dans Platform à l’aide de la fonction [!DNL Flow Service] API](../../collect/database-nosql.md)
