---
description: Cette page répertorie et décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point d’entrée d’API `/authoring/destination-servers`. Les spécifications du serveur et du modèle pour votre destination peuvent être configurées dans Adobe Experience Platform Destination SDK via le point d’entrée commun `/authoring/destination-servers`.
title: Opérations de l’API du point d’entrée du serveur de destination
exl-id: a144b0fb-d34f-42d1-912b-8576296e59d2
source-git-commit: 557db5b7eefdd7902895e428f7bc34e3ad8a6f58
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 95%

---

# Opérations de l’API du point d’entrée du serveur de destination

>[!IMPORTANT]
>
>**Point d’entrée de l’API **: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Cette page répertorie et décrit toutes les opérations de l’API que vous pouvez effectuer à l’aide du point d’entrée de l’API `/authoring/destination-servers`. Les spécifications de serveur et de modèle pour votre destination peuvent être configurées dans Adobe Experience Platform Destination SDK via le point d’entrée commun `/authoring/destination-servers`. Pour obtenir une description de la fonctionnalité offerte par ce point d’entrée, reportez-vous à la section [Spécifications de serveur et de modèle](./server-and-template-configuration.md).

## Prise en main des opérations de l’API du serveur de destination {#get-started}

Avant de poursuivre, veuillez consulter la section [Guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de destination requise et les en-têtes requis.

## Créer une configuration pour un serveur de destination de diffusion en continu {#create}

Vous pouvez créer une nouvelle configuration de serveur de destination pour une destination de diffusion en continu en adressant une requête POST au point d’entrée `/authoring/destination-servers`.

**Format d’API**

```http
POST /authoring/destination-servers
```

**Requête**

La requête suivante crée une nouvelle configuration de serveur de destination, configurée en fonction des paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres acceptés par le point d’entrée `/authoring/destination-servers`. Notez que vous n’avez pas à ajouter tous les paramètres à l’appel et que le modèle est personnalisable, conformément aux exigences de votre API.

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
| `destinationServerType` | Chaîne | *Obligatoire.* Définissez sur `URL_BASED` pour les destinations de diffusion en continu. |
| `urlBasedDestination.url.templatingStrategy` | Chaîne | *Obligatoire.* <ul><li>Utilisez `PEBBLE_V1` si Adobe doit transformer l’URL dans le champ `value` ci-dessous. Utilisez cette option si vous disposez d’un point d’entrée tel que : `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Utilisez `NONE` si aucune transformation n’est nécessaire du côté d’Adobe, par exemple si vous avez un point d’entrée tel que : `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Chaîne | *Obligatoire.* Renseignez l’adresse du point d’entrée d’API auquel Experience Platform doit se connecter. |
| `httpTemplate.httpMethod` | Chaîne | *Obligatoire.* Méthode qu’Adobe utilise dans les appels vers votre serveur. Les options sont les suivantes : `GET`, `PUT`, `POST`, `DELETE` ou `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Chaîne | *Obligatoire.* Cette chaîne est la version avec échappement par des caractères qui transforme les données des clients Platform au format attendu par votre service. <br> <ul><li> Pour plus d’informations sur l’écriture du modèle, lisez la section [Utilisation des modèles](./message-format.md#using-templating). </li><li> Pour plus d’informations sur l’échappement des caractères, reportez-vous à la section [Norme RFC JSON, section 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Pour un exemple de transformation simple, reportez-vous à la transformation [Attributs de profil](./message-format.md#attributes). </li></ul> |
| `httpTemplate.contentType` | Chaîne | *Obligatoire.* Type de contenu que votre serveur accepte. Cette valeur est probablement `application/json`. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.

## Créer une configuration pour un serveur de destination basé sur des fichiers {#create-file-based}

### Exemple de configuration du serveur de destination SFTP {#sftp-server-sample}

+++Afficher un exemple pour un [!DNL SFTP] configuration du serveur de destination

Vous pouvez créer une nouvelle configuration de serveur de destination SFTP en effectuant une requête POST vers le point d’entrée `/authoring/destination-servers`.

**Format d’API**

```http
POST /authoring/destination-servers
```

**Requête**

La requête suivante crée une nouvelle configuration de serveur de destination, configurée en fonction des paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres acceptés par le point d’entrée `/authoring/destination-servers`. Notez que vous n’avez pas à ajouter tous les paramètres à l’appel et que le modèle est personnalisable, conformément aux exigences de votre API.


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
   "fileBasedSftpDestination":{
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

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.
+++

### [!DNL Amazon S3] Exemple de configuration du serveur de destination {#s3-server-sample}

+++Afficher un exemple pour un [!DNL Amazon S3] configuration du serveur de destination

Vous pouvez créer une nouvelle configuration de serveur de destination Amazon S3 en effectuant une requête POST au point d’entrée `/authoring/destination-servers`.

**Format d’API**

```http
POST /authoring/destination-servers
```

**Requête**

La requête suivante crée une nouvelle configuration de serveur de destination, configurée en fonction des paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres acceptés par le point d’entrée `/authoring/destination-servers`. Notez que vous n’avez pas à ajouter tous les paramètres à l’appel et que le modèle est personnalisable, conformément aux exigences de votre API.

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

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.
+++

### [!DNL Azure Blob] Exemple de configuration du serveur de destination {#blob-server-sample}

+++Afficher un exemple pour un [!DNL Azure Blob] configuration du serveur de destination

Vous pouvez créer une configuration de serveur de destination Azure Blob en effectuant une requête POST au point d’entrée `/authoring/destination-servers`.

**Format d’API**

```http
POST /authoring/destination-servers
```

**Requête**

La requête suivante crée une nouvelle configuration de serveur de destination, configurée en fonction des paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres acceptés par le point d’entrée `/authoring/destination-servers`. Notez que vous n’avez pas à ajouter tous les paramètres à l’appel et que le modèle est personnalisable, conformément aux exigences de votre API.

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

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.
+++

### [!DNL Azure Data Lake Storage] Exemple de configuration du serveur de destination {#adls-server-sample}

+++Afficher un exemple pour un [!DNL Azure Data Lake Storage (ADLS)] configuration du serveur de destination

Vous pouvez créer une nouvelle configuration de serveur de destination en effectuant une requête POST vers le point d’entrée `/authoring/destination-servers`.

**Format d’API**

```http
POST /authoring/destination-servers
```

**Requête**

La requête suivante crée une nouvelle configuration de serveur de destination, configurée en fonction des paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres acceptés par le point d’entrée `/authoring/destination-servers`. Notez que vous n’avez pas à ajouter tous les paramètres à l’appel et que le modèle est personnalisable, conformément aux exigences de votre API.

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

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.
+++

### [!DNL Data Landing Zone] Exemple de configuration du serveur de destination (DLZ) {#dlz-server-sample}

+++Afficher un exemple pour un [!DNL Data Landing Zone (DLZ)] configuration du serveur de destination

[!DNL Data Landing Zone] ([!DNL DLZ]) est une interface de stockage [!DNL Azure Blob] fournie par Adobe Experience Platform et qui vous permet d’accéder à une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud pour importer des fichiers dans Platform.

Vous pouvez créer une nouvelle configuration de serveur de destination DLZ en effectuant une requête POST vers le point d’entrée `/authoring/destination-servers`.

**Format d’API**

```http
POST /authoring/destination-servers
```

**Requête**

La requête suivante crée une nouvelle configuration de serveur de destination, configurée en fonction des paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres acceptés par le point d’entrée `/authoring/destination-servers`. Notez que vous n’avez pas à ajouter tous les paramètres à l’appel et que le modèle est personnalisable, conformément aux exigences de votre API.

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

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.
+++

## Liste des configurations de serveur de destination {#retrieve-list}

Vous pouvez récupérer une liste de toutes les configurations de serveur de destination pour votre organisation IMS en effectuant une requête GET sur le point d’entrée `/authoring/destination-servers`.

**Format d’API**

```http
GET /authoring/destination-servers
```

**Requête**

La requête suivante récupère la liste des configurations de serveur de destination auxquelles vous avez accès, en fonction de la configuration de l’organisation IMS et de la configuration de la sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse suivante renvoie un état HTTP 200 avec une liste des configurations de serveur de destination auxquelles vous avez accès, en fonction de l’identifiant de l’organisation IMS et du nom de la sandbox que vous avez utilisés. Un `instanceId` correspond au modèle d’un serveur de destination. La réponse est tronquée à des fins de brièveté.

```json
{
   "items":[
      {
         "instanceId":"2307ec2b-4798-45a4-9239-5d0a2fb0ed67",
         "createdDate":"2020-11-17T06:49:24.331012Z",
         "lastModifiedDate":"2020-11-17T06:49:24.331012Z",
         "name":"Moviestar Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      },
      {
         "instanceId":"d88de647-a352-4824-8b46-354afc7acbff",
         "createdDate":"2020-11-17T16:50:59.635228Z",
         "lastModifiedDate":"2020-11-17T16:50:59.635228Z",
         "name":"Test11 Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      }
   ]
}
    
```

## Mettre à jour une configuration de serveur de destination existante {#update}

Vous pouvez mettre à jour une configuration de serveur de destination existante en adressant une requête PUT au point d’entrée `/authoring/destination-servers` et en fournissant l’identifiant d’instance de la configuration de serveur de destination que vous souhaitez mettre à jour. Dans le corps de l’appel, indiquez la configuration de serveur de destination mise à jour.

**Format d’API**

```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | Identifiant de la configuration de serveur de destination que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour une configuration de serveur de destination existante, configurée par les paramètres fournis dans la payload.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
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

## Récupérer une configuration de serveur de destination spécifique {#get}

Vous pouvez récupérer des informations détaillées sur une configuration de serveur de destination spécifique en adressant une requête GET au point d’entrée `/authoring/destination-servers` et en fournissant l’identifiant d’instance de la configuration de serveur de destination que vous souhaitez mettre à jour.

**Format d’API**

```http
GET /authoring/destination-servers/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | Identifiant de la configuration de serveur de destination que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la configuration de serveur de destination spécifiée.

```json
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

## Supprimer une configuration de serveur de destination spécifique {#delete}

Vous pouvez supprimer une configuration de serveur de destination spécifiée en effectuant une requête DELETE au point d’entrée `/authoring/destination-servers` et en fournissant l’identifiant de la configuration de serveur de destination que vous souhaitez supprimer du chemin d’accès de la requête.

**Format d’API**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{INSTANCE_ID}` | `id` de la configuration de serveur de destination que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une réponse HTTP vide.

## Gestion des erreurs d’API

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant comment configurer votre serveur de destination et créer des modèles à l’aide du point d’entrée de l’API `/authoring/destination-servers`. Lisez [Comment utiliser le Destination SDK pour configurer une destination](./configure-destination-instructions.md) et comprendre où cette étape s’inscrit dans le processus de configuration d’une destination.
