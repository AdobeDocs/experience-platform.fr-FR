---
description: Utilisez les modèles de métadonnées d’audience pour créer, mettre à jour ou supprimer des audiences par programmation dans votre destination. Adobe fournit un modèle de métadonnées d’audience extensible que vous pouvez configurer en fonction des spécifications de votre API marketing. Une fois le modèle défini, testé et envoyé, il sera utilisé par Adobe pour structurer les appels API vers votre destination.
title: Gérer les métadonnées d’audience
exl-id: 795e8adb-c595-4ac5-8d1a-7940608d01cd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 73%

---

# Gérer les métadonnées d’audience

Utilisez les modèles de métadonnées d’audience pour créer, mettre à jour ou supprimer des audiences par programmation dans votre destination. Adobe fournit un modèle de métadonnées d’audience extensible que vous pouvez configurer en fonction des spécifications de votre API marketing. Une fois la configuration définie, testée et envoyée, elle sera utilisée par Adobe pour structurer les appels API vers votre destination.

Vous pouvez configurer les fonctionnalités décrites dans ce document à l’aide du point d’entrée de lʼAPI `/authoring/audience-templates`. Consultez la section [Création d’un modèle de métadonnées](../metadata-api/create-audience-template.md) pour obtenir une liste complète des opérations que vous pouvez effectuer sur le point d’entrée.

## Quand utiliser le point d’entrée de la gestion des métadonnées d’audience {#when-to-use}

Selon la configuration de votre API, vous devrez peut-être utiliser le point d’entrée de la gestion des métadonnées d’audience, car vous configurez votre destination dans Experience Platform. Utilisez le diagramme d’arborescence de décision ci-dessous pour savoir quand utiliser le point d’entrée des métadonnées d’audience et comment configurer un modèle de métadonnées d’audience pour votre destination.

![Diagramme d’arborescence de décision](../assets/functionality/audience-metadata-decision-tree.png)

## Cas d’utilisation pris en charge par la gestion des métadonnées d’audience {#use-cases}

Grâce à la prise en charge des métadonnées d’audience dans Destination SDK, lorsque vous configurez votre destination Experience Platform, vous pouvez proposer aux utilisateurs d’Experience Platform de choisir entre plusieurs options lorsqu’ils mappent et activent des audiences vers votre destination. Vous pouvez contrôler les options disponibles pour l’utilisateur via les paramètres de la section [Configuration des métadonnées d’audience](../functionality/destination-configuration/audience-metadata-configuration.md) de la configuration de destination.

### Cas d’utilisation 1 : vous disposez d’une API tierce et les utilisateurs et utilisatrices n’ont pas besoin de saisir les identifiants de mappage

Si vous disposez d’un point d’entrée de l’API pour créer/mettre à jour/supprimer des audiences, vous pouvez utiliser des modèles de métadonnées d’audience pour configurer Destination SDK afin qu’il corresponde aux spécifications de votre point d’entrée de création/mise à jour/suppression d’audiences. Experience Platform peut créer/mettre à jour/supprimer des audiences par programmation et synchroniser les métadonnées avec Experience Platform.

Lors de l’activation d’audiences vers votre destination dans l’interface utilisateur (IU) dʼExperience Platform, les personnes n’ont pas besoin de remplir manuellement un champ d’identifiant de mappage d’audiences dans le workflow d’activation.

### Cas d’utilisation 2 : les personnes doivent d’abord créer une audience dans votre destination et saisir manuellement l’identifiant de mappage

Si des audiences et d’autres métadonnées doivent être créées manuellement par des partenaires ou des personnes dans votre destination, les personnes doivent renseigner manuellement le champ identifiant de mappage d’audiences dans le workflow d’activation pour synchroniser les métadonnées d’audiences entre votre destination et Experience Platform.

![Identifiant de mappage d’entrée](../assets/functionality/input-mapping-id.png)

### Cas d’utilisation 3 : votre destination accepte l’identifiant d’audience Experience Platform et les personnes n’ont pas besoin de saisir manuellement l’identifiant de mappage

Si votre système de destination accepte l’identifiant de l’audience Experience Platform, vous pouvez le configurer dans votre modèle de métadonnées d’audience. Les personnes n’ont pas à renseigner d’identifiant de mappage d’audience lors de l’activation d’un segment.

## Modèle d’audience générique et extensible {#generic-and-extensible}

Afin de prendre en charge les cas d’utilisation répertoriés ci-dessus, Adobe fournit un modèle générique qui peut être personnalisé pour s’adapter aux spécifications de votre API.

Vous pouvez utiliser le modèle générique pour [créer un modèle d’audience](../metadata-api/create-audience-template.md) si votre API prend en charge les éléments suivants :

* Méthodes HTTP : POST, GET, PUT, DELETE et PATCH
* Types d’authentification : OAuth 1, OAuth 2 avec jeton d’actualisation et OAuth 2 avec jeton porteur
* Fonctions : créer une audience, mettre à jour une audience, obtenir une audience, supprimer une audience et valider des informations d’identification

L’équipe d’ingénieurs Adobe peut collaborer avec vous pour développer le modèle générique avec des champs personnalisés si vos cas d’utilisation le demandent.


## Événements de modèle pris en charge {#supported-events}

Le tableau ci-dessous décrit les événements pris en charge par les modèles de métadonnées d’audience.

| Section modèles | Description |
|--- |--- |
| `create` | Inclut tous les composants requis (URL, méthode HTTP, en-têtes, requête et corps de réponse) pour effectuer un appel HTTP vers votre API afin de créer par programmation des segments/audiences dans votre plateforme et de resynchroniser les informations avec Adobe Experience Platform. |
| `update` | Inclut tous les composants requis (URL, méthode HTTP, en-têtes, requête et corps de réponse) pour effectuer un appel HTTP vers votre API, pour mettre à jour par programmation les segments/audiences de votre plateforme et resynchroniser les informations avec Adobe Experience Platform. |
| `delete` | Inclut tous les composants requis (URL, méthode HTTP, en-têtes, requête et corps de réponse) pour effectuer un appel HTTP vers votre API afin de supprimer par programmation les segments/audiences de votre plateforme. |
| `validate` | Exécute des validations pour tous les champs de la configuration du modèle avant d’effectuer un appel vers l’API du partenaire. Par exemple, vous pouvez vérifier que l’identifiant de compte de l’utilisateur est saisi correctement. |
| `notify` | S’applique uniquement aux destinations basées sur des fichiers. Inclut tous les composants requis (URL, méthode HTTP, en-têtes, requête et corps de réponse) pour effectuer un appel HTTP vers votre API afin de vous informer de la réussite des exportations de fichiers. |
| `createDestination` | Inclut tous les composants requis (URL, méthode HTTP, en-têtes, requête et corps de réponse) pour effectuer un appel HTTP vers votre API afin de créer par programmation un flux de données dans votre plateforme et de resynchroniser les informations avec Adobe Experience Platform. |
| `updateDestination` | Inclut tous les composants requis (URL, méthode HTTP, en-têtes, requête et corps de réponse) pour effectuer un appel HTTP vers votre API, pour mettre à jour par programmation un flux de données dans votre plateforme et resynchroniser les informations avec Adobe Experience Platform. |
| `deleteDestination` | Inclut tous les composants requis (URL, méthode HTTP, en-têtes, requête et corps de réponse) pour effectuer un appel HTTP vers votre API afin de supprimer par programmation un flux de données de votre plateforme. |

{style="table-layout:auto"}

## Exemples de configurations {#configuration-examples}

Cette section comprend des exemples de configurations génériques de métadonnées d’audience, à titre de référence.

Notez les différences entre l’URL, les en-têtes et les corps de requête entre les trois exemples de configuration. Cela est dû aux différentes spécifications de l’API marketing des trois exemples de plateformes.

Notez que dans certains exemples les champs de macro tels que `{{authData.accessToken}}` ou `{{segment.name}}` sont utilisés dans l’URL et que dans d’autres exemples ils sont utilisés dans les en-têtes ou dans le corps de la requête. Leur utilisation dépend des spécifications de votre API marketing.

+++Exemple de diffusion en continu 1

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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

+++

+++Exemple de diffusion en continu 2

```json
{
   "instanceId":"12c78017-5af3-4d4e-8f9c-d330c547c482",
   "createdDate":"2021-07-20T13:27:37.029490Z",
   "lastModifiedDate":"2021-07-20T18:53:03.622306Z",
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

+++

+++Exemple de diffusion en continu 3

```json
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
```

+++

+++Exemple basé sur des fichiers

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
      "notify":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
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

+++

Recherchez des descriptions de tous les paramètres du modèle dans la référence de l’API [Création d’un modèle d’audience](../metadata-api/create-audience-template.md).

## Macros utilisées dans les modèles de métadonnées d’audience {#macros}

Afin de transmettre des informations telles que des ID d’audience, des jetons d’accès, des messages d’erreur, etc. entre Experience Platform et votre API, les modèles d’audience incluent des macros que vous pouvez utiliser. Lisez ci-dessous une description des macros utilisées dans les trois exemples de configuration de cette page :

| Macro | Description |
|--- |--- |
| `{{segment.alias}}` | Permet d’accéder à l’alias de l’audience dans Experience Platform. |
| `{{segment.name}}` | Permet d’accéder au nom de l’audience dans Experience Platform. |
| `{{segment.id}}` | Permet d’accéder à l’ID de l’audience dans Experience Platform. |
| `{{customerData.accountId}}` | Permet d’accéder au champ d’identifiant de compte que vous configurez dans la configuration de destination. |
| `{{oauth2ServiceAccessToken}}` | Permet de générer dynamiquement un jeton d’accès en fonction de votre configuration OAuth 2. |
| `{{authData.accessToken}}` | Permet de transmettre le jeton d’accès à votre point d’entrée d’API. Utilisez `{{authData.accessToken}}` si Experience Platform doit utiliser des jetons non expirants pour se connecter à votre destination, sinon utilisez `{{oauth2ServiceAccessToken}}` pour générer un jeton d’accès. |
| `{{body.segments[0].segment.id}}` | Renvoie l’identifiant unique de l’audience créée, sous la forme de la valeur de la clé `externalAudienceId`. |
| `{{error.message}}` | Renvoie un message d’erreur qui sera visible pour les utilisateurs dans l’interface utilisateur d’Experience Platform. |
| `{{{segmentEnrichmentAttributes}}}` | Permet d’accéder à tous les attributs d’enrichissement pour une audience spécifique.  Cette macro est prise en charge par les événements `create`, `update` et `delete`. Les attributs d’enrichissement sont disponibles uniquement pour les [&#x200B; audiences de chargement personnalisées &#x200B;](destination-configuration/schema-configuration.md#external-audiences). Consultez le [guide d’activation des audiences par lot](../../ui/activate-batch-profile-destinations.md#select-enrichment-attributes) pour découvrir comment fonctionne la sélection d’attributs d’enrichissement. |
| `{{destination.name}}` | Renvoie le nom de la destination. |
| `{{destination.sandboxName}}` | Renvoie le nom du sandbox Experience Platform dans lequel la destination est configurée. |
| `{{destination.id}}` | Renvoie l’identifiant de votre configuration de destination. |
| `{{destination.imsOrgId}}` | Renvoie l’identifiant de l’organisation IMS où la destination est configurée. |
| `{{destination.enrichmentAttributes}}` | Permet d’accéder à tous les attributs d’enrichissement pour toutes les audiences mappées à une destination. Cette macro est prise en charge par les événements `createDestination`, `updateDestination` et `deleteDestination`. Les attributs d’enrichissement sont disponibles uniquement pour les [&#x200B; audiences de chargement personnalisées &#x200B;](destination-configuration/schema-configuration.md#external-audiences). Consultez le [guide d’activation des audiences par lot](../../ui/activate-batch-profile-destinations.md#select-enrichment-attributes) pour découvrir comment fonctionne la sélection d’attributs d’enrichissement. |
| `{{destination.enrichmentAttributes.<namespace>.<segmentId>}}` | Permet d’accéder aux attributs d’enrichissement pour des audiences externes spécifiques mappées à une destination. Les attributs d’enrichissement sont disponibles uniquement pour les [&#x200B; audiences de chargement personnalisées &#x200B;](destination-configuration/schema-configuration.md#external-audiences). Consultez le [guide d’activation des audiences par lot](../../ui/activate-batch-profile-destinations.md#select-enrichment-attributes) pour découvrir comment fonctionne la sélection d’attributs d’enrichissement. |

{style="table-layout:auto"}
