---
keywords: Experience Platform;accueil;rubriques les plus consultées;Snowflake;snowflake
solution: Experience Platform
title: Création d’une connexion de base de Snowflake à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Snowflake à l’aide de l’API Flow Service.
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 0928da0ad15ce23d3677fec7b9866d079f3db407
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 10%

---

# Créez un [!DNL Snowflake] connexion de base à l’aide de [!DNL Flow Service] API

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous guide tout au long des étapes pour créer une connexion de base pour [!DNL Snowflake] en utilisant la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### Utilisation des API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur [Prise en main des API Platform](../../../../../landing/api-guide.md).

La section suivante fournit des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL Snowflake] en utilisant la variable [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] pour vous connecter à [!DNL Snowflake], vous devez fournir les propriétés de connexion suivantes :

| Credential | Description |
| --- | --- |
| `account` | Le nom complet du compte associé à votre [!DNL Snowflake] compte . Une personne entièrement qualifiée [!DNL Snowflake] nom du compte inclut le nom de votre compte, votre région et votre plateforme cloud. Par exemple : `cj12345.east-us-2.azure`. Pour plus d&#39;informations sur les noms de compte, reportez-vous à cette section [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| `warehouse` | Le [!DNL Snowflake] l’entrepôt gère le processus d’exécution des requêtes de l’application. Chaque [!DNL Snowflake] L’entrepôt est indépendant l’un de l’autre et doit être accessible individuellement lors de l’importation de données vers Platform. |
| `database` | Le [!DNL Snowflake] La base de données contient les données que vous souhaitez importer dans Platform. |
| `username` | Nom d’utilisateur de la variable [!DNL Snowflake] compte . |
| `password` | Le mot de passe du [!DNL Snowflake] compte utilisateur. |
| `connectionString` | Chaîne de connexion utilisée pour se connecter à votre [!DNL Snowflake] instance. Le modèle de chaîne de connexion pour [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions base et source. L’identifiant de spécification de connexion pour [!DNL Snowflake] is `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

Pour plus d’informations sur la prise en main, reportez-vous à cette section [[!DNL Snowflake] document](https://docs.snowflake.com/en/user-guide/oauth-custom.html).

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au `/connections` point de terminaison lors de la fourniture de [!DNL Snowflake] informations d’identification d’authentification dans le corps de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL Snowflake]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Snowflake base connection",
        "description": "Snowflake base connection",
        "auth": {
            "specName": "Basic Authentication for Snowflake,
            "params": {
                "connectionString": "{CONNECTION_STRING}"
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
| `connectionSpec.id` | Le [!DNL Snowflake] identifiant de spécification de connexion : `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

**Réponse**

Une réponse réussie renvoie la connexion nouvellement créée, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

En suivant ce tutoriel, vous avez créé une [!DNL Snowflake] connexion à l’aide de la fonction [!DNL Flow Service] et ont obtenu la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant de connexion dans le tutoriel suivant pendant que vous apprenez à [explorer des bases de données à l’aide de l’API Flow Service](../../explore/database-nosql.md).
