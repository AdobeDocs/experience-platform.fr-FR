---
description: Cette page répertorie et décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point de terminaison API `/authoring/destination-servers. Les spécifications du serveur et du modèle pour votre destination peuvent être configurées dans le SDK de destination Adobe Experience Platform via le point de terminaison commun `/authoring/destination-servers`.
title: Opérations de l’API du point d’entrée du serveur de destination
exl-id: a144b0fb-d34f-42d1-912b-8576296e59d2
source-git-commit: bd65cfa557fb42d23022578b98bc5482e8bd50b1
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 5%

---

# Opérations de l’API du point d’entrée du serveur de destination

>[!IMPORTANT]
>
>**Point de terminaison de l’API**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Cette page répertorie et décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point de terminaison de l’API `/authoring/destination-servers`. Les spécifications du serveur et du modèle pour votre destination peuvent être configurées dans le SDK de destination Adobe Experience Platform via le point de terminaison commun `/authoring/destination-servers`. Pour une description de la fonctionnalité fournie par ce point de terminaison, lisez [les spécifications du serveur et du modèle](./server-and-template-configuration.md).

## Prise en main des opérations de l’API du serveur de destination {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de destination requise et les en-têtes requis.

## Création d’une configuration pour un serveur de destination {#create}

Vous pouvez créer une configuration de serveur de destination en envoyant une requête de POST au point de terminaison `/authoring/destination-servers` .

**Format d’API**


```http
POST /authoring/destination-servers
```

**Requête**

La requête suivante crée une configuration de serveur de destination, configurée par les paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres acceptés par le point de terminaison `/authoring/destination-servers`. Notez que vous n’avez pas à ajouter tous les paramètres à l’appel et que le modèle est personnalisable, conformément aux exigences de votre API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Chaîne | Représente un nom convivial de votre serveur, visible uniquement par Adobe. Ce nom n’est pas visible par les partenaires ou les clients. Exemple `Moviestar destination server`. |
| `destinationServerType` | Chaîne | `URL_BASED` est actuellement la seule option disponible. |
| `urlBasedDestination.url.templatingStrategy` | Chaîne | <ul><li>Utilisez `PEBBLE_V1` si l’Adobe doit transformer l’URL dans le champ `value` ci-dessous. Utilisez cette option si vous disposez d’un point de terminaison du type : `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Utilisez `NONE` si aucune transformation n’est nécessaire côté Adobe, par exemple si vous avez un point de terminaison comme : `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Chaîne | Renseignez l’adresse du point de terminaison de l’API auquel l’Experience Platform doit se connecter. |
| `urlBasedDestination.maxUsersPerRequest` | Entier | Adobe peut agréger plusieurs profils exportés en un seul appel HTTP. Indiquez le nombre maximal de profils que votre point de terminaison doit recevoir dans un seul appel HTTP. Notez qu’il s’agit d’une agrégation du meilleur effort. Par exemple, si vous indiquez la valeur 100, Adobe peut envoyer n’importe quel nombre de profils inférieur à 100 lors d’un appel. <br> Si votre serveur n’accepte pas plusieurs utilisateurs par demande, définissez cette valeur sur 1. |
| `urlBasedDestination.splitUserById` | Booléen | Utilisez cet indicateur si l’appel à la destination doit être divisé par l’identité. Définissez cet indicateur sur `true` si votre serveur n’accepte qu’une seule identité par appel, pour un espace de noms donné. |
| `httpTemplate.httpMethod` | Chaîne | Méthode que l’Adobe utilisera dans les appels à votre serveur. Les options sont `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Chaîne | Utilisez `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Chaîne | Cette chaîne est la version avec échappement par des caractères qui transforme les données des clients Platform au format attendu par votre service. <br> <ul><li> Pour plus d’informations sur la façon d’écrire le modèle, consultez la [section Utilisation de modèles](./message-format.md#using-templating). </li><li> Pour plus d’informations sur l’échappement des caractères, reportez-vous à la [norme JSON RFC, section 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Pour un exemple de transformation simple, reportez-vous à la transformation [Attributs de profil](./message-format.md#attributes) . </li></ul> |
| `httpTemplate.contentType` | Chaîne | Type de contenu que votre serveur accepte. Cette valeur est probablement `application/json`. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la configuration du serveur de destination que vous venez de créer.

## Liste des configurations de serveur de destination {#retrieve-list}

Vous pouvez récupérer une liste de toutes les configurations de serveur de destination pour votre organisation IMS en envoyant une requête GET au point de terminaison `/authoring/destination-servers` .

**Format d’API**


```http
GET /authoring/destination-servers
```

**Requête**

La requête suivante récupère la liste des configurations de serveur de destination auxquelles vous avez accès, en fonction de la configuration de l’organisation IMS et de l’environnement de test.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse suivante renvoie un état HTTP 200 avec une liste des configurations de serveur de destination auxquelles vous avez accès, en fonction de l’identifiant de l’organisation IMS et du nom de l’environnement de test que vous avez utilisés. Un `instanceId` correspond au modèle d’un serveur de destination. La réponse est tronquée pour la concision.

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

Vous pouvez mettre à jour une configuration de serveur de destination existante en envoyant une requête de PUT au point de terminaison `/authoring/destination-servers` et en fournissant l’ID d’instance de la configuration de serveur de destination que vous souhaitez mettre à jour. Dans le corps de l’appel , indiquez la configuration mise à jour du serveur de destination.

**Format d’API**


```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | L’identifiant de la configuration du serveur de destination que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour une configuration de serveur de destination existante, configurée par les paramètres fournis dans la payload.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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





## Récupération d’une configuration de serveur de destination spécifique {#get}

Vous pouvez récupérer des informations détaillées sur une configuration de serveur de destination spécifique en envoyant une requête GET au point de terminaison `/authoring/destination-servers` et en fournissant l’ID d’instance de la configuration de serveur de destination que vous souhaitez mettre à jour.

**Format d’API**


```http
GET /authoring/destination-servers/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | L’identifiant de la configuration du serveur de destination que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la configuration du serveur de destination spécifié.

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


## Suppression d’une configuration de serveur de destination spécifique {#delete}

Vous pouvez supprimer la configuration de serveur de destination spécifiée en effectuant une requête de DELETE sur le point de terminaison `/authoring/destination-servers` et en fournissant l’identifiant de la configuration de serveur de destination que vous souhaitez supprimer dans le chemin d’accès de la requête.

**Format d’API**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{INSTANCE_ID}` | `id` de la configuration du serveur de destination que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une réponse HTTP vide.

## Gestion des erreurs d’API

Les points d’entrée de l’API du SDK de destination suivent les principes généraux des messages d’erreur de l’API Experience Platform. Reportez-vous aux sections [Codes d’état d’API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) et [erreurs d’en-tête de requête](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant comment configurer votre serveur de destination et votre modèle à l’aide du point de terminaison de l’API `/authoring/destination-servers`. Lisez la section [Comment utiliser le SDK de destination pour configurer votre destination](./configure-destination-instructions.md) afin de comprendre où cette étape correspond au processus de configuration de votre destination.
