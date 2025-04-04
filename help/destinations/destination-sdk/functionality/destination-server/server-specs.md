---
description: Découvrez comment configurer les spécifications de serveur de destination dans Adobe Experience Platform Destination SDK via le point d’entrée `/authoring/destination-servers`.
title: Spécifications de serveur pour les destinations créées avec Destination SDK
exl-id: 62202edb-a954-42ff-9772-863cea37a889
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2753'
ht-degree: 89%

---

# Spécifications de serveur pour les destinations créées avec Destination SDK

Les spécifications du serveur de destination définissent le type de plateforme de destination qui recevra les données de Adobe Experience Platform, ainsi que les paramètres de communication entre Experience Platform et la destination. Par exemple :

* Une spécification du serveur de destination [streaming](#streaming-example) définit le point d’entrée du serveur HTTP qui recevra les messages HTTP d’Experience Platform. Pour savoir comment configurer les appels HTTP au point d’entrée, consultez la page [Spécifications du modèle](templating-specs.md).
* Une spécification du serveur de destination [Amazon S3](#s3-example) définit le nom du compartiment [!DNL S3] et le chemin d’accès où Experience Platform exportera les fichiers.
* Une spécification du serveur de destination [SFTP](#sftp-example) définit le nom d’hôte, le répertoire racine, le port de communication et le type de chiffrement du serveur SFTP sur lequel Experience Platform exportera les fichiers.

Pour comprendre la place de ce composant dans une intégration créée avec Destination SDK, consultez le diagramme de la documentation [Options de configuration](../configuration-options.md) ou consultez les pages de vue d’ensemble de la configuration de destination suivantes :

* [Utiliser Destination SDK pour configurer une destination de diffusion en streaming](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Utilisation de Destination SDK pour configurer une destination basée sur des fichiers](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

Vous pouvez configurer les spécifications du serveur de destination via le point d’entrée `/authoring/destination-servers`. Pour obtenir des exemples d’appels API détaillés dans lesquels vous pouvez configurer les composants affichés sur cette page, consultez les pages de référence de l’API suivantes.

* [Création d’une configuration de serveur de destination](../../authoring-api/destination-server/create-destination-server.md)
* [Mise à jour d’une configuration de serveur de destination](../../authoring-api/destination-server/update-destination-server.md)

Cette page montre tous les types de serveurs de destination pris en charge par Destination SDK, avec tous leurs paramètres de configuration. Pendant la création de la destination, remplacez les valeurs de paramètre par les vôtres.

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Types d’intégration pris en charge {#supported-integration-types}

Pour en savoir plus sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page, consultez le tableau ci-dessous.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (streaming) | Oui |
| Intégrations basées sur des fichiers (par lots) | Oui |

Pendant la [création](../../authoring-api/destination-server/create-destination-server.md) ou la [mise à jour](../../authoring-api/destination-server/update-destination-server.md) d’un serveur de destination, utilisez l’une des configurations de type de serveur décrites sur cette page. En fonction des exigences de votre intégration, veillez à remplacer les exemples de valeurs de paramètre de ces exemples par les vôtres.

## Champs codés en dur ou modélisés {#templatized-fields}

Pendant la création d’un serveur de destination avec Destination SDK, vous pouvez définir des valeurs de paramètre de configuration en les codant en dur dans la configuration ou en utilisant des champs modélisés. Les champs modélisés vous permettent de lire les valeurs fournies par l’utilisateur à partir de l’interface utilisateur d’Experience Platform.

Les paramètres du serveur de destination comportent deux champs configurables. Ces options indiquent si vous utilisez des valeurs codées en dur ou modélisées.

| Paramètre | Type | Description |
|---|---|---|
| `templatingStrategy` | Chaîne | *Obligatoire.* Définit s’il existe une valeur codée en dur fournie via le champ `value` ou une valeur configurable par l’utilisateur dans l’interface utilisateur. Valeurs prises en charge : <ul><li>`NONE` : utilisez cette valeur quand vous codez en dur la valeur du paramètre via le paramètre `value` (voir la ligne suivante). Exemple : `"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1` : utilisez cette valeur quand vous souhaitez que vos utilisateurs fournissent une valeur de paramètre dans l’interface utilisateur. Exemple : `"value": "{{customerData.bucket}}"`. </li></ul> |
| `value` | Chaîne | *Obligatoire*. Définit la valeur du paramètre. Types de valeur pris en charge : <ul><li>**Valeur codée en dur** : utilisez une valeur codée en dur (telle que `"value": "my-storage-bucket"`) quand vous n’avez pas besoin que les utilisateurs saisissent une valeur de paramètre dans l’interface utilisateur. Quand vous codez une valeur en dur, `templatingStrategy` doit toujours être définie sur `NONE`.</li><li>**Valeur modélisée** : utilisez une valeur modélisée (telle que `"value": "{{customerData.bucket}}"`) quand vous souhaitez que vos utilisateurs fournissent une valeur de paramètre dans l’interface utilisateur. Pendant l’utilisation de valeurs modélisées, `templatingStrategy` doit toujours être définie sur `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### Quand préférer les champs codés en dur aux champs modélisés ?

Les champs codés en dur et modélisés ont chacun leur propre utilité dans Destination SDK, selon le type d’intégration que vous créez.

**Connexion à la destination sans entrée utilisateur**

Lorsque les utilisateurs [se connectent à la destination](../../../ui/connect-destination.md) dans l’interface utilisateur d’Experience Platform, vous pouvez gérer le processus de connexion de destination sans qu’ils aient à intervenir.

Pour ce faire, vous pouvez coder en dur les paramètres de connexion de la plateforme de destination dans la spécification du serveur. Quand vous utilisez des valeurs de paramètre codées en dur dans la configuration de votre serveur de destination, la connexion entre Adobe Experience Platform et votre plateforme de destination est gérée sans que l’utilisateur ait à intervenir.

Dans l’exemple ci-dessous, un partenaire crée un serveur de destination de zone d’entrée de données avec le fichier `path.value` codé en dur.

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"NONE",
         "value":"Your/hardcoded/path/here"
      },
      "useCase": "Your use case"
   }
}
```

Ainsi, quand les utilisateurs consultent le [tutoriel de connexion à la destination](../../../ui/connect-destination.md), ils ne verront pas l’[étape d’authentification](../../../ui/connect-destination.md#authenticate). Au lieu de cela, l’authentification est gérée par Experience Platform, comme illustré dans l’image ci-dessous.

![Image de l’interface utilisateur affichant l’écran d’authentification entre Experience Platform et une destination DLZ.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**Connexion à la destination avec entrée utilisateur**

Lorsque la connexion entre Experience Platform et la destination doit être établie à la suite d’une entrée utilisateur spécifique dans l’interface utilisateur d’Experience Platform, telle que la sélection d’un point d’entrée de l’API ou la fourniture d’une valeur de champ, vous pouvez utiliser des champs modélisés dans la spécification du serveur pour lire la saisie utilisateur et vous connecter à votre plateforme de destination.

Dans l’exemple ci-dessous, un partenaire crée une intégration en [temps réel (streaming)](#streaming-example) et le champ `url.value` utilise le paramètre modélisé `{{customerData.region}}` pour personnaliser une partie du point d’entrée de l’API en fonction de l’entrée utilisateur.

```json
{
   "name":"Templatized API endpoint example",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.yourcompany.com/data/{{customerData.region}}/items"
      }
   }
}
```

Pour permettre aux utilisateurs de sélectionner une valeur dans l’interface utilisateur d’Experience Platform, le paramètre `region` doit également être défini dans la [configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md) en tant que champ de données client, comme illustré ci-dessous :

```json
"customerDataFields":[
   {
      "name":"region",
      "title":"Region",
      "description":"Select an option",
      "type":"string",
      "isRequired":true,
      "readOnly":false,
      "enum":[
         "US",
         "EU"
      ]
   }
```

Ainsi, quand les utilisateurs consultent le [tutoriel de connexion à la destination](../../../ui/connect-destination.md), ils doivent sélectionner une zone géographique avant de pouvoir se connecter à la plateforme de destination. Quand ils se connectent à la destination, le champ modélisé `{{customerData.region}}` est remplacé par la valeur sélectionnée par l’utilisateur dans l’interface utilisateur, comme illustré dans l’image ci-dessous.

![Image de l’interface utilisateur affichant l’écran de connexion de destination avec un sélecteur de zone géographique.](../../assets/functionality/destination-server/server-spec-template-region.png)

## Serveur de destination en temps réel (streaming) {#streaming-example}

Ce type de serveur de destination vous permet d’exporter des données d’Adobe Experience Platform vers la destination via des requêtes HTTP. La configuration de serveur contient des informations sur le serveur recevant les messages (le serveur de votre côté).

Ce processus fournit des données utilisateur sous forme d’une série de messages HTTP vers votre plateforme de destination. Les paramètres ci-dessous forment le modèle de spécifications du serveur HTTP.

L’exemple ci-dessous montre un modèle de configuration de serveur de destination pour une destination en temps réel (streaming).

```json
{
   "name":"Your destination server name",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{YOUR_API_ENDPOINT}"
      }
   }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | *Obligatoire.* Représente le nom convivial de votre serveur, visible uniquement par Adobe. Ce nom n’est pas visible pour les partenaires ou les clients. Exemple : `Moviestar destination server`. |
| `destinationServerType` | Chaîne | *Obligatoire.* Définissez-le sur `URL_BASED` pour les destinations de diffusion en streaming. |
| `templatingStrategy` | Chaîne | *Obligatoire.* <ul><li>Utilisez `PEBBLE_V1` si vous utilisez un champ modélisé au lieu d’une valeur codée en dur dans le champ `value`. Utilisez cette option si vous disposez d’un point d’entrée du type `https://api.moviestar.com/data/{{customerData.region}}/items`, où les utilisateurs doivent sélectionner la région du point d’entrée dans l’interface utilisateur d’Experience Platform. </li><li> Utilisez `NONE` si aucune transformation de modèle n’est nécessaire du côté d’Adobe, par exemple si vous avez un point d’entrée, tel que `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Chaîne | *Obligatoire.* Renseignez l’adresse du point d’entrée de l’API auquel Experience Platform doit se connecter. |

{style="table-layout:auto"}

## Serveur de destination [!DNL Amazon S3] {#s3-example}

Ce serveur de destination vous permet d’exporter des fichiers contenant des données Adobe Experience Platform vers votre enregistrement Amazon S3.

L’exemple ci-dessous montre un modèle de configuration de serveur de destination pour une destination Amazon S3.

```json
{
   "name":"Amazon S3 destination",
   "destinationServerType":"FILE_BASED_S3",
   "fileBasedS3Destination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Nom de votre serveur de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour exporter des fichiers vers un compartiment [!DNL Amazon S3], définissez cette valeur sur `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans le champ `bucket.value`.<ul><li>Si vous souhaitez que vos utilisateurs saisissent leur propre nom de compartiment dans l’interface utilisateur d’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser le champ `value` pour lire une valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur. Ce cas d’utilisation est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un nom de compartiment codé en dur pour votre intégration, tel que `"bucket.value":"MyBucket"`, définissez cette valeur sur `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | Chaîne | Nom de l’intervalle [!DNL Amazon S3] à utiliser par cette destination. Il peut s’agir d’un champ modélisé qui lit la valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans le champ `path.value`.<ul><li>Si vous souhaitez que vos utilisateurs saisissent leur propre chemin dans l’interface utilisateur d’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser le champ `path.value` pour lire une valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur. Ce cas d’utilisation est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un chemin d’accès codé en dur pour votre intégration, tel que `"bucket.value":"/path/to/MyBucket"`, définissez cette valeur sur `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | Chaîne | Chemin d’accès à l’intervalle [!DNL Amazon S3] à utiliser par cette destination. Il peut s’agir d’un champ modélisé qui lit la valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## Serveur de destination [!DNL SFTP] {#sftp-example}

Ce serveur de destination vous permet d’exporter des fichiers contenant des données Adobe Experience Platform vers votre serveur de stockage [!DNL SFTP].

L’exemple ci-dessous montre un modèle de configuration de serveur de destination pour une destination SFTP.

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSFTPDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port":22,
      "encryptionMode":"PGP"
   }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Nom de votre serveur de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour exporter des fichiers vers une destination [!DNL SFTP], définissez cette valeur sur `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans le champ `rootDirectory.value`.<ul><li>Si vous souhaitez que vos utilisateurs saisissent leur propre chemin d’accès au répertoire racine dans l’interface utilisateur d’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser le champ `rootDirectory.value` pour lire une valeur fournie par l’utilisateur à partir des [champs de données client](../destination-configuration/customer-data-fields.md) renseigné. Ce cas d’utilisation est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un chemin d’accès au répertoire racine codé en dur pour votre intégration, tel que `"rootDirectory.value":"Storage/MyDirectory"`, définissez cette valeur sur `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | Chaîne | Chemin d’accès au répertoire qui hébergera les fichiers exportés. Il peut s’agir d’un champ modélisé qui lit la valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans le champ `hostName.value`.<ul><li>Si vous souhaitez que vos utilisateurs saisissent leur propre nom d’hôte dans l’interface utilisateur d’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser le champ `hostName.value` pour lire une valeur fournie par l’utilisateur à partir des [champs de données client](../destination-configuration/customer-data-fields.md) renseigné. Ce cas d’utilisation est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un nom d’hôte codé en dur pour votre intégration, tel que `"hostName.value":"my.hostname.com"`, définissez cette valeur sur `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | Chaîne | Nom d’hôte de votre serveur SFTP. Il peut s’agir d’un champ modélisé qui lit la valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `"hostName.value":"my.hostname.com"`. |
| `port` | Nombre entier | Port du serveur de fichiers SFTP. |
| `encryptionMode` | Chaîne | Indique s’il faut utiliser le chiffrement de fichier. Valeurs prises en charge : <ul><li>PGP</li><li>Aucun</li></ul> |

{style="table-layout:auto"}

## Serveur de destination [!DNL Azure Data Lake Storage] ([!DNL ADLS]) {#adls-example}

Ce serveur de destination vous permet d’exporter des fichiers contenant des données Adobe Experience Platform vers votre compte [!DNL Azure Data Lake Storage].

L’exemple ci-dessous montre un modèle de configuration de serveur de destination pour une destination [!DNL Azure Data Lake Storage].

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Nom de votre connexion de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour les destinations [!DNL Azure Data Lake Storage], définissez ce paramètre sur `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans le champ `path.value`.<ul><li>Si vous souhaitez que vos utilisateurs saisissent leur chemin d’accès au dossier [!DNL ADLS] dans l’interface utilisateur d’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser le champ `path.value` pour lire une valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur. Ce cas d’utilisation est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un chemin d’accès codé en dur pour votre intégration, tel que `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`, définissez cette valeur sur `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | Chaîne | Le chemin d’accès à votre dossier de stockage [!DNL ADLS]. Il peut s’agir d’un champ modélisé qui lit la valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## Serveur de destination [!DNL Azure Blob Storage] {#blob-example}

Ce serveur de destination vous permet d’exporter des fichiers contenant des données Adobe Experience Platform vers votre conteneur [!DNL Azure Blob Storage].

L’exemple ci-dessous montre un modèle de configuration de serveur de destination pour une destination [!DNL Azure Blob Storage].

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
   }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Nom de votre connexion de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour les destinations [!DNL Azure Blob Storage], définissez ce paramètre sur `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans le champ `path.value`.<ul><li>Si vous souhaitez que vos utilisateurs saisissent leur propre [URI de compte de stockage](https://learn.microsoft.com/fr-fr/azure/storage/blobs/storage-blobs-introduction) [!DNL Azure Blob] dans l’interface utilisateur d’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser le champ `path.value` pour lire la valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur. Ce cas d’utilisation est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un chemin d’accès codé en dur pour votre intégration, tel que `"path.value": "https://myaccount.blob.core.windows.net/"`, définissez cette valeur sur `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | Chaîne | Le chemin d’accès à votre espace de stockage [!DNL Azure Blob]. Il peut s’agir d’un champ modélisé qui lit la valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans le champ `container.value`.<ul><li>Si vous souhaitez que vos utilisateurs saisissent leur propre [nom de conteneur](https://learn.microsoft.com/fr-fr/azure/storage/blobs/storage-blobs-introduction) [!DNL Azure Blob] dans l’interface utilisateur d’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser le champ `container.value` pour lire la valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur. Ce cas d’utilisation est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un nom de conteneur codé en dur pour votre intégration, tel que `"path.value: myContainer"`, définissez cette valeur sur `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | Chaîne | Nom du conteneur Azure Blob Storage à utiliser pour cette destination. Il peut s’agir d’un champ modélisé qui lit la valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `myContainer`. |

{style="table-layout:auto"}

## Serveur de destination [!DNL Data Landing Zone] ([!DNL DLZ]) {#dlz-example}

Ce serveur de destination vous permet d’exporter des fichiers contenant des données Experience Platform vers un espace de stockage [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md).

L’exemple ci-dessous montre un modèle de configuration de serveur de destination pour une destination [!DNL Data Landing Zone] ([!DNL DLZ]).

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Nom de votre connexion de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour les destinations [!DNL Data Landing Zone], définissez ce paramètre sur `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans le champ `path.value`.<ul><li>Si vous souhaitez que vos utilisateurs saisissent leur propre compte [!DNL Data Landing Zone] dans l’interface utilisateur d’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser le champ `path.value` pour lire une valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur. Ce cas d’utilisation est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un chemin d’accès codé en dur pour votre intégration, tel que `"path.value": "https://myaccount.blob.core.windows.net/"`, définissez cette valeur sur `NONE`. |
| `fileBasedDlzDestination.path.value` | Chaîne | Chemin d’accès au dossier de destination qui hébergera les fichiers exportés. |

{style="table-layout:auto"}

## Serveur de destination [!DNL Google Cloud Storage] {#gcs-example}

Ce serveur de destination vous permet d’exporter des fichiers contenant des données Experience Platform vers votre compte [!DNL Google Cloud Storage].

L’exemple ci-dessous montre un modèle de configuration de serveur de destination pour une destination [!DNL Google Cloud Storage].

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
   }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Nom de votre connexion de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour les destinations [!DNL Google Cloud Storage], définissez ce paramètre sur `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans le champ `bucket.value`.<ul><li>Si vous souhaitez que vos utilisateurs saisissent leur propre nom de compartiment [!DNL Google Cloud Storage] dans l’interface utilisateur d’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser le champ `bucket.value` pour lire une valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur. Ce cas d’utilisation est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un nom de compartiment codé en dur pour votre intégration, tel que `"bucket.value": "my-bucket"`, définissez cette valeur sur `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Chaîne | Nom de l’intervalle [!DNL Google Cloud Storage] à utiliser par cette destination. Il peut s’agir d’un champ modélisé qui lit la valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans le champ `path.value`.<ul><li>Si vous souhaitez que vos utilisateurs saisissent leur propre chemin d’accès au compartiment [!DNL Google Cloud Storage] dans l’interface utilisateur d’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser le champ `path.value` pour lire une valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur. Ce cas d’utilisation est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un chemin d’accès codé en dur pour votre intégration, tel que `"path.value": "/path/to/my-bucket"`, définissez cette valeur sur `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | Chaîne | Chemin d’accès au dossier [!DNL Google Cloud Storage] qui sera utilisé par cette destination. Il peut s’agir d’un champ modélisé qui lit la valeur des [champs de données client](../destination-configuration/customer-data-fields.md) renseignés par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de cet article. À présent, vous devriez mieux comprendre la spécification d’un serveur de destination et comment le configurer.

Pour en savoir plus sur les autres composants de serveur de destination, consultez les articles suivants :

* [Spécifications du modèle](templating-specs.md)
* [Format des messages](message-format.md)
* [Configuration du formatage des fichiers](file-formatting.md)
