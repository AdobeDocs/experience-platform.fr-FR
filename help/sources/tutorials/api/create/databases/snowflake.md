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
>La source [!DNL Snowflake] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Utilisez le tutoriel suivant pour apprendre à créer une connexion de base pour [!DNL Snowflake] à l’aide de l’ [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../../../landing/api-guide.md).

La section suivante fournit des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL Snowflake] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Vous devez fournir des valeurs pour les propriétés d’identification suivantes pour authentifier votre source [!DNL Snowflake].

>[!BEGINTABS]

>[!TAB  Authentification par clé de compte ]

| Informations d’identification | Description |
| ---------- | ----------- |
| `account` | Un nom de compte identifie de manière unique un compte au sein de votre organisation. Dans ce cas, vous devez identifier de manière unique un compte parmi différentes organisations [!DNL Snowflake]. Pour ce faire, vous devez ajouter le nom de votre organisation en préfixe sur le nom du compte. Par exemple : `orgname-account_name`. Pour plus d&#39;informations sur les noms de compte, consultez la documentation [!DNL Snowflake] sur les [identifiants de compte](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | L’entrepôt [!DNL Snowflake] gère le processus d’exécution de requête pour l’application. Chaque entrepôt [!DNL Snowflake] est indépendant l’un de l’autre et doit être accessible individuellement lors de la transmission de données à Platform. |
| `database` | La base de données [!DNL Snowflake] contient les données que vous souhaitez importer dans Platform. |
| `username` | Nom d’utilisateur du compte [!DNL Snowflake]. |
| `password` | Mot de passe du compte utilisateur [!DNL Snowflake]. |
| `role` | Rôle de contrôle d’accès par défaut à utiliser dans la session [!DNL Snowflake]. Le rôle doit être un rôle existant qui a déjà été attribué à l’utilisateur spécifié. Le rôle par défaut est `PUBLIC`. |
| `connectionString` | Chaîne de connexion utilisée pour se connecter à votre instance [!DNL Snowflake]. Le modèle de chaîne de connexion pour [!DNL Snowflake] est `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Authentification par paire de clés]

Pour utiliser l’authentification par paire de clés, vous devez générer une paire de clés RSA 2 048 bits, puis fournir les valeurs suivantes lors de la création d’un compte pour votre source [!DNL Snowflake].

| Informations d’identification | Description |
| --- | --- |
| `account` | Un nom de compte identifie de manière unique un compte au sein de votre organisation. Dans ce cas, vous devez identifier de manière unique un compte parmi différentes organisations [!DNL Snowflake]. Pour ce faire, vous devez ajouter le nom de votre organisation en préfixe sur le nom du compte. Par exemple : `orgname-account_name`. Pour plus d&#39;informations sur les noms de compte, consultez la documentation [!DNL Snowflake] sur les [identifiants de compte](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Nom d’utilisateur de votre compte [!DNL Snowflake]. |
| `privateKey` | La clé privée [!DNL Base64-] codée de votre compte [!DNL Snowflake]. Vous pouvez générer des clés privées chiffrées ou non chiffrées. Si vous utilisez une clé privée chiffrée, vous devez également fournir un mot de passe de clé privée lors de l’authentification par rapport à un Experience Platform. |
| `privateKeyPassphrase` | La phrase secrète de clé privée est une couche supplémentaire de sécurité que vous devez utiliser lors de l’authentification avec une clé privée chiffrée. Vous n’êtes pas tenu de fournir la phrase secrète si vous utilisez une clé privée non chiffrée. |
| `database` | La base de données [!DNL Snowflake] qui contient les données que vous souhaitez ingérer à l’Experience Platform. |
| `warehouse` | L’entrepôt [!DNL Snowflake] gère le processus d’exécution de requête pour l’application. Chaque entrepôt [!DNL Snowflake] est indépendant l’un de l’autre et doit être accessible individuellement lors de la transmission de données à Experience Platform. |

Pour plus d’informations sur ces valeurs, consultez le [[!DNL Snowflake] guide d’authentification de paire de clés](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>Vous devez définir l’indicateur `PREVENT_UNLOAD_TO_INLINE_URL` sur `FALSE` pour autoriser le déchargement des données de votre base de données [!DNL Snowflake] vers l’Experience Platform.

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au point de terminaison `/connections` tout en fournissant vos informations d’authentification [!DNL Snowflake] dans le cadre du corps de la requête.

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
| `auth.params.connectionString` | Chaîne de connexion utilisée pour se connecter à votre instance [!DNL Snowflake]. Le modèle de chaîne de connexion pour [!DNL Snowflake] est `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Snowflake] : `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

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


>[!TAB  Authentification de paire de clés avec clé privée chiffrée ]

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
| `auth.params.database` | La base de données [!DNL Snowflake] à partir de laquelle les données seront extraites. |
| `auth.params.privateKey` | La clé privée [!DNL Base64-] codée et chiffrée de votre compte [!DNL Snowflake]. |
| `auth.params.privateKeyPassphrase` | La phrase secrète qui correspond à votre clé privée. |
| `auth.params.warehouse` | L’entrepôt [!DNL Snowflake] que vous utilisez. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Snowflake] : `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

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

>[!TAB  Authentification de paire de clés avec clé privée non chiffrée ]

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
| `auth.params.account` | Nom de votre compte [!DNL Snowflake]. |
| `auth.params.username` | Nom d’utilisateur associé à votre compte [!DNL Snowflake]. |
| `auth.params.database` | La base de données [!DNL Snowflake] à partir de laquelle les données seront extraites. |
| `auth.params.privateKey` | La clé privée [!DNL Base64-] codée et non chiffrée de votre compte [!DNL Snowflake]. |
| `auth.params.warehouse` | L’entrepôt [!DNL Snowflake] que vous utilisez. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Snowflake] : `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

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

>[!ENDTABS]

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Snowflake] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de base de données dans Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/database-nosql.md)
