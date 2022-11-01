---
title: Personnalisation hybride à l’aide du SDK Web et de l’API Edge Network Server
description: Cet article explique comment utiliser le SDK Web conjointement avec l’API du serveur pour déployer la personnalisation hybride sur vos propriétés web.
keywords: la personnalisation; hybride; api du serveur ; côté serveur ; mise en oeuvre hybride;
source-git-commit: f280d4cbcde434ccf36df37e95f1902cfd02c96c
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 3%

---


# Personnalisation hybride à l’aide du SDK Web et de l’API Edge Network Server

## Présentation {#overview}

La personnalisation hybride décrit le processus de récupération du contenu de personnalisation côté serveur, à l’aide du [API du serveur réseau Edge](../..//server-api/overview.md), et de le rendre côté client, à l’aide de la variable [SDK Web](../home.md).

Vous pouvez utiliser la personnalisation hybride avec des solutions de personnalisation telles qu’Adobe Target ou Offer Decisioning, la différence étant le contenu de la variable [!UICONTROL API du serveur] payload.

## Conditions préalables {#prerequisites}

Avant d’implémenter une personnalisation hybride sur vos propriétés web, assurez-vous de respecter les conditions suivantes :

* Vous avez décidé quelle solution de personnalisation vous souhaitez utiliser. Cela aura un impact sur le contenu de la variable [!UICONTROL API du serveur] payload.
* Vous avez accès à un serveur d’applications que vous pouvez utiliser pour effectuer les opérations suivantes : [!UICONTROL API du serveur] appels .
* Vous avez accès au [API du serveur réseau Edge](../../server-api/authentication.md).
* Vous avez correctement [configuré et déployé](../fundamentals/configuring-the-sdk.md) SDK Web sur les pages que vous souhaitez personnaliser.

## Diagramme de flux {#flow-diagram}

Le diagramme de flux ci-dessous décrit l’ordre des étapes effectuées pour fournir une personnalisation hybride.

![Diagramme de flux visuel présentant l’ordre des étapes effectuées pour fournir une personnalisation hybride.](assets/hybrid-personalization-diagram.png)

1. Tout cookie existant précédemment stocké par le navigateur, précédé du préfixe `kndctr_`, sont inclus dans la requête du navigateur.
1. Le navigateur Web client demande la page Web à votre serveur d’applications.
1. Lorsque le serveur d’applications reçoit la demande de page, il effectue une `POST` à la fonction [Point d’entrée de la collecte de données interactive de l’API serveur](../../server-api/interactive-data-collection.md) pour récupérer du contenu de personnalisation. Le `POST` contient une `event` et un `query`. Si elles sont disponibles, les cookies de l’étape précédente sont inclus dans la variable `meta>state>entries` tableau.
1. L’API du serveur renvoie le contenu de personnalisation à votre serveur d’applications.
1. Le serveur d’applications renvoie une réponse HTML au navigateur client, contenant la variable [cookies d’identité et de cluster](#cookies).
1. Sur la page client, la variable [!DNL Web SDK] `applyResponse` est appelée, en transmettant les en-têtes et le corps de la fonction [!UICONTROL API du serveur] réponse de l’étape précédente.
1. Le [!DNL Web SDK] effectue le rendu du chargement de page [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) propose automatiquement, car la variable `renderDecisions` L’indicateur est défini sur `true`.
1. D’après les formulaires [!DNL JSON] les offres sont appliquées manuellement par l’intermédiaire de la fonction `applyPersonalization` pour mettre à jour la méthode [!DNL DOM] en fonction de l’offre de personnalisation.
1. Pour les activités basées sur des formulaires, les événements d’affichage doivent être envoyés manuellement pour indiquer le moment où l’offre a été affichée. Pour ce faire, utilisez l’option `sendEvent` .

## Cookies {#cookies}

Les cookies sont utilisés pour conserver l’identité de l’utilisateur et les informations de cluster.  Lors de l’utilisation d’une mise en oeuvre hybride, le serveur d’applications Web gère le stockage et l’envoi de ces cookies pendant le cycle de vie des demandes.

| Cookie | Rôle | Stockée par | Envoyé par |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Contient les détails de l’identité de l’utilisateur. | Serveur applicatif | Serveur applicatif |
| `kndctr_AdobeOrg_cluster` | Indique la grappe Edge Network qui doit être utilisée pour répondre aux demandes. | Serveur applicatif | Serveur applicatif |

## Demander l’emplacement {#request-placement}

Les demandes d’API de serveur sont nécessaires pour obtenir des propositions et envoyer une notification d’affichage. Lors de l’utilisation d’une mise en oeuvre hybride, le serveur d’applications envoie ces requêtes à l’API du serveur.

| Requête | Fabriqué par |
|---|---|
| Demande d’interaction pour récupérer des propositions | Serveur applicatif |
| Demande d’interaction pour envoyer des notifications d’affichage | Serveur applicatif |

## implications Analytics {#analytics}

Lors de la mise en oeuvre d’une personnalisation hybride, vous devez accorder une attention particulière afin que les accès aux pages ne soient pas comptabilisés plusieurs fois dans Analytics.

Lorsque vous [configuration d’un flux de données](../datastreams/overview.md) dans Analytics, les événements sont automatiquement transférés afin que les accès à la page soient capturés.

L’exemple de cette mise en oeuvre utilise deux flux de données différents :

* Un flux de données configuré pour Analytics. Ce flux de données est utilisé pour les interactions du SDK Web.
* Une seconde banque de données sans configuration Analytics. Ce flux de données est utilisé pour les demandes d’API de serveur.

Ainsi, la requête côté serveur n’enregistre aucun événement Analytics, contrairement aux requêtes côté client. Cela entraîne un comptage précis des requêtes Analytics.


## Requête côté serveur {#server-side-request}

L’exemple de requête ci-dessous illustre une requête d’API de serveur que votre serveur d’applications peut utiliser pour récupérer le contenu de personnalisation.

>[!IMPORTANT]
>
>Cet exemple de requête utilise Adobe Target en tant que solution de personnalisation. Votre demande peut varier en fonction de la solution de personnalisation choisie.


**Format d’API**

```http
POST /ee/v2/interact
```

### Requête {#request}

```shell
curl -X POST "https://edge.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Content-Type: text/plain" 
-d '{
   "event":{
      "xdm":{
         "web":{
            "webPageDetails":{
               "URL":"http://localhost/"
            },
            "webReferrer":{
               "URL":""
            }
         },
         "identityMap":{
            "FPID":[
               {
                  "id":"xyz",
                  "authenticatedState":"ambiguous",
                  "primary":true
               }
            ]
         },
         "timestamp":"2022-06-23T22:21:00.878Z"
      },
      "data":{
         
      }
   },
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      },
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/default-content-item",
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "sample-json-offer"
         ]
      }
   },
   "meta":{
      "state":{
         "domain":"localhost",
         "cookiesEnabled":true,
         "entries":[
            {
               "key":"kndctr_XXX_AdobeOrg_identity",
               "value":"abc123"
            },
            {
               "key":"kndctr_XXX_AdobeOrg_cluster",
               "value":"or2"
            }
         ]
      }
   }
}'
```

| Paramètre | Type | Obligatoire | Description |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Oui. | L’identifiant de la banque de données que vous utilisez pour transmettre les interactions au réseau Edge. Voir [présentation des jeux de données](../datastreams/overview.md) pour savoir comment configurer un flux de données. |
| `requestId` | `String` | Non | Identifiant aléatoire permettant de corréler les requêtes du serveur interne. Si aucun n’est fourni, le réseau Edge en génère un et le renvoie dans la réponse . |

### Réponse côté serveur {#server-response}

L’exemple de réponse ci-dessous indique à quoi pourrait ressembler la réponse de l’API de serveur.


```json
{
   "requestId":"5c539bd0-33bf-43b6-a054-2924ac58038b",
   "handle":[
      {
         "payload":[
            {
               "id":"XXX",
               "namespace":{
                  "code":"ECID"
               }
            }
         ],
         "type":"identity:result"
      },
      {
         "payload":[
            {
               "..."
            },
            {
               "..."
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      }
   ]
}
```

## Requête côté client {#client-request}

Sur la page client, la variable [!DNL Web SDK] `applyResponse` est appelée, en transmettant les en-têtes et le corps de la réponse côté serveur.

```js
   alloy("applyResponse", {
      "renderDecisions": true,
      "responseHeaders": {
         "cache-control": "no-cache, no-store, max-age=0, no-transform, private",
         "connection": "close",
         "content-encoding": "deflate",
         "content-type": "application/json;charset=utf-8",
         "date": "Mon, 11 Jul 2022 19:42:01 GMT",
         "server": "jag",
         "strict-transport-security": "max-age=31536000; includeSubDomains",
         "transfer-encoding": "chunked",
         "vary": "Origin",
         "x-adobe-edge": "OR2;9",
         "x-content-type-options": "nosniff",
         "x-konductor": "22.6.78-BLACKOUTSERVERDOMAINS:7fa23f82",
         "x-rate-limit-remaining": "599",
         "x-request-id": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "x-xss-protection": "1; mode=block"
      },
      "responseBody": {
         "requestId": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "handle": [
         {
            "payload": [
               {
               "id": "XXX",
               "namespace": {
                  "code": "ECID"
               }
               }
            ],
            "type": "identity:result"
         },
         {
            "payload": [
               {...}, 
               {...}
            ],
            "type": "personalization:decisions",
            "eventIndex": 0
         }
         ]
      }
   }
   ).then(applyPersonalization("sample-json-offer"));
```

D’après les formulaires [!DNL JSON] les offres sont appliquées manuellement par l’intermédiaire de la fonction `applyPersonalization` pour mettre à jour la méthode [!DNL DOM] en fonction de l’offre de personnalisation. Pour les activités basées sur des formulaires, les événements d’affichage doivent être envoyés manuellement pour indiquer le moment où l’offre a été affichée. Pour ce faire, utilisez l’option `sendEvent` .

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        xdm: {
            eventType: "decisioning.propositionDisplay",
            _experience: {
                decisioning: {
                    propositions: [
                        {
                            id: id,
                            scope: scope,
                            scopeDetails: scopeDetails,
                        },
                    ],
                },
            },
        },
    });
}
```

## Exemple d’application {#sample-app}

Pour vous aider à expérimenter et à en savoir plus sur ce type de personnalisation, nous vous proposons un exemple d’application que vous pouvez télécharger et utiliser pour les tests. Vous pouvez télécharger l’application, ainsi que des instructions détaillées sur son utilisation, à partir de cette page. [Référentiel GitHub](https://github.com/adobe/alloy-samples).






