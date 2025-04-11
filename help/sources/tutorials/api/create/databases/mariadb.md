---
title: Connecter MariaDB à Experience Platform à l’aide de l’API Flow Service
description: Découvrez comment connecter votre compte MariaDB à Experience Platform à l’aide d’API.
exl-id: 9b7ff394-ca55-4ab4-99ef-85c80b04a6df
source-git-commit: d5d47f9ca3c01424660fe33f8310586a70a32875
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 18%

---

# Connexion de [!DNL MariaDB] à Experience Platform à l’aide de l’API [!DNL Flow Service]

Lisez ce guide pour savoir comment connecter votre compte [!DNL MariaDB] à Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet l’ingestion de données à partir de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de services Experience Platform.
* [Environnements](../../../../../sandboxes/home.md) de test : Experience Platform fournit des environnements de test virtuels qui partitionnent une seule instance de Experience Platform dans des environnements virtuels distincts pour aider à développer et à faire évoluer les applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires que vous devrez connaître pour réussir à vous connecter à [!DNL MariaDB] l’aide de l’API [!DNL Flow Service] .

### Collecter les informations d’identification requises

Lisez la [[!DNL MariaDB] présentation](../../../../connectors/databases/mariadb.md#prerequisites) pour plus d’informations sur l’authentification.

### Utilisation des API Experience Platform

Lisez le guide sur [Prise en main des API Experience Platform](../../../../../landing/api-guide.md) pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform.

## Connecter [!DNL MariaDB] à Experience Platform sur Azure {#azure}

Pour plus d’informations sur la connexion de votre compte [!DNL MariaDB] à Experience Platform sur Azure, lisez les étapes ci-dessous.

### Créer une connexion de base pour [!DNL MariaDB] Experience Platform sur Azure {#azure-base}

Une connexion de base conserve les informations entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre ID de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

**Format d’API**

```https
POST /connections
```

Pour créer un ID de connexion de base, faites une demande POST au `/connections` point de terminaison et fournissez les informations d’identification d’authentification appropriées pour votre [!DNL MariaDB] compte.

>[!BEGINTABS]

>[!TAB Authentification basée sur la chaîne de connexion]

**Requête**

La requête suivante crée une connexion de base pour une source [!DNL MariaDB] à l’aide de l’authentification par chaîne de connexion .

+++Afficher l’exemple de requête

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/connections' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d '{
    "name": "MariaDB connection",
    "description": "MariaDB connection",
    "auth": {
        "specName": "Connection String Based Authentication",
        "params": {
            "connectionString": "Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "3000eb99-cd47-43f3-827c-43caf170f015",
        "version": "1.0"
    }
}'
```

| Propriété | Description |
| -------- | ----------- |
| `auth.params.connectionString` | Chaîne de connexion associée à votre [!DNL MariaDB] authentification. Le [!DNL MariaDB] modèle de chaîne de connexion est : `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL MariaDB] est : `3000eb99-cd47-43f3-827c-43caf170f015`. |

+++

**Réponse**

Une réponse positive renvoie les détails de la connexion de base nouvellement créée, y compris son identifiant unique (`id`).

+++Afficher l’exemple de réponse

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

+++

>[!TAB  Authentification de base ]

**Requête**

La requête suivante crée une connexion de base pour une source [!DNL MariaDB] à l’aide de l’authentification de base.

+++Afficher l’exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MariaDB on Experience Platform using basic auth",
      "description": "MariaDB on Experience Platform using basic auth",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.server` | Le nom ou l’adresse IP de votre [!DNL MariaDB] base de données. |
| `auth.params.database` | Nom de votre base de données. |
| `auth.params.username` | Nom d’utilisateur correspondant à votre base de données. |
| `auth.params.password` | Mot de passe correspondant à votre base de données. |
| `auth.params.sslMode` | Méthode de chiffrement des données durant le transfert des données. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL MariaDB] est : `3000eb99-cd47-43f3-827c-43caf170f015`. |

+++

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle connexion de base, y compris son identifiant unique (`id`).

+++Afficher l’exemple de réponse

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

>[!ENDTABS]

## Connexion de [!DNL MariaDB] à Experience Platform sur Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la vue d’ensemble [](../../../../../landing/multi-cloud.md)Experience Platform multicloud.

Pour plus d’informations sur la connexion de votre compte [!DNL MariaDB] à Experience Platform sur AWS, lisez les étapes ci-dessous.

### Créer une connexion de base pour [!DNL MariaDB] sur Experience Platform sur AWS {#aws-base}

**Format d’API**

```https
POST /connections
```

**Requête**

La demande suivante crée une connexion de base pour [!DNL MariaDB] se connecter à Experience Platform sur AWS.

+++Voir l’exemple de demande

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MariaDB on Experience Platform AWS",
      "description": "MariaDB on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `auth.params.server` | Le nom ou l’adresse IP de votre [!DNL MariaDB] base de données. |
| `auth.params.database` | Nom de votre base de données. |
| `auth.params.username` | Nom d’utilisateur correspondant à votre base de données. |
| `auth.params.password` | Mot de passe correspondant à votre base de données. |
| `auth.params.sslMode` | Méthode de chiffrement des données lors du transfert de données. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL MariaDB] est : `3000eb99-cd47-43f3-827c-43caf170f015`. |

+++

**Réponse**

Une réponse positive renvoie les détails de la connexion de base nouvellement créée, y compris son identifiant unique (`id`).

+++Afficher l’exemple de réponse

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++


## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL MariaDB] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer les données de la base de données dans Experience Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/database-nosql.md)
