---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Explorez un système d’enregistrement cloud à l’aide de l’API de service de flux.
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 14%

---


# Explorez un système d’enregistrement cloud à l’aide de l’ [!DNL Flow Service] API.

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates au sein de l’Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’ [!DNL Flow Service] API pour explorer un système d’enregistrement cloud tiers.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../home.md): [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully connect to a cloud storage system using the [!DNL Flow Service] API.

### Obtention d’une connexion de base

Pour explorer un enregistrement cloud tiers à l’aide [!DNL Platform] d’API, vous devez posséder un identifiant de connexion de base valide. Si vous ne disposez pas déjà d’une connexion de base pour l’enregistrement que vous souhaitez utiliser, vous pouvez en créer une à l’aide des didacticiels suivants :

* [Amazon S3](../create/cloud-storage/s3.md)
* [Azure Blob](../create/cloud-storage/blob.md)
* [Enregistrement Azure Data Lake Gen2](../create/cloud-storage/adls-gen2.md)
* [Google Cloud Store](../create/cloud-storage/google.md)
* [SFTP](../create/cloud-storage/sftp.md)

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Explorez votre enregistrement cloud

En utilisant la connexion de base pour votre enregistrement cloud, vous pouvez explorer des fichiers et des répertoires en exécutant des demandes de GET. Lorsque vous effectuez des demandes de GET pour explorer votre enregistrement cloud, vous devez inclure les paramètres de requête répertoriés dans le tableau ci-dessous :

| Paramètre | Description |
| --------- | ----------- |
| `objectType` | Type d’objet que vous souhaitez explorer. Définissez cette valeur comme suit : <ul><li>`folder`: Explorer un répertoire spécifique</li><li>`root`: Explorez le répertoire racine.</li></ul> |
| `object` | Ce paramètre n’est requis que lors de l’affichage d’un répertoire spécifique. Sa valeur représente le chemin du répertoire que vous souhaitez explorer. |

Utilisez l&#39;appel suivant pour trouver le chemin d&#39;accès au fichier que vous souhaitez importer [!DNL Platform]:

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID d’une connexion de base d’enregistrement cloud. |
| `{PATH}` | Chemin d’accès d’un répertoire. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau de fichiers et de dossiers trouvés dans le répertoire interrogé. Notez la `path` propriété du fichier que vous souhaitez transférer, car vous devez la fournir à l’étape suivante pour inspecter sa structure.

```json
[
    {
        "type": "File",
        "name": "data.csv",
        "path": "/some/path/data.csv"
    },
    {
        "type": "Folder",
        "name": "foobar",
        "path": "/some/path/foobar"
    }
]
```

## Inspect de la structure d’un fichier

Pour inspecter la structure du fichier de données à partir de votre enregistrement cloud, effectuez une demande de GET tout en fournissant le chemin d’accès du fichier en tant que paramètre de requête.

**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID d’une connexion de base d’enregistrement cloud. |
| `{FILE_PATH}` | Chemin d’accès à un fichier. |
| `{FILE_TYPE}` | Type du fichier. Les types de fichiers pris en charge sont les suivants :<ul><li>DÉLIMITÉ</code>: Valeur séparée par des délimiteurs. Les fichiers DSV doivent être séparés par des virgules.</li><li>JSON</code>: Notation d’objet JavaScript. Les fichiers JSON doivent être compatibles XDM</li><li>PARQUET</code>: Parquet Apache. Les fichiers de parquets doivent être conformes à XDM.</li></ul> |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/some/path/data.csv&fileType=DELIMITED' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure du fichier interrogé, y compris les noms de table et les types de données.

```json
[
    {
        "name": "Id",
        "type": "String"
    },
    {
        "name": "FirstName",
        "type": "String"
    },
    {
        "name": "LastName",
        "type": "String"
    },
    {
        "name": "Email",
        "type": "String"
    },
    {
        "name": "Phone",
        "type": "String"
    }
]
```

## Étapes suivantes

En suivant ce didacticiel, vous avez exploré votre système d’enregistrement de cloud, trouvé le chemin d’accès au fichier que vous souhaitez importer [!DNL Platform]et consulté sa structure. Vous pouvez utiliser ces informations dans le didacticiel suivant pour [collecter des données à partir de votre enregistrement cloud et les importer dans Platform](../collect/cloud-storage.md).