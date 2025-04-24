---
title: Identification des visiteurs avec FPID
description: Découvrez comment identifier de manière cohérente les visiteurs via l’API Edge Network à l’aide du FPID
seo-description: Learn how to consistently identify visitors via the Edge Network API, by using the FPID
keywords: edge network;passerelle;api;visiteur;identification;fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 95%

---

# Identification des visiteurs avec FPID

Les [!DNL First-party IDs] (`FPIDs`) sont des identifiants d’appareil générés, gérés et stockés par les clients. Cela permet aux clients de contrôler l’identification des appareils utilisateur. En envoyant les `FPIDs`, Edge Network ne génère pas de tout nouveau `ECID` pour une requête qui n’en contient pas.

Le `FPID` peut être inclus dans le corps de la requête API dans le cadre du `identityMap` ou peut être envoyé sous la forme d’un cookie.

Un `FPID` peut être traduit de manière déterministe en `ECID` par Edge Network de sorte que les identités `FPID` soient entièrement compatibles avec les solutions Experience Cloud. L’obtention d’un `ECID` à partir d’un `FPID` spécifique produit toujours le même résultat, de sorte que les utilisateurs bénéficient d’une expérience cohérente.

Le `ECID` obtenu de cette manière peut être récupéré à travers une requête `identity.fetch` :

```json
{
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      }
   }
}
```

Pour les requêtes qui contiennent à la fois un `FPID` et un `ECID`, le `ECID` déjà présent dans la requête est prioritaire par rapport à celui qui peut être généré à partir du `FPID`. En d’autres termes, Edge Network utilise le `ECID` déjà fourni et ignore le `FPID`. Un nouveau `ECID` n’est généré que lorsqu’un `FPID` est fourni seul.

En termes d’identifiants d’appareil, les flux de données du `server` doivent utiliser le `FPID` comme identifiant de l’appareil. Les autres identités (c’est-à-dire `EMAIL`) peuvent également être fournies dans le corps de la requête, mais Edge Network exige qu’une identité principale soit explicitement fournie. L’identité principale est l’identité de base dans laquelle les données de profil seront stockées.

>[!NOTE]
>
>Les requêtes qui n’ont pas d’identité, respectivement aucune identité principale explicitement définie dans le corps de la requête, échoueront.

Le groupe de champs du `identityMap` suivant est correctement formé pour une requête des flux de données du `server` :

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous",
            "primary":true
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

Le groupe de champs du `identityMap` suivant entraîne une réponse d’erreur lorsqu’il est défini sur une requête de flux de données du `server` :

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous"
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

Dans ce cas, la réponse d’erreur renvoyée par Edge Network est similaire à ce qui suit :

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0306-400",
   "status":400,
   "title":"No primary identity set in request (event)",
   "detail":"No primary identity found in the input event. Update the request accordingly to your schema and try again.",
   "report":{
      "requestId":"{REQUEST_ID}",
      "configId":"{CONFIG_ID}",
      "orgId":"{ORG_ID}"
   }
}
```

## Identification des visiteurs avec `FPID`

Pour identifier des utilisateurs à l’aide du `FPID`, assurez-vous que le cookie du `FPID` a été envoyé avant d’envoyer toute requête à Edge Network. Le `FPID` peut être transmis dans un cookie ou dans le `identityMap` du corps de la requête.

<!--

## Request with `FPID` passed as cookie header

```shell
curl -X POST 'https://edge.adobedc.net/v2/interact?dataStreamId={Data Stream ID}' \
-H 'cookie: FPID=e98f38e6-6183-442d-8cd2-0e384f4c8aa8' \
-H 'Content-Type: application/json' \
-d '{
    "event": 
        {
            "xdm": {
                "web": {
                    "webPageDetails": {
                        "URL": "https://alloystore.dev"
                    },
                    "webReferrer": {
                        "URL": ""
                    }
                },
                "device": {
                    "screenHeight": 1440,
                    "screenWidth": 3440,
                    "screenOrientation": "landscape"
                },
                "environment": {
                    "type": "browser",
                    "browserDetails": {
                        "viewportWidth": 1907,
                        "viewportHeight": 545
                    }
                },
                "placeContext": {
                    "localTime": "2022-03-21T21:32:59.991-06:00",
                    "localTimezoneOffset": 360
                },
                "timestamp": "2022-03-22T03:32:59.992Z",
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "1.0",
                    "environment": "serverapi"
                }
            }
        },
    "query": {
        "identity": {
            "fetch": [
                "ECID"
            ]
        }
    },
    "meta":
        {
            "state":
            {
                "domain": "alloystore.dev",
                "cookiesEnabled": true
            }
        }
}'
```
-->

## Requête avec le `FPID` transmis sous forme de champ `identityMap`.

L’exemple ci-dessous transmet le [!DNL FPID] sous forme de paramètre du `identityMap`.

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "FPID": [
               {
                  "id": "e98f38e6-6183-442d-8cd2-0e384f4c8aa8",
                  "authenticatedState": "ambiguous",
                  "primary": true
               }
            ]
         },
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev"
            },
            "webReferrer": {
               "URL": ""
            }
         },
         "device": {
            "screenHeight": 1440,
            "screenWidth": 3440,
            "screenOrientation": "landscape"
         },
         "environment": {
            "type": "browser",
            "browserDetails": {
               "viewportWidth": 1907,
               "viewportHeight": 545
            }
         },
         "placeContext": {
            "localTime": "2022-03-21T21:32:59.991-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-22T03:32:59.992Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "1.0",
            "environment": "serverapi"
         }
      }
   },
   "query": {
      "identity": {
         "fetch": [
            "ECID"
         ]
      }
   }
}'
```
