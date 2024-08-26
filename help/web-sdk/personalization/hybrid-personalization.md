---
title: Personnalisation hybride à l’aide du SDK Web et de l’API Edge Network Server
description: Cet article explique comment utiliser le SDK Web conjointement avec l’API du serveur pour déployer la personnalisation hybride sur vos propriétés web.
keywords: personnalisation;hybride;api du serveur;côté serveur;implémentation hybride;
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: 9489b5345c2b13b9d05b26d646aa7f1576840fb8
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 84%

---

# Personnalisation hybride à l’aide du SDK Web et de l’API Edge Network Server

## Présentation {#overview}

La personnalisation hybride décrit le processus de récupération du contenu de personnalisation côté serveur, à l’aide de l’[API Edge Network Server](../../server-api/overview.md), et de le rendre côté client, à l’aide du [SDK Web](../home.md).

Vous pouvez utiliser la personnalisation hybride avec des solutions de personnalisation comme Adobe Target, Adobe Journey Optimizer ou Offer Decisioning, la différence étant le contenu de la payload [!UICONTROL Server API].

## Conditions préalables {#prerequisites}

Avant d’implémenter une personnalisation hybride sur vos propriétés web, assurez-vous de respecter les conditions suivantes :

* Vous avez choisi la solution de personnalisation que vous souhaitez utiliser. Cela aura un impact sur le contenu de la payload de l’[!UICONTROL API du serveur].
* Vous avez accès à un serveur d’applications que vous pouvez utiliser pour effectuer les appels de l’[!UICONTROL API du serveur].
* Vous avez accès a l’[API Edge Network Server](../../server-api/authentication.md).
* Vous avez correctement [configuré](/help/web-sdk/commands/configure/overview.md) et déployé le SDK Web sur les pages que vous souhaitez personnaliser.

## Diagramme de flux {#flow-diagram}

Le diagramme de flux ci-dessous décrit l’ordre des étapes effectuées pour fournir une personnalisation hybride.

![Diagramme de flux visuel présentant l’ordre des étapes effectuées pour fournir une personnalisation hybride.](assets/hybrid-personalization-diagram.png)

1. Tout cookie existant précédemment stocké par le navigateur, préfixé par `kndctr_`, est inclus dans la requête du navigateur.
1. Le navigateur web client demande la page web à votre serveur d’applications.
1. Lorsque le serveur d’applications reçoit la requête de page, il effectue une requête `POST` au [point d’entrée de la collecte de données interactive de l’API du serveur](../../server-api/interactive-data-collection.md) pour récupérer du contenu de personnalisation. La requête `POST` contient un `event` et une `query`. S’ils sont disponibles, les cookies de l’étape précédente sont inclus dans le tableau `meta>state>entries`.
1. L’API du serveur renvoie le contenu de personnalisation à votre serveur d’applications.
1. Le serveur d’applications renvoie une réponse HTML au navigateur client, contenant les [cookies d’identité et de cluster](#cookies).
1. Sur la page client, la commande [!DNL Web SDK] `applyResponse` est appelée, en transmettant les en-têtes et le corps de la réponse de l’[!UICONTROL API du serveur] de l’étape précédente.
1. Le [!DNL Web SDK] effectue automatiquement le rendu des offres Target [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) et des éléments de canal web Journey Optimizer, car l’indicateur `renderDecisions` est défini sur `true`.
1. Les offres [!DNL HTML]/[!DNL JSON] basées sur des formulaires Target et les expériences basées sur du code Journey Optimizer sont appliquées manuellement par le biais de la méthode `applyProposition`, afin de mettre à jour l’ [!DNL DOM] en fonction du contenu de personnalisation dans la proposition.
1. Pour les offres [!DNL HTML]/[!DNL JSON] basées sur des formulaires Target et les expériences basées sur du code Journey Optimizer, des événements d’affichage doivent être envoyés manuellement pour indiquer le moment où le contenu renvoyé a été affiché. Cela s’effectue via la commande `sendEvent`.

## Cookies {#cookies}

Les cookies sont utilisés pour conserver l’identité de l’utilisateur et les informations de cluster.  Lors de l’utilisation d’une implémentation hybride, le serveur d’applications web gère le stockage et l’envoi de ces cookies pendant le cycle de vie des requêtes.

| Cookie | Rôle | Stocké par | Envoyé par |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Contient des détails de l’identité de l’utilisateur. | Serveur d’applications | Serveur d’applications |
| `kndctr_AdobeOrg_cluster` | Indique quel cluster Edge Network doit être utilisé pour répondre aux requêtes. | Serveur d’applications | Serveur d’applications |

## Demander l’emplacement {#request-placement}

Les requêtes d’API du serveur sont nécessaires pour obtenir des propositions et envoyer une notification d’affichage. Lors de l’utilisation d’une implémentation hybride, le serveur d’applications envoie ces requêtes à l’API du serveur.

| Requête | Créée par |
|---|---|
| Requête d’interaction pour récupérer des propositions | Serveur d’applications |
| Requête d’interaction pour envoyer des notifications d’affichage | Serveur d’applications |

## Implications Analytics {#analytics}

Lors de l’implémentation d’une personnalisation hybride, vous devez faire particulièrement attention à ce que les accès aux pages ne soient pas comptabilisés plusieurs fois dans Analytics.

Lorsque vous [configurez un flux de données](../../datastreams/overview.md) dans Analytics, les événements sont automatiquement transférés afin que les accès à la page soient capturés.

L’exemple de cette mise en œuvre utilise deux flux de données différents :

* Un flux de données configuré pour Analytics. Ce flux de données est utilisé pour les interactions du SDK Web.
* Un second flux de données sans configuration Analytics. Ce flux de données est utilisé pour les demandes d’API de serveur. Vous devez configurer ce flux de données avec la même configuration de destination que celle que vous avez configurée pour Analytics.

Ainsi, la requête côté serveur n’enregistre aucun événement Analytics, contrairement aux requêtes côté client. Cela entraîne un comptage précis des requêtes Analytics.


## Requête côté serveur {#server-side-request}

L’exemple de requête ci-dessous illustre une requête d’API du serveur que votre serveur d’applications peut utiliser pour récupérer le contenu de personnalisation.

>[!IMPORTANT]
>
>Cet exemple de requête utilise Adobe Target comme solution de personnalisation. Votre requête peut varier en fonction de la solution de personnalisation choisie.


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
| `dataStreamId` | `String` | Oui. | L’identifiant du flux de données que vous utilisez pour transmettre les interactions à Edge Network. Voir la [présentation des flux de données](../../datastreams/overview.md) pour savoir comment configurer un flux de données. |
| `requestId` | `String` | Non | Un identifiant aléatoire permettant de corréler les requêtes internes du serveur. Si aucun n’est fourni, le Edge Network en génère un et le renvoie dans la réponse. |

### Réponse côté serveur {#server-response}

L’exemple de réponse ci-dessous indique à quoi pourrait ressembler la réponse de l’API du serveur.


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

Sur la page client, la commande [!DNL Web SDK] `applyResponse` est appelée, transmettant les en-têtes et le corps de la réponse côté serveur.

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

Les offres [!DNL JSON] basées sur des formulaires sont appliquées manuellement par l’intermédiaire de la méthode `applyPersonalization` pour mettre à jour le [!DNL DOM] en fonction de l’offre de personnalisation. Pour les activités basées sur des formulaires, les événements d’affichage doivent être envoyés manuellement pour indiquer le moment où l’offre a été affichée. Cela s’effectue via la commande `sendEvent`.

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        "xdm": {
            "eventType": "decisioning.propositionDisplay",
            "_experience": {
                "decisioning": {
                    "propositions": [{
                        "id": id,
                        "scope": scope,
                        "scopeDetails": scopeDetails
                    }],
                    "propositionEventType": {
                        "display": 1
                    }
                }
            }
        }
    });
}
```

## Exemple d’application {#sample-app}

Pour vous aider à expérimenter et à en savoir plus sur ce type de personnalisation, nous vous proposons un exemple d’application que vous pouvez télécharger et utiliser pour les tests. Vous pouvez télécharger l’application, ainsi que des instructions détaillées sur son utilisation, à partir de ce [référentiel GitHub](https://github.com/adobe/alloy-samples).
