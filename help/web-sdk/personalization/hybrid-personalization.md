---
title: Personnalisation hybride à l’aide des API Web SDK et Edge Network
description: Cet article explique comment utiliser Web SDK conjointement avec l’API Edge Network pour déployer une personnalisation hybride sur vos propriétés web.
keywords: personnalisation;hybride;api du serveur;côté serveur;implémentation hybride;
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 41%

---

# Personnalisation hybride à l’aide des API Web SDK et Edge Network

## Vue d’ensemble {#overview}

La personnalisation hybride décrit le processus de récupération du contenu de personnalisation côté serveur, à l’aide de l’API [Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/), et de le rendre côté client, à l’aide du [SDK Web](../home.md).

Vous pouvez utiliser la personnalisation hybride avec des solutions de personnalisation telles qu’Adobe Target, Adobe Journey Optimizer ou Offer Decisioning, la différence étant le contenu de la payload de l’[!UICONTROL API Edge Network].

## Conditions préalables {#prerequisites}

Avant d’implémenter une personnalisation hybride sur vos propriétés web, assurez-vous de respecter les conditions suivantes :

* Vous avez choisi la solution de personnalisation que vous souhaitez utiliser. Cela aura un impact sur le contenu de la payload de l’[!UICONTROL API Edge Network].
* Vous avez accès à un serveur d’applications que vous pouvez utiliser pour effectuer les appels de l’[!UICONTROL API Edge Network].
* Vous avez accès à l’[API Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/).
* Vous avez correctement [configuré](/help/web-sdk/commands/configure/overview.md) et déployé le Web SDK sur les pages que vous souhaitez personnaliser.

## Diagramme de flux {#flow-diagram}

Le diagramme de flux ci-dessous décrit l’ordre des étapes effectuées pour fournir une personnalisation hybride.

![Diagramme de flux visuel présentant l’ordre des étapes effectuées pour fournir une personnalisation hybride.](assets/hybrid-personalization-diagram.png)

1. Tout cookie existant précédemment stocké par le navigateur, précédé de `kndctr_`, est inclus dans la demande du navigateur.
1. Le navigateur web client demande la page web à votre serveur d’applications.
1. Lorsque le serveur d’applications reçoit la requête de page, il effectue une requête `POST` au point d’entrée de la collecte de données interactive de l’API [Edge Network](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) afin de récupérer du contenu de personnalisation. La requête `POST` contient un `event` et une `query`. S’ils sont disponibles, les cookies de l’étape précédente sont inclus dans le tableau `meta>state>entries`.
1. L’API Edge Network renvoie le contenu de personnalisation à votre serveur d’applications.
1. Le serveur d’applications renvoie une réponse HTML au navigateur client, contenant les [cookies d’identité et de cluster](#cookies).
1. Sur la page client, la commande [!DNL Web SDK] `applyResponse` est appelée, en transmettant les en-têtes et le corps de la réponse [!UICONTROL API Edge Network] de l’étape précédente.
1. Le [!DNL Web SDK] effectue automatiquement le rendu des offres Target [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=fr) et des éléments du canal web Journey Optimizer, car l’indicateur `renderDecisions` est défini sur `true`.
1. Les offres [!DNL HTML]/[!DNL JSON] basées sur des formulaires de Target et les expériences basées sur du code Journey Optimizer sont appliquées manuellement par l’intermédiaire de la méthode `applyProposition` afin de mettre à jour le [!DNL DOM] en fonction du contenu de personnalisation de la proposition.
1. Pour les offres [!DNL HTML]/[!DNL JSON] basées sur des formulaires de Target et les expériences basées sur du code de Journey Optimizer, les événements d’affichage doivent être envoyés manuellement pour indiquer le moment où le contenu renvoyé a été affiché. Cela s’effectue via la commande `sendEvent`.

## Cookies {#cookies}

Les cookies sont utilisés pour conserver l’identité de l’utilisateur et les informations de cluster.  Lors de l’utilisation d’une implémentation hybride, le serveur d’applications web gère le stockage et l’envoi de ces cookies pendant le cycle de vie des requêtes.

| Cookie | Rôle | Stocké par | Envoyé par |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Contient des détails de l’identité de l’utilisateur. | Serveur d’applications | Serveur d’applications |
| `kndctr_AdobeOrg_cluster` | Indique quel cluster Edge Network doit être utilisé pour répondre aux requêtes. | Serveur d’applications | Serveur d’applications |

## Demander l’emplacement {#request-placement}

Les requêtes d’API Edge Network sont nécessaires pour obtenir des propositions et envoyer une notification d’affichage. Lors de l’utilisation d’une implémentation hybride, le serveur d’applications envoie ces requêtes à l’API Edge Network.

| Requête | Créée par |
|---|---|
| Requête d’interaction pour récupérer des propositions | Serveur d’applications |
| Requête d’interaction pour envoyer des notifications d’affichage | Serveur d’applications |


## Définir l’hôte régional Edge Network {#regional-host}

Pour établir l’hôte régional Edge Network, lisez d’abord l’indice d’emplacement du cookie `kndctr_<orgId>_AdobeOrg_cluster`, qui peut avoir les valeurs suivantes :

* `va6`
* `or2`
* `irl1`
* `ind1`
* `sgp3`
* `jpn3`
* `aus3`

Exemple : `kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_cluster: va6`

L’hôte régional Edge Network utilise le format suivant :`<location_hint>.server.adobedc.net` et peut avoir les valeurs suivantes :

* `va6.server.adobedc.net`
* `or2.server.adobedc.net`
* `irl1.server.adobedc.net`
* `ind1.server.adobedc.net`
* `sgp3.server.adobedc.net`
* `jpn3.server.adobedc.net`
* `aus3.server.adobedc.net`

En utilisant ces hôtes spécifiques, les requêtes seront dirigées vers le même emplacement Edge Network que celui visité précédemment par l’utilisateur. Le système sera en mesure de fournir la meilleure expérience, car les données utilisateur y sont présentes.

Si aucune indication d’emplacement (c’est-à-dire aucun cookie) n’est présente, utilisez l’hôte par défaut : `server.adobedc.net`.

>[!TIP]
>
>Il est recommandé d’utiliser une liste d’emplacements autorisés. Cela empêche toute altération de l’indicateur d’emplacement, car il est fourni via des cookies côté client.

## Implications Analytics {#analytics}

Lors de l’implémentation d’une personnalisation hybride, vous devez faire particulièrement attention à ce que les accès aux pages ne soient pas comptabilisés plusieurs fois dans Analytics.

Lorsque vous [configurez un flux de données](../../datastreams/overview.md) dans Analytics, les événements sont automatiquement transférés afin que les accès à la page soient capturés.

L’exemple de cette mise en œuvre utilise deux flux de données différents :

* Un flux de données configuré pour Analytics. Ce flux de données est utilisé pour les interactions du SDK Web.
* Un second flux de données sans configuration Analytics. Ce flux de données est utilisé pour les requêtes d’API Edge Network. Vous devez configurer ce flux de données avec la même configuration de destination que celle du flux de données que vous avez configuré pour Analytics.

Ainsi, la requête côté serveur n’enregistre aucun événement Analytics, contrairement aux requêtes côté client. Cela entraîne un comptage précis des requêtes Analytics.

## Créer la requête côté serveur {#server-side-request}

L’exemple de requête ci-dessous illustre une requête d’API Edge Network que votre serveur d’applications peut utiliser pour récupérer le contenu de personnalisation.

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
         "entries": [{
           "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
           "value":"CiY0NzE0NzkwMTUyMzYzMzI4NDAxMjc3NDcwNzA2NTcxMjI3OTI1NVIRCJ_S-uCRMRABGAEqBElSTDHwAZ_S-uCRMQ=="
         }, {
           "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
           "value": "general=in"
         }, {
            "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_cluster",
            "value": "va6"
         }]
      }
   }
}'
```

| Paramètre | Type | Obligatoire | Description |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Oui. | L’identifiant du flux de données que vous utilisez pour transmettre les interactions à Edge Network. Voir la [présentation des flux de données](../../datastreams/overview.md) pour savoir comment configurer un flux de données. |
| `requestId` | `String` | Non | Un identifiant aléatoire permettant de corréler les requêtes internes du serveur. Si aucun n’est fourni, le Edge Network en génère un et le renvoie dans la réponse. |

### En-têtes de proxy {#proxy-headers}

Les en-têtes suivants sont requis pour traiter correctement la requête.

* `Referer`
* `X-Forwarded-For`
* `X-Forwarded-Proto`
* `X-Forwarded-Host`

Veillez à les définir correctement pour pointer vers les informations réelles du client. Par exemple, l’en-tête `X-Forwarded-For` doit contenir l’adresse IP du client pour qu’une géolocalisation correcte soit effectuée.

### En-têtes User-Agent {#user-agent-headers}

Utilisez les en-têtes user-agent suivants pour traiter correctement la requête.

**Par défaut**

* `User-Agent`

**Faible entropie (obligatoire) :**

* `Sec-CH-UA`
* `Sec-CH-UA-Mobile`
* `Sec-CH-UA-Platform`

**entropie élevée (facultatif) :**

* `Sec-CH-UA-Platform-Version`
* `Sec-CH-UA-Arch`
* `Sec-CH-UA-Model`
* `Sec-CH-UA-Bitness`
* `Sec-CH-UA-WoW64`

La requête doit être envoyée comme indiqué dans la spécification [API Edge Network](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/). Consultez la [documentation sur la personnalisation](https://developer.adobe.com/data-collection-apis/docs/getting-started/personalization/) si votre cas d’utilisation le requiert.

### Réponse côté serveur {#server-response}

La réponse d’Edge Network contiendra des instructions `state:store`, qui doivent être transformées en en-têtes `Set-Cookie`. Ils sont enregistrés dans le navigateur et peuvent être utilisés par l’implémentation de Web SDK.

Les cookies doivent être définis sur le domaine de niveau supérieur, de sorte qu’ils soient envoyés avec les requêtes à l’implémentation du serveur et à celle du client. (Ou au moins un sous-domaine commun utilisé par les deux mises en œuvre)

Exemple :

* Les appels côté serveur utilisent `api.example.com`
* Les appels côté client utilisent `adobe.example.com`

Les cookies doivent être définis sur `.example.com` afin qu’ils soient partagés dans les deux cas.

La réponse côté serveur est organisée en fragments appelés `Handles`, qui sont générés en fonction de la configuration du train de données. Par exemple, les moteurs de personnalisation en temps réel renvoient des descripteurs `personalization:decisions`, tandis que le moteur d’activation en temps réel génère des descripteurs `activation:pull`.

L’exemple de réponse ci-dessous montre à quoi pourrait ressembler la réponse de l’API Edge Network.

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
