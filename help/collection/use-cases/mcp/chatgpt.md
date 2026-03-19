---
title: Collecter des analyses et appliquer une personnalisation dans les applications ChatGPT (collecte de données MCP)
description: Utilisez un serveur MCP hybride + modèle applyResponse de Web SDK pour envoyer des événements à Adobe Experience Platform Edge Network et effectuer le rendu de la personnalisation dans une interface utilisateur d'application ChatGPT.
keywords: Adobe Experience Platform, Web SDK, Edge Network, MCP, applications ChatGPT, applyResponse, point d’entrée d’interaction, personnalisation, analyse
source-git-commit: c848f821ea911c82531c6784a17df0116572cd86
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---

# Collecter des analyses et appliquer une personnalisation dans les applications ChatGPT (collecte de données MCP)

Ce cas pratique montre comment connecter une application ChatGPT (Model Context Protocol + composants facultatifs de l’interface utilisateur) à Adobe Experience Platform Edge Network. Ce type de collecte de données vous permet d’enregistrer des analyses pour les interactions conversationnelles qui appellent vos outils et de fournir des décisions de personnalisation à partir d’Edge Network dans un widget rendu par ChatGPT.

>[!NOTE]
>
>Ce document est mis à jour en fonction des dernières mises à jour disponibles des équipes de collecte de données d’Adobe et des dernières mises à jour technologiques d’OpenAI. Par conséquent, Adobe s’attend à ce que ce document évolue au fil du temps et recommande de vérifier les mises à jour.

Ce cas d’utilisation privilégie une approche hybride, utilisant à la fois une implémentation côté serveur pour la collecte de données et une implémentation côté client pour le rendu du contenu personnalisé. Cette approche est idéale, car l’appel de l’outil MCP est le moment le plus fiable pour collecter des analyses. Le widget s’exécute dans un contexte de navigateur et est l’endroit approprié pour stocker l’identité (dans un cookie) et appliquer les décisions de personnalisation.

Ce cas d’utilisation est accompagné d’un exemple de code entièrement opérationnel. Voir [Application ChatGPT + Adobe Experience Platform Edge](https://github.com/adobe/alloy-samples/tree/main/chatgpt-app) dans le référentiel `alloy-samples` sur GitHub pour obtenir un exemple de code et des instructions d’implémentation.

>[!IMPORTANT]
>
>Cette page présente une implémentation de référence destinée à illustrer un modèle d’intégration. Examinez les exigences en matière de sécurité, de confidentialité, de consentement et de production avant d’adopter cette approche dans votre application.

## Architecture

À un niveau élevé, il existe cinq parties mobiles :

1. **Hôte MCP (ChatGPT)** : ChatGPT appelle les outils exposés par votre serveur MCP et fournit un identifiant d’utilisateur pseudonyme stable dans les métadonnées de requête.
1. **Serveur MCP (serveur principal)** : appartient à votre organisation. Il met en œuvre des outils tels que la mise en liste des éléments, la récupération des détails ou l’envoi de requêtes.
1. **Adobe IMS** : émet des jetons d’accès utilisés par votre serveur MCP pour appeler les API de collecte de données Adobe.
1. **Adobe Experience Platform Edge Network** : reçoit les événements d’expérience envoyés par votre serveur MCP et renvoie les accusés de réception d’analyses, les mises à jour d’état (comme l’identité) et les décisions de personnalisation.
1. **Interface utilisateur web intégrée (widget frontal rendu par l’hôte MCP)** : affiche les résultats structurés et applique les métadonnées Adobe reçues du serveur principal MCP.

## Flux de données

1. **Utilisateur** invite **ChatGPT** à l’aide de votre serveur MCP.
1. **ChatGPT** interprète l’intention de l’invite et appelle l’**outil MCP principal approprié**.
1. Le **serveur MCP principal** utilise les API Data Collection (point d’entrée `interact`) pour envoyer un événement d’expérience à **Edge Network** pour la collecte d’analyses et la personnalisation facultative.
1. **Edge Network** renvoie les handles de réponse, y compris les mises à jour d’état et les décisions de personnalisation, à l’outil **MCP principal**.
1. **Outil MCP principal** renvoie un résultat d’outil contenant des données métier dans les métadonnées `structuredContent` et Adobe en `_meta` à **ChatGPT**.
1. **ChatGPT** fournit le résultat de l’outil au **widget frontend**, qui effectue le rendu des données métier et applique les métadonnées Adobe à l’aide de la commande `applyResponse` de la bibliothèque JavaScript Web SDK. Cette commande hydrate l’état côté client et rend les décisions de personnalisation éligibles dans l’interface utilisateur.

Les sections suivantes décrivent en détail chaque étape.

## Étape 1 : l&#39;utilisateur invite ChatGPT en utilisant votre serveur MCP

Cette étape est le point d’entrée du workflow. L’utilisateur indique l’intention du langage naturel :

```text
"Use the Adobe Office Information Tool to show me details about which office that is the most pet-friendly."
```

Voir [Créer votre serveur MCP](https://developers.openai.com/apps-sdk/build/mcp-server/) dans la documentation OpenAI Developers pour plus d’informations.

## Étape 2 : ChatGPT interprète l&#39;intention et appelle un outil MCP

En fonction des métadonnées de votre serveur MCP, ChatGPT interprète l’intention et appelle le gestionnaire d’outils approprié sur votre serveur MCP. Cet appel d’outil crée un point de vérité côté serveur pour l’interaction, qui est indépendant de la réussite du rendu de l’interface utilisateur. L’un de vos outils peut avoir les métadonnées suivantes :

```json
{
  "name": "office_details",
  "description": "Fetch details for a single office by ID and return personalization handles for the UI.",
  "inputSchema": {
    "type": "object",
    "properties": {
      "sessionId": { "type": "string", "description": "Server-issued session identifier." },
      "officeId": { "type": "string", "description": "Office identifier." }
    },
    "required": ["sessionId", "officeId"],
    "additionalProperties": false
  },
  "_meta": {
    "ui": {
      "visibility": ["model", "app"]
    }
  }
}
```

Consultez [Définir des outils](https://developers.openai.com/apps-sdk/plan/tools/) dans la documentation OpenAI destinée aux développeurs pour plus d’informations sur la manière d’indiquer à ChatGPT ce que fait chaque outil MCP.

## Étape 3 : votre serveur MCP envoie un événement d’expérience à Edge Network

Lorsque votre serveur MCP reçoit une demande, il déclenche un appel à l’Edge Network Adobe Experience Platform pour enregistrer les données d’analyse et éventuellement demander la prise de décision/personnalisation. Comme cette requête est serveur à serveur, utilisez le point d’entrée de [`interact`](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) authentifié dans le cadre des [API de collecte de données](https://developer.adobe.com/data-collection-apis/docs/). Adobe recommande d’utiliser un [espace de noms personnalisé](https://experienceleague.adobe.com/fr/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities) pour transmettre l’identifiant unique OpenAI. Assurez-vous que l’espace de noms que vous créez dans l’interface utilisateur Identités et l’espace de noms d’identité que vous définissez dans votre appel correspondent (sensible à la casse).

```sh
curl -X POST "https://server.adobedc.net/ee/v2/interact?datastreamId={DATASTREAM_ID}"
  -H "Authorization: Bearer {TOKEN}"
  -H "x-gw-ims-org-id: {ORG_ID}"
  -H "x-api-key: {API_KEY}"
  -H "Content-Type: application/json"
  -d '{
    "event": {
      "xdm": {
        "eventType": "office.details.view",
        "identityMap": {
          "{IDENTITY_NAMESPACE}": [
            { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
          ]
        },
        "timestamp": "YYYY-02-20T19:00:00.000Z"
      }
    },
    "query": {
      "personalization": {
        "decisionScopes": ["__view__"]
      }
    },
    "meta": {
      "state": {
        "entries": [
          { "key": "kndctr_orgid_cluster", "value": "{CLUSTER_HINT_IF_KNOWN}" },
          { "key": "kndctr_orgid_identity", "value": "{ECID_BLOB_IF_KNOWN}" }
        ]
      }
    }
  }'
```

## Étape 4 : L’Edge Network renvoie les poignées

Lorsque l’Edge Network reçoit votre appel `interact`, elle répond avec un tableau `handle`. Ce tableau peut inclure des décisions d’identité et de personnalisation, selon la configuration de votre flux de données. Voici un exemple de réponse :

```json
{
  "requestId": "60a2f...2294d",
  "handle": [
    {
      "type": "locationHint:result",
      "payload": [
        { "scope": "EdgeNetwork", "hint": "or2", "ttlSeconds": 1800 }
      ]
    },
    {
      "type": "state:store",
      "payload": [
        { "key": "kndctr_..._identity", "value": "CiYzM...snTI=", "maxAge": 34128000 },
        { "key": "kndctr_..._cluster", "value": "or2", "maxAge": 1800 }
      ]
    }
  ]
}
```

Votre serveur MCP peut ensuite extraire des informations de la réponse Edge Network pour conserver les informations d’identité :

```ts
type EdgeHandle = { type: string; payload?: Array<{ key?: string; value?: string }> };

export function extractStateStore(handles: EdgeHandle[]) {
  const store = handles.find(h => h.type === "state:store");
  const entries = store?.payload ?? [];

  const identity = entries.find(e => e.key?.includes("_identity"))?.value;
  const cluster  = entries.find(e => e.key?.includes("_cluster"))?.value;

  return { identity, cluster };
}
```

## Étape 5 : le serveur MCP renvoie la sortie d&#39;outil structuré plus les métadonnées Adobe à ChatGPT

Votre réponse de l’outil MCP inclut la sortie de l’outil structuré et la personnalisation à partir d’Edge Network.

* L’objet `structuredContent` contient des données commerciales que ChatGPT peut lire et commenter en toute sécurité.
* L’objet `_meta` contient les handles de réponse Adobe et les `identityMap` calculées par le serveur afin que le widget puisse les lire sans exposer ces données à ChatGPT. La conservation de ces informations dans `_meta.adobe` vous permet d’être cohérent quant à l’emplacement de ces données. Transmettre le même transfert de `identityMap` permet au widget d’utiliser la même identité personnalisée sur tous les événements ultérieurs côté interface utilisateur.

```json
{
  "content": "Displayed details for office seattle.",
  "structuredContent": {
    "office": {
      "id": "seattle",
      "name": "Seattle",
      "amenities": ["Pet Friendly", "Cafe", "Bike Storage"]
    }
  },
  "_meta": {
    "adobe": {
      "identityMap": {
        "{IDENTITY_NAMESPACE}": [
          { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
        ]
      },
      "handles": [
        {
          "type": "state:store",
          "payload": [
            { "key": "kndctr_..._identity", "value": "..." }
          ]
        },
        {
          "type": "personalization:decisions",
          "payload": [
            { "id": "..." }
          ]
        }
      ]
    }
  }
}
```

Voir [Résultats de l’outil](https://developers.openai.com/apps-sdk/reference/#tool-results) dans la référence du développeur OpenAI pour plus d’informations.

## Étape 6 : le widget effectue le rendu du résultat et l’applique `_adobe.handles` utilisant `applyResponse`

Le widget effectue le rendu des données métier à partir de `structuredContent`, puis lit les métadonnées Adobe à partir de `_meta.adobe`. Dans ChatGPT, les mêmes données sont disponibles pour le widget via la couche de compatibilité :

* `window.openai.toolOutput` contient du `structuredContent`
* `window.openai.toolResponseMetadata` contient du `_meta`

Le widget utilise la commande [`applyResponse`](../../js/commands/applyresponse.md) de la bibliothèque JavaScript de Web SDK pour décompresser l’état côté client et rendre les décisions de personnalisation renvoyées par l’appel de `interact` côté serveur. Veillez à appeler la commande [`configure`](../../js/commands/configure/overview.md) avant de `applyResponse` appeler. Étant donné que votre serveur MCP a effectué un appel `interact`, vous n’avez pas besoin d’appeler immédiatement la commande [`sendEvent`](../../js/commands/sendevent/overview.md) pour l’interaction d’appel de l’outil.

```js
// Configure the Web SDK before any other commands.
alloy("configure", {
  datastreamId: "YOUR_DATASTREAM_ID",
  orgId: "YOUR_EXPERIENCE_CLOUD_ORG_ID"
});

// Business data exposed to ChatGPT and the widget.
const { office } = window.openai?.toolOutput ?? {};

// Adobe metadata available only to the widget.
const adobe = window.openai?.toolResponseMetadata?.adobe ?? {};
const { identityMap, handles } = adobe;

// Hydrate client-side state and render personalization decisions from the
// server-side interact response.
alloy("applyResponse", {
  renderDecisions: true,
  responseBody: { handle: handles ?? [] }
});
```

Si le widget envoie ultérieurement des événements supplémentaires côté interface utilisateur, vous pouvez inclure le même `identityMap` sur ces appels :

```js
alloy("sendEvent", {
  xdm: {
    eventType: "office.details.widgetView",
    identityMap
  }
});
```

Ce modèle permet d’aligner l’utilisation des identités côté serveur et côté interface utilisateur tout en permettant à l’appel `interact` côté serveur de rester la source de vérité pour la collecte d’analyses et la prise de décision.

## Validation

Une fois toutes les étapes ci-dessus configurées, vous pouvez valider les éléments suivants :

* **Collecte de données :** vérifiez que les événements atteignent le jeu de données souhaité et que chaque événement est traité comme prévu.
* **Personalization:** Vérifiez que les décisions sont renvoyées par l’Edge Network et que ces décisions sont rendues par votre widget.

## Considérations relatives à la sécurité et à la confidentialité

* Traitez les identifiants de ChatGPT comme sensibles, même s&#39;ils sont pseudonymes.
* Veillez à appliquer les pratiques de consentement et de gouvernance des données de votre organisation à ce workflow.
* Adobe recommande d’utiliser les workflows OAuth 2.1 pour l’autorisation.
* Assurez-vous que les jetons d’accès et les secrets n’atteignent jamais le client ou l’interface utilisateur.
