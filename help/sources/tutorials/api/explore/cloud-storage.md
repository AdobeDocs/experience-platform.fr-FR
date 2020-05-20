---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Explorez un système d’enregistrement cloud à l’aide de l’API de service de flux.
topic: overview
translation-type: tm+mt
source-git-commit: 7cd9bec7336d0e1d9f3036cf862633f498002af8
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 2%

---


# Explorez un système d’enregistrement cloud à l’aide de l’API de service de flux.

Le service de flux permet de collecter et de centraliser les données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources prises en charge sont connectables.

Ce didacticiel utilise l’API Flow Service pour explorer un système d’enregistrement cloud tiers.

## Prise en main

Ce guide nécessite une bonne compréhension des composants suivants d’Adobe Experience Platform :

* [Sources](../../../home.md): Experience Platform permet d’importer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de la plate-forme.
* [Sandbox](../../../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour vous connecter à un système d’enregistrement cloud à l’aide de l’API de service de flux.

### Obtention d’une connexion de base

Pour explorer un enregistrement cloud tiers à l’aide des API de plateforme, vous devez posséder un ID de connexion de base valide. Si vous ne disposez pas déjà d’une connexion de base pour l’enregistrement que vous souhaitez utiliser, vous pouvez en créer une à l’aide des didacticiels suivants :

* [Amazon S3](../create/cloud-storage/s3.md)
* [Azure Blob](../create/cloud-storage/blob.md)
* [Enregistrement Azure Data Lake Gen2](../create/cloud-storage/adls-gen2.md)
* [Google Cloud Store](../create/cloud-storage/google.md)
* [SFTP](../create/cloud-storage/sftp.md)

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience, y compris celles appartenant au service de flux, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de support supplémentaire :

* Content-Type : `application/json`

## Explorez votre enregistrement cloud

En utilisant la connexion de base pour votre enregistrement cloud, vous pouvez explorer des fichiers et des répertoires en exécutant des requêtes GET. Lorsque vous exécutez des requêtes GET pour explorer votre enregistrement cloud, vous devez inclure les paramètres de requête répertoriés dans le tableau ci-dessous :

| Paramètre | Description |
| --------- | ----------- |
| `objectType` | Type d’objet que vous souhaitez explorer. Définissez cette valeur comme suit : <ul><li>`folder`: Explorer un répertoire spécifique</li><li>`root`: Explorez le répertoire racine.</li></ul> |
| `object` | Ce paramètre n’est requis que lors de l’affichage d’un répertoire spécifique. Sa valeur représente le chemin du répertoire que vous souhaitez explorer. |

Utilisez l&#39;appel suivant pour trouver le chemin d&#39;accès du fichier que vous souhaitez importer dans la plate-forme :

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

## Inspection de la structure d’un fichier

Pour inspecter la structure du fichier de données à partir de votre enregistrement cloud, exécutez une requête GET tout en fournissant le chemin d’accès du fichier en tant que paramètre de requête.

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

En suivant ce didacticiel, vous avez exploré votre système d&#39;enregistrement cloud, trouvé le chemin d&#39;accès du fichier que vous souhaitez apporter à Platform et consulté sa structure. Vous pouvez utiliser ces informations dans le didacticiel suivant pour [collecter des données à partir de votre enregistrement cloud et les importer dans Platform](../collect/cloud-storage.md).