---
title: Connexion de votre compte de diffusion en continu de Snowflake à Adobe Experience Platform
description: Découvrez comment connecter Adobe Experience Platform à Snowflake Streaming à l’aide de l’API Flow Service.
badgeBeta: label="Version bêta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3fc225a4-746c-4a91-aa77-bbeb091ec364
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 26%

---

# Diffuser des données [!DNL Snowflake] vers l’Experience Platform à l’aide de l’API [!DNL Flow Service]

>[!IMPORTANT]
>
>* La source de diffusion [!DNL Snowflake] est en version bêta. Pour plus d’informations sur l’utilisation de sources étiquetées bêta, consultez la [Présentation des sources](../../../../home.md#terms-and-conditions).
>* La source de diffusion en continu [!DNL Snowflake] est disponible dans l’API pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Ce tutoriel décrit les étapes à suivre pour connecter et diffuser des données de votre compte [!DNL Snowflake] vers Adobe Experience Platform à l’aide de l’ [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Pour obtenir des informations sur la configuration préalable et des informations sur la source de diffusion [!DNL Snowflake]. Veuillez lire la [[!DNL Snowflake] présentation de la source de diffusion en continu](../../../../connectors/databases/snowflake-streaming.md).

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur la [Prise en main des API Platform](../../../../../landing/api-guide.md).

## Créer une connexion de base {#create-a-base-connection}

Une connexion de base conserve les informations échangées entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au point de terminaison `/connections` tout en fournissant vos informations d’authentification [!DNL Snowflake] dans le cadre du corps de la requête.

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
| `auth.params.account` | Nom de votre compte de diffusion [!DNL Snowflake]. |
| `auth.params.database` | Nom de la base de données [!DNL Snowflake] à partir de laquelle les données seront extraites. |
| `auth.params.warehouse` | Nom de votre entrepôt [!DNL Snowflake]. L’entrepôt [!DNL Snowflake] gère le processus d’exécution de requête pour l’application. Chaque entrepôt est indépendant l’un de l’autre et doit être accessible individuellement lors de l’importation de données vers Platform. |
| `auth.params.username` | Nom d’utilisateur de votre compte de diffusion [!DNL Snowflake] en continu. |
| `auth.params.schema` | (Facultatif) Le schéma de base de données associé à votre compte de diffusion en continu [!DNL Snowflake]. |
| `auth.params.password` | Mot de passe de votre compte de diffusion [!DNL Snowflake] en continu. |
| `auth.params.role` | (Facultatif) Le rôle de l’utilisateur pour cette connexion [!DNL Snowflake]. Si elle n’est pas fournie, cette valeur est définie par défaut sur `public`. |
| `connectionSpec.id` | ID de spécification de connexion [!DNL Snowflake] : `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**Réponse**

Une réponse réussie renvoie la connexion de base nouvellement créée et son etag correspondant.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Exploration des tableaux de données {#explore-your-data-tables}

Ensuite, utilisez l’identifiant de connexion de base pour explorer et parcourir les tableaux de données de votre source en effectuant une requête GET sur le point de terminaison `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` tout en fournissant votre identifiant de connexion de base en tant que paramètre.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | L’identifiant de connexion de base de votre source de diffusion en continu [!DNL Snowflake]. |


**Requête**

La requête suivante récupère la structure et le contenu de votre compte de diffusion [!DNL Snowflake].

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
| `items.type` | Type du tableau. |
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
| `baseConnectionId` | L’identifiant de connexion de base authentifié pour votre source de diffusion en continu [!DNL Snowflake]. Cet identifiant a été généré lors d’une étape précédente. |
| `connectionSpec.id` | Identifiant de spécification de connexion pour la source de diffusion en continu [!DNL Snowflake]. |
| `params.tableName` | Le nom de la table dans la base de données [!DNL Snowflake] que vous souhaitez importer dans Platform. |
| `params.timestampColumn` | Nom de la colonne d’horodatage qui sera utilisée pour récupérer les valeurs incrémentielles. |
| `params.backfill` | Indicateur booléen qui détermine si les données sont récupérées à partir du début (0 époque) ou à partir du moment où la source est lancée. Pour plus d’informations sur cette valeur, consultez la [[!DNL Snowflake] présentation de la source de diffusion en continu](../../../../connectors/databases/snowflake-streaming.md). |
| `params.timezoneValue` | La valeur du fuseau horaire indique l’heure actuelle du fuseau horaire à récupérer lors de l’interrogation de la base de données [!DNL Snowflake]. Ce paramètre doit être fourni si la colonne d’horodatage de la configuration est définie sur `TIMESTAMP_NTZ`. Si non fourni, `timezoneValue` est défini par défaut sur UTC. |

**Réponse**

Une réponse réussie renvoie votre identifiant de connexion source et son etag correspondant. L’identifiant de connexion source sera utilisé ultérieurement pour créer un flux de données.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Créer un flux de données

Pour créer un flux de données permettant de diffuser des données depuis le compte [!DNL Snowflake] vers Platform, vous devez envoyer une requête de POST au point de terminaison `/flows` tout en fournissant les valeurs suivantes :

>[!TIP]
>
>Suivez les liens ci-dessous pour obtenir des guides détaillés sur la manière de récupérer les ID suivants.

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
| `sourceConnectionIds` | L’identifiant de connexion source pour votre source de diffusion en continu [!DNL Snowflake]. |
| `targetConnectionIds` | L’identifiant de connexion cible pour votre source de diffusion en continu [!DNL Snowflake]. |
| `flowSpec.id` | Identifiant de spécification de flux pour créer un flux de données pour une source de diffusion en continu [!DNL Snowflake]. Cet identifiant de spécification de flux vous permet de créer un flux de données en continu avec des transformations de mappage. Cet identifiant est fixe et est : `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `transformations.params.mappingId` | L’identifiant de mappage de votre flux de données. |

**Réponse**

Une réponse réussie renvoie votre identifiant de flux et son etag correspondant.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données en continu pour vos données [!DNL Snowflake] à l’aide de l’API [!DNL Flow Service]. Pour plus d’informations sur les sources Adobe Experience Platform, consultez la documentation suivante :

* [Présentation des sources](../../../../home.md)
* [Surveillance de votre flux de données à l’aide d’API](../../monitor.md)
