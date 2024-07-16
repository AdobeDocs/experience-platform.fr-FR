---
title: Utilisation de l’Offer decisioning avec le SDK Web Platform
description: Le SDK Web de Adobe Experience Platform peut diffuser et générer des offres personnalisées gérées dans Offer Decisioning. Vous pouvez créer vos offres et d’autres objets associés à l’aide de l’interface utilisateur ou de l’API Offer Decisioning.
keywords: offer decisioning;prise de décision;SDK Web;SDK Web Platform;offres personnalisées;diffuser des offres;diffusion d’offres;personnalisation des offres ;
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: 22477c11a977059849d9b47871a5c2aef1da4b24
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 12%

---

# Utilisation de l’Offer decisioning avec le SDK Web Platform

>[!NOTE]
>
>L’utilisation d’Offer Decisioning dans le SDK Web de Adobe Experience Platform est disponible en accès anticipé pour certains utilisateurs. Cette fonctionnalité n’est pas disponible pour toutes les organisations 

Adobe Experience Platform [!DNL Web SDK] peut diffuser et générer des offres personnalisées gérées en Offer decisioning. Vous pouvez créer vos offres et d’autres objets associés à l’aide de l’interface utilisateur (IU) ou des API d’Offer decisioning.

## Conditions préalables

* L’organisation est activée pour la prise de décision Edge
* Offres, Activités créées
* Datastream est publié

## Terminologie

Il est important de comprendre la terminologie suivante lorsque vous utilisez Offer Decisioning. Pour plus d’informations et pour afficher des termes supplémentaires, consultez le [glossaire Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **Portées de décision :** Pour l’Offer decisioning, les portées de décision sont les chaînes codées Base64 de JSON contenant l’activité et les ID d’emplacement que le service d’offer decisioning doit utiliser pour proposer des offres.

  *JSON de portée de décision :*

  ```json
  {
    "activityId":"xcore:offer-activity:11cfb1fa93381aca",
    "placementId":"xcore:offer-placement:1175009612b0100c"
  }
  ```

  *Chaîne codée de la portée de décision Base64 :*

  ```json
  "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
  ```

  >[!TIP]
  >
  >Vous pouvez copier la valeur de la portée de décision à partir de la page **Activity Overview** dans l’interface utilisateur.

  ![Paramètres de copie de décision.](assets/decision-scope-copy.png)

* **Datastreams:** Pour plus d’informations, consultez la documentation [datastreams](/help/datastreams/overview.md).

* **Identity** : Pour plus d’informations, consultez cette documentation décrivant comment [Platform Web SDK utilise Identity Service](../../identity/overview.md).

## Activation de l’Offer decisioning

Pour activer l’Offer decisioning, procédez comme suit :

1. Activation de Adobe Experience Platform dans votre [datastream](/help/datastreams/overview.md) et cochez la case &quot;Offer decisioning&quot;

   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)

1. Suivez les instructions pour [installer le SDK](/help/web-sdk/install/overview.md) (le SDK peut être installé autonome ou via l’interface utilisateur). Pour plus d’informations, consultez le [guide de démarrage rapide des balises](/help/tags/quick-start/quick-start.md).
1. Configurez le SDK pour Offer decisioning à l’aide de `personalization.decisionScopes`. Vous trouverez ci-dessous d’autres étapes spécifiques à l’Offer decisioning.

   * Installation du SDK autonome

      1. Configuration de l’action &quot;sendEvent&quot; avec `personalization.decisionScopes`

     ```javascript
     alloy("sendEvent", {
       ...
       "personalization": {
         "decisionScopes": [
           "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
           "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
         ]
       }
     });
     ```

   * Installation du SDK par le biais de balises

      1. [Créer une propriété de balise](/help/tags/ui/administration/companies-and-properties.md)
      1. [Ajouter du code incorporé](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html?lang=fr)
      1. Installez et configurez l’extension SDK Web Platform avec le Datastream que vous avez créé en sélectionnant la configuration dans la liste déroulante &quot;Datastream&quot;. Consultez la documentation relative aux [extensions](/help/tags/ui/managing-resources/extensions/overview.md).

         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)

      1. Créez les [Éléments de données](/help/tags/ui/managing-resources/data-elements.md) nécessaires. Au minimum, vous devez créer un mappage d’identité SDK web Platform et un élément de données objet XDM du SDK web Platform.

         ![ identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)

      1. Créez vos [Règles](/help/tags/ui/managing-resources/rules.md).

         * Ajoutez une action Envoyer l’événement du SDK Web Platform et ajoutez le `decisionScopes` approprié à la configuration de cette action.

         ![send-event-action-décisionScopes](./assets/send-event-action-decisionScopes.png)

      1. [ Créez et publiez une bibliothèque ](/help/tags/ui/publishing/libraries.md) contenant toutes les règles, éléments de données et extensions que vous avez configurés.

## Exemples de requêtes et de réponses

### Une valeur `decisionScopes`

**Requête**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
          ]
        }
      }
    }
  ]
}
```

| Propriété | Obligatoire | Description | Limites | Exemple |
|---|---|---|---|---|
| `identityMap` | Oui | Reportez-vous à cette [documentation Identity Service](../../identity/overview.md). | Une identité par demande. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Remarque : Les utilisateurs n’ont pas besoin d’inclure le paramètre `ECID` dans l’appel API. Si nécessaire, ce paramètre est automatiquement ajouté à l’appel . |
| `decisionScopes` | Oui | Tableau de chaînes codées Base64 de JSON contenant les identifiants d’activité et d’emplacement. | Maximum 30 `decisionScopes` par requête. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

**Réponse**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p>20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| Propriété | Description | Exemple |
|---|---|---|
| `scope` | Portée de décision qui a abouti aux offres proposées. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | Identifiant unique de l’activité d’offre. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | Identifiant unique de l’emplacement de l’offre. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | L’identifiant de l’offre proposée. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Le schéma du contenu associé à l’offre proposée. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | L’identifiant de l’offre proposée. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Format du contenu associé à l’offre proposée. | `"format": "text/html"` |
| `language` | Tableau de langues associées au contenu de l’offre proposée. | `"language": [ "en-US" ]` |
| `content` | Contenu associé à l’offre proposée au format d’une chaîne. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenu de l&#39;image associé à l&#39;offre proposée au format d&#39;une URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Caractéristiques associées à l’offre proposée au format d’un objet JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### Plusieurs valeurs `decisionScopes`

**Requête**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ=="
          ]
        }
      }
    }
  ]
}
```

| Propriété | Obligatoire | Description | Limites | Exemple |
|---|---|---|---|---|
| `identityMap` | Oui | Reportez-vous à cette [documentation Identity Service](../../identity/overview.md). | Une identité par demande. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Remarque : Les utilisateurs n’ont pas besoin d’inclure le paramètre `ECID` dans l’appel API. Si nécessaire, ce paramètre est automatiquement ajouté à l’appel . |
| `decisionScopes` | Oui | Tableau de chaînes codées Base64 de JSON contenant les identifiants d’activité et d’emplacement. | Maximum 30 `decisionScopes` par requête. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

**Réponse**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MTEyMyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDExMjMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381123",
            "etag": "1"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b01123",
            "etag": "3"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a22954123",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "etag": "2",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a22954123",
                "format": "text/text",
                "language": [
                  "en"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2"
                }
              }
            }
          ]
        },
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a2295415d",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a2295415d",
                "format": "image/png",
                "language": [
                  "en"
                ],
                "deliveryURL": "https://image.jpeg",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| Propriété | Description | Exemple |
|---|---|---|
| `scope` | Portée de décision qui a abouti aux offres proposées. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | Identifiant unique de l’activité d’offre. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | Identifiant unique de l’emplacement de l’offre. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | L’identifiant de l’offre proposée. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | Le schéma du contenu associé à l’offre proposée. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | L’identifiant de l’offre proposée. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | Format du contenu associé à l’offre proposée. | `"format": "text/text"` |
| `language` | Tableau de langues associées au contenu de l’offre proposée. | `"language": [ "en-US" ]` |
| `content` | Contenu associé à l’offre proposée au format d’une chaîne. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenu de l&#39;image associé à l&#39;offre proposée au format d&#39;une URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Caractéristiques associées à l’offre proposée au format d’un objet JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

## Limites

Certaines contraintes d’offre ne sont actuellement pas prises en charge avec les workflows d’Edge Network mobile, par exemple la limitation. La valeur du champ Limitation indique le nombre de fois où une offre peut être présentée à tous les utilisateurs. Pour plus d’informations, voir [Documentation sur les règles d’éligibilité et les contraintes d’offres](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html#eligibility).
