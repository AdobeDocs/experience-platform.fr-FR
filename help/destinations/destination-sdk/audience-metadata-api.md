---
description: Cette page décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point dʼentrée de l’API « /authoring/audience-templates ».
title: Opérations de l’API du point d’entrée des métadonnées d’audience
exl-id: 3444da8c-b2be-4254-980a-8cce7560134d
source-git-commit: afdabdebe9b82d828cb1941edb99ca2518a941a2
workflow-type: ht
source-wordcount: '879'
ht-degree: 100%

---

# Opérations de l’API du point d’entrée des métadonnées d’audience

>[!IMPORTANT]
>
>**Point dʼentrée de l’API** : `platform.adobe.io/data/core/activation/authoring/audience-templates`

Cette page répertorie et décrit toutes les opérations de l’API que vous pouvez effectuer à l’aide du point d’entrée de l’API `/authoring/audience-templates`. Pour plus dʼinformations sur lʼutilisation de ce point dʼentrée, consultez la section [Gestion des métadonnées d’audience](./audience-metadata-management.md).

## Prise en main des opérations de l’API des modèles d’audience {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md), qui contient des informations importantes à connaître pour réussir à effectuer des appels vers l’API, notamment pour obtenir lʼautorisation de création de destination et les en-têtes requis.

## Créer un modèle d’audience {#create}

Vous pouvez créer un modèle d’audience en effectuant une requête POST vers le point dʼentrée `/authoring/audience-templates`.

**Format d’API**

```http
POST /authoring/audience-templates
```

**Requête**

La requête suivante crée un modèle de métadonnées d’audience configuré en fonction des paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres acceptés par le point dʼentrée `/authoring/audience-templates`. Notez que vous n’avez pas à ajouter tous les paramètres à l’appel et que le modèle est personnalisable, conformément aux exigences de votre API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "name":"string",
      "create":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "update":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "delete":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "validate":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "notify":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      }
   },
   "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| Propriété | Type | Description |
| -------- | ----------- | ----------- |
| `name` | Chaîne | Nom du modèle de métadonnées d’audience pour votre destination. Ce nom apparaît dans tout message d’erreur spécifique au partenaire dans l’interface utilisateur d’Experience Platform, suivi du message d’erreur analysé à partir de `metadataTemplate.create.errorSchemaMap`. |
| `url` | Chaîne | L’URL et le point de terminaison de votre API, qui est utilisé pour créer, mettre à jour, supprimer ou valider les audiences/segments dans votre plateforme. Deux exemples de secteurs sont : `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` et `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | Chaîne | Méthode utilisée sur votre point dʼentrée pour créer, mettre à jour, supprimer ou valider par programmation le segment/l’audience dans votre destination. Par exemple : `POST`, `PUT`, `DELETE`. |
| `headers.header` | Chaîne | Spécifie les en-têtes HTTP à ajouter à l’appel de votre API. Par exemple : `"Content-Type"`. |
| `headers.value` | Chaîne | Indique la valeur des en-têtes HTTP à ajouter à l’appel de votre API. Par exemple : `"application/x-www-form-urlencoded"`. |
| `requestBody` | Chaîne | Indique le contenu du corps du message qui doit être envoyé à votre API. Les paramètres qui doivent être ajoutés à l’objet `requestBody` dépendent des champs que votre API accepte. Pour obtenir un exemple, consultez le [premier exemple de modèle](./audience-metadata-management.md#example-1) dans le document sur les fonctionnalités des métadonnées d’audience. |
| `responseFields.name` | Chaîne | Spécifie les champs de réponse que votre API renvoie lorsqu’elle est appelée. Pour obtenir un exemple, consultez les [exemples de modèles](./audience-metadata-management.md#examples) dans le document sur les fonctionnalités des métadonnées d’audience. |
| `responseFields.value` | Chaîne | Spécifie la valeur de tout champ de réponse que votre API renvoie lorsqu’elle est appelée. |
| `responseErrorFields.name` | Chaîne | Spécifie les champs de réponse que votre API renvoie lorsqu’elle est appelée. Pour obtenir un exemple, consultez les [ exemples de modèles](./audience-metadata-management.md#examples) dans le document sur les fonctionnalités des métadonnées d’audience. |
| `responseErrorFields.value` | Chaîne | Analyse tous les messages d’erreur renvoyés par les réponses d’appel API de votre destination. Ces messages d’erreur seront affichés aux utilisateurs dans l’interface utilisateur d’Experience Platform. |
| `validations.field` | Chaîne | Indique si les validations doivent être exécutées pour tout champ avant que des appels d’API ne soient effectués vers votre destination. Par exemple, vous pouvez utiliser `{{validations.accountId}}` pour valider l’identifiant de compte de l’utilisateur. |
| `validations.regex` | Chaîne | Indique la structure du champ pour que la validation soit réussie. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails du modèle dʼaudience que vous venez de créer.

## Mettre à jour le modèle d’audience {#update}

Vous pouvez mettre à jour un modèle d’audience existant en adressant une requête PUT au point dʼentrée `/authoring/audience-templates` et en fournissant l’identifiant d’instance du modèle d’audience que vous souhaitez mettre à jour. Dans le corps de l’appel, fournissez le modèle mis à jour.

**Format d’API**

```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | Identifiant du modèle de métadonnées d’audience à mettre à jour. |

**Requête**

La requête suivante met à jour un modèle de métadonnées d’audience existant, configuré par les paramètres fournis dans la payload.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1.0/{{customerData.accountId}}/customaudiences?fields=name,description,account_id&subtype=CUSTOM&name={{segment.name}}&customer_file_source={{segment.metadata.customer_file_source}}&access_token={{authData.accessToken}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?field=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}&&name={{segment.name}}&description={{segment.description}}&customer_file_source={{segment.metadata.customer_file_source}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?fields=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "validate":{
         "url":"https://api.moviestar.com/v1.0/permissions?access_token={{authData.accessToken}}",
         "httpMethod":"GET",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.data[0].permission}}",
               "name":"Id"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      }
   }
}
```

## Récupérer une liste de modèles dʼaudience {#retrieve-list}

Vous pouvez récupérer une liste de tous les modèles dʼaudience pour votre organisation IMS en effectuant une requête GET au point dʼentrée `/authoring/audience-templates`.

**Format d’API**


```http
GET /authoring/audience-templates
```

**Requête**

La requête suivante récupère la liste des modèles d’audience auxquels vous avez accès, en fonction de la configuration de l’organisation IMS et du sandbox.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse suivante renvoie un état HTTP 200 avec une liste de modèles de métadonnées d’audience auxquels vous avez accès, en fonction de l’identifiant de l’organisation IMS et du nom de sandbox que vous avez utilisés. Une valeur `instanceId` correspond au modèle pour une destination. La réponse est tronquée à des fins de brièveté.

```json
{
   "items":[
      {
         "instanceId":"12a3238f-b509-4a40-b8fb-0a5006e7901d",
         "createdDate":"2021-07-20T13:30:30.843054Z",
         "lastModifiedDate":"2021-07-21T16:33:05.787472Z",
         "metadataTemplate":{
            "create":{
               "url":"https://api.moviestar.com/v2/dmpSegments",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "name":"{{segment.name}}",
                     "type":"USER",
                     "account":"{{customerData.accountId}}",
                     "accessPolicy":"PRIVATE",
                     "destinations":[
                        {
                           "destination":"MOVIESTAR"
                        }
                     ],
                     "sourcePlatform":"ADOBE"
                  }
               },
               "responseFields":[
                  {
                     "value":"{{headers.x-moviestar-id}}",
                     "name":"externalAudienceId"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "update":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "patch":{
                        "$set":{
                           "name":"{{segment.name}}"
                        }
                     }
                  }
               },
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "delete":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"DELETE",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "name":"Moviestar audience template - Third example"
         }
      }
   ]
}
```

## Récupérer un modèle d’audience spécifique {#get}

Vous pouvez récupérer des informations détaillées sur un modèle d’audience spécifique en effectuant une requête GET au point dʼentrée `/authoring/audience-templates` et en fournissant l’identifiant d’instance du modèle d’audience que vous souhaitez récupérer.

**Format d’API**

```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | Identifiant du modèle de métadonnées d’audience à récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur le modèle d’audience spécifié.

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```


## Supprimer un modèle d’audience spécifique {#delete}

Vous pouvez supprimer un modèle d’audience en effectuant une requête DELETE au point dʼentrée `/authoring/audience-templates` et en fournissant l’identifiant du modèle dʼaudience que vous souhaitez supprimer du chemin d’accès de la requête.

**Format d’API**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{INSTANCE_ID}` | Valeur `id` du modèle d’audience à supprimer. |

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une réponse HTTP vide.

## Gestion des erreurs d’API

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes d’état d’API](../../landing/troubleshooting.md#api-status-codes) et [Erreurs d’en-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez à quel moment utiliser les modèles de métadonnées d’audience et comment configurer un modèle de métadonnées d’audience à l’aide du point dʼentrée d’API `/authoring/audience-templates`. Poursuivez votre apprentissage dans la section [Comment utiliser Destination SDK pour configurer votre destination](./configure-destination-instructions.md) et obtenez une vue dʼensemble du processus de configuration de votre destination.
