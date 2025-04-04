---
title: Connecter Google BigQuery à Experience Platform à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à Google BigQuery à l’aide de l’API Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 24%

---

# Connexion de [!DNL Google BigQuery] à Experience Platform à l’aide de l’API [!DNL Flow Service]

>[!IMPORTANT]
>
>La source [!DNL Google BigQuery] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Lisez ce guide pour savoir comment connecter votre base de données [!DNL Google BigQuery] à Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Commencer

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

### Collecter les informations d’identification requises

Lisez le [[!DNL Google BigQuery] guide d’authentification](../../../../connectors/databases/bigquery.md#prerequisites) pour obtenir des instructions détaillées sur la récupération de vos informations d’identification [!DNL Google BigQuery].

## Connecter [!DNL Google BigQuery] à Experience Platform sur Azure {#azure}

Pour plus d’informations sur la connexion de votre source [!DNL Google BigQuery] à Experience Platform sur Azure, lisez les étapes ci-dessous.

### Créer une connexion de base pour [!DNL Google BigQuery] sur Experience Platform sur Azure {#azure-base}

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Google BigQuery] dans les paramètres de la requête.

**Format d’API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Utiliser l’authentification de base]

+++Requête

La requête suivante crée une connexion de base pour [!DNL Google BigQuery] à l’aide de l’authentification de base.

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
| `auth.params.project` | Identifiant de projet du projet [!DNL Google BigQuery] par défaut à interroger. contre. |
| `auth.params.clientId` | Valeur d’identifiant utilisée pour générer le jeton d’actualisation. |
| `auth.params.clientSecret` | Valeur client utilisée pour générer le jeton d’actualisation. |
| `auth.params.refreshToken` | Jeton d’actualisation obtenu de [!DNL Google] utilisé pour autoriser l’accès à [!DNL Google BigQuery]. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Google BigQuery] : `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

+++

+++Réponse

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!TAB Utiliser l’authentification de service]


+++Requête

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
| `auth.params.projectId` | Identifiant de projet du projet [!DNL Google BigQuery] par défaut à interroger. contre. |
| `auth.params.keyFileContent` | Fichier de clé utilisé pour authentifier le compte de service. Vous devez encoder le contenu du fichier de clé en [!DNL Base64]. |
| `auth.params.largeResultsDataSetId` | (Facultatif) Identifiant de jeu de données [!DNL Google BigQuery] précréé et requis pour permettre la prise en charge de jeux de résultats volumineux. |

+++

+++Réponse

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!ENDTABS]

## Connexion de [!DNL Google BigQuery] à Experience Platform sur Amazon Web Services (AWS) {#aws}

Pour plus d’informations sur la connexion de votre base de données [!DNL Google BigQuery] à Experience Platform sur AWS, lisez les étapes ci-dessous.

### Créer une connexion de base pour [!DNL Google BigQuery] sur Experience Platform sur AWS

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../../../landing/multi-cloud.md).

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour se connecter [!DNL Google BigQuery] à Experience Platform sur AWS.

+++Sélectionner pour afficher l’exemple

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google BigQuery base connection on AWS",
      "description": "Google BigQuery base connection on AWS",
      "auth": {
          "specName": "Service Authentication",
          "params": {
                  "projectId": "{PROJECT_ID}",
                  "keyFileContent": "{KEY_FILE_CONTENT},
                  "datasetId": "{DATASET_ID}"
      },
      "connectionSpec": {
          "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.projectId` | Identifiant de projet du projet [!DNL Google BigQuery] par défaut à interroger. contre. |
| `auth.params.keyFileContent` | Fichier de clé utilisé pour authentifier le compte de service. Vous devez encoder le contenu du fichier de clé en [!DNL Base64]. |
| `auth.params.datasetId` | Identifiant du jeu de données qui correspond à votre source de [!DNL Google BigQuery]. Cet identifiant représente l’emplacement des tables de données. |

+++

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer votre stockage dans le tutoriel suivant.

+++Sélectionner pour afficher l’exemple

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL Google BigQuery] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer les données de la base de données dans Experience Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/database-nosql.md)
