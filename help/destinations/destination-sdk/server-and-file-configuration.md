---
description: Les spécifications de configuration du serveur et des fichiers pour les destinations basées sur des fichiers peuvent être configurées dans Adobe Experience Platform Destination SDK via le point dʼentrée « /destination-servers ».
title: (Version Beta) Options de configuration pour les spécifications de serveur de destination basées sur des fichiers
exl-id: 56434e36-0458-45d9-961d-f6505de998f7
source-git-commit: 7a72c190d28d63c7bcd1bf12d8a52efc4589b848
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 90%

---

# (Version Beta) Configuration du serveur et des fichiers pour les spécifications de serveur de destination basées sur des fichiers

## Présentation {#overview}

>[!IMPORTANT]
>
>La fonctionnalité de configuration et d’envoi de destinations basées sur des fichiers à l’aide de Destination SDK d’Adobe Experience Platform est actuellement en version Beta. La documentation et la fonctionnalité peuvent changer.

Cette page détaille toutes les options de configuration de serveur pour vos serveurs de destination basés sur des fichiers et vous indique comment configurer diverses options de configuration de fichier pour les utilisateurs qui exportent des fichiers depuis Experience Platform vers votre destination.

Les spécifications de configuration du serveur et des fichiers pour les destinations basées sur des fichiers peuvent être configurées dans Adobe Experience Platform Destination SDK via le point dʼentrée `/destination-servers`. Pour obtenir une liste complète des opérations que vous pouvez effectuer sur le point dʼentrée, consultez la section [Opérations de point d’entrée de l’API du serveur de destination](./destination-server-api.md).

## Spécification du serveur de destination Amazon S3 basé sur des fichiers {#s3-example}

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Nom de votre connexion de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour [!DNL Amazon S3], définissez ce paramètre sur `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | Chaîne | Nom de l’intervalle [!DNL Amazon S3] à utiliser par cette destination. |
| `fileBasedS3Destination.path.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | Chaîne | Chemin d’accès au dossier de destination qui hébergera les fichiers exportés. |
| `fileConfigurations` | Objet | Voir [configuration du formatage de fichier](#file-configuration) pour obtenir des explications détaillées sur cette section. |

{style=&quot;table-layout:auto&quot;}

## Spécification du serveur de destination SFTP basé sur des fichiers {#sftp-example}

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port": 22,
      "encryptionMode" : "PGP"
   },
    "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Nom de votre connexion de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour les destinations [!DNL SFTP], définissez ce paramètre sur `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | Chaîne | Répertoire racine de lʼespace de stockage de destination. |
| `fileBasedSftpDestination.hostName.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | Chaîne | Nom d’hôte de lʼespace de stockage de destination. |
| `port` | Nombre entier | Port du serveur de fichiers SFTP. |
| `encryptionMode` | Chaîne | Indique s’il faut utiliser le chiffrement de fichier. Valeurs prises en charge : <ul><li>PGP</li><li>Aucun</li></ul> |
| `fileConfigurations` | Objet | Voir [configuration du formatage de fichier](#file-configuration) pour obtenir des explications détaillées sur cette section. |

{style=&quot;table-layout:auto&quot;}

## Spécification du serveur de destination basé sur des fichiers [!DNL Azure Data Lake Storage] ([!DNL ADLS]) {#adls-example}

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Nom de votre connexion de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour les destinations [!DNL Azure Data Lake Storage], définissez ce paramètre sur `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Chaîne | Chemin d’accès au dossier de destination qui hébergera les fichiers exportés. |
| `fileConfigurations` | Objet | Voir [configuration du formatage de fichier](#file-configuration) pour obtenir des explications détaillées sur cette section. |

{style=&quot;table-layout:auto&quot;}

## Spécification du serveur de destination basé sur des fichiers [!DNL Azure Blob Storage] {#blob-example}

```json
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Nom de votre connexion de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour les destinations [!DNL Azure Blob Storage], définissez ce paramètre sur `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | Chaîne | Chemin d’accès au dossier de destination qui hébergera les fichiers exportés. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | Chaîne | Nom du conteneur [!DNL Azure Blob Storage] à utiliser par cette destination. |
| `fileConfigurations` | Objet | Voir [configuration du formatage de fichier](#file-configuration) pour obtenir des explications détaillées sur cette section. |

{style=&quot;table-layout:auto&quot;}

## Spécification du serveur de destination basé sur des fichiers [!DNL Data Landing Zone] ([!DNL DLZ]) {#dlz-example}

```json
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   },
   "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Nom de votre connexion de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour les destinations [!DNL Data Landing Zone], définissez ce paramètre sur `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Chaîne | *Obligatoire.*  Utilisez `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Chaîne | Chemin d’accès au dossier de destination qui hébergera les fichiers exportés. |
| `fileConfigurations` | Objet | Voir [configuration du formatage de fichier](#file-configuration) pour obtenir des explications détaillées sur cette section. |

{style=&quot;table-layout:auto&quot;}

## Spécification du serveur de destination basé sur des fichiers [!DNL Google Cloud Storage] {#gcs-example}

```json
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
   "fileConfigurations":{
      // See the file formatting configuration section further below on this page
   }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Nom de votre connexion de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour les destinations [!DNL Google Cloud Storage], définissez ce paramètre sur `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Chaîne | *Obligatoire.*  Utilisez `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Chaîne | Nom de l’intervalle [!DNL Google Cloud Storage] à utiliser par cette destination. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | Chaîne | Chemin d’accès au dossier de destination qui hébergera les fichiers exportés. |
| `fileConfigurations` | Objet | Voir [configuration du formatage de fichier](#file-configuration) pour obtenir des explications détaillées sur cette section. |

{style=&quot;table-layout:auto&quot;}

## Configuration du formatage de fichier {#file-configuration}

Cette section décrit les paramètres de formatage de fichier pour les fichiers `CSV` exportés. Vous pouvez modifier plusieurs propriétés des fichiers exportés pour répondre aux exigences du système de réception de fichiers de votre côté, afin de lire et interpréter de manière optimale les fichiers reçus d’Experience Platform.

>[!NOTE]
>
>Les options CSV ne sont disponibles que lors de l’exportation de fichiers CSV. La section `fileConfigurations` n’est pas obligatoire lors de la configuration d’un nouveau serveur de destination. Si vous ne transmettez aucune valeur dans l’appel API pour les options CSV, les valeurs par défaut du tableau ci-dessous seront utilisées.

```json
"fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "lineSep": {
                "templatingStrategy": "NONE",
                "value": "\n"
            }
        },
        "maxFileRowCount":5000000
    }
```

| Champ | Obligatoire / Facultatif | Description | Valeur par défaut |
|---|---|---|---|
| `compression.value` | Facultatif | Codec de compression à utiliser lors de l’enregistrement de données dans un fichier. Valeurs prises en charge : `none`, `bzip2`, `gzip`, `lz4` et `snappy`. | `none` |
| `fileType.value` | Facultatif | Indique le format du fichier de sortie. Valeurs prises en charge : `csv`, `parquet` et `json`. | `csv` |
| `csvOptions.quote.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit un caractère unique utilisé pour lʼéchappement des valeurs entre guillemets où le séparateur peut faire partie de la valeur. | `null` |
| `csvOptions.quoteAll.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique si toutes les valeurs doivent toujours être placées entre guillemets. La valeur par défaut est lʼéchappement des valeurs contenant un guillemet. | `false` |
| `csvOptions.escape.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit un caractère unique utilisé pour lʼéchappement des guillemets dans une valeur déjà entre guillemets. | `\` |
| `csvOptions.escapeQuotes.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique si les valeurs contenant des guillemets doivent toujours être placées entre guillemets. La valeur par défaut est lʼéchappement de toutes les valeurs contenant un guillemet. | `true` |
| `csvOptions.header.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique s’il faut écrire les noms des colonnes comme première ligne. | `true` |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique s’il faut supprimer les espaces de tête des valeurs. | `true` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique s’il faut supprimer les espaces de fin des valeurs. | `true` |
| `csvOptions.nullValue.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit la représentation sous forme de chaîne d’une valeur nulle. | `""` |
| `csvOptions.dateFormat.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique le format de date. | `yyyy-MM-dd` |
| `csvOptions.timestampFormat.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit la chaîne qui indique un format d’horodatage. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` |
| `csvOptions.charToEscapeQuoteEscaping.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit un caractère unique utilisé pour l’échappement du caractère de guillemet. | `\` lorsque les caractères d’échappement et de guillemet sont différents. `\0` lorsque les caractères d’échappement et de guillemet sont identiques. |
| `csvOptions.emptyValue.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit la représentation sous forme de chaîne d’une valeur vide. | `""` |
| `csvOptions.lineSep.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit le séparateur de ligne à utiliser pour l’écriture. Longueur maximale : 1 caractère. | `\n` |
| `maxFileRowCount` | Facultatif | Nombre maximal de lignes que le fichier exporté peut contenir. Configurez ce paramètre en fonction des exigences de taille de fichier de la plateforme de destination. | S.O. |

{style=&quot;table-layout:auto&quot;}