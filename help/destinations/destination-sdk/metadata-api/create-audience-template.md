---
description: Cette page illustre comment l’appel API est utilisé pour créer un modèle d’audience avec Adobe Experience Platform Destination SDK.
title: Création d’un modèle d’audience
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 100%

---


# Création d’un modèle d’audience

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/audience-templates`

Pour certaines destinations créées à l’aide de Destination SDK, vous devez créer une configuration de métadonnées d’audience afin de concevoir, mettre à jour ou supprimer des métadonnées de segment dans la destination par programmation. Cette page montre comment utiliser le point d’entrée `/authoring/audience-templates` de l’API pour créer la configuration.

Pour obtenir une description détaillée des fonctionnalités configurables avec ce point d’entrée, consultez l’article sur la [gestion des métadonnées d’audience](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations de l’API des modèles d’audience {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Création d’un modèle d’audience {#create}

Vous pouvez créer un modèle d’audience en effectuant une requête `POST` au point dʼentrée `/authoring/audience-templates`.

**Format d’API**

```http
POST /authoring/audience-templates
```

+++Requête

La requête suivante crée un modèle d’audience configuré en fonction des paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres acceptés par le point dʼentrée `/authoring/audience-templates`. Notez que vous n’avez pas à ajouter tous les paramètres à l’appel et que le modèle est personnalisable, conformément aux exigences de votre API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Chaîne | Nom du modèle de métadonnées d’audience pour la destination. Ce nom apparaît dans tout message d’erreur spécifique au partenaire dans l’interface utilisateur d’Experience Platform, suivi du message d’erreur analysé à partir de `metadataTemplate.create.errorSchemaMap`. |
| `url` | Chaîne | L’URL et le point d’entrée de votre API, qui est utilisé pour créer, mettre à jour, supprimer ou valider les audiences/segments dans votre plateforme. Deux exemples de secteurs sont : `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` et `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | Chaîne | Méthode utilisée sur votre point dʼentrée pour créer, mettre à jour, supprimer ou valider par programmation le segment/l’audience dans la destination. Par exemple : `POST`, `PUT`, `DELETE`. |
| `headers.header` | Chaîne | Spécifie les en-têtes HTTP à ajouter à l’appel de votre API. Par exemple : `"Content-Type"`. |
| `headers.value` | Chaîne | Indique la valeur des en-têtes HTTP à ajouter à l’appel de votre API. Par exemple : `"application/x-www-form-urlencoded"`. |
| `requestBody` | Chaîne | Indique le contenu du corps du message qui doit être envoyé à votre API. Les paramètres qui doivent être ajoutés à l’objet `requestBody` dépendent des champs que votre API accepte. Pour obtenir un exemple, consultez le [premier exemple de modèle](../functionality/audience-metadata-management.md#example-1) dans le document sur les fonctionnalités des métadonnées d’audience. |
| `responseFields.name` | Chaîne | Spécifie les champs de réponse que votre API renvoie lorsqu’elle est appelée. Pour obtenir un exemple, consultez les [exemples de modèles](../functionality/audience-metadata-management.md#examples) dans le document sur les fonctionnalités des métadonnées d’audience. |
| `responseFields.value` | Chaîne | Spécifie la valeur de tout champ de réponse que votre API renvoie lorsqu’elle est appelée. |
| `responseErrorFields.name` | Chaîne | Spécifie les champs de réponse que votre API renvoie lorsqu’elle est appelée. Pour obtenir un exemple, consultez les [exemples de modèles](../functionality/audience-metadata-management.md#examples) dans le document sur les fonctionnalités des métadonnées d’audience. |
| `responseErrorFields.value` | Chaîne | Analyse tous les messages d’erreur renvoyés par les réponses d’appel API de la destination. Ces messages d’erreur seront affichés aux utilisateurs dans l’interface utilisateur d’Experience Platform. |
| `validations.field` | Chaîne | Indique si les validations doivent être exécutées pour tout champ avant que des appels d’API ne soient effectués vers votre destination. Par exemple, vous pouvez utiliser `{{validations.accountId}}` pour valider l’identifiant de compte de l’utilisateur. |
| `validations.regex` | Chaîne | Indique la structure du champ pour que la validation soit réussie. |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 200 avec les détails du modèle dʼaudience que vous venez de créer.

+++

## Gestion des erreurs d’API

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez quand utiliser les modèles d’audience et comment configurer un modèle d’audience à l’aide du point dʼentrée `/authoring/audience-templates` de l’API. Consultez la documentation [Comment utiliser Destination SDK pour configurer la destination](../guides/configure-destination-instructions.md) afin de comprendre la place de cette étape dans le processus de configuration de la destination.
