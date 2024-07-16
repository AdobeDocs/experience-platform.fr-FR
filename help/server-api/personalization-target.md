---
title: Personnalisation via Adobe Target
description: Découvrez comment utiliser l’API serveur pour diffuser et générer des expériences personnalisées créées dans Adobe Target.
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: ddffe9bf30741b457f7de1099b50ac1624fca927
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 3%

---

# Personnalisation via Adobe Target

## Vue d’ensemble {#overview}

L’API du serveur Edge Network peut fournir et générer des expériences personnalisées créées dans Adobe Target, avec l’aide du [ compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=fr).

>[!IMPORTANT]
>
>Les expériences Personalization créées via le [compositeur d’expérience visuelle (VEC) Target](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) ne sont pas entièrement prises en charge par l’API serveur. L’API serveur peut **récupérer** activités créées par le VEC, mais l’API serveur ne peut pas **rendre** activités créées par le VEC. Si vous souhaitez effectuer le rendu des activités créées par VEC, implémentez [la personnalisation hybride](../web-sdk/personalization/hybrid-personalization.md) à l’aide du SDK Web et de l’API serveur Edge Network.

## Configuration de votre flux de données {#configure-your-datastream}

Avant de pouvoir utiliser l’API serveur conjointement avec Adobe Target, vous devez activer la personnalisation Adobe Target sur votre configuration de flux de données.

Pour plus d’informations sur l’activation d’Adobe Target, reportez-vous au [guide sur l’ajout de services à un flux de données](../datastreams/overview.md#adobe-target-settings).

Lors de la configuration de votre flux de données, vous pouvez (éventuellement) fournir des valeurs pour [!DNL Property Token], [!DNL Target Environment ID] et [!DNL Target Third Party ID Namespace].

![Image de l’interface utilisateur montrant l’écran de configuration du service de flux de données, avec Adobe Target sélectionné](assets/target-datastream.png)

## Paramètres personnalisés {#custom-parameters}

La plupart des champs de la partie [!DNL XDM] de chaque requête sont sérialisés en notation par points, puis envoyés à Target sous forme de paramètres personnalisés ou [!DNL mbox].


### Exemple {#custom-parameters-example}

Compte tenu de l’exemple XDM suivant :

```json
"xdm":{
   "marketing":{
      "campaignGroup":"winter22",
      "campaignName":"homeOwnerPromo22",
      "trackingCode":"hop22"
   }
}
```

Lors de la création d’audiences dans Target, les valeurs suivantes sont disponibles en tant que paramètres personnalisés :

* `marketing.campaignGroup`
* `marketing.campaignName`
* `marketing.trackingCode`

## Mises à jour des profils Target {#profile-update}

L’ [!DNL Server API] permet des mises à jour du profil Target. Pour mettre à jour un profil Target, assurez-vous que les données de profil sont transmises dans la partie `data` de la requête au format suivant :

```json
"data":  {
    "__adobe.target": {
        "profile.eyeColor": "brown",
        "profile.hairColor": "brown"
    }
}
```

## Requête sur les activités Target {#querying-target-activities}

### Schémas {#schemas}

La partie requête de la requête détermine le contenu renvoyé par Target. Sous l’objet `personalization`, `schemas` détermine le type de contenu à renvoyer par Target.

Dans les cas où vous ne savez pas quel type d’offres vous allez récupérer, vous devez inclure les quatre schémas dans votre requête de personnalisation à l’Edge Network :

* **Offres par HTML :**
https://ns.adobe.com/personalization/html-content-item
* **Offres basées sur JSON :**
https://ns.adobe.com/personalization/json-content-item
* **Offres de redirection Target**
https://ns.adobe.com/personalization/redirect-item
* **Offres de manipulation DOM Target**
https://ns.adobe.com/personalization/dom-action

### Portées de décision {#decision-scopes}

Les noms Adobe Target [!DNL mbox] doivent être inclus dans le tableau `decisionScopes` pour renvoyer le contenu approprié.

#### Exemple {#decision-scopes-example}

Dans l’exemple ci-dessous, les quatre types d’offres sont demandés avec une activité Target appelée `serverapimbox`.

```json
"query":{
   "personalization":{
      "schemas":[
         "https://ns.adobe.com/personalization/html-content-item",
         "https://ns.adobe.com/personalization/json-content-item",
         "https://ns.adobe.com/personalization/redirect-item",
         "https://ns.adobe.com/personalization/dom-action"
      ],
      "decisionScopes":[
         "serverapimbox"
      ]
   }
}
```

## Exemple d’appel API {#api-example}

**Format d’API**

```http
POST /ee/v2/interact
```

### Requête {#request}

Vous trouverez ci-dessous une requête complète comprenant un objet XDM complet, des paramètres de profil et la requête Target appropriée.

```shell
curl -X POST 'https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org: {ORG_ID}' \
--header 'Authorization: Bearer {TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "event": {
        "xdm": {
            "eventType": "web.webpagedetails.pageViews",
            "identityMap": {
                "ECID": [
                    {
                        "id": "05907638112924484241029082405297151763",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
            },
            "web": {
                "webPageDetails": {
                    "URL": "https://alloystore.dev",
                    "name": "Home Page"
                },
                "webReferrer": {
                    "URL": ""
                }
            },
            "device": {
                "screenHeight": 1440,
                "screenWidth": 3440,
                "screenOrientation": "landscape"
            },
            "environment": {
                "type": "browser",
                "browserDetails": {
                    "viewportWidth": 3440,
                    "viewportHeight": 1440
                }
            },
            "placeContext": {
                "localTime": "2022-03-22T22:45:21.193-06:00",
                "localTimezoneOffset": 360
            },
            "timestamp": "2022-03-23T04:45:21.193Z",
            "implementationDetails": {
                "name": "https://ns.adobe.com/experience/alloy/reactor",
                "version": "1.0",
                "environment": "serverapi"
            },
            "data": {
                "__adobe": {
                    "target": {
                        "profile.eyeColor": "brown",
                        "profile.hairColor": "brown",
                        "profile.shoeColor": "black"
                    }
                }
            }
        }
    },
    "query": {
        "personalization": {
            "schemas": [
                "https://ns.adobe.com/personalization/html-content-item",
                "https://ns.adobe.com/personalization/json-content-item",
                "https://ns.adobe.com/personalization/redirect-item",
                "https://ns.adobe.com/personalization/dom-action"
            ],
            "decisionScopes": [
                "serverapimbox"
            ]
        }
    }
}'
```

### Réponse {#response}

L’Edge Network renvoie une réponse similaire à celle ci-dessous.

```json
{
   "requestId":"10959bbf-f83d-40e1-9521-d9145f19cdc5",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTQwMjgxIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"serverapimbox",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"140281"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ],
                  "characteristics":{
                     "eventToken":"xycjBJlZhwVV5MN0kMkmoGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
                  }
               },
               "items":[
                  {
                     "id":"282484",
                     "schema":"https://ns.adobe.com/personalization/json-content-item",
                     "meta":{
                        "offer.name":"/server_apiform/experiences/0/pages/0/zones/0/1648103551041",
                        "experience.id":"0",
                        "activity.name":"Server API Form",
                        "activity.id":"140281",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"282484"
                     },
                     "data":{
                        "id":"282484",
                        "format":"application/json",
                        "content":{
                           "value":"a/b json experience a",
                           "platform":"server"
                        }
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCL-pwpv9LxgBKgNPUjLwAb-pwpv9Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

Si le visiteur est admissible pour une activité de personnalisation basée sur les données envoyées à Adobe Target, le contenu de l’activité correspondante se trouve sous l’objet `handle`, où le type est `personalization:decisions`.

D’autres contenus seront parfois renvoyés sous `handle`. D’autres types de contenu ne sont pas pertinents pour la personnalisation de Target. Si le visiteur est admissible pour plusieurs activités, chaque activité sera un objet `personalization` distinct dans le tableau .

Le tableau ci-dessous explique les éléments clés de cette partie de la réponse.

| Propriété | Description | Exemple |
|---|---|---|
| `scope` | Nom de la mbox Target qui a généré les offres proposées. | `"scope": "serverapimbox"` |
| `items[].schema` | Le schéma du contenu associé à l’offre proposée. Ce lien sera lié au type d’activité que vous avez sélectionné lors de la création de l’activité de personnalisation. | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | Identifiant unique de l’activité d’offre. En règle générale, il s’agit d’un nombre à 6 chiffres. | `"activity.id": "140281"` |
| `items[].meta.activity.name` | Nom de l’activité d’offre spécifiée par l’utilisateur. Ceci est fourni lors de l’étape de création de l’activité. | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | Identifiant unique de l’expérience de personnalisation. | `"experience.id": "0"` |
| `items[].meta.experience.name` | Nom unique de l’expérience de personnalisation. | `"experience.name": "Experience A"` |
| `items[].data.id` | L’identifiant de l’offre proposée. | `"id": "282484"` |
| `items[].data.format` | Format du contenu associé à l’offre proposée. | `"format: "application/json` |
| `items[].data.content` | Contenu associé à l’offre proposée. Il sera utilisé pour la personnalisation du contenu de l&#39;application appelante. | `"content": "<CONTENT CONFIGURED IN TARGET>"` |

## Exemple d’application de personnalisation côté serveur {#sample}

L’exemple d’application trouvé à l’adresse [cette URL](https://github.com/adobe/alloy-samples/tree/main/target/personalization-server-side) illustre l’utilisation de Adobe Experience Platform pour obtenir du contenu de personnalisation d’Adobe Target. La page web change en fonction du contenu de personnalisation renvoyé.

Cet exemple ne dépend _pas_ des bibliothèques côté client telles que [!DNL Web SDK] pour obtenir du contenu de personnalisation. Il utilise plutôt les API Adobe Experience Platform pour récupérer le contenu de personnalisation. Ensuite, l’implémentation génère l’HTML côté serveur en fonction du contenu de personnalisation renvoyé.
