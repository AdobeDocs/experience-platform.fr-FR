---
solution: Experience Platform
title: Prise en main des API Media Edge
description: Guide de dépannage des API Media Edge
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 98%

---


# Guide de dépannage de l’API Media Edge

Ce guide fournit des instructions de dépannage pour corriger les erreurs et obtenir les bonnes réponses.

## Utiliser les aides des réponses en erreur

Pour aider à résoudre les problèmes de réponses infructueuses, les erreurs sont accompagnées d’un corps de réponse contenant un objet d’erreur. Dans ce cas, le corps de la réponse contient les détails du problème, tels que définis dans le document [RFC 7807 - Détails du problème pour les API HTTP](https://datatracker.ietf.org/doc/html/rfc7807). Pour améliorer l’expérience client de l’API, les détails du problème sont descriptifs (les détails des clés du tableau sont affichés à l’aide d’une expression JsonPath sur le champ manquant ou non valide). Ils sont également cumulatifs (tous les champs non valides sont signalés dans la même requête).


## Valider les débuts de session

La plupart des problèmes rencontrés lors de la création de requêtes de début de session entraînent une réponse 207 multi-statut.
La payload est similaire à [API du serveur](../error-handling.md)est des erreurs non fatales. Toutes les
erreurs Media Analytics sont du type suivant : `https://ns.adobe.com/aep/errors/va-edge-0XXX-XXX`. les nombres affichés dans la réponse correspondent au statut d’erreur.

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

Dans l’exemple ci-dessus, les deux problèmes sont signalés par les champs `name` et `reason` sous `details` : le premier champ « reason » indique `missing required field` et le second décrit la non-conformité à la norme ISO 8601.


>[!NOTE]
>
> En cas d’erreur en amont de Media Analytics, Adobe recommande de continuer le traitement de la session multimédia générée.

## Valider les événements

La plupart des requêtes d’événement non valides génèrent une réponse 400 Bad Request. Dans ce cas, la payload est similaire aux erreurs fatales de l’API Server.

Pour les requêtes d’événement, le service d’API Media Edge effectue des vérifications supplémentaires qui ne sont pas capturées dans le modèle XDM lui-même. Il s’agit notamment de s’assurer que le paramètre `eventType` du chemin correspond au paramètre `eventType` dans la payload de la requête.


L’exemple suivant illustre une incohérence entre les paramètres `eventType` avec une payload `adBreakStart` envoyée à `ee/va/v1/chapterStart` :

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

L’exemple suivant montre une vérification supplémentaire de l’API Media Edge, qui détecte un appel `chapterStart` dépourvu d’informations `chapterDetails` :

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

## Gérer les erreurs de niveau 400 et 500

Le tableau suivant fournit des instructions pour gérer les erreurs de réponse de statut :


| Code d’erreur | Description |
| ---------- | --------- |
| 4xx Bad request | La plupart des erreurs 4xx (par exemple, `400`, `403` et `404`) ne doivent pas faire l’objet d’une nouvelle tentative par l’utilisateur ou par l’utilisatrice. Toute nouvelle tentative de la requête sera vaine. L’utilisateur ou l’utilisatrice doit corriger l’erreur avant de retenter la requête. Les événements qui entraînent un code de statut 4xx ne sont pas suivis, ce qui peut potentiellement affecter la précision des données dans les sessions qui ont reçu des réponses 4xx. |
| 410 Gone | Indique que la session prévue pour le suivi n’est plus calculée côté serveur. La raison évidente est que la session dure plus de 24 heures. Après avoir reçu l’erreur `410`, essayez de démarrer une nouvelle session et de la suivre. |
| 429 Too many requests | Ce code de réponse indique que le serveur limite le débit des requêtes. Suivez attentivement les instructions **Retry-After** dans l’en-tête de réponse. Toutes les réponses renvoyées doivent comporter le code de réponse HTTP avec un code d’erreur spécifique au domaine. |
| 500 Internal server error | Les erreurs `500` sont des erreurs génériques « fourre-tout ». Les erreurs `500` ne doivent pas être retentées, à l’exception des erreurs `502`, `503` et `504`. |
| 502 Bad gateway | Ce code d’erreur indique que le serveur, lorsqu’il agissait en tant que passerelle, a reçu une réponse non valide des serveurs en amont. Cela peut être dû à des problèmes réseau entre les serveurs. Notez que le problème temporaire de réseau peut se résoudre spontanément. Réessayez donc la requête pour en avoir le cœur net. |
| 503 Service unavailable | Ce code d’erreur indique que le service est temporairement indisponible. Cela peut se produire pendant les périodes de maintenance. Les personnes qui reçoivent des erreurs `503` peuvent réessayer la requête, mais ils doivent également scrupuleusement suivre les instructions de l’en-tête **Retry-After**. |


## Événements de mise en file d’attente lorsque les réponses de session sont lentes

Après le démarrage d’une session de suivi multimédia, le lecteur multimédia peut se déclencher avant que la réponse de début de session ne soit renvoyée (avec le paramètre d’ID de session) à partir du serveur principal. Dans ce cas, votre application doit mettre en file d’attente tout événement de suivi ayant lieu entre la requête de début de session et sa réponse. Lorsque la réponse sessions arrive, vous devez d’abord traiter les événements mis en file d’attente, puis commencer à traiter les événements en direct.

Pour de meilleurs résultats, consultez le lecteur de référence dans votre distribution pour obtenir des instructions sur le traitement des événements avant de recevoir un ID de session.

L’exemple suivant illustre une méthode de traitement des événements avant la réception d’un ID de session :


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


