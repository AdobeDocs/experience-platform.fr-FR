---
keywords: Experience Platform ; accueil ; sujets populaires ; Apache Cassandra ; apache cassandra ; Cassandra ; cassandra
solution: Experience Platform
title: Création d’une connexion à la source Apache Cassandra à l’aide de l’API du service de flux
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Apache Cassandra à Adobe Experience Platform à l’aide de l’API Flow Service.
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 25%

---


# Créez une connexion source [!DNL Apache Cassandra] à l’aide de l’API [!DNL Flow Service].

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l&#39;API [!DNL Flow Service] pour vous guider dans les étapes de connexion de [!DNL Apache Cassandra] (ci-après appelée &quot;Cassandra&quot;) à [!DNL Experience Platform].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) :  [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à Cassandra à l&#39;aide de l&#39;API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] puisse se connecter à [!DNL Cassandra], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Adresse IP ou nom d’hôte du serveur [!DNL Cassandra]. |
| `port` | port TCP utilisé par le serveur [!DNL Cassandra] pour écouter les connexions client. Le port par défaut est `9042`. |
| `username` | Nom d’utilisateur utilisé pour la connexion au serveur [!DNL Cassandra] pour l’authentification. |
| `password` | Mot de passe de connexion au serveur [!DNL Cassandra] pour l&#39;authentification. |
| `connectionSpec.id` | Identificateur unique nécessaire pour créer une connexion. L&#39;ID de spécification de connexion pour [!DNL Cassandra] est `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Pour plus d&#39;informations sur la prise en main, consultez [ce document Cassandra](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* x-sandbox-name: `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Un seul connecteur est requis par compte [!DNL Cassandra], car il peut être utilisé pour créer plusieurs connecteurs source pour importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une connexion [!DNL Cassandra], l&#39;identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande du POST. L&#39;ID de spécification de connexion pour [!DNL Cassandra] est `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.port` | port TCP utilisé par le serveur [!DNL Cassandra] pour écouter les connexions client. Le port par défaut est `9042`. |
| `auth.params.username` | Nom d’utilisateur utilisé pour la connexion au serveur [!DNL Cassandra] pour l’authentification. |
| `auth.params.password` | Mot de passe de connexion au serveur [!DNL Cassandra] pour l&#39;authentification. |
| `connectionSpec.id` | ID de la spécification de connexion [!DNL Cassandra] : `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion [!DNL Cassandra] à l&#39;aide de l&#39;API [!DNL Flow Service] et obtenu la valeur d&#39;ID unique de la connexion. Vous pouvez utiliser cet identifiant dans le didacticiel suivant lorsque vous apprendrez à [explorer des bases de données à l’aide de l’API Flow Service](../../explore/database-nosql.md).
