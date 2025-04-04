---
description: Cette page illustre l’appel API utilisé pour mettre à jour une configuration de serveur de destination existante avec Adobe Experience Platform Destination SDK.
title: Mise à jour d’une configuration de serveur de destination
exl-id: 579d2cc1-5110-4fba-9dcc-ff4b8d259827
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 96%

---

# Mise à jour d’une configuration de serveur de destination

Cette page illustre la requête d’API et la payload que vous pouvez utiliser pour mettre à jour une configuration de serveur de destination existante à l’aide du point d’entrée `/authoring/destination-servers` de l’API.

>[!TIP]
>
>Toute opération de mise à jour sur des destinations produites/publiques n’est visible qu’après avoir utilisé l’[API de publication](../../publishing-api/create-publishing-request.md) et envoyé la mise à jour pour révision Adobe.

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

## Mise à jour d’une configuration de serveur de destination {#update}

Vous pouvez mettre à jour une configuration de serveur de destination [existante](create-destination-server.md) en effectuant une requête `PUT` au point d’entrée `/authoring/destination-servers` avec la payload mise à jour.

>[!TIP]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/destination-servers`

Pour obtenir une configuration de serveur de destination existante et son `{INSTANCE_ID}` correspondant, consultez l’article sur la [récupération d’une configuration de serveur de destination](retrieve-destination-server.md).

**Format d’API**

```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | Identifiant de la configuration de serveur de destination que vous souhaitez mettre à jour. Pour obtenir une configuration de serveur de destination existante et son `{INSTANCE_ID}` correspondant, consultez la section [Récupération d’une configuration de destination](retrieve-destination-server.md). |

Les requêtes suivantes mettent à jour une configuration de serveur de destination existante, configurée par les paramètres fournis dans la payload.

Sélectionnez chaque onglet ci-dessous pour afficher la payload correspondante.

>[!BEGINTABS]

>[!TAB Temps réel (streaming)]

+++Requête

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
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
      "httpMethod":"PUT",
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
| `urlBasedDestination.url.templatingStrategy` | Chaîne | *Obligatoire.* <ul><li>Utilisez `PEBBLE_V1` si Adobe doit transformer l’URL dans le champ `value` ci-dessous. Utilisez cette option si vous disposez d’un point d’entrée tel que : `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Utilisez `NONE` si aucune transformation n’est nécessaire du côté d’Adobe, par exemple si vous avez un point d’entrée tel que : `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Chaîne | *Obligatoire.* Renseignez l’adresse du point d’entrée d’API auquel Experience Platform doit se connecter. |
| `httpTemplate.httpMethod` | Chaîne | *Obligatoire.* Méthode qu’Adobe utilise dans les appels vers votre serveur. Les options sont les suivantes : `GET`, `PUT`, `PUT`, `DELETE` ou `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Chaîne | *Obligatoire.* Cette chaîne est la version avec caractères d’échappement qui transforme les données des clients Experience Platform au format attendu par votre service. <br> <ul><li> Pour plus d’informations sur l’écriture du modèle, lisez la section [Utilisation des modèles](../../functionality/destination-server/message-format.md#using-templating). </li><li> Pour plus d’informations sur l’échappement des caractères, reportez-vous à la section [Norme RFC JSON, section 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Pour obtenir un exemple de transformation simple, consultez la transformation des [attributs de profil](../../functionality/destination-server/message-format.md#attributes). </li></ul> |
| `httpTemplate.contentType` | Chaîne | *Obligatoire.* Type de contenu que votre serveur accepte. Cette valeur est probablement `application/json`. |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de mettre à jour.

+++

>[!TAB Amazon S3]

+++Requête

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
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

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de mettre à jour.

+++

>[!TAB SFTP]

+++Requête

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de mettre à jour.

+++

>[!TAB Azure Data Lake Storage]

+++Requête

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de mettre à jour.

+++

>[!TAB Stockage Azure Blob]

+++Requête

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_D} \
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

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de mettre à jour.

+++

>[!TAB Zone d’entrée des données (DLZ)]

+++Requête

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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
      "useCase": "Your use case"
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

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de mettre à jour.

+++

>[!TAB Google Cloud Storage]

+++Requête

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

Une réponse réussie renvoie le statut HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de mettre à jour.

+++

>[!ENDTABS]

## Gestion des erreurs d’API {#error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes d’état API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs d’en-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de ce document. À présent, vous savez comment mettre à jour une configuration de serveur de destination avec le point d’entrée `/authoring/destination-servers` Destination SDK de l’API.

Pour en savoir plus sur les fonctionnalités offertes par ce point d’entrée, consultez les articles suivants :

* [Création d’une configuration de serveur de destination](create-destination-server.md)
* [Récupération d’une configuration de serveur de destination](retrieve-destination-server.md)
* [Mise à jour d’une configuration de serveur de destination](update-destination-server.md)
