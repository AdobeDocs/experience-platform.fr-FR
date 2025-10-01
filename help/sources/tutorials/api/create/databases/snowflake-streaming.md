---
title: Connexion de votre compte de streaming Snowflake à Adobe Experience Platform
description: Découvrez comment connecter Adobe Experience Platform à Snowflake Streaming à l’aide de l’API Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3fc225a4-746c-4a91-aa77-bbeb091ec364
source-git-commit: a4a464f1f3b61311754a39f2a6e6a4ef21af3ab0
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 20%

---

# Diffuser des données de [!DNL Snowflake] vers Experience Platform à l’aide de l’API [!DNL Flow Service]

>[!IMPORTANT]
>
>
> La source de diffusion en continu [!DNL Snowflake] est disponible dans l’API pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Ce tutoriel décrit les étapes à suivre pour connecter et diffuser des données de votre compte [!DNL Snowflake] vers Adobe Experience Platform à l’aide de l’API [[!DNL Flow Service] ](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

### Collecter les informations d’identification requises

Lisez la [[!DNL Snowflake] présentation](../../../../connectors/databases/snowflake-streaming.md#prerequisites) pour plus d’informations sur l’authentification.

## Créer une connexion de base {#create-a-base-connection}

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Snowflake] dans le corps de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante permet de créer une connexion de base pour [!DNL Snowflake] :

>[!TIP]
>
>La valeur `auth.specName` doit être saisie exactement comme dans l’exemple ci-dessous, y compris les espaces vides.

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
          "specName": "Basic Authentication for Snowflake",
          "params": {
              "account": "wixnnnd-ui60793.snowflakecomputing.com",
              "database": "ACME_DB",
              "warehouse": "ACME_WH",
              "username": "nikola15",
              "schema": "PUBLIC",
              "password": "xxxx",
              "role": "ACCOUNTADMIN"
          }
      },
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.account` | Nom de votre compte de streaming [!DNL Snowflake]. |
| `auth.params.database` | Nom de la base de données [!DNL Snowflake] à partir de laquelle les données seront extraites. |
| `auth.params.warehouse` | Nom de votre entrepôt de [!DNL Snowflake]. L’entrepôt de [!DNL Snowflake] gère le processus d’exécution de la requête pour l’application. Chaque entrepôt est indépendant les uns des autres et doit être accessible individuellement lors de l’importation de données dans Experience Platform. |
| `auth.params.username` | Nom d’utilisateur de votre compte de streaming [!DNL Snowflake]. |
| `auth.params.schema` | (Facultatif) Schéma de base de données associé à votre compte de diffusion en continu [!DNL Snowflake]. |
| `auth.params.password` | Mot de passe de votre compte de streaming [!DNL Snowflake]. |
| `auth.params.role` | (Facultatif) Rôle de l’utilisateur pour cette connexion [!DNL Snowflake]. Si elle n’est pas fournie, cette valeur est `public` par défaut. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Snowflake] : `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion de base et son etag correspondant.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Explorer vos tableaux de données {#explore-your-data-tables}

Ensuite, utilisez l’identifiant de connexion de base pour explorer et parcourir les tableaux de données de votre source en envoyant une requête GET au point d’entrée `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` tout en fournissant votre identifiant de connexion de base en tant que paramètre.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identifiant de connexion de base de votre source de diffusion en continu [!DNL Snowflake]. |


**Requête**

La requête suivante récupère la structure et le contenu de votre compte de diffusion en continu [!DNL Snowflake].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/1b614dc0-b76e-41e1-b25f-09f4a9d3f111/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure et le contenu des données de votre source au niveau racine.

```json
{
    "items": [
        {
            "type": "table",
            "name": "ACME"
        }
    ]
}
```

| Propriété | Description |
| --- | --- |
| `items.type` | Type de la table. |
| `items.names` | Nom de la table. |

## Créer une connexion source {#create-a-source-connection}

Une connexion source crée et gère la connexion à la source externe à partir de laquelle les données sont ingérées.

Pour créer une connexion source, envoyez une requête POST au point d’entrée `/sourceConnections` de l’API [!DNL Flow Service].

**Format d’API**

```http
POST /sourceConnections
```

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Snowflake Streaming Source Connection",
      "description": "A source connection for Snowflake Streaming data",
      "baseConnectionId": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      },
      "params": {
          "tableName": "ACME",
          "timestampColumn": "dOb",
          "backfill": "true",
          "timezoneValue": "PST"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `baseConnectionId` | Identifiant de connexion de base authentifié pour votre source de diffusion en continu [!DNL Snowflake]. Cet identifiant a été généré lors d’une étape précédente. |
| `connectionSpec.id` | Identifiant de spécification de connexion pour la source de diffusion en continu [!DNL Snowflake]. |
| `params.tableName` | Nom de la table de votre base de données [!DNL Snowflake] que vous souhaitez importer dans Experience Platform. |
| `params.timestampColumn` | Nom de la colonne d’horodatage qui sera utilisée pour récupérer des valeurs incrémentielles. |
| `params.backfill` | Indicateur booléen qui détermine si les données sont récupérées depuis le début (0 heure d’époque) ou depuis le moment où la source est lancée. Pour plus d’informations sur cette valeur, consultez la [[!DNL Snowflake] présentation de la source de streaming](../../../../connectors/databases/snowflake-streaming.md). |
| `params.timezoneValue` | La valeur de fuseau horaire indique quel fuseau horaire actuel doit être récupéré lors de l’interrogation de la base de données [!DNL Snowflake]. Ce paramètre doit être fourni si la colonne timestamp de la configuration est définie sur `TIMESTAMP_NTZ`. S’il n’est pas fourni, `timezoneValue` est défini par défaut sur UTC. |

**Réponse**

Une réponse réussie renvoie votre identifiant de connexion source et son etag correspondant. L’identifiant de connexion source sera utilisé à une étape ultérieure pour créer un flux de données.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Créer un flux de données

>[!NOTE]
>
>Après avoir créé ou mis à jour un flux de données en continu, une brève pause de 5 minutes dans l’ingestion des données est nécessaire pour éviter toute instance potentielle de perte de données ou d’abandon de données.

Pour créer un flux de données afin de diffuser des données de votre compte [!DNL Snowflake] vers Experience Platform, vous devez effectuer une requête POST au point d’entrée `/flows` tout en fournissant les valeurs suivantes :

>[!TIP]
>
>Suivez les liens ci-dessous pour obtenir des guides détaillés sur la manière de récupérer les identifiants suivants.

* [ID de connexion source](#create-a-source-connection)
* [ID de connexion cible](../../collect/database-nosql.md#create-a-target-connection)
* [Identifiant de spécification de flux](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [Identifiant de mappage](../../collect/database-nosql.md#create-a-mapping)

**Format d’API**

```http
POST /flows
```

**Requête**

La requête suivante crée un flux de données en continu pour votre compte [!DNL Snowflake].

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake Streaming Dataflow",
      "description": "A dataflow for Snowflake streaming data",
      "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
      ],
      "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
      ],
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

| Propriété | Description |
| --- | --- |
| `sourceConnectionIds` | Identifiant de connexion source pour votre source de diffusion en continu [!DNL Snowflake]. |
| `targetConnectionIds` | Identifiant de connexion cible pour votre source de diffusion en continu [!DNL Snowflake]. |
| `flowSpec.id` | Identifiant de spécification de flux pour créer un flux de données pour une source de diffusion en continu [!DNL Snowflake]. Cet identifiant de spécification de flux vous permet de créer un flux de données en continu avec des transformations de mappage. Cet identifiant est fixe et est : `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `transformations.params.mappingId` | Identifiant de mappage pour votre flux de données. |

**Réponse**

Une réponse réussie renvoie votre identifiant de flux et son etag correspondant.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer un flux de données en continu pour vos données [!DNL Snowflake] à l’aide de l’API [!DNL Flow Service]. Consultez la documentation suivante pour plus d’informations sur les sources Adobe Experience Platform :

* [Présentation des sources](../../../../home.md)
* [Surveiller votre flux de données à l’aide d’API](../../monitor.md)
