---
keywords: Experience Platform;accueil;rubriques les plus consultées;espace de stockage dans le cloud;espace de stockage dans le cloud
title: Exploration d’un dossier de stockage dans le cloud à l’aide de l’API Flow Service
description: Ce tutoriel utilise l’API Flow Service pour explorer un système de stockage dans le cloud tiers.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: 88e6f084ce1b857f785c4c1721d514ac3b07e80b
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 19%

---

# Explorez vos dossiers de stockage dans le cloud à l’aide de la méthode [!DNL Flow Service] API

Ce tutoriel décrit les étapes à suivre pour explorer et prévisualiser la structure et le contenu de votre espace de stockage dans le cloud à l’aide du [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API.

>[!NOTE]
>
>Pour explorer votre espace de stockage dans le cloud, vous devez déjà disposer d’un identifiant de connexion de base valide pour une source de stockage dans le cloud. Si vous ne disposez pas de cet identifiant, reportez-vous à la section [présentation des sources](../../../home.md#cloud-storage) pour obtenir la liste des sources de stockage dans le cloud avec lesquelles vous pouvez créer une connexion de base.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../home.md) : [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuelles qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../../landing/api-guide.md).

## Explorez les dossiers de stockage dans le cloud

Vous pouvez récupérer des informations sur la structure de vos dossiers de stockage dans le cloud en adressant une demande de GET à la variable [!DNL Flow Service] de l’API tout en fournissant l’identifiant de connexion de base de votre source.

Lors de l’exécution de requêtes GET pour explorer votre espace de stockage dans le cloud, vous devez inclure les paramètres de requête répertoriés dans le tableau ci-dessous :

| Paramètre | Description |
| --------- | ----------- |
| `objectType` | Type d’objet que vous souhaitez explorer. Définissez cette valeur comme suit : <ul><li>`folder`: Exploration d’un répertoire spécifique</li><li>`root`: Explorez le répertoire racine.</li></ul> |
| `object` | Ce paramètre est requis uniquement lors de l’affichage d’un répertoire spécifique. Sa valeur représente le chemin dʼaccès au répertoire que vous souhaitez explorer. |


**Format d’API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identifiant de connexion de base de votre source de stockage dans le cloud. |
| `{PATH}` | Chemin d’accès d’un répertoire. |

**Requête**

```shell
curl -X GET \
  'http://platform.adobe.io/data/foundation/flowservice/connections/dc3c0646-5e30-47be-a1ce-d162cb8f1f07/explore?objectType=folder&object=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau de fichiers et de dossiers trouvés dans le répertoire interrogé. Prenez note de la `path` du fichier que vous souhaitez charger, car vous devez le fournir à l’étape suivante pour examiner sa structure.

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
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=FILE&object={FILE_PATH}&preview=true&ileType=delimited&encoding=ISO-8859-1;
```

| Paramètre | Description |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Identifiant de connexion de votre connecteur source de stockage dans le cloud. |
| `{FILE_PATH}` | Le chemin d’accès au fichier que vous souhaitez inspecter. |
| `{FILE_TYPE}` | Type du fichier. Les types de fichiers pris en charge sont les suivants :<ul><li>DELIMITED</code>: Valeur séparée par un délimiteur. Les fichiers DSV doivent être séparés par des virgules.</li><li>JSON</code>: Notation d’objet JavaScript. Les fichiers JSON doivent être conformes à XDM</li><li>PARQUET</code>: Apache Parquet. Les fichiers parquet doivent être conformes à XDM.</li></ul> |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs pouvant être utilisés pour filtrer les résultats. Voir la section sur [paramètres de requête](#query) pour plus d’informations. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Le [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) prend en charge l’utilisation de paramètres de requête pour prévisualiser et inspecter différents types de fichiers.

| Paramètre | Description |
| --------- | ----------- |
| `columnDelimiter` | La valeur à caractère unique que vous avez spécifiée comme délimiteur de colonne pour inspecter les fichiers CSV ou TSV. Si le paramètre n’est pas fourni, la valeur est définie par défaut sur une virgule. `(,)`. |
| `compressionType` | Paramètre de requête requis pour la prévisualisation d’un fichier délimité compressé ou JSON. Les fichiers compressés pris en charge sont les suivants : <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | Définit le type de codage à utiliser lors de la prévisualisation du rendu. Les types de codage pris en charge sont les suivants : `UTF-8` et `ISO-8859-1`. **Remarque**: Le `encoding` n’est disponible que lors de l’ingestion de fichiers CSV délimités. Les autres types de fichiers seront ingérés avec le codage par défaut, `UTF-8`. |

## Étapes suivantes

En suivant ce tutoriel, vous avez exploré votre système de stockage dans le cloud et trouvé le chemin d’accès au fichier auquel vous souhaitez apporter votre contribution. [!DNL Platform], et a consulté sa structure. Vous pouvez utiliser ces informations dans le tutoriel suivant pour [collecter des données à partir de votre espace de stockage dans le cloud et les importer dans Platform ;](../collect/cloud-storage.md).
