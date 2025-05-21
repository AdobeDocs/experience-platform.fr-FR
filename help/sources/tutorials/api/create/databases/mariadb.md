---
title: Connecter MariaDB à Experience Platform à l’aide de l’API Flow Service
description: Découvrez comment connecter votre compte MariaDB à Experience Platform à l’aide d’API.
exl-id: 9b7ff394-ca55-4ab4-99ef-85c80b04a6df
source-git-commit: bca4f40d452f0a5e70a388872a65640d1fd58533
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 22%

---

# Connexion de [!DNL MariaDB] à Experience Platform à l’aide de l’API [!DNL Flow Service]

Lisez ce guide pour savoir comment connecter votre compte [!DNL MariaDB] à Adobe Experience Platform à l’aide de l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Commencer

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour réussir à vous connecter à [!DNL MariaDB] à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Lisez la [[!DNL MariaDB] présentation](../../../../connectors/databases/mariadb.md#prerequisites) pour plus d’informations sur l’authentification.

### Utilisation des API Experience Platform

Lisez le guide sur [Prise en main des API Experience Platform](../../../../../landing/api-guide.md) pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform.

## Connexion de [!DNL MariaDB] à Experience Platform

Pour plus d’informations sur la connexion de votre compte [!DNL MariaDB] à Experience Platform, lisez les étapes ci-dessous.

### Créer une connexion de base pour [!DNL MariaDB]

Une connexion de base conserve les informations échangées entre votre source et Experience Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

**Format d’API**

```https
POST /connections
```

Pour créer un identifiant de connexion de base, envoyez une requête POST au point d’entrée `/connections` et indiquez les informations d’authentification appropriées pour votre compte [!DNL MariaDB].

>[!BEGINTABS]

>[!TAB Authentification basée sur une chaîne de connexion]

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
| `auth.params.connectionString` | Chaîne de connexion associée à votre authentification [!DNL MariaDB]. Le modèle de chaîne de connexion [!DNL MariaDB] est : `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL MariaDB] est : `3000eb99-cd47-43f3-827c-43caf170f015`. |

+++

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle connexion de base, y compris son identifiant unique (`id`).

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
| `auth.params.server` | Nom ou adresse IP de la base de données [!DNL MariaDB]. |
| `auth.params.database` | Nom de la base de données. |
| `auth.params.username` | Nom d’utilisateur correspondant à votre base de données. |
| `auth.params.password` | Mot de passe correspondant à votre base de données. |
| `auth.params.sslMode` | Méthode de chiffrement des données lors du transfert de données. |
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


## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion de base à [!DNL MariaDB] à l’aide de l’API [!DNL Flow Service]. Vous pouvez utiliser cet identifiant de connexion de base dans les tutoriels suivants : 

* [Explorez la structure et le contenu de vos tableaux de données à l’aide de l’API  [!DNL Flow Service] .](../../explore/tabular.md)
* [Créez un flux de données pour importer les données de la base de données dans Experience Platform à l’aide de l’API  [!DNL Flow Service] ](../../collect/database-nosql.md)
