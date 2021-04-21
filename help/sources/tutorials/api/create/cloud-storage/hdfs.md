---
keywords: Experience Platform ; accueil ; sujets populaires ; Apache Hadoop Distributed File System ; Apache hadoop ; hdfs ; HDFS
solution: Experience Platform
title: Création d’une connexion source Apache HDFS à l’aide de l’API du service de flux
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter un système de fichiers distribué d'Hadoop Apache à Adobe Experience Platform à l'aide de l'API de service de flux.
exl-id: 04fa65db-073c-48e1-b981-425185ae08aa
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 26%

---

# Créez une connexion source [!DNL Apache] HDFS à l&#39;aide de l&#39;API [!DNL Flow Service]

>[!NOTE]
>
>Le connecteur Apache HDFS est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../../../home.md#terms-and-conditions).

[!DNL Flow Service] sert à collecter et à centraliser les données client provenant de diverses sources disparates pour les importer dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l&#39;API [!DNL Flow Service] pour vous guider dans les étapes de connexion d&#39;un système de fichiers distribué d&#39;Hadoop Apache (ci-après appelé &quot;HDFS&quot;) à [!DNL Experience Platform].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) :  [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Sandbox](../../../../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour établir une connexion réussie à HDFS à l&#39;aide de l&#39;API [!DNL Flow Service].

### Collecte des informations d’identification requises

| Informations d’identification | Description |
| ---------- | ----------- |
| `url` | L’URL définit les paramètres d’authentification requis pour la connexion anonyme à HDFS. Pour plus d&#39;informations sur la façon d&#39;obtenir cette valeur, consultez [ce document HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |
| `connectionSpec.id` | Identificateur nécessaire pour créer une connexion. L&#39;ID de spécification de connexion fixe pour HDFS est `54e221aa-d342-4707-bcff-7a4bceef0001`. |

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

Une connexion spécifie une source et contient vos informations d’identification pour cette source. Une seule connexion est requise par compte HDFS, car elle peut être utilisée pour créer plusieurs connecteurs source pour importer des données différentes.

**Format d’API**

```http
POST /connections
```

**Requête**

La demande suivante crée une nouvelle connexion HDFS, configurée par les propriétés fournies dans la charge utile :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "HDFS test connection",
        "description": "A test connection for an HDFS source",
        "auth": {
            "specName": "Anonymous Authentication",
            "params": {
                "url": "{URL}"
                }
        },
        "connectionSpec": {
            "id": "54e221aa-d342-4707-bcff-7a4bceef0001",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `auth.params.url` | URL qui définit les paramètres d&#39;authentification requis pour la connexion anonyme à HDFS |
| `connectionSpec.id` | ID de spécification de connexion HDFS : `54e221aa-d342-4707-bcff-7a4bceef0001`. |

**Réponse**

Une réponse réussie renvoie les détails de la connexion nouvellement créée, y compris son identifiant unique (`id`). Cet identifiant est nécessaire pour explorer vos données dans le didacticiel suivant.

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion HDFS à l&#39;aide de l&#39;API [!DNL Flow Service] et obtenu la valeur d&#39;ID unique de la connexion. Vous pouvez utiliser cet identifiant dans le didacticiel suivant lorsque vous apprendrez à [explorer un enregistrement cloud tiers à l’aide de l’API Flow Service](../../explore/cloud-storage.md).
