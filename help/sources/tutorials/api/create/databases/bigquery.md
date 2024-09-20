---
title: Création d’une connexion Google BigQuery Base à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à Google BigQuery à l’aide de l’API Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 1fa79b31b5a257ebb3cbd60246b757d8a4a63d7c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 53%

---

# Créez une connexion de base à [!DNL Google BigQuery] à l’aide de l’API [!DNL Flow Service].

>[!IMPORTANT]
>
>La source [!DNL Google BigQuery] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Une connexion de base représente la connexion authentifiée entre une source et Adobe Experience Platform.

Lisez ce guide pour savoir comment créer une connexion de base pour [!DNL Google BigQuery] à l’aide de l’ [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Commencer

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL Google BigQuery] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Lisez le [[!DNL Google BigQuery] guide d&#39;authentification](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) pour obtenir des instructions détaillées sur la collecte de vos informations d&#39;identification requises.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Google BigQuery] dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB  Utilisation de l’authentification de base ]

**Requête**

La requête suivante crée une connexion de base pour [!DNL Google BigQuery] à l’aide de l’authentification de base :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection with basic authentication",
        "description": "Google BigQuery connection with basic authentication",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.project` | ID de projet par défaut du projet [!DNL Google BigQuery] à interroger. par rapport à . |
| `auth.params.clientId` | La valeur d’identifiant utilisée pour générer le jeton d’actualisation. |
| `auth.params.clientSecret` | La valeur client utilisée pour générer le jeton d’actualisation. |
| `auth.params.refreshToken` | Jeton d’actualisation obtenu à partir de [!DNL Google] utilisé pour autoriser l’accès à [!DNL Google BigQuery]. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Google BigQuery] : `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

>[!TAB Utiliser l’authentification de service]


**Requête**

La requête suivante crée une connexion de base pour [!DNL Google BigQuery] à l’aide de l’authentification de service :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery base connection with service account",
        "description": "Google BigQuery connection with service account",
        "auth": {
            "specName": "Service Authentication",
            "params": {
                    "projectId": "{PROJECT_ID}",
                    "keyFileContent": "{KEY_FILE_CONTENT},
                    "largeResultsDataSetId": "{LARGE_RESULTS_DATASET_ID}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.projectId` | ID de projet par défaut du projet [!DNL Google BigQuery] à interroger. par rapport à . |
| `auth.params.keyFileContent` | Fichier clé utilisé pour authentifier le compte de service. Vous devez coder le contenu du fichier clé dans [!DNL Base64]. |
| `auth.params.largeResultsDataSetId` | (Facultatif) L’identifiant de jeu de données [!DNL Google BigQuery] précréé qui est requis pour activer la prise en charge des jeux de résultats volumineux. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

>[!ENDTABS]


## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Google BigQuery] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer des données de base de données dans Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/database-nosql.md)
