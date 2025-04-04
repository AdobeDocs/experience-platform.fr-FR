---
keywords: Experience Platform;accueil;rubriques populaires;Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: Créer une connexion Source Apache Cassandra à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Apache Cassandra à Adobe Experience Platform à l’aide de l’API Flow Service.
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 47%

---


# Créer une connexion source [!DNL Apache Cassandra] à l’aide de l’API [!DNL Flow Service]

[!DNL Flow Service] est utilisé pour collecter et centraliser les données client provenant de diverses sources dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir desquelles toutes les sources prises en charge peuvent être connectées.

Ce tutoriel utilise l’API [!DNL Flow Service] pour vous guider tout au long des étapes de connexion de [!DNL Apache Cassandra] (ci-après dénommé « Cassandra ») à [!DNL Experience Platform].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin afin de réussir à vous connecter à Cassandra à l’aide de l’API [!DNL Flow Service].

### Collecter les informations d’identification requises

Pour connecter [!DNL Flow Service] à [!DNL Cassandra], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Adresse IP ou nom d’hôte du serveur [!DNL Cassandra]. |
| `port` | Port TCP utilisé par le serveur [!DNL Cassandra] pour écouter les connexions client. Le port par défaut est `9042`. |
| `username` | Nom d’utilisateur utilisé pour la connexion au serveur [!DNL Cassandra] pour l’authentification. |
| `password` | Mot de passe pour la connexion au serveur [!DNL Cassandra] pour l’authentification. |
| `connectionSpec.id` | Identifiant unique nécessaire à la création d’une connexion. L’identifiant de spécification de connexion pour [!DNL Cassandra] est `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Pour plus d’informations sur la prise en main, consultez [ce document Cassandra](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Experience Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{ORG_ID}`

Toutes les ressources d’[!DNL Experience Platform], y compris celles appartenant à l’[!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Un seul connecteur est requis par compte [!DNL Cassandra], car il peut être utilisé pour créer plusieurs connecteurs source afin d’importer différentes données.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une connexion [!DNL Cassandra], son identifiant de spécification de connexion unique doit être fourni dans le cadre de la requête POST. L’identifiant de spécification de connexion pour [!DNL Cassandra] est `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cassandra test connection",
        "description": "A test connection for Cassandra",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST},
                    "port": "{PORT}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
            "version": "1.0"
        }
    }'
```

| Paramètre | Description |
| --------- | ----------- |
| `auth.params.host` | Adresse IP ou nom d’hôte du serveur [!DNL Cassandra]. |
| `auth.params.port` | Port TCP utilisé par le serveur [!DNL Cassandra] pour écouter les connexions client. Le port par défaut est `9042`. |
| `auth.params.username` | Nom d’utilisateur utilisé pour la connexion au serveur [!DNL Cassandra] pour l’authentification. |
| `auth.params.password` | Mot de passe pour la connexion au serveur [!DNL Cassandra] pour l’authentification. |
| `connectionSpec.id` | L’identifiant de spécification de connexion [!DNL Cassandra] : `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le tutoriel suivant.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion [!DNL Cassandra] à l’aide de l’API [!DNL Flow Service] et d’obtenir la valeur d’identifiant unique de la connexion. Vous pouvez utiliser cet identifiant dans le tutoriel suivant lorsque vous apprendrez à [explorer des bases de données à l’aide de l’API Flow Service](../../explore/database-nosql.md).
