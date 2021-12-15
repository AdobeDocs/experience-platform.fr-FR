---
description: Cette page fournit toutes les informations dont vous avez besoin pour soumettre une révision pour une destination créée à l’aide de Destination SDK.
title: Envoyer pour révision d’une destination créée dans Destination SDK
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: 468b9309c5184684c0b25c2656a9eef37715af53
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# Envoyer pour révision d’une destination créée dans Destination SDK

## Présentation {#overview}

Avant que votre destination ne puisse être publiée dans la variable [Catalogue des destinations Experience Platform](/help/destinations/catalog/overview.md), vous devez fournir à l’Adobe certaines informations sur la destination et les tests que vous avez effectués, afin de vous assurer que les utilisateurs bénéficient de la meilleure expérience possible lors de l’activation des données vers votre plateforme.

Cette page répertorie toutes les informations que vous devez fournir lors de l’envoi ou de la mise à jour d’une destination que vous avez créée à l’aide de Adobe Experience Platform Destination SDK. Pour envoyer une destination dans Adobe Experience Platform, envoyez un courrier électronique à <aepdestsdk@adobe.com> qui inclut :

* Description des cas d’utilisation résolus par votre destination. Cela n’est pas nécessaire si vous mettez à jour une configuration de destination existante.
* Testez les résultats après avoir utilisé le point d’entrée de l’API de destination de test pour effectuer un appel HTTP vers votre destination. Partagez avec l’Adobe :
   * Appel API effectué sur votre point de terminaison de destination.
   * Réponse de l’API reçue de votre point de terminaison de destination.
* Preuve que vous avez envoyé une requête de publication de destination pour votre destination à l’aide de la variable [API de publication de destination](./destination-publish-api.md).
* (Pour les intégrations productives uniquement) une documentation PR (requête de tirage), suivant les instructions décrites dans la section [processus de documentation en libre-service](./docs-framework/documentation-instructions.md).
* Un fichier image qui s’affichera sous forme de logo pour votre carte de destination dans le catalogue des destinations Experience Platform.

Vous trouverez des informations détaillées sur chaque élément dans les sections ci-dessous :

## Description du cas d’utilisation

Fournissez une description des cas d’utilisation que votre destination résout pour les clients Experience Platform. Vos descriptions peuvent être similaires aux cas d’utilisation des partenaires existants :

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): Créez des audiences à partir des listes de clients, des personnes qui ont visité votre site ou des personnes qui ont déjà interagi avec votre contenu sur Pinterest.
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases): Les API DataX sont disponibles pour les annonceurs qui souhaitent cibler un groupe d’audience spécifique en dehors des adresses électroniques dans Verizon Media (VMG). Elles peuvent rapidement créer un nouveau segment et pousser le groupe d’audience souhaité à l’aide de l’API en temps quasi réel de VMG.

## Résultats du test après l’utilisation de l’API de destination du test

Fournir des résultats de test après avoir utilisé la méthode [API de destination du test](./test-destination.md) point de terminaison pour effectuer un appel HTTP vers votre destination. Cela inclut :
* La requête API complète (en-têtes et corps) effectuée sur votre point de terminaison de destination, à l’aide de l’API de test.
* Réponse de l’API reçue de votre point de terminaison de destination.

Par exemple, votre requête et votre réponse peuvent ressembler aux exemples ci-dessous :

**Requête**

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

**Réponse**

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

## Preuve que vous avez envoyé une demande de publication de destination

Après avoir testé votre destination, vous devez utiliser la variable [API de publication de destination](./destination-publish-api.md) pour envoyer la destination à l’Adobe pour révision et publication.

Indiquez l’identifiant de la requête de publication pour votre destination. Pour plus d’informations sur la manière de récupérer l’ID de requête de publication, consultez [Liste des requêtes de publication de destination](./destination-publish-api.md#retrieve-list).

## Documentation de destination PR (requête de tirage) pour les intégrations productives

Si vous êtes un fournisseur de logiciels indépendant (ISV) ou un intégrateur de système (SI), créez une [intégration productive](./overview.md#productized-custom-integrations), utilisez le [processus de documentation en libre-service](./docs-framework/documentation-instructions.md) pour créer une page de documentation du produit pour votre destination. Dans le cadre du processus d’envoi, fournissez la demande d’extraction (PR) pour votre documentation de destination.

## Logo de votre destination

Le catalogue des destinations comprend un logo pour chaque carte de destination. Dans le courrier électronique d’envoi, incluez une image avec le logo pour votre destination.

Les exigences d’image sont les suivantes :
* **Format**: `SVG`
* **Taille**: moins de 2 Mo

## Télécharger un exemple d’email

[Télécharger](./assets/sample-email-submit-destination.rtf) un exemple d’email contenant toutes les informations que vous devez fournir à Adobe.
