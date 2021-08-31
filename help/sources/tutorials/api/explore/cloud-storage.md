---
keywords: Experience Platform;accueil;rubriques les plus consultées;espace de stockage dans le cloud;espace de stockage dans le cloud
solution: Experience Platform
title: Exploration d’un système de stockage cLoud à l’aide de l’API Flow Service
topic-legacy: overview
description: Ce tutoriel utilise l’API Flow Service pour explorer un système de stockage dans le cloud tiers.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 25%

---

# Explorez un système de stockage dans le cloud à l’aide de l’API [!DNL Flow Service]

Ce tutoriel utilise l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) pour explorer un système de stockage cloud tiers.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../home.md) :  [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Environnements de test](../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à un système de stockage dans le cloud à l’aide de l’API [!DNL Flow Service].

### Obtention d’un identifiant de connexion

Pour explorer un espace de stockage dans le cloud tiers à l’aide des API [!DNL Platform], vous devez posséder un identifiant de connexion valide. Si vous ne disposez pas déjà d’une connexion pour le stockage que vous souhaitez utiliser, vous pouvez en créer une via les tutoriels suivants :

* [[!DNL Amazon S3]](../create/cloud-storage/s3.md)
* [[!DNL Azure Blob]](../create/cloud-storage/blob.md)
* [[!DNL Azure Data Lake Storage Gen2]](../create/cloud-storage/adls-gen2.md)
* [[!DNL Azure File Storage]](../create/cloud-storage/azure-file-storage.md)
* [[!DNL FTP]](../create/cloud-storage/ftp.md)
* [[!DNL Google Cloud Storage]](../create/cloud-storage/google.md)
* [HDFS](../create/cloud-storage/hdfs.md)
* [[!DNL Oracle Object Storage]](../create/cloud-storage/oracle-object-storage.md)
* [[!DNL SFTP]](../create/cloud-storage/sftp.md)

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L&#39;exemple JSON renvoyé dans les réponses de l&#39;API est également fourni. Pour plus d&#39;informations sur les conventions utilisées dans la documentation pour les exemples d&#39;appels d&#39;API, voir la section concernant la [lecture d&#39;exemples d&#39;appels d&#39;API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d&#39;abord suivre le [tutoriel d&#39;authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Le tutoriel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d&#39;API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources qui se trouvent dans [!DNL Experience Platform], y compris celles liées à la [!DNL Flow Service], sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Explorez votre espace de stockage dans le cloud

À l’aide de l’identifiant de connexion de votre espace de stockage dans le cloud, vous pouvez explorer les fichiers et les répertoires en effectuant des requêtes GET. Lors de l’exécution de requêtes GET pour explorer votre espace de stockage dans le cloud, vous devez inclure les paramètres de requête répertoriés dans le tableau ci-dessous :

| Paramètre | Description |
| --------- | ----------- |
| `objectType` | Type d’objet que vous souhaitez explorer. Définissez cette valeur comme suit : <ul><li>`folder`: Exploration d’un répertoire spécifique</li><li>`root`: Explorez le répertoire racine.</li></ul> |
| `object` | Ce paramètre est requis uniquement lors de l’affichage d’un répertoire spécifique. Sa valeur représente le chemin du répertoire que vous souhaitez explorer. |

Utilisez l’appel suivant pour trouver le chemin d’accès au fichier que vous souhaitez importer dans [!DNL Platform] :

**Format d’API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
GET /connections/{CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Paramètre | Description |
| --- | --- |
| `{CONNECTION_ID}` | Identifiant de connexion de votre connecteur source de stockage dans le cloud. |
| `{PATH}` | Chemin d’accès d’un répertoire. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau de fichiers et de dossiers trouvés dans le répertoire interrogé. Prenez note de la propriété `path` du fichier que vous souhaitez télécharger, car vous devez la fournir à l’étape suivante pour examiner sa structure.

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "/test-connectors/testFolder-fileIngestion/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "profileData.json",
        "path": "/test-connectors/testFolder-fileIngestion/profileData.json",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "sampleprofile--3.parquet",
        "path": "/test-connectors/testFolder-fileIngestion/sampleprofile--3.parquet",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect de la structure d’un fichier

Pour examiner la structure du fichier de données à partir de votre espace de stockage dans le cloud, effectuez une requête de GET tout en fournissant le chemin d’accès du fichier et saisissez comme paramètre de requête.

Vous pouvez examiner la structure d’un fichier de données à partir de votre source de stockage dans le cloud en exécutant une requête de GET tout en fournissant le chemin et le type du fichier. Vous pouvez également examiner différents types de fichiers, tels que CSV, TSV ou JSON compressé et les fichiers délimités, en spécifiant leurs types de fichiers dans les paramètres de requête.

**Format d’API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Identifiant de connexion de votre connecteur source de stockage dans le cloud. |
| `{FILE_PATH}` | Le chemin d’accès au fichier que vous souhaitez inspecter. |
| `{FILE_TYPE}` | Type du fichier. Les types de fichiers pris en charge sont les suivants :<ul><li>DELIMITED</code> : Valeur séparée par un délimiteur. Les fichiers DSV doivent être séparés par des virgules.</li><li>JSON</code> : Notation d’objet JavaScript. Les fichiers JSON doivent être conformes à XDM</li><li>PARQUET</code> : Apache Parquet. Les fichiers parquet doivent être conformes à XDM.</li></ul> |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs pouvant être utilisés pour filtrer les résultats. Voir la section [Paramètres de requête](#query) pour plus d’informations. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
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

## Utilisation des paramètres de requête {#query}

[[!DNL Flow Service] L’API](https://www.adobe.io/experience-platform-apis/references/flow-service/) prend en charge l’utilisation de paramètres de requête pour prévisualiser et inspecter différents types de fichiers.

| Paramètre | Description |
| --------- | ----------- |
| `columnDelimiter` | La valeur à caractère unique que vous avez spécifiée comme délimiteur de colonne pour inspecter les fichiers CSV ou TSV. Si le paramètre n’est pas fourni, la valeur est par défaut une virgule `(,)`. |
| `compressionType` | Paramètre de requête requis pour la prévisualisation d’un fichier délimité compressé ou JSON. Les fichiers compressés pris en charge sont les suivants : <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |

## Étapes suivantes

En suivant ce tutoriel, vous avez exploré votre système de stockage dans le cloud, trouvé le chemin d’accès au fichier que vous souhaitez importer dans [!DNL Platform] et consulté sa structure. Vous pouvez utiliser ces informations dans le tutoriel suivant pour [collecter des données à partir de votre espace de stockage dans le cloud et les importer dans Platform](../collect/cloud-storage.md).
