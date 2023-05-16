---
description: Découvrez comment configurer les spécifications de serveur de destination en Adobe Experience Platform Destination SDK via le point de terminaison `/authoring/destination-servers`.
title: Spécifications de serveur pour les destinations créées avec Destination SDK
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2750'
ht-degree: 11%

---


# Spécifications de serveur pour les destinations créées avec Destination SDK

Les spécifications du serveur de destination définissent le type de plateforme de destination qui recevra les données de Adobe Experience Platform, ainsi que les paramètres de communication entre Platform et votre destination. Par exemple :

* A [diffusion en continu](#streaming-example) La spécification du serveur de destination définit le point de terminaison du serveur HTTP qui recevra les messages HTTP de Platform. Pour savoir comment configurer les appels HTTP au point de terminaison, lisez la section [spécifications du modèle](templating-specs.md) page.
* Un [Amazon S3](#s3-example) la spécification du serveur de destination définit la variable [!DNL S3] nom du compartiment et chemin d’accès où Platform exportera les fichiers.
* Un [SFTP](#sftp-example) la spécification du serveur de destination définit le nom d’hôte, le répertoire racine, le port de communication et le type de chiffrement du serveur SFTP sur lequel Platform exportera les fichiers.

Pour comprendre où ce composant entre dans une intégration créée avec Destination SDK, reportez-vous au diagramme de la section [options de configuration](../configuration-options.md) ou consultez les pages de présentation de la configuration de destination suivantes :

* [Utiliser Destination SDK pour configurer une destination de diffusion en continu](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Utiliser Destination SDK pour configurer une destination basée sur des fichiers](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

Vous pouvez configurer les spécifications du serveur de destination via le `/authoring/destination-servers` point de terminaison . Consultez les pages de référence d’API suivantes pour obtenir des exemples d’appels d’API détaillés dans lesquels vous pouvez configurer les composants affichés dans cette page.

* [Création d’une configuration de serveur de destination](../../authoring-api/destination-server/create-destination-server.md)
* [Mise à jour de la configuration d’un serveur de destination](../../authoring-api/destination-server/update-destination-server.md)

Cette page affiche tous les types de serveur de destination pris en charge par Destination SDK, avec tous leurs paramètres de configuration. Lors de la création de votre destination, remplacez les valeurs de paramètre par les vôtres.

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Types d’intégration pris en charge {#supported-integration-types}

Reportez-vous au tableau ci-dessous pour plus d’informations sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (diffusion en continu) | Oui |
| Intégrations basées sur des fichiers (par lots) | Oui |

When [création](../../authoring-api/destination-server/create-destination-server.md) ou [mise à jour](../../authoring-api/destination-server/update-destination-server.md) un serveur de destination, utilisez l’une des configurations de type de serveur décrites dans cette page. En fonction des exigences de votre intégration, veillez à remplacer les exemples de valeurs de paramètre de ces exemples par les vôtres.

## Champs codés en dur ou modélisés {#templatized-fields}

Lors de la création d’un serveur de destination via Destination SDK, vous pouvez définir des valeurs de paramètre de configuration soit en les codant en dur dans la configuration, soit en utilisant des champs modélisés. Les champs modèles vous permettent de lire les valeurs fournies par l’utilisateur à partir de l’interface utilisateur de Platform.

Les paramètres du serveur de destination comportent deux champs configurables. Ces options indiquent si vous utilisez des valeurs codées en dur ou modélisées.

| Paramètre | Type | Description |
|---|---|---|
| `templatingStrategy` | Chaîne | *Obligatoire.* Définit s’il existe une valeur codée en dur fournie via la variable `value` ou une valeur configurable par l’utilisateur dans l’interface utilisateur. Valeurs prises en charge : <ul><li>`NONE`: Utilisez cette valeur lorsque vous codez en dur la valeur du paramètre via la variable `value` (voir la ligne suivante). Exemple : `"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`: Utilisez cette valeur lorsque vous souhaitez que vos utilisateurs fournissent une valeur de paramètre dans l’interface utilisateur. Exemple : `"value": "{{customerData.bucket}}"`. </li></ul> |
| `value` | Chaîne | *Obligatoire*. Définit la valeur du paramètre. Types de valeurs pris en charge : <ul><li>**Valeur codée en dur**: Utilisez une valeur codée en dur (telle que `"value": "my-storage-bucket"`) lorsque vous n’avez pas besoin que les utilisateurs saisissent une valeur de paramètre dans l’interface utilisateur. Lorsque vous codez une valeur de manière irréversible, `templatingStrategy` doit toujours être défini sur `NONE`.</li><li>**Valeur modèle**: Utilisez une valeur de modèle (telle que `"value": "{{customerData.bucket}}"`) lorsque vous souhaitez que vos utilisateurs fournissent une valeur de paramètre dans l’interface utilisateur. Lors de l’utilisation de valeurs modélisées, `templatingStrategy` doit toujours être défini sur `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### Quand préférer les champs codés en dur aux champs modélisés ?

Les champs codés en dur et modélisés ont chacun leur propre utilité dans Destination SDK, selon le type d’intégration que vous créez.

**Connexion à votre destination sans intervention de l’utilisateur**

Quand les utilisateurs [se connecter à votre destination](../../../ui/connect-destination.md) dans l’interface utilisateur de Platform, vous pouvez gérer le processus de connexion de destination sans leur entrée.

Pour ce faire, vous pouvez coder en dur les paramètres de connexion de la plateforme de destination dans la spécification du serveur. Lorsque vous utilisez des valeurs de paramètre codées en dur dans la configuration de votre serveur de destination, la connexion entre Adobe Experience Platform et votre plateforme de destination est gérée sans aucune entrée de l’utilisateur.

Dans l’exemple ci-dessous, un partenaire crée un serveur de destination de zone d’entrée de données avec la variable `path.value` étant codé en dur.

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

Par conséquent, lorsque les utilisateurs passent par la variable [tutoriel sur la connexion à destination](../../../ui/connect-destination.md), ils ne verront pas d’ [étape d’authentification](../../../ui/connect-destination.md#authenticate). Au lieu de cela, l’authentification est gérée par Platform, comme illustré dans l’image ci-dessous.

![Image de l’interface utilisateur affichant l’écran d’authentification entre Platform et une destination DLZ.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**Connexion à votre destination à l’aide des entrées utilisateur**

Lorsque la connexion entre Platform et votre destination doit être établie à la suite d’une entrée utilisateur spécifique dans l’interface utilisateur de Platform, comme la sélection d’un point de terminaison API ou la spécification d’une valeur de champ, vous pouvez utiliser des champs modélisés dans la spécification du serveur pour lire la saisie utilisateur et vous connecter à votre plateforme de destination.

Dans l’exemple ci-dessous, un partenaire crée une [temps réel (diffusion en continu)](#streaming-example) l’intégration et la `url.value` utilise le paramètre modélisé `{{customerData.region}}` pour personnaliser une partie du point de terminaison de l’API en fonction des entrées de l’utilisateur.

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

Pour permettre aux utilisateurs de sélectionner une valeur dans l’interface utilisateur de Platform, la variable `region` doit également être défini dans la variable [configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md) en tant que champ de données client, comme illustré ci-dessous :

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

Par conséquent, lorsque les utilisateurs passent par la variable [tutoriel sur la connexion à destination](../../../ui/connect-destination.md), ils doivent sélectionner une région avant de pouvoir se connecter à la plateforme de destination. Lorsqu’ils se connectent à la destination, le champ de modèle `{{customerData.region}}` est remplacé par la valeur sélectionnée par l’utilisateur dans l’interface utilisateur, comme illustré dans l’image ci-dessous.

![Image de l’interface utilisateur affichant l’écran de connexion de destination avec un sélecteur de région.](../../assets/functionality/destination-server/server-spec-template-region.png)

## Serveur de destination en temps réel (diffusion en continu) {#streaming-example}

Ce type de serveur de destination vous permet d’exporter des données de Adobe Experience Platform vers votre destination via des requêtes HTTP. La configuration de serveur contient des informations sur le serveur recevant les messages (le serveur de votre côté).

Ce processus fournit des données utilisateur sous forme d’une série de messages HTTP vers votre plateforme de destination. Les paramètres ci-dessous forment le modèle de spécifications du serveur HTTP.

L’exemple ci-dessous illustre un exemple de configuration de serveur de destination pour une destination en temps réel (diffusion en continu).

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
| `destinationServerType` | Chaîne | *Obligatoire.* Définissez cette variable sur `URL_BASED` pour les destinations de diffusion en continu. |
| `templatingStrategy` | Chaîne | *Obligatoire.* <ul><li>Utilisation `PEBBLE_V1` si vous utilisez un champ modélisé au lieu d’une valeur codée en dur dans la variable `value` champ . Utilisez cette option si vous disposez d’un point de terminaison du type : `https://api.moviestar.com/data/{{customerData.region}}/items`, où les utilisateurs doivent sélectionner la région du point de terminaison dans l’interface utilisateur de Platform. </li><li> Utilisation `NONE` si aucune transformation modélisée n’est nécessaire côté Adobe, par exemple si vous avez un point de terminaison comme : `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Chaîne | *Obligatoire.* Renseignez l’adresse du point d’entrée de l’API auquel Experience Platform doit se connecter. |

{style="table-layout:auto"}

## [!DNL Amazon S3] serveur de destination {#s3-example}

Ce serveur de destination vous permet d’exporter des fichiers contenant des données Adobe Experience Platform vers votre stockage Amazon S3.

L’exemple ci-dessous illustre un exemple de configuration de serveur de destination pour une destination Amazon S3.

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
| `name` | Chaîne | Nom du serveur de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour exporter des fichiers vers un [!DNL Amazon S3] compartiment, définissez ce paramètre sur `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans la variable `bucket.value` champ .<ul><li>Si vous souhaitez que vos utilisateurs saisissent leur propre nom de compartiment dans l’interface utilisateur de l’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser la variable `value` pour lire une valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseigné par l’utilisateur. Ce cas pratique est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un nom de compartiment codé en dur pour votre intégration, tel que `"bucket.value":"MyBucket"`, puis définissez cette valeur sur `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | Chaîne | Nom de l’intervalle [!DNL Amazon S3] à utiliser par cette destination. Il peut s’agir d’un champ de modèle qui lit la valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseignée par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans la variable `path.value` champ .<ul><li>Si vous souhaitez que vos utilisateurs saisissent leur propre chemin dans l’interface utilisateur de l’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser la variable `path.value` pour lire une valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseigné par l’utilisateur. Ce cas pratique est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un chemin d’accès codé en dur pour votre intégration, tel que `"bucket.value":"/path/to/MyBucket"`, puis définissez cette valeur sur `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | Chaîne | Le chemin d’accès à [!DNL Amazon S3] compartiment à utiliser par cette destination. Il peut s’agir d’un champ de modèle qui lit la valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseignée par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] serveur de destination {#sftp-example}

Ce serveur de destination vous permet d’exporter des fichiers contenant des données Adobe Experience Platform vers vos [!DNL SFTP] serveur de stockage.

L’exemple ci-dessous illustre un exemple de configuration de serveur de destination pour une destination SFTP.

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
| `name` | Chaîne | Nom du serveur de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour exporter des fichiers vers un [!DNL SFTP] destination, définissez ce paramètre sur `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans la variable `rootDirectory.value` champ .<ul><li>Si vous souhaitez que vos utilisateurs saisissent leur propre chemin d’accès au répertoire racine dans l’interface utilisateur de l’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser la variable `rootDirectory.value` pour lire une valeur fournie par l’utilisateur à partir du champ [Champs de données client](../destination-configuration/customer-data-fields.md) renseigné par l’utilisateur. Ce cas pratique est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un chemin d’accès au répertoire racine codé en dur pour votre intégration, tel que `"rootDirectory.value":"Storage/MyDirectory"`, puis définissez cette valeur sur `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | Chaîne | Le chemin d’accès au répertoire qui hébergera les fichiers exportés. Il peut s’agir d’un champ de modèle qui lit la valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseignée par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans la variable `hostName.value` champ .<ul><li>Si vous souhaitez que vos utilisateurs saisissent leur propre nom d’hôte dans l’interface utilisateur de l’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser la variable `hostName.value` pour lire une valeur fournie par l’utilisateur à partir du champ [Champs de données client](../destination-configuration/customer-data-fields.md) renseigné par l’utilisateur. Ce cas pratique est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un nom d’hôte codé en dur pour votre intégration, tel que `"hostName.value":"my.hostname.com"`, puis définissez cette valeur sur `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | Chaîne | Nom d’hôte de votre serveur SFTP. Il peut s’agir d’un champ de modèle qui lit la valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseignée par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `"hostName.value":"my.hostname.com"`. |
| `port` | Nombre entier | Port du serveur de fichiers SFTP. |
| `encryptionMode` | Chaîne | Indique s’il faut utiliser le chiffrement de fichier. Valeurs prises en charge : <ul><li>PGP</li><li>Aucun</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS]) serveur de destination {#adls-example}

Ce serveur de destination vous permet d’exporter des fichiers contenant des données Adobe Experience Platform vers vos [!DNL Azure Data Lake Storage] compte .

L’exemple ci-dessous illustre un exemple de configuration d’un serveur de destination pour une [!DNL Azure Data Lake Storage] destination.

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
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans la variable `path.value` champ .<ul><li>Si vous souhaitez que vos utilisateurs saisissent le [!DNL ADLS] chemin du dossier dans l’interface utilisateur de l’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser la variable `path.value` pour lire une valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseigné par l’utilisateur. Ce cas pratique est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un chemin d’accès codé en dur pour votre intégration, tel que `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`, puis définissez cette valeur sur `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | Chaîne | Le chemin d’accès à [!DNL ADLS] dossier de stockage. Il peut s’agir d’un champ de modèle qui lit la valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseignée par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] serveur de destination {#blob-example}

Ce serveur de destination vous permet d’exporter des fichiers contenant des données Adobe Experience Platform vers vos [!DNL Azure Blob Storage] conteneur.

L’exemple ci-dessous illustre un exemple de configuration d’un serveur de destination pour une [!DNL Azure Blob Storage] destination.

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
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans la variable `path.value` champ .<ul><li>Si vous souhaitez que vos utilisateurs saisissent les leurs. [!DNL Azure Blob] [URI du compte de stockage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) dans l’interface utilisateur de l’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser la variable `path.value` pour lire la valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseigné par l’utilisateur. Ce cas pratique est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un chemin d’accès codé en dur pour votre intégration, tel que `"path.value": "https://myaccount.blob.core.windows.net/"`, puis définissez cette valeur sur `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | Chaîne | Le chemin d’accès à [!DNL Azure Blob] stockage. Il peut s’agir d’un champ de modèle qui lit la valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseignée par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans la variable `container.value` champ .<ul><li>Si vous souhaitez que vos utilisateurs saisissent les leurs. [!DNL Azure Blob] [nom du conteneur](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) dans l’interface utilisateur de l’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser la variable `container.value` pour lire la valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseigné par l’utilisateur. Ce cas pratique est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un nom de conteneur codé en dur pour votre intégration, tel que `"path.value: myContainer"`, puis définissez cette valeur sur `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | Chaîne | Nom du conteneur de stockage Azure Blob à utiliser pour cette destination. Il peut s’agir d’un champ de modèle qui lit la valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseignée par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ]) serveur de destination {#dlz-example}

Ce serveur de destination vous permet d’exporter des fichiers contenant des données Platform vers un [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md) stockage.

L’exemple ci-dessous illustre un exemple de configuration de serveur de destination pour un [!DNL Data Landing Zone] ([!DNL DLZ]).

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
| `fileBasedDlzDestination.path.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans la variable `path.value` champ .<ul><li>Si vous souhaitez que vos utilisateurs saisissent les leurs. [!DNL Data Landing Zone] dans l’interface utilisateur de l’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser la variable `path.value` pour lire une valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseigné par l’utilisateur. Ce cas pratique est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un chemin d’accès codé en dur pour votre intégration, tel que `"path.value": "https://myaccount.blob.core.windows.net/"`, puis définissez cette valeur sur `NONE`. |
| `fileBasedDlzDestination.path.value` | Chaîne | Chemin d’accès au dossier de destination qui hébergera les fichiers exportés. |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] serveur de destination {#gcs-example}

Ce serveur de destination vous permet d’exporter des fichiers contenant des données Platform vers vos [!DNL Google Cloud Storage] compte .

L’exemple ci-dessous illustre un exemple de configuration de serveur de destination pour un [!DNL Google Cloud Storage] destination.

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
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans la variable `bucket.value` champ .<ul><li>Si vous souhaitez que vos utilisateurs saisissent les leurs. [!DNL Google Cloud Storage] nom du compartiment dans l’interface utilisateur de l’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser la variable `bucket.value` pour lire une valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseigné par l’utilisateur. Ce cas pratique est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un nom de compartiment codé en dur pour votre intégration, tel que `"bucket.value": "my-bucket"`, puis définissez cette valeur sur `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Chaîne | Nom de l’intervalle [!DNL Google Cloud Storage] à utiliser par cette destination. Il peut s’agir d’un champ de modèle qui lit la valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseignée par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Chaîne | *Obligatoire*. Définissez cette valeur en fonction du type de valeur utilisé dans la variable `path.value` champ .<ul><li>Si vous souhaitez que vos utilisateurs saisissent les leurs. [!DNL Google Cloud Storage] chemin du compartiment dans l’interface utilisateur de l’Experience Platform, définissez cette valeur sur `PEBBLE_V1`. Dans ce cas, vous devez modéliser la variable `path.value` pour lire une valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseigné par l’utilisateur. Ce cas pratique est illustré dans l’exemple ci-dessus.</li><li>Si vous utilisez un chemin d’accès codé en dur pour votre intégration, tel que `"path.value": "/path/to/my-bucket"`, puis définissez cette valeur sur `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | Chaîne | Le chemin d’accès à [!DNL Google Cloud Storage] dossier à utiliser par cette destination. Il peut s’agir d’un champ de modèle qui lit la valeur de la variable [Champs de données client](../destination-configuration/customer-data-fields.md) renseignée par l’utilisateur (comme illustré dans l’exemple ci-dessus) ou une valeur codée en dur, telle que `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## Étapes suivantes {#next-steps}

Après avoir lu cet article, vous devriez mieux comprendre la spécification d’un serveur de destination et la manière dont vous pouvez le configurer.

Pour en savoir plus sur les autres composants du serveur de destination, consultez les articles suivants :

* [Spécifications du modèle](templating-specs.md)
* [Format des messages](message-format.md)
* [Configuration du formatage des fichiers](file-formatting.md)
