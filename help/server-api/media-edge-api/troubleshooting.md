---
keywords: Experience Platform;bannière multimédia;rubriques les plus consultées;période
solution: Experience Platform
title: Prise en main des API Media Edge
description: Guide de dépannage des API Media Edge
source-git-commit: b4687fa7f1a2eb8f206ad41eae0af759b0801b83
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 1%

---


# Guide de dépannage de l’API Media Edge

Ce guide fournit des instructions de dépannage pour gérer les erreurs et obtenir des réponses réussies.

## Utilisation des aides de réponse aux erreurs

Pour aider à résoudre les problèmes de réponses infructueuses, les erreurs sont accompagnées d’un corps de réponse contenant un objet d’erreur. Dans ce cas, le corps de la réponse contient les détails du problème, tels que définis par [RFC 7807 - Détails du problème pour les API HTTP](https://datatracker.ietf.org/doc/html/rfc7807). Pour améliorer l’expérience utilisateur de l’API, les détails du problème sont descriptifs (les détails des clés du tableau sont affichés à l’aide de JsonPath sur le champ manquant ou non valide). Ils sont également cumulatifs (tous les champs non valides seront signalés dans la même requête).


## Validation des démarrages de session

La plupart des problèmes de création de requêtes de démarrage de session entraînent une réponse à plusieurs états 207.
La payload est similaire aux erreurs non fatales de l’API du serveur réseau Experience Edge. Toutes les erreurs Media Analytics sont du type suivant :  `https://ns.adobe.com/aep/errors/va-edge-0XXX-XXX`. Les nombres affichés dans la réponse correspondent à l’état d’erreur.

L’exemple suivant illustre un corps de réponse pour une requête de début de session qui ne comporte pas de champ obligatoire et dont le champ n’est pas valide.

```
{
    "requestId": "d4be4f91-a535-41e7-80c6-bdd031d3a365",
    "handle": [
        ...
    ],
    "errors": [
        {
            "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
            "status": 400,
            "title": "Invalid request",
            "report": {
                "eventIndex": 0,
                "details": [
                    {
                        "name": "$.xdm.mediaCollection.sessionDetails.name",
                        "reason": "Missing required field"
                    },
                    {
                        "name": "$.xdm.timestamp",
                        "reason": "Field should respect ISO 8601 standard for presenting date and time with offset to UTC (e.g. 2022-05-19T19:31:02Z, 2022-05-19T21:31:02+02:00, 2022-05-19T21:31:02.234+02:00)"
                    }
                ]
            }
        }
    ]
}
```

Dans l’exemple ci-dessus, les deux problèmes sont indiqués par `name` et `reason` under `details`: le premier motif s’affiche. `missing required field` et la seconde décrit la non-conformité à la norme ISO 8601.


>[!NOTE]
>
> Pour les erreurs provoquées en amont à partir de Media Analytics, Adobe vous recommande de continuer à traiter la session multimédia générée.

## Validation des événements

La plupart des requêtes d’événement non valides génèrent une réponse 400 Bad Request. Dans ce cas, la charge utile est similaire aux erreurs fatales de l’API du serveur réseau Experience Edge.

Pour les requêtes d’événement, le service d’API Media Edge inclut des vérifications supplémentaires qui ne sont pas capturées dans le modèle XDM lui-même. Cela inclut une vérification que le chemin d’accès `eventType` correspond à la charge utile de requête. `eventType`.


L’exemple suivant illustre une `eventType` incohérence avec un `adBreakStart` payload envoyée à `ee/va/v1/chapterStart`:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": "The payload eventType adBreakStart was different from the path eventType chapterStart"
    }
}
```

L’exemple suivant illustre une vérification supplémentaire de l’API Media Edge pour trouver un `chapterStart` appel manquant `chapterDetails` info:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": [
            {
                "name": "$.events[0].xdm.mediaCollection.chapterDetails",
                "reason": "Missing required field"
            }
        ]
    }
}
```

## Gestion des erreurs de niveau 400 et 500

Le tableau suivant fournit des instructions pour gérer les erreurs de réponse d’état :


| Code d’erreur | Description |
| ---------- | --------- |
| 4xx Mauvaise requête | La plupart des erreurs 4xx (par exemple, 400, 403, 404) ne doivent pas être relancées par l’utilisateur. Une nouvelle tentative de la requête n’entraîne pas de réponse réussie. L’utilisateur doit corriger l’erreur avant de retenter la requête. Les événements qui résultent en codes d’état 4xx ne sont pas suivis, ce qui peut potentiellement affecter la précision des données dans les sessions qui ont reçu des réponses 4xx. |
| 410 Gone | Indique que la session prévue pour le suivi n’est plus calculée côté serveur. La raison la plus courante est que la session dure plus de 24 heures. Après avoir reçu 410, essayez de démarrer une nouvelle session et de la suivre. |
| 429 Too many requests | Ce code de réponse indique que le serveur limite le débit des requêtes. Suivez la **Retry-After** instructions dans l’en-tête de réponse avec précaution. Toutes les réponses renvoyées doivent comporter le code de réponse HTTP avec un code d’erreur spécifique au domaine. |
| 500 Erreur interne du serveur | Les erreurs 500 sont génériques, des erreurs fourre-tout. Les erreurs 500 ne doivent pas être retentées, à l’exception des erreurs 502, 503 et 504. |
| 502 Bad gateway | Ce code d’erreur Indique que le serveur, lorsqu’il agissait en tant que passerelle, a reçu une réponse non valide des serveurs en amont. Cela peut être dû à des problèmes réseau entre les serveurs. Le problème de réseau temporaire peut se résoudre de manière à ce que la nouvelle tentative de requête puisse résoudre le problème. |
| Service indisponible | Ce code d’erreur indique que le service est temporairement indisponible. Cela peut se produire pendant les périodes de maintenance. Les destinataires avec une erreur 503 peuvent réessayer la requête, mais doivent également suivre le **Retry-After** instructions d’en-tête. |


Événements de mise en file d’attente lorsque les réponses de session sont lentes

Après le démarrage d’une session de suivi multimédia, le lecteur multimédia peut se déclencher avant que la réponse de début de session ne soit renvoyée (avec le paramètre d’ID de session) depuis le serveur principal. Si cela se produit, votre application doit mettre en file d’attente tous les événements de suivi qui arrivent entre la requête Session et sa réponse. Lorsque la réponse sessions arrive, vous devez d’abord traiter les événements placés dans la file d’attente, puis commencer à traiter les événements en direct.

Pour de meilleurs résultats, consultez le lecteur de référence dans votre distribution pour obtenir des instructions sur le traitement des événements avant de recevoir un ID de session.

L’exemple suivant illustre une méthode de traitement des événements avant la réception d’un ID de session :


```
// For event payload format, see "Request body" sections of "Session Start Request", "Event Requests" respectively.  *
 
VideoPlayer.prototype._collectEvent = function(event) {
    var sessionID = event.events[0].xdm.mediaCollection.sessionID
    var eventType = event.events[0].xdm.eventType.substring("media.".length);
    // If we don't have a Session ID yet,
    // queue the event and return...
    if (sessionId === undefined) {
        console.log("[Player] Queueing event")
        _pendingEvents.push(event)
        return;
    }
 
    // If we DO have a Session ID, process the
    // tracking event...
    apiClient.request({
        "baseUrl": `${endpoint}`,
        "path": `ee/va/v1/${eventType}`,
        "method": `POST`,
        "data": `${event}`
    }).then((response) => {
        if (eventType === "sessionStart") {
            var newSessionID = response.json().handle.filter((h) => h.type === "media-analytics:new-session")[0].payload[0].sessionId;
            _processPendingEvents(newSessionID);
        }
        […]
    }
}
 
VideoPlayer.prototype._processPendingEvents function(sessionID) {
    _pendingEvents.forEach((event) => {
        event.events[0].xdm.mediaCollection.sessionID = sessionID;
        _collectEvent(event);
    });
    _pendingEvents = [];
}
```


