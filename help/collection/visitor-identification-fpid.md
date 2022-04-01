---
title: Identification des visiteurs via FPID
description: Découvrez comment identifier de manière cohérente les visiteurs via l’API serveur, à l’aide du FPID
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: réseau Edge;passerelle;api;visiteur;identification;fpid
source-git-commit: eaeab8fe96a9af399f8288b62b6ca9f31d949cfa
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# Identification des visiteurs via FPID

## Présentation

[!DNL First-party IDs] (`FPIDs`) sont des identifiants d’appareil générés, gérés et stockés par les clients. Cela permet aux clients de contrôler l’identification des appareils utilisateur. Par envoi `FPIDs`, le réseau Edge ne génère pas de toute nouvelle `ECID` pour une requête qui n’en contient pas.

Le `FPID` peut être inclus dans le corps de la requête API dans le cadre de la fonction `identityMap` ou peut être envoyé sous la forme d’un cookie.

Un `FPID` peut être traduit de manière déterministe en `ECID` par le réseau Edge, `FPID` Les identités sont entièrement compatibles avec les solutions Experience Cloud. Obtention d’une `ECID` à partir d’une `FPID` produit toujours le même résultat, de sorte que les utilisateurs disposent d’une expérience cohérente.

Le `ECID` obtenu de cette manière peut être récupéré via un `identity.fetch` query :

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

Pour les requêtes qui contiennent à la fois une `FPID` et un `ECID`, la variable `ECID` déjà présent dans la requête est prioritaire par rapport à celui qui peut être généré à partir de `FPID`. Par conséquent, le réseau Edge utilise la variable `ECID` déjà fourni et ne le calculera pas à partir de `FPID`.

En termes d’identifiants d’appareil, la variable `server` datastreams doit utiliser `FPID` comme identifiant d’appareil. Autres identités (c’est-à-dire `EMAIL`) peut également être fourni dans le corps de la requête, mais le réseau Edge exige qu’une identité Principale soit explicitement fournie. L’identité Principal est l’identité de base dans laquelle les données de profil seront stockées.

>[!NOTE]
>
>Les requêtes qui n’ont pas d’identité, respectivement aucune identité Principale explicitement définie dans le corps de la requête, échoueront.

Les éléments suivants `identityMap` groupe de champs correctement formé pour un `server` requête datastream :

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

Les éléments suivants `identityMap` un groupe de champs entraîne une réponse d’erreur lorsqu’il est défini sur une `server` requête datastream :

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

La réponse d’erreur renvoyée par le réseau Edge dans ce cas est similaire à ce qui suit :

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

Pour identifier des utilisateurs via `FPID`, assurez-vous que la variable `FPID` a été envoyé avant toute demande au réseau Edge. Le `FPID` peut être transmis dans un cookie ou dans le cadre du `identityMap` dans le corps de la requête.

<!--

## Request with `FPID` passed as cookie header

```shell
curl -X POST 'https://edge.adobedc.net/ee/v2/interact?dataStreamId={Data Stream ID}' \
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

## Demander avec `FPID` transmis comme `identityMap` field

L’exemple ci-dessous transmet la variable [!DNL FPID] as a `identityMap` .

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {IMS_ORG_ID}"
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
