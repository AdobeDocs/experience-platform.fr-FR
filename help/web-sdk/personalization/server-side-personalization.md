---
title: Personnalisation côté serveur à l’aide de l’API Edge Network
description: Cet article explique comment utiliser l’API Edge Network pour déployer la personnalisation côté serveur sur vos propriétés web.
keywords: personnalisation;api du serveur;edge network;côté serveur;
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 82%

---


# Personnalisation côté serveur à l’aide de l’API Edge Network

## Vue d’ensemble {#overview}

La personnalisation côté serveur implique l’utilisation de l’API [Edge Network](https://developer.adobe.com/data-collection-apis/docs/getting-started/) pour personnaliser l’expérience client sur vos propriétés web.

Dans l’exemple décrit dans cet article, le contenu de personnalisation est récupéré côté serveur, à l’aide de l’API Edge Network. Ensuite, le code HTML est rendu côté serveur, en fonction du contenu de personnalisation récupéré.

Le tableau ci-dessous présente un exemple de contenu personnalisé et non personnalisé.

| Exemple de page sans personnalisation | Exemple de page avec personnalisation |
|---|---|
| ![Exemple de page web sans personnalisation](assets/plain.png) | ![Exemple de page web avec personnalisation](assets/personalized.png) |

## Considérations {#considerations}

### Cookies {#cookies}

Les cookies sont utilisés pour conserver l’identité de l’utilisateur et les informations de cluster.  Lors de l’utilisation d’une mise en œuvre côté serveur, le serveur d’applications gère le stockage et l’envoi de ces cookies pendant le cycle de vie des requêtes.

| Cookie | Rôle | Stocké par | Envoyé par |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Contient des détails de l’identité de l’utilisateur. | Serveur d’applications | Serveur d’applications |
| `kndctr_AdobeOrg_cluster` | Indique quel cluster Edge Network doit être utilisé pour répondre aux requêtes. | Serveur d’applications | Serveur d’applications |

### Demander l’emplacement {#request-placement}

Les requêtes de personnalisation sont nécessaires pour obtenir des propositions et envoyer une notification d’affichage. Lors de l’utilisation d’une mise en œuvre côté serveur, le serveur d’applications envoie ces requêtes à l’API Edge Network.

| Requête | Créée par |
|---|---|
| Requête d’interaction pour récupérer des propositions | Serveur applicatif appelant l’API Edge Network. |
| Requête d’interaction pour envoyer des notifications d’affichage | Serveur applicatif appelant l’API Edge Network. |

## Exemple d’application {#sample-app}

Le processus décrit ci-dessous utilise un exemple d’application que vous pouvez utiliser comme point de départ pour tester et en savoir plus sur ce type de personnalisation.

Vous pouvez télécharger cet exemple et le personnaliser selon vos besoins. Par exemple, vous pouvez modifier les variables d’environnement afin que l’exemple d’application puisse extraire les offres de votre propre configuration Experience Platform.

Pour ce faire, ouvrez le fichier `.env` à la racine du référentiel et modifiez les variables en fonction de votre configuration. Redémarrez l’exemple d’application et vous êtes prêt à tester votre propre contenu de personnalisation.

### Exécution de l’exemple {#running-sample}

Suivez les étapes ci-dessous pour exécuter l’exemple d’application.

1. Clonez [ce référentiel](https://github.com/adobe/alloy-samples) sur votre ordinateur local.
2. Ouvrez une fenêtre de terminal et accédez au dossier `personalization-server-side`.
3. Exécutez `npm install`.
4. Exécutez `npm start`.
5. Ouvrez votre navigateur web et accédez à `http://localhost`.

## Présentation des processus {#process}

Cette section décrit les étapes de récupération du contenu de personnalisation.

1. [Express](https://expressjs.com/fr/) est utilisé pour une mise en œuvre côté serveur allégée. Il gère les requêtes de serveur et le routage de base.
2. Le navigateur demande la page web. Tous les cookies précédemment stockés par le navigateur, précédés du préfixe `kndctr_`, sont inclus.
3. Lorsque la page est demandée auprès du serveur d’applications, un événement est envoyé au [point d’entrée de la collecte de données interactive](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) pour récupérer du contenu de personnalisation. L’exemple d’application utilise des méthodes d’assistance pour simplifier la création et l’envoi de requêtes à l’API (voir [aepEdgeClient.js](https://github.com/adobe/alloy-samples/blob/main/common/aepEdgeClient.js)). La requête `POST` contient un `event` et une `query`. S’ils sont disponibles, les cookies de l’étape précédente sont inclus dans le tableau `meta>state>entries`.

   ```js
   fetch(
   "https://edge.adobedc.net/ee/v2/interact?dataStreamId=abc&requestId=123",
   {
      headers: {
         accept: "*/*",
         "accept-language": "en-US,en;q=0.9",
         "cache-control": "no-cache",
         "content-type": "text/plain; charset=UTF-8",
         pragma: "no-cache",
         "sec-fetch-dest": "empty",
         "sec-fetch-mode": "cors",
         "sec-fetch-site": "cross-site",
         "sec-gpc": "1",
         "Referrer-Policy": "strict-origin-when-cross-origin",
         Referer: "http://localhost/",
      },
      body: JSON.stringify({
         event: {
         xdm: {
            web: {
               webPageDetails: {
               URL: "http://localhost/",
               },
               webReferrer: {
               URL: "",
               },
            },
            identityMap: {
               FPID: [
               {
                  id: "xyz",
                  authenticatedState: "ambiguous",
                  primary: true,
               },
               ],
            },
            timestamp: "2022-06-23T22:21:00.878Z",
         },
         data: {},
         },
         query: {
         identity: {
            fetch: ["ECID"],
         },
         personalization: {
            schemas: [
               "https://ns.adobe.com/personalization/default-content-item",
               "https://ns.adobe.com/personalization/html-content-item",
               "https://ns.adobe.com/personalization/json-content-item",
               "https://ns.adobe.com/personalization/redirect-item",
               "https://ns.adobe.com/personalization/dom-action",
            ],
            decisionScopes: ["__view__", "sample-json-offer"],
         },
         },
         meta: {
         state: {
            domain: "localhost",
            cookiesEnabled: true,
            entries: [
               {
               "key": "kndctr_XXX_AdobeOrg_identity",
               "value": "abc123"
               },
               {
               "key": "kndctr_XXX_AdobeOrg_cluster",
               "value": "or2"
               }
            ],
         },
         },
      }),
      method: "POST",
   }
   ).then((res) => res.json());
   ```

4. L’offre Target de l’activité basée sur des formulaires est lue à partir de la réponse et utilisée lors de la production de la réponse HTML.
5. Pour les activités basées sur des formulaires, les événements d’affichage doivent être envoyés manuellement dans la mise en œuvre pour indiquer le moment où l’offre a été affichée. Dans cet exemple, la notification est envoyée côté serveur, pendant le cycle de vie de la requête.

   ```js
   function sendDisplayEvent(aepEdgeClient, req, propositions, cookieEntries) {
   const address = getAddress(req);
   
   aepEdgeClient.interact(
      {
         event: {
         xdm: {
            web: {
               webPageDetails: { URL: address },
               webReferrer: { URL: "" },
            },
            timestamp: new Date().toISOString(),
            eventType: "decisioning.propositionDisplay",
            _experience: {
               decisioning: {
               propositions: propositions.map((proposition) => {
                  const { id, scope, scopeDetails } = proposition;
   
                  return {
                     id,
                     scope,
                     scopeDetails,
                  };
               }),
               },
            },
         },
         },
         query: { identity: { fetch: ["ECID"] } },
         meta: {
         state: {
            domain: "",
            cookiesEnabled: true,
            entries: [...cookieEntries],
         },
         },
      },
      {
         Referer: address,
      }
   );
   }
   ```

6. Les offres [!DNL Visual Experience Composer (VEC)] sont ignorées, puisqu’elles ne peuvent être rendues que par le biais du SDK Web.
7. Lorsque la réponse HTML est renvoyée, les cookies d’identité et de cluster sont définis sur la réponse par le serveur d’applications.