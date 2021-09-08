---
description: Dans le cadre du SDK de destination, Adobe fournit des outils de développement pour vous aider à configurer et à tester votre destination. Cette page décrit comment tester votre configuration de destination.
title: Test de votre configuration de destination
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: 3d7151645bc90a2dcbd6b31251ed459029ab77c9
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 1%

---

# Test de votre configuration de destination {#developer-tools}

## Présentation {#overview}

Dans le cadre du SDK de destination, Adobe fournit des outils de développement pour vous aider à configurer et à tester votre destination. Cette page décrit comment tester votre configuration de destination. Pour plus d’informations sur la création d’un modèle de transformation de message, consultez la section [Créer et tester un modèle de transformation de message](./create-template.md).

Pour **tester si votre destination est configurée correctement et pour vérifier l’intégrité des flux de données vers votre destination configurée**, utilisez l’*outil de test de destination*. Grâce à cet outil, vous pouvez tester la configuration de votre destination en envoyant des messages à votre point de terminaison API REST.

Vous trouverez ci-dessous la manière dont le test de votre destination s’insère dans le [workflow de configuration de destination](./configure-destination-instructions.md) du SDK de destination :

![Graphique indiquant où l’étape de test de destination correspond au workflow de configuration de destination](./assets/test-destination-step.png)

## Outil de test de destination {#destination-testing-tool}

Utilisez cet outil pour tester la configuration de votre destination en envoyant des messages au point de terminaison du partenaire que vous avez fourni dans la [configuration du serveur](./server-and-template-configuration.md).

Avec cet outil, après avoir configuré votre destination, vous pouvez :
* Testez si votre destination est correctement configurée ;
* Vérifiez l’intégrité des flux de données vers la destination configurée.

### Mode d’emploi {#how-to-use}

>[!NOTE]
>
>Pour consulter la documentation de référence complète sur l’API, voir [Opérations de l’API de test de destination](./destination-testing-api.md).

Vous pouvez effectuer des appels vers le point de terminaison de l’API de test de destination avec ou sans ajouter de profils sur la requête.

Si vous n’ajoutez aucun profil dans la requête, Adobe les génère en interne et les ajoute à la requête. Si vous souhaitez générer des profils à utiliser dans cette requête, reportez-vous à la [Référence de l’API de génération d’exemples de profils](./sample-profile-generation-api.md). Vous devez générer des profils en fonction du schéma XDM source, comme indiqué dans la [référence API](./sample-profile-generation-api.md#generate-sample-profiles-source-schema). Notez que le schéma source est le [schéma d’union](https://experienceleague.adobe.com/docs/experience-platform/profile/union-schemas/union-schema.html?lang=en) de l’environnement de test que vous utilisez.

La réponse contient le résultat du traitement de la requête de destination. La demande comprend trois sections principales :
* La requête générée par Adobe pour la destination.
* Réponse reçue de votre destination.
* La liste des profils envoyés dans la requête, que les profils aient été [ajoutés par vous dans la requête](./destination-testing-api.md/#test-with-added-profiles) ou générés par Adobe si [le corps de la requête de test de destination était vide](./destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>Adobe peut générer plusieurs paires de requête et de réponse. Par exemple, si vous envoyez 10 profils vers une destination ayant une valeur `maxUsersPerRequest` de 7, il y aura une requête avec 7 profils et une autre requête avec 3 profils.

**Exemple de requête avec paramètre de profil dans le corps**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
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
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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

Pour obtenir des descriptions des paramètres de requête et de réponse, voir [Opérations de l’API de test de destination](./destination-testing-api.md).

## Étapes suivantes

Après avoir testé votre destination et confirmé qu’elle est correctement configurée, utilisez l’[API de publication de destination](./destination-publish-api.md) pour envoyer votre configuration à Adobe pour révision.
