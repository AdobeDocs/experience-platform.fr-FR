---
description: Les spécifications du serveur et du modèle peuvent être configurées dans le SDK de destination Adobe Experience Platform via le point de terminaison commun `/authoring/destination-servers`.
title: Options de configuration des spécifications de serveur et de modèle dans le SDK de destination
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: bd65cfa557fb42d23022578b98bc5482e8bd50b1
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 7%

---

# Options de configuration des spécifications de serveur et de modèle

## Présentation {#overview}

Les spécifications du serveur et du modèle peuvent être configurées dans le SDK de destination Adobe Experience Platform via le point de terminaison commun `/authoring/destination-servers`. Lisez [Opérations de point d’entrée de l’API Destinations](./destination-server-api.md) pour obtenir la liste complète des opérations que vous pouvez effectuer sur le point d’entrée.

## Exemple de configuration  {#example-configuration}

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

## Spécifications du serveur {#server-specs}

![Configuration du serveur mise en surbrillance](./assets/server-configuration.png)

Les clients pourront activer les données de Adobe Experience Platform vers votre destination par le biais d’exportations HTTP. La configuration du serveur contient des informations sur le serveur recevant les messages (le serveur de votre côté).

Ce processus fournit des données utilisateur sous la forme d’une série de messages HTTP vers votre plateforme de destination. Les paramètres ci-dessous forment le modèle de spécifications du serveur HTTP.

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | Représente un nom convivial de votre serveur, visible uniquement par Adobe. Ce nom n’est pas visible par les partenaires ou les clients. Exemple `Moviestar destination server`. |
| `destinationServerType` | Chaîne | `URL_BASED` est actuellement la seule option disponible. |
| `templatingStrategy` | Chaîne | <ul><li>Utilisez `PEBBLE_V1` si l’Adobe doit transformer l’URL dans le champ `value` ci-dessous. Utilisez cette option si vous disposez d’un point de terminaison du type : `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> Utilisez `NONE` si aucune transformation n’est nécessaire côté Adobe, par exemple si vous avez un point de terminaison comme : `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Chaîne | Renseignez l’adresse du point de terminaison de l’API auquel l’Experience Platform doit se connecter. |

{style=&quot;table-layout:auto&quot;}

<!--

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |
|`httpMethod` | String | The method that Adobe will use in calls to your server. Options are `GET`, `PUT`, `POST`, `DELETE`, `PATCH`, `OPTIONS`, `HEAD`. |
|`contentType` | String | Defines how to structure the content sent to your servers. Supported options are JSON and XML. |

-->

## Spécifications des modèles {#template-specs}

![Mise en surbrillance de la configuration des modèles](./assets/template-configuration.png)

La spécification du modèle vous permet de configurer le format du message exporté vers votre destination. Adobe utilise un langage de modèle similaire à [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) pour transformer les champs du schéma XDM en un format pris en charge par votre destination. Pour plus d’informations sur la transformation, consultez les liens ci-dessous :

* [Format du message](./message-format.md)
* [Utilisation d’une langue de modèle pour les transformations d’identité, d’attributs et d’appartenance aux segments ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe propose un [outil de développement](./create-template.md) qui permet de créer et de tester un modèle de transformation des messages.

| Paramètre | Type | Description |
|---|---|---|
| `httpMethod` | Chaîne | Méthode que l’Adobe utilisera dans les appels à votre serveur. Les options sont `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Chaîne | Utilisez `PEBBLE_V1`. |
| `value` | Chaîne | Cette chaîne est la version avec échappement par des caractères qui transforme les données des clients Platform au format attendu par votre service. <br> Pour plus d’informations sur l’écriture du modèle, consultez la section  [Utilisation de modèles](./message-format.md#using-templating). <br> Pour plus d’informations sur l’échappement des caractères, reportez-vous à la  [norme RFC JSON, section 7](https://tools.ietf.org/html/rfc8259#section-7). <br> Pour un exemple de transformation simple, reportez-vous à la transformation  [Attributs de profil ](./message-format.md#attributes) . |
| `contentType` | Chaîne | Type de contenu que votre serveur accepte. Cette valeur est probablement `application/json`. |

{style=&quot;table-layout:auto&quot;}

<!--

|`requestBody` | String | The request body contains the data exported from Real-time CDP, activated to your destination. <br> We need to know which data format macros your destination should support. See [Outbound Template Macros](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-template-macros.html) and [Outbound Macro Examples](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-macro-examples.html) for examples from Adobe's DMP, Audience Manager. <br> See also, [Message format](#message-format) for further information.  |
|`queryParameters` | String | Request parameters defined as macros. See above.|



<br>&nbsp;

#### Example

A valid HTTP specs template could look like below:

```

{
  "name": "ACME company HTTP template",
  "type": "HTTP", 
  "httpTemplate": {
    "httpMethod": "POST",
    "requestBody": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "queryParameters": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "contentType": "JSON"
  }
}

```

// commenting out this part as these types of destination specs are not supported in phase one

### File specifications

File-based destinations deliver file exports containing segment qualifications and profile attributes to your preferred storage location. If you want to set up a batch file-based destination, the template we'll use will be as below:

## Server specs

The server configuration contains information about the server receiving the messages (the server on your side). 
Adobe Real-time CDP currently supports three types of server configurations:
* URL
* File-based SFTP
* File-based S3

For URL destinations, you would provide us your server's information, for File-based SFTP and File-based S3 you would provide information as to the storage locations where files should be delivered.
Provide us the necessary information about your server or storage locations, as shown in the sections below.


**urlBasedDestination**

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |


// commenting out this part as these types of destination specs are not supported in phase one

**SFTP Destinations**

For FTP destinations, we need the protocol details below:

Parameter | Type | 
---------|----------|
 hostname | String | 
 port | integer | 
 rootDirectory | String | 
 moveToWhenCompleted | integer | 
 tmpFileRename | integer | 
 encryptionMode | String |
 filenameSuffix | String | 

**Amazon S3 Destinations**

For Amazon S3 destinations, we need the protocol details below:

Parameter | Description | 
---------|----------|
 bucket | Your Amazon S3 bucket name | 
 path | Your Amazon S3 bucket path | 

-->
