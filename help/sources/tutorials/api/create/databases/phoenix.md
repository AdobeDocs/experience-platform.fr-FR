---
keywords: Experience Platform;home;popular topics;Phoenix;phoenix
solution: Experience Platform
title: Création d’un connecteur Phoenix à l’aide de l’API Flow Service
topic: overview
type: Tutorial
description: Ce didacticiel utilise l’API Flow Service pour vous guider à travers les étapes de connexion d’une base de données Phoenix à un Experience Platform.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 14%

---


# Création d’un [!DNL Phoenix] connecteur à l’aide de l’ [!DNL Flow Service] API

>[!NOTE]
>
>Le [!DNL Phoenix] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’ [!DNL Flow Service] API pour vous guider dans les étapes de connexion d’une [!DNL Phoenix] base de données à [!DNL Experience Platform].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully connect to [!DNL Phoenix] using the [!DNL Flow Service] API.

### Collecte des informations d’identification requises

Pour [!DNL Flow Service] établir une connexion avec [!DNL Phoenix], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Adresse IP ou nom d’hôte du [!DNL Phoenix] serveur. |
| `username` | Nom d’utilisateur utilisé pour accéder au [!DNL Phoenix] serveur. |
| `password` | Mot de passe correspondant à l’utilisateur. |
| `port` | port TCP utilisé par le [!DNL Phoenix] serveur pour écouter les connexions client. Si vous vous connectez à [!DNL Azure] HDInsights, spécifiez le port 443. |
| `httpPath` | URL partielle correspondant au [!DNL Phoenix] serveur. Spécifiez /hbasephoenix0 si vous utilisez [!DNL Azure] la grappe HDInsights. |
| `enableSsl` | Valeur booléenne. Indique si les connexions au serveur sont chiffrées à l’aide de SSL. |
| `connectionSpec.id` | Identificateur unique nécessaire pour créer une connexion. L&#39;ID de spécification de connexion pour [!DNL Phoenix] est : `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Pour plus d&#39;informations sur la prise en main, consultez [ce document](https://python-phoenixdb.readthedocs.io/en/latest/api.html)Phoenix.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../../../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par [!DNL Phoenix] compte, car elle peut être utilisée pour créer plusieurs connecteurs source pour importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

Pour créer une [!DNL Phoenix] connexion, son identifiant de spécification de connexion unique doit être fourni dans le cadre de la demande du POST. L&#39;ID de spécification de connexion pour [!DNL Phoenix] est `102706fb-a5cd-42ee-afe0-bc42f017ff43`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}",
            "port" : {PORT},
            "httpPath" : "{PATH}",
            "enableSsl" : {SSL}
            }
        },
        "connectionSpec": {
            "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.host` | The host of the [!DNL Phoenix] server. |
| `auth.params.username` | Nom d’utilisateur associé à votre [!DNL Phoenix] connexion. |
| `auth.params.password` | Mot de passe associé à votre [!DNL Phoenix] connexion. |
| `auth.params.port` | Port TCP de votre [!DNL Phoenix] connexion. |
| `auth.params.httpPath` | Chemin d’accès http partiel pour votre [!DNL Phoenix] connexion. |
| `auth.params.enableSsl` | Valeur booléenne qui spécifie si les connexions au serveur sont chiffrées à l’aide de SSL. |
| `connectionSpec.id` | ID de spécification de [!DNL Phoenix] connexion : `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une [!DNL Phoenix] connexion à l’aide de l’ [!DNL Flow Service] API et obtenu la valeur d’ID unique de la connexion. Vous pouvez utiliser cet identifiant dans le didacticiel suivant lorsque vous apprendrez à [explorer des bases de données à l’aide de l’API](../../explore/database-nosql.md)Flow Service.