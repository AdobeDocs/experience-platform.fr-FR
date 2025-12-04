---
description: Cette page illustre comment l’appel API est utilisé pour créer un serveur de destination avec Adobe Experience Platform Destination SDK.
title: Création d’une configuration de serveur de destination
exl-id: 5c6b6cf5-a9d9-4c8a-9fdc-f8a95ab2a971
source-git-commit: e1dd6ae9bf28014e8e84de85bdf67707744ea0ad
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 86%

---

# Création d’une configuration de serveur de destination

La création d’un serveur de destination est la première étape de la création de votre propre destination avec Destination SDK. Le serveur de destination comprend des options de configuration pour les spécifications [de serveur](../../functionality/destination-server/server-specs.md) et [de modèle](../../functionality/destination-server/templating-specs.md) et pour les options [format du message](../../functionality/destination-server/message-format.md), et [formatage de fichier](../../functionality/destination-server/file-formatting.md) (pour les destinations basées sur des fichiers).

Cette page illustre la requête d’API et la payload que vous pouvez utiliser pour créer votre propre serveur de destination à l’aide du point d’entrée de l’API `/authoring/destination-servers`.

Pour obtenir une description détaillée des fonctionnalités configurables avec ce point d’entrée, consultez les articles suivants :

* [Spécifications de serveur pour les destinations créées avec Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Spécifications de modèle pour les destinations créées avec Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Format des messages](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuration du formatage des fichiers](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations de l’API du serveur de destination {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Création d’une configuration de serveur de destination {#create}

Vous pouvez créer une configuration de serveur de destination en effectuant une requête `POST` au point d’entrée `/authoring/destination-servers`.

>[!TIP]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/destination-servers`

**Format d’API**

```http
POST /authoring/destination-servers
```

Selon le type de destination que vous créez, vous devez configurer un type de serveur de destination légèrement différent.

### Créer des serveurs de destination de schéma statique {#static-destination-servers}

Les onglets ci-dessous proposent des exemples de serveurs de destination pour les destinations qui utilisent des [schémas statiques](../../functionality/destination-configuration/schema-configuration.md#attributes-schema).

Les exemples de payloads ci-dessous incluent tous les paramètres pris en charge par chaque type de serveur de destination. Il n’est pas nécessaire d’inclure tous les paramètres dans votre requête. La payload peut être personnalisée en fonction de vos besoins.

Sélectionnez chaque onglet ci-dessous pour afficher la requête d’API correspondante.

>[!BEGINTABS]

>[!TAB Temps réel (streaming)]

**Création d’un serveur de destination en temps réel (streaming)**

Vous devez créer un serveur de destination en temps réel (streaming) similaire à celui illustré ci-dessous quand vous configurez une intégration basée sur l’API (streaming) en temps réel.

+++Requête

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| Paramètre | Type | Description |
| -------- | ----------- | ----------- |
| `name` | Chaîne | *Obligatoire.* Représente le nom convivial de votre serveur, visible uniquement par Adobe. Ce nom n’est pas visible pour les partenaires ou les clients. Par exemple, `Moviestar destination server`. |
| `destinationServerType` | Chaîne | *Obligatoire.* Définissez-le sur `URL_BASED` quand les destinations sont diffusées en temps réel (streaming). |
| `urlBasedDestination.url.templatingStrategy` | Chaîne | *Obligatoire.* <ul><li>Utilisez `PEBBLE_V1` si Adobe doit transformer l’URL dans le champ `value` ci-dessous. Utilisez cette option si vous disposez d’un point d’entrée tel que `https://api.moviestar.com/data/{{customerData.region}}/items`, où la partie `region` peut différer d’une personne à l’autre. Dans ce cas, vous devez également configurer `region` en tant que [champ de données client](../../functionality/destination-configuration/customer-data-fields.md) dans la [configuration de destination]&#x200B;(../destination-configuration/create-destination-configuration.md). </li><li> Utilisez `NONE` si aucune transformation n’est nécessaire du côté d’Adobe, par exemple si vous avez un point d’entrée tel que : `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Chaîne | *Obligatoire.* Renseignez l’adresse du point d’entrée d’API auquel Experience Platform doit se connecter. |
| `httpTemplate.httpMethod` | Chaîne | *Obligatoire.* Méthode qu’Adobe utilise dans les appels vers votre serveur. Les options sont les suivantes : `GET`, `PUT`, `POST`, `DELETE` ou `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Chaîne | *Obligatoire.* Cette chaîne est la version avec caractères d’échappement qui transforme les données des clients Experience Platform au format attendu par votre service. <br> <ul><li> Pour plus d’informations sur l’écriture du modèle, lisez la section [Utilisation des modèles](../../functionality/destination-server/message-format.md#using-templating). </li><li> Pour plus d’informations sur l’échappement des caractères, reportez-vous à la section [Norme RFC JSON, section 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Pour obtenir un exemple de transformation simple, consultez la transformation des [attributs de profil](../../functionality/destination-server/message-format.md#attributes). </li></ul> |
| `httpTemplate.contentType` | Chaîne | *Obligatoire.* Type de contenu que votre serveur accepte. Cette valeur est probablement `application/json`. |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.

+++

>[!TAB Amazon S3]

**Création d’un serveur de destination Amazon S3**

Vous devez créer un serveur de destination [!DNL Amazon S3] similaire à celui illustré ci-dessous au moment de la configuration d’une destination [!DNL Amazon S3] basée sur des fichiers.

+++Requête

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
            }
        }
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
| `fileConfigurations` | S/O | Pour en savoir plus sur la manière de configurer ces paramètres, consultez la [configuration du formatage de fichier](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.

+++

>[!TAB SFTP]

**Création d’un serveur de destination [!DNL SFTP]**

Vous devez créer un serveur de destination [!DNL SFTP] similaire à celui illustré ci-dessous au moment de la configuration d’une destination [!DNL SFTP] basée sur des fichiers.

+++Requête

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
      "port": 22,
      "encryptionMode" : "PGP"
   },
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
            }
        }
    }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Nom de votre connexion de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour les destinations [!DNL SFTP], définissez ce paramètre sur `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `fileBasedSFTPDestination.rootDirectory.value` | Chaîne | Répertoire racine de lʼespace de stockage de destination. |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `fileBasedSFTPDestination.hostName.value` | Chaîne | Nom d’hôte de lʼespace de stockage de destination. |
| `port` | Nombre entier | Port du serveur de fichiers SFTP. |
| `encryptionMode` | Chaîne | Indique s’il faut utiliser le chiffrement de fichier. Valeurs prises en charge : <ul><li>PGP</li><li>Aucun</li></ul> |
| `fileConfigurations` | S/O | Pour en savoir plus sur la manière de configurer ces paramètres, consultez la [configuration du formatage de fichier](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.

+++

>[!TAB Azure Data Lake Storage]

**Création d’un serveur de destination [!DNL Azure Data Lake Storage]**

Vous devez créer un serveur de destination [!DNL Azure Data Lake Storage] similaire à celui illustré ci-dessous au moment de la configuration d’une destination [!DNL Azure Data Lake Storage] basée sur des fichiers.

+++Requête

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
            }
        }
    }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Nom de votre connexion de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour les destinations [!DNL Azure Data Lake Storage], définissez ce paramètre sur `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Chaîne | Chemin d’accès au dossier de destination qui hébergera les fichiers exportés. |
| `fileConfigurations` | S/O | Pour en savoir plus sur la manière de configurer ces paramètres, consultez la [configuration du formatage de fichier](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.

+++

>[!TAB Stockage Azure Blob]

**Création d’un serveur de destination [!DNL Azure Blob Storage]**

Vous devez créer un serveur de destination [!DNL Azure Blob Storage] similaire à celui illustré ci-dessous au moment de la configuration d’une destination [!DNL Azure Blob Storage] basée sur des fichiers.

+++Requête

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
            }
        }
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
| `fileConfigurations` | S/O | Pour en savoir plus sur la manière de configurer ces paramètres, consultez la [configuration du formatage de fichier](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.

+++

>[!TAB Zone d’entrée des données (DLZ)]

**Création d’un serveur de destination [!DNL Data Landing Zone (DLZ)]**

Vous devez créer un serveur de destination [!DNL Data Landing Zone (DLZ)] similaire à celui illustré ci-dessous au moment de la configuration d’une destination [!DNL Data Landing Zone (DLZ)] basée sur des fichiers.

+++Requête

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "dlz_destination"
   },
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
            }
        }
    }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Nom de votre connexion de destination. |
| `destinationServerType` | Chaîne | Définissez cette valeur en fonction de votre plateforme de destination. Pour les destinations [!DNL Data Landing Zone], définissez ce paramètre sur `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Chaîne | *Obligatoire.*  Utilisez `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Chaîne | Chemin d’accès au dossier de destination qui hébergera les fichiers exportés. |
| `fileConfigurations` | S/O | Pour en savoir plus sur la manière de configurer ces paramètres, consultez la [configuration du formatage de fichier](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.

+++

>[!TAB Google Cloud Storage]

**Création d’un serveur de destination [!DNL Google Cloud Storage]**

Vous devez créer un serveur de destination [!DNL Google Cloud Storage] similaire à celui illustré ci-dessous au moment de la configuration d’une destination [!DNL Google Cloud Storage] basée sur des fichiers.

+++Requête

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
            }
        }
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
| `fileConfigurations` | S/O | Pour en savoir plus sur la manière de configurer ces paramètres, consultez la [configuration du formatage de fichier](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.

+++

>[!ENDTABS]

### Créer des serveurs de destination de schéma dynamique {#dynamic-schema-servers}

Les schémas dynamiques vous permettent de récupérer dynamiquement les attributs cibles pris en charge et de générer des schémas basés sur votre propre API. Vous devez configurer un serveur de destination pour les schémas dynamiques avant de pouvoir configurer le schéma.

Consultez dans l’onglet ci-dessous un exemple de serveur de destination pour les destinations qui utilisent les [schémas dynamiques](../../functionality/destination-configuration/schema-configuration.md#dynamic-schema-configuration).

L’exemple de payload ci-dessous inclut tous les paramètres requis pour un serveur de schéma dynamique.

>[!BEGINTABS]

>[!TAB Serveur de schéma dynamique]

**Création d’un serveur de schéma dynamique**

Vous devez créer un serveur de schéma dynamique similaire à celui illustré ci-dessous quand vous configurez une destination qui récupère son schéma de profil à partir de votre propre point d’entrée de l’API. Contrairement à un schéma statique, un schéma dynamique n’utilise pas de tableau `profileFields`, mais un serveur de schéma dynamique qui se connecte à votre propre API à partir de laquelle il récupère la configuration du schéma.

+++Requête

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Dynamic Schema Server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://YOUR_API_ENDPOINT/"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET"
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"type\":\"object\",\n    \"title\": \"Contact Schema\",\n    \"properties\": {\n        {% for setDefinition in response.body.items %}\n            \"{{setDefinition.key}}\": {\n                \"title\" : \"{{setDefinition.name.value}}\",\n                \"type\" : \"object\",\n                \"properties\": {\n                    {% for attribute in setDefinition.attributes %}\n                        \"{{attribute.key}}\": {\n                            \"title\" : \"{{attribute.name.value}}\",\n                            \"type\" : \"string\"\n                        }\n                        {% if not loop.last %},{%endif%}\n                    {% endfor %}\n                }\n            }\n            {% if not loop.last %},{%endif%}\n        {% endfor %}\n    }\n}",
         "name":"schema"
      }
   ]
}
```

| Paramètre | Type | Description |
| -------- | ----------- | ----------- |
| `name` | Chaîne | *Obligatoire.* Représente le nom convivial du serveur de votre schéma dynamique, visible uniquement par Adobe. |
| `destinationServerType` | Chaîne | *Obligatoire.* Définissez-le sur `URL_BASED` quand les serveurs de schéma sont dynamiques. |
| `urlBasedDestination.url.templatingStrategy` | Chaîne | *Obligatoire.* <ul><li>Utilisez `PEBBLE_V1` si Adobe doit transformer l’URL dans le champ `value` ci-dessous. Utilisez cette option si vous disposez d’un point d’entrée tel que : `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Utilisez `NONE` si aucune transformation n’est nécessaire du côté d’Adobe, par exemple si vous avez un point d’entrée tel que : `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Chaîne | *Obligatoire.* Renseignez l’adresse du point d’entrée de l’API auquel Experience Platform doit se connecter et récupérez les champs de schéma à remplir en tant que champs cibles dans l’étape de mappage du workflow d’activation. |
| `httpTemplate.httpMethod` | Chaîne | *Obligatoire.* Méthode qu’Adobe utilise dans les appels vers votre serveur. Quand les serveurs de schéma sont dynamiques, utilisez `GET`. |
| `responseFields.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `responseFields.value` | Chaîne | *Obligatoire.* Cette chaîne est le modèle de transformation de caractères d’échappement transformant la réponse reçue de l’API du partenaire en schéma du partenaire qui s’affichera dans l’interface utilisateur d’Experience Platform. <br> <ul><li> Pour plus d’informations sur l’écriture du modèle, lisez la section [Utilisation des modèles](../../functionality/destination-server/message-format.md#using-templating). </li><li> Pour plus d’informations sur l’échappement des caractères, reportez-vous à la section [Norme RFC JSON, section 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Pour obtenir un exemple de transformation simple, consultez la transformation des [attributs de profil](../../functionality/destination-server/message-format.md#attributes). </li></ul> |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.

+++


>[!ENDTABS]


### Créer des serveurs de destination de liste déroulante dynamique {#dynamic-dropdown-servers}

Utilisez les [listes déroulantes dynamiques](../../functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) pour récupérer et remplir dynamiquement des champs de données client de liste déroulante, en fonction de votre propre API. Par exemple, vous pouvez récupérer une liste de comptes d’utilisateurs existants que vous souhaitez utiliser pour une connexion à la destination.

Vous devez configurer un serveur de destination pour les listes déroulantes dynamiques avant de pouvoir configurer le champ de données client de la liste déroulante dynamique.

Consultez dans l’onglet ci-dessous un exemple de serveur de destination utilisé pour récupérer dynamiquement les valeurs à afficher dans un sélecteur de liste déroulante à partir d’une API.

L’exemple de payload ci-dessous inclut tous les paramètres requis pour un serveur de schéma dynamique.

>[!BEGINTABS]

>[!TAB  Serveur de liste déroulante dynamique ]

**Créer un serveur de liste déroulante dynamique**

Vous devez créer un serveur de liste déroulante dynamique similaire à celui illustré ci-dessous au moment de la configuration d’une destination qui récupère les valeurs d’un champ de données client de liste déroulante à partir de votre propre point d’entrée de l’API.

+++Requête

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Server for dynamic dropdown",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.users}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET",
      "headers":[
         {
            "header":"Authorization",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"My Bearer Token"
            }
         },
         {
            "header":"x-integration",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.integrationId}}"
            }
         },
         {
            "header":"Accept",
            "value":{
               "templatingStrategy":"NONE",
               "value":"application/json"
            }
         }
      ]
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% set list = [] %} {% for record in response.body %} {% set list = list|merge([{'name' : record.name, 'value' : record.id }]) %} {% endfor %}{{ {'list': list} | toJson | raw }}",
         "name":"list"
      }
   ]
}
```

| Paramètre | Type | Description |
| -------- | ----------- | ----------- |
| `name` | Chaîne | *Obligatoire.* représente le nom convivial du serveur de liste déroulante dynamique, visible uniquement par Adobe. |
| `destinationServerType` | Chaîne | *Obligatoire.* Définissez sur `URL_BASED` pour les serveurs de liste déroulante dynamiques. |
| `urlBasedDestination.url.templatingStrategy` | Chaîne | *Obligatoire.* <ul><li>Utilisez `PEBBLE_V1` si Adobe doit transformer l’URL dans le champ `value` ci-dessous. Utilisez cette option si vous disposez d’un point d’entrée tel que : `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Utilisez `NONE` si aucune transformation n’est nécessaire du côté d’Adobe, par exemple si vous avez un point d’entrée tel que : `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Chaîne | *Obligatoire.* Renseignez l’adresse du point d’entrée de l’API auquel Experience Platform doit se connecter et récupérez les valeurs des listes déroulantes. |
| `httpTemplate.httpMethod` | Chaîne | *Obligatoire.* Méthode qu’Adobe utilise dans les appels vers votre serveur. Pour les serveurs de liste déroulante dynamique, utilisez `GET`. |
| `httpTemplate.headers` | Objet | *Facultatif.l* Incluez les en-têtes requis pour la connexion au serveur de liste déroulante dynamique. |
| `responseFields.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `responseFields.value` | Chaîne | *Obligatoire.* Cette chaîne est le modèle de transformation de caractères d’échappement transformant la réponse reçue de votre API en valeurs qui s’afficheront dans l’interface utilisateur d’Experience Platform. <br> <ul><li> Pour plus d’informations sur l’écriture du modèle, lisez la section [Utilisation des modèles](../../functionality/destination-server/message-format.md#using-templating). </li><li> Pour plus d’informations sur l’échappement des caractères, reportez-vous à la section [Norme RFC JSON, section 7](https://tools.ietf.org/html/rfc8259#section-7). |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.

+++

>[!ENDTABS]

## Gestion des erreurs d’API {#error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes d’état API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs d’en-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de ce document. À présent, vous savez comment créer un serveur de destination avec le point d’entrée `/authoring/destination-servers` Destination SDK de l’API.

Pour en savoir plus sur les fonctionnalités offertes par ce point d’entrée, consultez les articles suivants :

* [Récupération d’une configuration de serveur de destination](retrieve-destination-server.md)
* [Mise à jour d’une configuration de serveur de destination](update-destination-server.md)
* [Suppression d’une configuration de serveur de destination](delete-destination-server.md)

Pour comprendre la place de ce point d’entrée dans le processus de création de destinations, consultez les articles suivants :

* [Utiliser Destination SDK pour configurer une destination de diffusion en streaming](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [Utilisation de Destination SDK pour configurer une destination basée sur des fichiers](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)
