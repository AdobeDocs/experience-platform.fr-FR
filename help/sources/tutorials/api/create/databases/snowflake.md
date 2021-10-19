---
keywords: Experience Platform ; accueil ; sujets populaires ; Snowflake ; snowflake
solution: Experience Platform
title: Création d’une connexion de base de Snowflake à l’aide de l’API du service de flux
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform au Snowflake à l’aide de l’API Flow Service.
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 76b3e3e9bcb27eb2bd6981ae6eb109410ae16336
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 10%

---

# Créer un [!DNL Snowflake] connexion de base à l’aide de [!DNL Flow Service] API

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Ce tutoriel vous explique les étapes à suivre pour créer une connexion de base pour [!DNL Snowflake] à l’aide de la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, étiqueter et améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### Utilisation des API de plate-forme

Pour plus d’informations sur la manière d’effectuer des appels vers les API de plate-forme, consultez le guide sur [prise en main des API de plate-forme](../../../../../landing/api-guide.md).

La section suivante fournit des informations supplémentaires que vous devez connaître pour vous connecter à [!DNL Snowflake] à l’aide de la [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] pour se connecter à [!DNL Snowflake], vous devez fournir les propriétés de connexion suivantes :

| Informations d&#39;identification | Description |
| --- | --- |
| `account` | Le nom complet du compte associé à votre [!DNL Snowflake] compte. Une personne pleinement qualifiée [!DNL Snowflake] le nom de compte comprend votre nom de compte, votre région et votre plate-forme cloud. Par exemple : `cj12345.east-us-2.azure`. Pour plus d’informations sur les noms de compte, reportez-vous à [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| `warehouse` | Le [!DNL Snowflake] l&#39;entrepôt gère le processus d&#39;exécution de la requête pour l&#39;application. Chacune [!DNL Snowflake] l&#39;entrepôt est indépendant l&#39;un de l&#39;autre et doit être accessible individuellement lors de l&#39;importation de données vers la plate-forme. |
| `database` | Le [!DNL Snowflake] contient les données que vous souhaitez importer dans la plate-forme. |
| `username` | Le nom d’utilisateur du [!DNL Snowflake] compte. |
| `password` | Le mot de passe pour le [!DNL Snowflake] compte utilisateur. |
| `connectionString` | La chaîne de connexion utilisée pour se connecter à votre [!DNL Snowflake] instance. Modèle de chaîne de connexion pour [!DNL Snowflake] est `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés de connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. ID de spécification de connexion pour [!DNL Snowflake] est `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

Pour plus d’informations sur la prise en main, reportez-vous à [[!DNL Snowflake] document](https://docs.snowflake.com/en/user-guide/oauth-custom.html).

## Création d’une connexion de base

Une connexion de base conserve les informations entre votre source et la plate-forme, y compris les informations d&#39;identification de votre source, l&#39;état actuel de la connexion et votre ID de connexion de base unique. L’ID de connexion de base vous permet d’explorer et de parcourir les fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez assimiler, y compris des informations concernant leurs types et formats de données.

Pour créer un ID de connexion de base, effectuez une demande de POST à l’adresse `/connections` point de terminaison lors de la fourniture de votre [!DNL Snowflake] les informations d&#39;identification d&#39;authentification dans le corps de la demande.

**Format d’API**

```https
POST /connections
```

**Requête**

La demande suivante crée une connexion de base pour [!DNL Snowflake]:

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
| `auth.params.connectionString` | La chaîne de connexion utilisée pour se connecter à votre [!DNL Snowflake] instance. Modèle de chaîne de connexion pour [!DNL Snowflake] est `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | Le [!DNL Snowflake] ID de spécification de connexion : `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

**Réponse**

Une réponse réussie renvoie la connexion nouvellement créée, y compris son identifiant de connexion unique (`id`). Cet ID est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

En suivant ce tutoriel, vous avez créé un fichier [!DNL Snowflake] connexion à l’aide de la [!DNL Flow Service] et ont obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet ID de connexion dans le tutoriel suivant pour apprendre à [exploration des bases de données à l’aide de l’API Flow Service](../../explore/database-nosql.md).
