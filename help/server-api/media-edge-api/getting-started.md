---
keywords: Experience Platform;bannière multimédia;rubriques les plus consultées;période
solution: Experience Platform
title: Prise en main des API Media Edge
description: Prise en main des API Media Edge
exl-id: null
source-git-commit: 696ddd93d87601f9f6dedfd651ee12573dc4990a
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 7%

---


# Prise en main de l’API Media Edge

Ce guide fournit des instructions pour établir des interactions initiales réussies avec le service d’API Media Edge. Cela inclut le démarrage d’une session multimédia, puis le suivi des événements envoyés à une solution Adobe Experience Platform (AEP) telle que Customer Journey Analytics (CJA). Le service d’API Media Edge est lancé avec le point de terminaison Démarrage de session. Une fois la session lancée, un ou plusieurs des événements suivants peuvent être suivis :

* play
* ping
* bitrateChange
* bufferStart
* pauseStart
* adBreakStart
* adStart
* adComplete
* adSkip
* adBreakComplete
* chapterStart
* chapterComplete
* chapterSkip
* error
* sessionEnd
* sessionComplete
* statesUpdate

Chaque événement possède son propre point de terminaison. Tous les points de terminaison de l’API Media Edge sont des méthodes de POST, avec des corps de requête JSON pour les données d’événement. Pour plus d’informations sur les points de terminaison, les paramètres et les exemples de l’API Media Edge, consultez le fichier Media Edge Swagger.

Ce guide explique comment effectuer le suivi des événements suivants après le démarrage de la session :

* Début de la mémoire tampon
* Play
* Fin de la session

## Mise en œuvre de l’API

Outre les différences mineures dans le modèle et les chemins appelés, l’API Media Edge est identique à l’API Media Collection. Les détails de mise en oeuvre de Media Collection restent valides pour l’API Media Edge, comme décrit dans la documentation suivante :

* [Définition du type de requête HTTP dans votre lecteur](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [Envoi d’événements ping](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [Conditions d’expiration](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-timeout.html?lang=en)
* [Contrôle de l’ordre des événements](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-ctrl-order.html?lang=en)

## Authorization

Actuellement, les API Media Edge ne nécessitent pas d’en-têtes d’autorisation dans leurs requêtes.


## Démarrage de la session

Pour démarrer la session multimédia sur le serveur, utilisez le point de terminaison Démarrage de session . Une réponse réussie inclut une `sessionId`, qui est un paramètre obligatoire pour les requêtes d’événement suivantes.

Avant d’effectuer la requête de démarrage de session, vous aurez besoin des éléments suivants :

* Le `datastreamId` est un paramètre obligatoire pour la requête Démarrage de session du POST. Pour récupérer une `datastreamId`, voir [Configuration d’un flux de données](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=fr).

* Objet JSON pour le payload de la requête contenant les données minimales requises (comme illustré dans l’exemple de requête ci-dessous).

Une fois que vous disposez de ces informations, fournissez la variable `datastreamId` dans l’appel suivant :

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionStart?configId={datastream ID} \`

### Exemple de requête

L’exemple suivant illustre une requête cURL de démarrage de session :

```
curl -i --request POST '{uri}/ee/va/v1/sessionStart?configId={dataStreamId}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Media Analytics API Sample",
            "playerName": "sample-html5-api-player",
            "contentType": "VOD",
            "length": 60,
            "channel": "sample-channel",
            "appVersion": "va-api-1.0.0"
          },
          "playhead": 0
        }
      }
    }
  ]
}'
```

Dans l’exemple de requête ci-dessus, la variable `eventType` contient le préfixe `media` selon la variable [Modèle de données d’expérience (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr) pour la spécification de domaines.

En outre, le mappage des types de données pour `eventType` dans l’exemple ci-dessus, les éléments suivants sont proposés :

| eventType | datatypes |
| -------- | ------ |
| mediaSessionStart | [sessionDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/sessiondetails.schema.md) |
| media.chapterStart | [chapterDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/chapterdetails.schema.md) |
| media.adBreakStart | [advertisingPodDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingpoddetails.schema.md) |
| media.adStart | [advertisingDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingdetails.schema.md) |
| media.error | [errorDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/errordetails.schema.md) |
| media.statesUpdate | [statesStart](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesstart): Tableau[playerStateData], [statesEnd](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesend): Tableau[playerStateData] |
| media.sessionStart, media.chapterStart, media.adStart | [customMetadata](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmcustommetadata) |
| tous | [qoeDataDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/qoedatadetails.schema.md) |

### Exemple de réponse

L’exemple suivant illustre une réponse réussie pour la requête de démarrage de session :

```
HTTP/2 200
x-request-id: 99603f5c-95cf-49ad-9afb-0ba6c5867fd7
x-rate-limit-remaining: 599
vary: Origin
date: Tue, 07 Mar 2023 14:37:58 GMT
x-konductor: 23.3.2:367bc7dc
x-adobe-edge: IRL1;6
server: jag
content-type: application/json;charset=utf-8
strict-transport-security: max-age=31536000; includeSubDomains
cache-control: no-cache, no-store, max-age=0, no-transform
x-xss-protection: 1; mode=block
x-content-type-options: nosniff

{
    "requestId": "df14bca1-ba0f-4574-ae80-a4e24a960c00",
    "handle": [
        {
            "payload": [
                {
                    "sessionId": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333"
                }
            ],
            "type": "media-analytics:new-session",
            "eventIndex": 0
        },
        {
            "payload": [
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_cluster",
                    "value": "irl1",
                    "maxAge": 1800
                },
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_identity",
                    "value": "CiY1MTkxMDM4OTc1MzkwMTY4NTQ1NjAxNDg4OTgzODU5MTAzMDcyMVIPCKKt8KnsMBgBKgRJUkwx8AGirfCp7DA=",
                    "maxAge": 34128000
                }
            ],
            "type": "state:store"
        }
    ]
}
```

Dans l’exemple de réponse ci-dessus, la variable `sessionId` s’affiche comme `af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333`. Vous utiliserez cet identifiant dans les demandes d’événement suivantes comme paramètre obligatoire.

Pour plus d’informations sur les paramètres de point de fin de début de session et des exemples, consultez le fichier Media Edge Swagger.

Pour plus d’informations sur les paramètres de données multimédia XDM, voir [Schéma d’informations sur les détails du média](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmplayhead).


## Requête d’événement de début de la mémoire tampon

L’événement Début de la mémoire tampon signale le démarrage de la mise en mémoire tampon sur le lecteur multimédia. La reprise de la mémoire tampon n’est pas un événement du service d’API ; au lieu de cela, il est déduit lorsqu’un événement play est envoyé après le début de la mémoire tampon. Pour effectuer une requête d’événement Buffer Start, utilisez `sessionId` dans la charge utile d’un appel au point de terminaison suivant :

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart \`

### Exemple de requête

L’exemple suivant illustre une requête cURL de début de la mémoire tampon :

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

Dans l’exemple de requête ci-dessus, la même `sessionId` qui est renvoyé dans l’appel précédent est utilisé comme paramètre requis dans la requête de début de la mémoire tampon.

Pour plus d’informations sur les paramètres du point de terminaison de début de la mémoire tampon et des exemples, consultez le fichier Media Edge Swagger.

La réponse réussie indique un état de 200 et n’inclut aucun contenu.

## Lire la requête d’événement

L’événement Play est envoyé lorsque le lecteur multimédia passe à l’état &quot;lecture&quot; à partir d’un autre état, tel que &quot;mise en mémoire tampon&quot;, &quot;mise en pause&quot; ou &quot;erreur&quot;. Pour effectuer une requête d’événement Play, utilisez `sessionId` dans la charge utile d’un appel au point de terminaison suivant :

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/play \`

### Exemple de requête

L’exemple suivant illustre une requête Play cURL :

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/play' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

La réponse réussie indique un état de 200 et n’inclut aucun contenu.

Pour plus d’informations sur les paramètres de point de terminaison de lecture et des exemples, consultez le fichier Media Edge Swagger.

## Demande d’événement de fin de session

L’événement Session Complete est envoyé lorsque la fin du contenu principal est atteinte. Pour effectuer une requête d’événement Session Complete , utilisez `sessionId` dans la charge utile d’un appel au point de terminaison suivant :

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete \`

### Exemple de requête

L’exemple suivant illustre une requête cURL de fin de session :

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

La réponse réussie indique un état de 200 et n’inclut aucun contenu.

## Codes de réponse

Le tableau suivant affiche les codes de réponse possibles résultant des demandes de l’API Media Edge :

| État | Description |
| ---------- | --------- |
| 200 | La session a été créée |
| 207 | Problème avec l’un des services qui se connectent à Experience Edge Network (voir plus dans le guide de dépannage) |
| 400-level | Requête incorrecte |
| 500-level | Erreur du serveur |

Pour plus d’informations sur la gestion des erreurs et des codes de réponse manquants, consultez le guide de dépannage de Media Edge .


