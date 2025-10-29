---
description: Découvrez comment utiliser l’API de test de destination pour tester si la destination de diffusion en streaming est configurée correctement et pour vérifier l’intégrité des flux de données vers la destination configurée.
title: Test de la destination de diffusion en streaming avec des profils types
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 99%

---


# Test de la destination de diffusion en streaming avec des profils types {#template-api-operations}

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

Cette page répertorie et décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point d’entrée `/authoring/testing/destinationInstance/` de l’API pour tester si la destination est configurée correctement et pour vérifier l’intégrité des flux de données vers la destination configurée. Pour obtenir une description des fonctionnalités prises en charge par ce point d’entrée, consultez [Test de la configuration de destination](streaming-destination-testing-overview.md).

Vous envoyez des requêtes au point d’entrée de test avec ou sans ajout de profils à l’appel. Si vous n’envoyez aucun profil à la requête, Adobe les génère en interne et les ajoute à la requête.

Vous pouvez utiliser la [génération de ’profils types API](sample-profile-generation-api.md) pour créer des profils à utiliser dans les requêtes de l’API de test de destination.

## Comment obtenir l’identifiant d’instance de destination {#get-destination-instance-id}

>[!IMPORTANT]
>
>* Pour utiliser cette API, vous devez disposer d’une connexion existante vers la destination dans l’interface utilisateur d’Experience Platform. Pour plus d’informations, consultez la documentation [Se connecter à la destination](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=fr) et [Activer des profils et des audiences vers cette destination](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html).
>* Après avoir établi la connexion à la destination, obtenez l’identifiant d’instance de destination que vous devez utiliser dans les appels API vers ce point d’entrée pendant la [recherche d’une connexion avec la destination ](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html).
>  >![Image de l’interface illustrant comment obtenir l’identifiant d’instance de destination](../../assets/testing-api/get-destination-instance-id.png)

## Prise en main des opérations dʼAPI de test de destination {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Test de la configuration de la destination sans ajout de profils à l’appel {#test-without-adding-profiles}

Vous pouvez tester votre configuration de destination en adressant une requête POST au point d’entrée `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` et en indiquant l’identifiant de l’instance de destination de la destination que vous testez.

**Format d’API**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Paramètre de requête | Description |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | Identifiant d’instance de destination de la destination que vous testez. |

**Requête**

La requête suivante appelle le point d’entrée de l’API REST de la destination. La requête est configurée par le paramètre de requête `{DESTINATION_INSTANCE_ID}`.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec la réponse de l’API provenant du point d’entrée de l’API REST de la destination.

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
| `aggregationKey` | Inclut des informations sur la politique d’agrégation configurée pour la destination. Pour plus d’informations, consultez la documentation [Politique d’agrégation](../../functionality/destination-configuration/aggregation-policy.md). |
| `traceId` | Identifiant unique de l’opération. En cas d’erreur, vous pouvez partager cet identifiant avec l’équipe Adobe pour faciliter le dépannage. |
| `results.httpCalls.request` | Inclut la requête qui a été envoyée par Adobe à la destination. |
| `results.httpCalls.response` | Inclut la réponse de la destination reçue par Adobe. |
| `inputProfiles` | Inclut les profils qui ont été exportés pendant l’appel vers la destination. Les profils correspondent à votre schéma source. |

{style="table-layout:auto"}

## Test de la configuration de la destination avec ajout de profils à l’appel {#test-with-added-profiles}

Vous pouvez tester votre configuration de destination en adressant une requête POST au point d’entrée `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` et en indiquant l’identifiant de l’instance de destination de la destination que vous testez.

**Format d’API**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Paramètre de requête | Description |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | Identifiant d’instance de destination de la destination que vous testez. |

**Requête**

La requête suivante appelle le point d’entrée de l’API REST de la destination. La requête est configurée par les paramètres fournis dans la payload et le paramètre de requête `{DESTINATION_INSTANCE_ID}`.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
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

Une réponse réussie renvoie le statut HTTP 200 avec la réponse de l’API provenant du point d’entrée de l’API REST de la destination.

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

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment tester la destination. Vous pouvez désormais utiliser le [processus de documentation en libre-service](../../docs-framework/documentation-instructions.md) d’Adobe pour créer une page de documentation pour la destination.
