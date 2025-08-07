---
title: Connecter la base de données Oracle à Experience Platform à l’aide de l’API Flow Service
description: Découvrez comment connecter la base de données Oracle à Experience Platform à l’aide d’API.
exl-id: b1cea714-93ff-425f-8e12-6061da97d094
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 5%

---

# Connexion de [!DNL Oracle DB] à Experience Platform à l’aide de l’API [!DNL Flow Service]

Lisez ce guide pour savoir comment connecter votre compte [!DNL Oracle DB] à Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à vous connecter à [!DNL Oracle] à l’aide de l’API [!DNL Flow Service].

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../../../landing/api-guide.md).

### Collecter les informations d’identification requises

Lisez la [[!DNL Oracle DB] présentation](../../../../connectors/databases/oracle.md#prerequisites) pour plus d’informations sur l’authentification.

## Connecter [!DNL Oracle DB] à Experience Platform sur Azure {#azure}

Pour plus d’informations sur la connexion de votre compte [!DNL Oracle DB] à Experience Platform sur Azure, lisez les étapes ci-dessous.

### Créer une connexion de base pour [!DNL Oracle DB] sur Experience Platform sur Azure {#azure-base}

Une connexion de base lie votre source à Experience Platform, stockant les détails d’authentification, le statut de connexion et un identifiant unique. Utilisez cet identifiant pour parcourir les fichiers sources et identifier les éléments spécifiques à ingérer, y compris leurs types et formats de données.

**Format d’API**

```https
POST /connections
```

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez vos informations d’authentification [!DNL Oracle DB] dans les paramètres de la requête.

**Requête**

La requête suivante crée une connexion de base pour [!DNL Oracle DB] à l’aide de l’authentification de chaîne de connexion.

+++Afficher la demande


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Oracle DB base connection",
    "description": "A base connection to connect Oracle DB to Experience Platform on Azure",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "Host={HOST};Port={PORT};Sid={SID};UserId={USERNAME};Password={PASSWORD}"
      }
    },
    "connectionSpec": {
      "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
      "version": "1.0"
    }
  }'
```

| Paramètre | Description |
| --------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion utilisée pour la connexion à [!DNL Oracle DB]. Le modèle de chaîne de connexion [!DNL Oracle DB] est : `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Identifiant de spécification de connexion [!DNL Oracle] : `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

+++

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle connexion de base, y compris son identifiant unique (`id`).

+++Afficher la réponse

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

+++

## Connexion de [!DNL Oracle DB] à Experience Platform sur Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../../../landing/multi-cloud.md).

Pour plus d’informations sur la connexion de votre compte [!DNL Oracle DB] à Experience Platform sur AWS, lisez les étapes ci-dessous.

### Créer une connexion de base pour [!DNL Oracle DB] sur Experience Platform sur AWS {#aws-base}

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour [!DNL Oracle DB] connecter à Experience Platform sur AWS.

+++Afficher la demande

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle DB on Experience Platform AWS",
      "description": "Oracle DB on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "diy.us-dawkins-1.oraclecloud.com",
              "port": "1521",
              "database": "mcmg_profits_diy.oraclecloud.com",
              "username": "Admin",
              "password": "xxxx",
              "schema": "ADMIN",
              "sslMode": "true"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.server` | L’adresse IP ou le nom d’hôte de votre serveur [!DNL Oracle DB]. |
| `auth.params.port` | Numéro de port du serveur [!DNL Oracle DB]. |
| `auth.params.database` | Nom de l’instance [!DNL Oracle DB] à laquelle vous vous connectez. |
| `auth.params.username` | Compte utilisateur associé à votre instance [!DNL Oracle DB]. |
| `auth.prams.password` | Mot de passe correspondant à votre compte utilisateur [!DNL Oracle DB]. |
| `auth.params.schema` | Schéma contenant les objets de la base de données. |
| `auth.params.sslMode` | Valeur booléenne qui indique si les mesures SSL sont appliquées ou non. |
| `connectionSpec.id` | Identifiant de spécification de connexion correspondant à la source [!DNL Oracle DB]. Cette valeur d’identifiant est fixe comme suit : `d6b52d86-f0f8-475f-89d4-ce54c8527328.` |

+++

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle connexion de base, y compris son identifiant unique (`id`) et l’identifiant correspondant. Vous pouvez utiliser l’identifiant pour [créer une connexion source](../../collect/database-nosql.md#create-a-source-connection) et l’`etag` pour [mettre à jour votre compte](../../update.md).

+++Afficher la réponse

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++


## Créer un flux de données pour les données [!DNL Oracle DB]

Maintenant que vous avez correctement connecté votre compte [!DNL Oracle DB], vous pouvez [créer un flux de données et ingérer les données de votre base de données dans Experience Platform](../../collect/database-nosql.md).