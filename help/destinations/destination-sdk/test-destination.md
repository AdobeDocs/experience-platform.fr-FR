---
description: Dans le cadre de la Destination SDK, Adobe fournit des outils de développement pour vous aider à configurer et tester votre destination. Cette page décrit comment tester votre configuration de destination.
title: Tester la configuration de votre destination
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 3%

---

# Tester la configuration de votre destination {#developer-tools}

## Présentation {#overview}

Dans le cadre de la Destination SDK, Adobe fournit des outils de développement pour vous aider à configurer et tester votre destination. Cette page décrit comment tester votre configuration de destination. Pour plus d’informations sur la création d’un modèle de transformation de message, reportez-vous à la section [Créer et tester un modèle de transformation de message](./create-template.md).

À **tester si votre destination est configurée correctement et vérifier l’intégrité des flux de données vers votre destination configurée ;**, utilisez le *Outil de test de destination*. Grâce à cet outil, vous pouvez tester la configuration de votre destination en envoyant des messages à votre point de terminaison API REST.

Illustré ci-dessous, le test de votre destination s’insère dans la variable [workflow de configuration des destinations](./configure-destination-instructions.md) en Destination SDK :

![Graphique indiquant où l’étape de test de destination correspond au workflow de configuration de destination](./assets/test-destination-step.png)

## Outil de test de destination - Objectif et conditions préalables {#destination-testing-tool}

Utilisez l’outil de test de destination pour tester la configuration de votre destination en envoyant des messages au point de terminaison du partenaire que vous avez fourni dans la variable [configuration du serveur](./server-and-template-configuration.md).

Avant d’utiliser l’outil, veillez à :
* Configurez votre destination en suivant les étapes décrites dans la section [workflow de configuration des destinations](./configure-destination-instructions.md) et
* établir une connexion à votre destination, comme indiqué dans la section [Comment obtenir l’ID d’instance de destination](./destination-testing-api.md#get-destination-instance-id).

Avec cet outil, après avoir configuré votre destination, vous pouvez :
* Testez si votre destination est correctement configurée ;
* Vérifiez l’intégrité des flux de données vers la destination configurée.

### Utilisation {#how-to-use}

>[!NOTE]
>
>Pour consulter la documentation de référence complète sur l’API, reportez-vous à la section [Opérations de l’API de test de destination](./destination-testing-api.md).

Vous pouvez effectuer des appels vers le point de terminaison de l’API de test de destination avec ou sans ajouter de profils sur la requête.

Si vous n’ajoutez aucun profil dans la requête, Adobe les génère en interne et les ajoute à la requête. Si vous souhaitez générer des profils à utiliser dans cette requête, reportez-vous à la section [Exemple de référence d’API de génération de profil](./sample-profile-generation-api.md). Vous devez générer des profils en fonction du schéma XDM source, comme indiqué dans la section [Référence d’API](./sample-profile-generation-api.md#generate-sample-profiles-source-schema). Notez que le schéma source est le [schéma d’union](https://experienceleague.adobe.com/docs/experience-platform/profile/union-schemas/union-schema.html?lang=en) de l’environnement de test que vous utilisez.

La réponse contient le résultat du traitement de la requête de destination. La demande comprend trois sections principales :
* La requête générée par Adobe pour la destination.
* Réponse reçue de votre destination.
* La liste des profils envoyés dans la requête, si les profils étaient [ajouté par vous dans la requête ;](./destination-testing-api.md/#test-with-added-profiles), ou générés par l’Adobe si [le corps de la requête de test de destination était vide.](./destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>Adobe peut générer plusieurs paires de requête et de réponse. Par exemple, si vous envoyez 10 profils à une destination qui comporte une `maxUsersPerRequest` valeur de 7, il y aura une requête avec 7 profils et une autre requête avec 3 profils.

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

Notez que le contenu de la variable `results.httpCalls` est spécifique à votre API REST.

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

Pour des descriptions des paramètres de requête et de réponse, reportez-vous à la section [Opérations de l’API de test de destination](./destination-testing-api.md).

## Étapes suivantes

Après avoir testé votre destination et confirmé qu’elle est correctement configurée, utilisez la variable [API de publication de destination](./destination-publish-api.md) pour envoyer votre configuration à Adobe en vue de la révision.
