---
description: Découvrez comment utiliser l’API de test de destination pour tester votre configuration de destination de diffusion en streaming avant de la publier.
title: Vue d’ensemble de l’API de test de destination en streaming
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 100%

---


# Vue d’ensemble de l’API de test de destination en streaming

Dans le cadre de Destination SDK, Adobe fournit des outils de développement pour vous aider à configurer et tester la destination. Cette page décrit comment tester la configuration de destination. Pour plus d’informations sur la création d’un modèle de transformation de message, consultez la page [Création et test d’un modèle de transformation de message](../../testing-api/streaming-destinations/create-template.md).

Pour **tester si la destination est configurée correctement et vérifier l’intégrité des flux de données vers la destination configurée**, utilisez l’*outil de test de destination*. Il vous permet de tester la configuration de la destination en envoyant des messages à votre point d’entrée de l’API REST.

L’illustration ci-dessous montre comment le test de la destination s’intègre dans le [workflow de configuration de la destination](../../guides/configure-destination-instructions.md) de Destination SDK :

![Graphique indiquant la place de l’étape de test de la destination dans le workflow de configuration de destination](../../assets/testing-api/test-destination-step.png)

## Outil de test de destination - Objectif et conditions préalables {#destination-testing-tool}

Utilisez l’outil de test de destination pour tester la configuration de la destination en envoyant des messages au point d’entrée de partenaire que vous avez fourni dans la [configuration du serveur](../../authoring-api/destination-server/create-destination-server.md).

Avant d’utiliser l’outil, veillez à :
* configurer la destination en suivant les étapes décrites dans le [workflow de configuration des destinations](../../authoring-api/destination-configuration/create-destination-configuration.md) ; et
* établir une connexion à la destination, comme indiqué dans la section [Comment obtenir l’identifiant d’instance de destination](../../testing-api/streaming-destinations/destination-testing-api.md#get-destination-instance-id).

Avec cet outil, après avoir configuré la destination, vous pouvez :
* tester si la destination est correctement configurée ;
* vérifier l’intégrité des flux de données vers la destination configurée.

### Utilisation {#how-to-use}

>[!NOTE]
>
>Pour consulter la documentation de référence complète sur l’API, consultez les [opérations d’API de test de destination ](../../testing-api/streaming-destinations/destination-testing-api.md).

Vous pouvez appeler le point d’entrée de l’API de test de destination avec ou sans ajout de profils à la requête.

Si vous n’ajoutez aucun profil à la requête, Adobe les génère en interne et les ajoute à la requête. Si vous souhaitez générer des profils à utiliser dans cette requête, consultez la [référence d’API de génération de profils types](../../testing-api/streaming-destinations/sample-profile-generation-api.md). Vous devez générer des profils en fonction du schéma XDM source, comme indiqué dans la [référence d’API](../../testing-api/streaming-destinations/sample-profile-generation-api.md#generate-sample-profiles-source-schema). Notez que le schéma source est le [schéma d’union](../../../../profile/ui/union-schema.md) du sandbox que vous utilisez.

La réponse contient le résultat du traitement de la requête de destination. La requête comprend trois sections principales :
* La requête générée par Adobe pour la destination.
* La réponse de la destination reçue.
* La liste des profils envoyés dans la requête, si les profils ont été [ajoutés par vous dans la requête](../../testing-api/streaming-destinations/destination-testing-api.md#test-with-added-profiles), ou générés par Adobe si [le corps de la requête de test de destination était vide](../../testing-api/streaming-destinations/destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>Adobe peut générer plusieurs paires de requêtes et de réponses. Par exemple, si vous envoyez 10 profils vers une destination qui comporte une valeur de 7 `maxUsersPerRequest`, une requête avec 7 profils et une autre requête avec 3 profils seront générées.

**Exemple de requête avec paramètre de profil dans le corps**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
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
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**Exemple de requête sans paramètre de profil dans le corps**


```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw ''
```

**Exemple de réponse**

Notez que le contenu du paramètre `results.httpCalls` est spécifique à votre API REST.

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
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
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

Pour les descriptions des paramètres de requête et de réponse, consultez les [opérations de l’API de test de destination](../../testing-api/streaming-destinations/destination-testing-api.md).

## Étapes suivantes

Après avoir testé la destination et confirmé qu’elle est correctement configurée, utilisez l’[API de publication de destination](../../publishing-api/create-publishing-request.md) pour envoyer votre configuration à Adobe pour révision.
