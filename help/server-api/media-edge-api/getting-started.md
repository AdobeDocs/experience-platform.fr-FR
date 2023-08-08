---
solution: Experience Platform
title: Prise en main des API Media Edge
description: Prise en main des API Media Edge
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 100%

---


# Prise en main de l’API Media Edge

Ce guide vous aide à démarrer avec le service d’API Media Edge. Apprenez à lancer une session multimédia et à suivre les événements envoyés à une solution Adobe Experience Platform telle que Customer Journey Analytics (CJA). Le service d’API Media Edge est lancé à l’aide du point d’entrée « Session Start ». Une fois la session lancée, un ou plusieurs des événements suivants peuvent faire l’objet d’un suivi :

* `play`
* `ping`
* `bitrateChange`
* `bufferStart`
* `pauseStart`
* `adBreakStart`
* `adStart`
* `adComplete`
* `adSkip`
* `adBreakComplete`
* `chapterStart`
* `chapterComplete`
* `chapterSkip`
* `error`
* `sessionEnd`
* `sessionComplete`
* `statesUpdate`

Chaque événement possède son propre point d’entrée. Tous les points d’entrée de l’API Media Edge sont des méthodes POST, avec des corps de requête JSON pour les données d’événement. Pour plus d’informations sur les points d’entrée de l’API Media Edge, les paramètres, et des exemples, consultez le [fichier Swagger Media Edge](swagger.md).

Ce guide décrit comment effectuer le suivi des événements suivants après le démarrage de la session :

* [Début de la mémoire tampon](#buffer-start-event-request)
* [Play](#play-event-request)
* [Fin de la session](#session-complete-event-request)

## Mise en œuvre de l’API {#implement-api}

Mis à part quelques différences mineures dans le modèle et les chemins appelés, l’API Media Edge partage l’implémentation de l’[API Media Collection](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=fr). Les détails de mise en oeuvre de l’API Media Collection restent valides pour l’API Media Edge, comme décrit dans la documentation suivante :

* [Définition du type de requête HTTP dans votre lecteur](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=fr)
* [Envoi d’événements ping](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=fr)
* [Conditions d’expiration](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-timeout.html?lang=fr)
* [Contrôle de l’ordre des événements](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-ctrl-order.html?lang=fr)

## Autorisation {#authorization}

Actuellement, les API Media Edge ne nécessitent pas d’en-têtes d’autorisation dans leurs requêtes.


## Démarrer la session {#start-session}

Pour démarrer la session multimédia sur le serveur, utilisez le point d’entrée « Session Start ». Une réponse réussie inclut `sessionId`, qui est un paramètre obligatoire pour les requêtes d’événement ultérieures.

Avant d’effectuer la requête de démarrage de session, vous devez disposer des éléments suivants :

* `datastreamId` est un paramètre obligatoire pour la requête POST de démarrage de session. Pour récupérer un paramètre `datastreamId`, consultez la section [Configurer un flux de données](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=fr).

* Objet JSON pour la payload de la requête contenant les données minimales requises (comme illustré dans l’exemple de requête ci-dessous).

Une fois que vous disposez de ces informations, indiquez le paramètre `datastreamId` dans l’appel suivant :

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionStart?configId={datastream ID} \`

### Exemple de requête

L’exemple suivant illustre une requête cURL de démarrage de session :

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

Dans l’exemple de requête ci-dessus, la valeur `eventType` contient le préfixe `media.` selon le [Modèle de données d’expérience (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr) pour spécifier les domaines.

En outre, le mappage des types de données pour `eventType` dans l’exemple ci-dessus sont les suivants :

| eventType | datatypes |
| -------- | ------ |
| media.SessionStart | [sessionDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/sessiondetails.schema.md) |
| media.chapterStart | [chapterDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/chapterdetails.schema.md) |
| media.adBreakStart | [advertisingPodDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingpoddetails.schema.md) |
| media.adStart | [advertisingDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingdetails.schema.md) |
| media.error | [errorDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/errordetails.schema.md) |
| media.statesUpdate | [statesStart](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesstart): Array[playerStateData], [statesEnd](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesend): Array[playerStateData] |
| media.sessionStart, media.chapterStart, media.adStart | [customMetadata](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmcustommetadata) |
| all | [qoeDataDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/qoedatadetails.schema.md) |

### Exemple de réponse

L’exemple suivant illustre une réponse réussie pour la requête de démarrage de session :

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

Dans l’exemple de réponse ci-dessus, le paramètre `sessionId` s’affiche comme `af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333`. Vous utiliserez cet identifiant dans les requêtes d’événement ultérieures en tant que paramètre obligatoire.

Pour plus d’informations sur les paramètres de point d’entrée « Session Start » et des exemples, consultez le fichier [Swagger Media Edge](swagger.md).

Pour plus d’informations sur les paramètres de données multimédia XDM, consultez la section [Schéma d’informations sur les détails de média](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmplayhead).


## Requête d’événement de début de la mémoire tampon {#buffer-start}

L’événement Début de la mémoire tampon signale le démarrage de la mise en mémoire tampon sur le lecteur multimédia. La reprise de la mémoire tampon n’est pas un événement du service d’API, mais intervient lorsqu’un événement de lecture est envoyé après le début de la mémoire tampon. Pour effectuer une requête d’événement de début de mémoire tampon, insérez `sessionId` dans la payload d’un appel au point d&#39;entrée suivant :

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart \`

### Exemple de requête

L’exemple suivant illustre une requête cURL de début de mémoire tampon :

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

Dans l’exemple de requête ci-dessus, le même paramètre `sessionId` que celui renvoyé dans l’appel précédent est utilisé en tant que paramètre obligatoire dans la requête de début de mémoire tampon.

La réponse réussie indique un statut 200 et n’inclut aucun contenu.

Pour plus d’informations sur les paramètres du point d’entrée de début de mémoire tampon et des exemples, consultez le fichier [Swagger Media Edge](swagger.md).


## Requête d’événement de lecture {#play-event}

L’événement de lecture est envoyé lorsque le lecteur multimédia passe d’un statut tel que « mise en mémoire tampon », « mise en pause » ou « erreur » au statut « lecture ». Pour effectuer une requête d’événement de lecture, insérez `sessionId` dans la payload d’un appel au point d’entrée suivant :

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/play \`

### Exemple de requête

L’exemple suivant illustre une requête cURL de lecture :

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

La réponse réussie indique un statut 200 et n’inclut aucun contenu.

Pour plus d’informations sur les paramètres de point d’entrée de lecture et des exemples, consultez le fichier [Swagger Media Edge](swagger.md).

## Requête d’événement de fin de session {#session-complete}

L’événement « Fin de session » est envoyé lorsque la fin du contenu principal est atteinte. Pour effectuer une requête d’événement de fin de session, insérez `sessionId` dans la payload d’un appel au point d’entrée suivant :

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete \`

### Exemple de requête

L’exemple suivant illustre une requête cURL de fin de session :

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

La réponse réussie indique un statut 200 et n’inclut aucun contenu.

Pour plus d’informations sur les paramètres de point d’entrée de fin de session et des exemples, consultez le fichier [Swagger Media Edge](swagger.md).

## Codes de réponse

Le tableau suivant affiche les codes de réponse possibles suite aux requêtes de l’API Media Edge :

| État | Description |
| ---------- | --------- |
| 200 | La session a été créée. |
| 207 | L’un des services qui se connectent à Experience Edge Network rencontre un problème (pour plus d’informations, consultez le [guide de dépannage](troubleshooting.md)) |
| 400-level | Requête incorrecte |
| 500-level | Erreur du serveur |

## Plus d’informations sur cette fonctionnalité

* [Guide de dépannage de Media Edge](troubleshooting.md)
* [Vue d’ensemble de l’API Media Edge](overview.md)


