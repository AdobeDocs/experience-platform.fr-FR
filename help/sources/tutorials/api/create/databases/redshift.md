---
keywords: Experience Platform ; accueil ; sujets populaires ; redshift ; Redshift ; Amazon Redshift ; amazon redshift
solution: Experience Platform
title: Création d’une connexion à la source Amazon Redshift à l’aide de l’API du service de flux
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Amazon Redshift à l’aide de l’API Flow Service.
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 26%

---

# Créez une connexion source [!DNL Amazon Redshift] à l’aide de l’API [!DNL Flow Service].

>[!NOTE]
>
>Le connecteur [!DNL Amazon Redshift] est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../../../home.md#terms-and-conditions).

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l&#39;API [!DNL Flow Service] pour vous guider à travers les étapes de connexion de [!DNL Experience Platform] à [!DNL Amazon Redshift] (ci-après appelée &quot;[!DNL Redshift]&quot;).

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) :  [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à [!DNL Redshift] à l&#39;aide de l&#39;API [!DNL Flow Service].

### Collecte des informations d’identification requises

Pour que [!DNL Flow Service] puisse se connecter à [!DNL Redshift], vous devez fournir les propriétés de connexion suivantes :

| **Informations d’identification** | **Description** |
| -------------- | --------------- |
| `server` | Serveur associé à votre compte [!DNL Redshift]. |
| `username` | Nom d&#39;utilisateur associé à votre compte [!DNL Redshift]. |
| `password` | Mot de passe associé à votre compte [!DNL Redshift]. |
| `database` | La base de données [!DNL Redshift] à laquelle vous accédez. |

Pour plus d&#39;informations sur la prise en main, consultez [ce document Redshift](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Création d’une connexion

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte [!DNL Redshift], car elle peut être utilisée pour créer plusieurs connecteurs source afin d’importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
            }
        },
        "connectionSpec": {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| ------------- | --------------- |
| `auth.params.server` | Votre serveur [!DNL Redshift]. |
| `auth.params.database` | Base de données associée à votre compte [!DNL Redshift]. |
| `auth.params.password` | Mot de passe associé à votre compte [!DNL Redshift]. |
| `auth.params.username` | Nom d&#39;utilisateur associé à votre compte [!DNL Redshift]. |
| `connectionSpec.id` | Spécification de connexion `id` de votre compte [!DNL Redshift] récupérée à l&#39;étape précédente. |

**Réponse**

Une réponse réussie renvoie la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion [!DNL Redshift] à l&#39;aide de l&#39;API [!DNL Flow Service] et obtenu la valeur d&#39;ID unique de la connexion. Vous pouvez utiliser cet ID de connexion dans le didacticiel suivant lorsque vous apprendrez à [explorer des bases de données ou des systèmes NoSQL à l’aide de l’API Flow Service](../../explore/database-nosql.md).
