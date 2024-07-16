---
description: Cette page illustre comment l’appel API est utilisé pour mettre à jour un modèle d’audience avec Adobe Experience Platform Destination SDK.
title: Mise à jour d’un modèle d’audience
exl-id: 8185a015-256d-46a7-af33-8475832fb6c1
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 100%

---

# Mise à jour d’un modèle d’audience

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/audience-templates`

Cette page illustre la requête d’API et la payload que vous pouvez utiliser pour mettre à jour un modèle d’audience à l’aide du point d’entrée `/authoring/audience-templates` de l’API.

Pour obtenir une description détaillée des fonctionnalités configurables avec ce point d’entrée, consultez l’article sur la [gestion des métadonnées d’audience](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations de l’API des modèles d’audience {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Mise à jour d’un modèle d’audience {#create}

Vous pouvez mettre à jour un modèle d’audience [existant](create-audience-template.md) en effectuant une requête `PUT` au point dʼentrée `/authoring/audience-templates` avec la payload mise à jour.

Pour obtenir un modèle d’audience existant et son `{INSTANCE_ID}` correspondant, consultez l’article sur la [récupération d’un modèle d’audience](retrieve-audience-template.md).

**Format d’API**

```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{INSTANCE_ID}` | Identifiant du modèle d’audience à mettre à jour. Pour obtenir un modèle d’audience existant et son `{INSTANCE_ID}` correspondant, consultez la section [Récupération d’un modèle d’audience](retrieve-audience-template.md). |

La requête suivante met à jour un modèle de métadonnées d’audience existant, configuré par les paramètres fournis dans la payload.

+++Requête

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
}'
```

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails du modèle dʼaudience mis à jour.

+++

## Gestion des erreurs d’API

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez quand utiliser les modèles d’audience et comment mettre à jour un modèle d’audience à l’aide du point dʼentrée `/authoring/audience-templates` de l’API. Consultez la documentation [Comment utiliser Destination SDK pour configurer la destination](../guides/configure-destination-instructions.md) afin de comprendre la place de cette étape dans le processus de configuration de la destination.
