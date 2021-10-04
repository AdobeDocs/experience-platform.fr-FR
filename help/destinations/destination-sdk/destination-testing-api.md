---
description: Cette page répertorie et décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point de terminaison de l’API `/authoring/testing/destinationInstance/`, afin de tester si votre destination est configurée correctement et de vérifier l’intégrité des flux de données vers votre destination configurée.
title: Opérations de l’API de test de destination
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: 45cff6f0c4d4fd63a17108087edec0184cbf9703
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 2%

---

# Opérations de l’API de test de destination {#template-api-operations}

>[!IMPORTANT]
>
>**Point de terminaison de l’API**: `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

Cette page répertorie et décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point de terminaison de l’API `/authoring/testing/destinationInstance/`, afin de tester si votre destination est configurée correctement et de vérifier l’intégrité des flux de données vers votre destination configurée. Pour une description des fonctionnalités prises en charge par ce point de terminaison, consultez la section [Test de votre configuration de destination](./test-destination.md).

Vous envoyez des requêtes au point de terminaison de test avec ou sans ajouter de profils à l’appel . Si vous n’envoyez aucun profil sur la requête, Adobe les génère en interne et les ajoute à la requête.

Vous pouvez utiliser l’[API de génération d’exemple de profil](./sample-profile-generation-api.md) pour créer des profils à utiliser dans les requêtes de l’API de test de destination.

## Comment obtenir l’ID d’instance de destination {#get-destination-instance-id}

>[!IMPORTANT]
>
>* Pour utiliser cette API, vous devez disposer d’une connexion existante à votre destination dans l’interface utilisateur de l’Experience Platform. Pour plus d’informations, consultez [Connexion à la destination](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) et [activation des profils et des segments vers une destination](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en). Après avoir établi la connexion à votre destination, récupérez l’ID d’instance de destination que vous devez utiliser dans les appels API vers ce point de terminaison à partir de l’URL lorsque vous [parcourez une connexion avec votre destination](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=en).
   >![Image de l’interface utilisateur comment obtenir l’ID d’instance de destination](./assets/get-destination-instance-id.png)


## Prise en main des opérations de l’API de test de destination {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de destination requise et les en-têtes requis.

## Tester la configuration de votre destination sans ajouter de profils à l’appel {#test-without-adding-profiles}

Vous pouvez tester la configuration de votre destination en envoyant une requête de POST au point de terminaison `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` et en fournissant l’identifiant de l’instance de destination de la destination que vous testez.

**Format d&#39;API**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Paramètre de requête | Description |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | L’ID d’instance de destination de la destination que vous testez. |

**Requête**

La requête suivante appelle le point de terminaison de l’API REST de votre destination. La requête est configurée par le paramètre de requête `{DESTINATION_INSTANCE_ID}` .

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec la réponse de l’API provenant du point de terminaison de l’API REST de votre destination.

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-vlnt6"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

| Propriété | Description |
| -------- | ----------- |
| `aggregationKey` | Inclut des informations sur la stratégie d’agrégation configurée pour la destination. Pour plus d’informations, consultez la section [Stratégie d’agrégation](./destination-configuration.md#aggregation) dans le document de configuration de destination. |
| `traceId` | Identifiant unique de l’opération. En cas d’erreur, vous pouvez partager cet identifiant avec l’équipe Adobe à des fins de dépannage. |
| `results.httpCalls.request` | Inclut la demande qui a été envoyée par Adobe à votre destination. |
| `results.httpCalls.response` | Inclut la réponse reçue par l’Adobe de votre destination. |
| `inputProfiles` | Inclut les profils qui ont été exportés lors de l’appel vers votre destination. Les profils correspondent à votre schéma source. |

{style=&quot;table-layout:auto&quot;}

## Tester la configuration de votre destination avec les profils ajoutés à l’appel {#test-with-added-profiles}

Vous pouvez tester la configuration de votre destination en envoyant une requête de POST au point de terminaison `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` et en fournissant l’identifiant de l’instance de destination de la destination que vous testez.

**Format d&#39;API**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Paramètre de requête | Description |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | L’ID d’instance de destination de la destination que vous testez. |

**Requête**

La requête suivante appelle le point de terminaison de l’API REST de votre destination. La requête est configurée par les paramètres fournis dans la payload et le paramètre de requête `{DESTINATION_INSTANCE_ID}`.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec la réponse de l’API provenant du point de terminaison de l’API REST de votre destination.

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}
```

## Gestion des erreurs d’API {#api-error-handling}

Les points d’entrée de l’API du SDK de destination suivent les principes généraux des messages d’erreur de l’API Experience Platform. Reportez-vous aux sections [Codes d’état d’API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) et [erreurs d’en-tête de requête](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant comment tester votre destination. Vous pouvez désormais utiliser le processus de documentation en libre-service [Adobe](./docs-framework/documentation-instructions.md) pour créer une page de documentation pour votre destination.
