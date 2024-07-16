---
title: Traitement des erreurs
description: Découvrez les erreurs que vous pouvez rencontrer lors de l’exécution de requêtes d’API vers l’API Adobe Experience Platform Edge Network Server.
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 9%

---

# Traitement des erreurs

## Vue d’ensemble {#overview}

Les erreurs d’API dans l’API Adobe Experience Platform Edge Network Server peuvent avoir diverses causes, internes (Edge Network lui-même) ou externes (d’entrée, de configuration ou liées en amont).

## Types d’erreur {#error-types}

| Erreur | Type | Description | Code d’état |
| --- | --- | --- | --- |
| `RequestProcessingError` | Interne | Erreur générale générée par l’Edge Network Adobe Experience Platform dans des circonstances inattendues. | `500` |
| `InputError` | Externe | Inclut les erreurs provoquées par une entrée incorrecte, ainsi que les erreurs de validation d’entité. | `4xx` |
| `ConfigurationError` | Externe | Erreurs de configuration côté serveur. | `422` |
| `UpstreamError` | Externe | Erreurs de communication avec les services en amont. | `207 Multi-Status` |

## Gravité

Les erreurs de l’API du serveur peuvent également être fractionnées par gravité :

* **Erreurs fatales** arrêtera le pipeline d’envoi.
* **Des erreurs non fatales** peuvent signaler un traitement partiel, tout en permettant la poursuite du traitement des demandes.
   * Lorsqu’il est présent, le code d’état global de la requête est remplacé par `207 Multi-Status`.

| Erreur | Type | Remarques         |
| --- | --- | --- |
| `RequestProcessingError` | Faux | Peut se produire à tout moment pendant le traitement des requêtes. |
| `InputError` | Faux | Se produit lors de l’acceptation de la demande, avant de la distribuer en amont. |
| `ConfigurationError` | Faux | Se produit lors de l’acceptation de la demande, avant de la distribuer en amont. |
| `UpstreamError` | Non fatale | Erreurs de communication avec les services en amont. |

### Erreurs fatales {#fatal-errors}

Des erreurs irrécupérables interrompent le traitement de la requête et entraînent le renvoi d’un état de réponse non 2xx. Consultez la section [types d’erreur](#error-types) pour voir le code d’état attendu, correspondant à chaque type d’erreur.

Les erreurs seront accompagnées d’un corps de réponse contenant un objet d’erreur. Dans ce cas, le corps de la réponse contient un détail de problème, tel que défini par [RFC 7807 Problem Details for HTTP APIs](https://tools.ietf.org/html/rfc7807).

Le type de contenu renvoyé est le type de média `application/problem+json`. Lorsqu’elle est présente, cette réponse contient des détails lisibles par l’ordinateur concernant l’erreur. Les détails du problème incluent un type d’URI.

Tous les objets d’erreur possèdent des propriétés de message `type`, `status`, `title`, `detail` et `report` afin que le client API puisse déterminer le problème.

| Propriété | Type | Description |
| -------- | ------ | ----------- |
| `type` | Chaîne | Une référence URI (RFC3986) qui identifie le type de problème, selon le format `https://ns.adobe.com/aep/errors/<ERROR-CODE>`. |
| `status` | Nombre | Code d’état HTTP généré par le serveur pour cette occurrence du problème. |
| `title` | Chaîne | Résumé court et lisible du type de problème. |
| `detail` | Chaîne | Description courte et lisible du type de problème. |
| `report` | Objet | Carte des propriétés supplémentaires qui aident au débogage, telles que l’ID de demande ou l’ID d’organisation. Dans certains cas, il peut contenir des données spécifiques à l’erreur en question, telles qu’une liste d’erreurs de validation. |

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0104-422",
   "status":422,
   "title":"Unprocessable entity",
   "detail":"Invalid request (report attached). Please check your input and try again.",
   "report":{
      "errors":[
         "Allowed Adobe version is 1.0 for standard 'Adobe' at index 0",
         "Allowed IAB version is 2.0 for standard 'IAB TCF' at index 1",
         "IAB consent string value must not be empty for standard 'IAB TCF' at index 1"
      ],
      "requestId":"0f8821e5-ed1a-4301-b445-5f336fb50ee8",
      "orgId":"53A16ACB5CC1D3760A495C99@AdobeOrg"
   }
}
```

### Erreurs non fatales {#non-fatal-errors}

Les erreurs non fatales peuvent être ventilées par :

* Erreurs : problèmes qui se sont produits lors du traitement de la requête, mais qui n’ont pas entraîné le rejet de l’ensemble de la requête (par exemple, un échec en amont non critique).
* Avertissements : messages provenant de services en amont qui peuvent signaler un traitement partiel de la demande.

En cas d’erreurs non fatales (à l’exclusion des avertissements), l’ [!DNL Server API] remplace l’état de réponse par `207 Multi-Status`.

Les avertissements, en revanche, sont essentiellement informatifs, car ils représentent généralement une condition potentiellement transitoire, qui n’a pas eu d’incidence totale sur la demande. Voici un exemple de profil partiel lu dans le moteur de segmentation, auquel cas la précision est affectée dans une certaine mesure, mais la fonctionnalité est toujours fournie.

Les erreurs non fatales sont représentées au format _Détails du problème_, mais sont incorporées directement dans la réponse standard de la passerelle Edge, de type `application/json`.

```json
{
  "requestId": "72eaa048-207e-4dde-bf16-0cb2b21336d5",
  "handle": [
  ],
  "errors": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0201-503",
      "status": 503,
      "title": "The 'com.adobe.experience.platform.ode' service is temporarily unable to serve this request. Please try again later."
    }
  ],
  "warnings": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0204-200",
      "status": 200,
      "title": "A warning occurred while calling the 'com.adobe.audiencemanager' service for this request.",
      "report": {
        "cause": {
          "message": "Cannot read related customer for device id: ...",
          "code": 202
        }
      }
    }
  ]
}
```

## Gestion des réponses `4xx` et `5xx`

| Code d’erreur | Description |
|---|---|
| `4xx Bad Request` | La plupart des erreurs `4xx`, telles que 400, 403, 404, ne doivent pas être retentées pour le compte du client, à l’exception de `429`. Il s’agit d’erreurs du client qui échoueront. Le client doit corriger l’erreur avant de retenter la requête. |
| `429 Too Many Requests` | `429` Le code de réponse HTTP indique que l’Edge Network Adobe Experience Platform ou un service en amont limite le débit des requêtes. Dans ce cas, dans un tel scénario, l’appelant doit respecter l’en-tête de réponse `Retry-After`. Toutes les réponses renvoyées doivent comporter le code de réponse HTTP avec un code d’erreur spécifique au domaine. |
| `500 Internal Server Error` | Les erreurs `500` sont des erreurs génériques « fourre-tout ». `500` Les erreurs ne doivent pas être retraitées, à l&#39;exception de `502` et `503`. Les intermédiaires doivent répondre avec une erreur `500` et peuvent répondre avec un code/message d’erreur générique, ou un code/message d’erreur plus spécifique au domaine. |
| `502 Bad Gateway` | Indique que l’Edge Network Adobe Experience Platform a reçu une réponse non valide des serveurs en amont. Cela peut être dû à des problèmes réseau entre les serveurs. Le problème de réseau temporaire peut être résolu. Par conséquent, une nouvelle tentative peut résoudre le problème. De ce fait, les destinataires des erreurs `502` peuvent réessayer la requête après un certain temps. |
| `503 Service Unavailable` | Ce code d’erreur indique que le service est temporairement indisponible. Cela peut se produire pendant les périodes de maintenance. Les destinataires des erreurs `503` peuvent réessayer la requête, mais doivent respecter l’en-tête `Retry-After`. |
| `504 Gateway Timeout` | Indique que la demande de l’Edge Network Adobe Experience Platform aux serveurs en amont a expiré. Cela peut être dû à des problèmes réseau entre les serveurs, des problèmes liés aux DNS ou d’autres problèmes de réseau. Les problèmes réseau temporaires peuvent être résolus après un certain temps et une nouvelle tentative peut résoudre le problème. |
