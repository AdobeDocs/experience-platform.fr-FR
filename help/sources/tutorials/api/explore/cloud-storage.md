---
keywords: Experience Platform ; accueil ; rubriques populaires ; enregistrement cloud ; enregistrement Cloud
solution: Experience Platform
title: Exploration d’un système d’Enregistrements à forte intensité à l’aide de l’API du service de flux
topic: aperçu
description: Ce didacticiel utilise l’API Flow Service pour explorer un système d’enregistrement cloud tiers.
translation-type: tm+mt
source-git-commit: 60a70352c2e13565fd3e8c44ae68e011a1d443a6
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 20%

---


# Explorez un système d’enregistrement cloud à l’aide de l’API [!DNL Flow Service]

Ce didacticiel utilise l&#39;[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) pour explorer un système d&#39;enregistrement cloud tiers.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../home.md) :  [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
* [Sandbox](../../../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour vous connecter à un système d&#39;enregistrement cloud à l&#39;aide de l&#39;API [!DNL Flow Service].

### Obtention d’un ID de connexion

Pour explorer un enregistrement cloud tiers à l’aide des API [!DNL Platform], vous devez posséder un identifiant de connexion valide. Si vous n’avez pas encore de connexion pour l’enregistrement que vous souhaitez utiliser, vous pouvez en créer une à l’aide des didacticiels suivants :

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

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Explorez votre enregistrement cloud

L’ID de connexion de votre enregistrement cloud vous permet d’explorer des fichiers et des répertoires en exécutant des demandes de GET. Lorsque vous effectuez des demandes de GET pour explorer votre enregistrement cloud, vous devez inclure les paramètres de requête répertoriés dans le tableau ci-dessous :

| Paramètre | Description |
| --------- | ----------- |
| `objectType` | Type d’objet que vous souhaitez explorer. Définissez cette valeur comme suit : <ul><li>`folder`: Explorer un répertoire spécifique</li><li>`root`: Explorez le répertoire racine.</li></ul> |
| `object` | Ce paramètre n’est requis que lors de l’affichage d’un répertoire spécifique. Sa valeur représente le chemin du répertoire que vous souhaitez explorer. |

Utilisez l&#39;appel suivant pour trouver le chemin d&#39;accès du fichier que vous souhaitez importer dans [!DNL Platform] :

**Format d’API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
GET /connections/{CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Paramètre | Description |
| --- | --- |
| `{CONNECTION_ID}` | ID de connexion de votre connecteur source d’enregistrement cloud. |
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

Une réponse réussie renvoie un tableau de fichiers et de dossiers trouvés dans le répertoire interrogé. Prenez note de la propriété `path` du fichier que vous souhaitez télécharger, car vous devez la fournir à l&#39;étape suivante pour inspecter sa structure.

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

Pour inspecter la structure du fichier de données à partir de votre enregistrement cloud, effectuez une demande de GET tout en indiquant le chemin d’accès du fichier et saisissez-le comme paramètre de requête.

Vous pouvez inspecter la structure d’un fichier CSV ou TSV en spécifiant un délimiteur personnalisé comme périmètre de requête. Toute valeur de caractère unique est un délimiteur de colonne autorisé. Si elle n’est pas fournie, une virgule `(,)` est utilisée comme valeur par défaut.

**Format d’API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&preview=true&fileType=delimited&columnDelimiter=;
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&preview=true&fileType=delimited&columnDelimiter=\t
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | ID de connexion de votre connecteur source d’enregistrement cloud. |
| `{FILE_PATH}` | Chemin d&#39;accès au fichier que vous souhaitez inspecter. |
| `{FILE_TYPE}` | Type du fichier. Les types de fichiers pris en charge sont les suivants :<ul><li>DELIMITED</code> : Valeur séparée par des délimiteurs. Les fichiers DSV doivent être séparés par des virgules.</li><li>JSON</code> : Notation d’objet JavaScript. Les fichiers JSON doivent être compatibles XDM</li><li>PARQUET</code> : Parquet Apache. Les fichiers de parquets doivent être conformes à XDM.</li></ul> |
| `columnDelimiter` | Valeur d’un caractère unique que vous avez spécifiée comme délimiteur de colonne pour inspecter les fichiers CSV ou TSV. Si le paramètre n&#39;est pas fourni, la valeur est par défaut une virgule `(,)`. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/some/path/data.csv&fileType=DELIMITED' \
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

En suivant ce didacticiel, vous avez exploré votre système d&#39;enregistrement cloud, trouvé le chemin d&#39;accès au fichier que vous souhaitez apporter à [!DNL Platform] et consulté sa structure. Vous pouvez utiliser ces informations dans le didacticiel suivant pour [collecter des données à partir de votre enregistrement cloud et les importer dans Platform](../collect/cloud-storage.md).