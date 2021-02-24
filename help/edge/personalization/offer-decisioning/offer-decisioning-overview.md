---
title: Utilisation de l'Offer decisioning avec le SDK Web de la plate-forme
description: Le Adobe Experience Platform Web SDK peut fournir et générer des offres personnalisées gérées dans l’Offer decisioning. Vous pouvez créer vos offres et d’autres objets associés à l’aide de l’interface utilisateur ou de l’API de l’Offer decisioning.
keywords: offer decisioning ; prise de décision ; SDK Web ; Platform Web SDK ; offres personnalisées ; diffuser des offres ; diffusion d'offre ; personnalisation des offres ;
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 16%

---


# Utilisation de l&#39;Offer decisioning avec le SDK Web de la plate-forme

>[!NOTE]
>
>L’utilisation d’Offer Decisioning dans le SDK web d’Adobe Experience Platform est actuellement possible en accès anticipé pour certains utilisateurs. Cette fonctionnalité n’est pas disponible pour toutes les organisations IMS.

Adobe Experience Platform [!DNL Web SDK] peut fournir et générer des offres personnalisées qui sont gérées dans l’Offer decisioning. Vous pouvez créer vos offres et autres objets associés à l’aide de l’interface utilisateur (interface utilisateur) ou des API de l’Offer decisioning.

## Conditions préalables

* L&#39;organisation IMS est activée pour la prise de décision d&#39;arête
* Offres, Activités créées
* Edge config est publié

## Terminologie

Il est important de comprendre la terminologie suivante lorsque vous travaillez avec l&#39;Offer decisioning. Pour plus d&#39;informations et pour vue des termes supplémentaires, veuillez consulter le [glossaire de l&#39;Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **Conteneur :** Un conteneur est un mécanisme d&#39;isolation qui permet de séparer les différentes préoccupations. L’ID de conteneur est le premier élément de chemin d’accès pour toutes les API du référentiel. Tous les objets de prise de décision résident dans un conteneur.

* **Etendues de décision :** Pour l’Offer decisioning, il s’agit des chaînes codées Base64 de JSON contenant les identifiants d’activité et de placement que le service d’offer decisioning doit utiliser pour proposer des offres.

   *Champ de décision JSON :*

   ```json
   {
     "activityId":"xcore:offer-activity:11cfb1fa93381aca",
     "placementId":"xcore:offer-placement:1175009612b0100c"
   }
   ```

   *Étendue de décision Chaîne codée en base64 :*

   ```json
   "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
   ```

   >[!TIP]
   >
   >Vous pouvez copier la valeur de l’étendue de la décision à partir de la page **Aperçu de l’Activité** de l’interface utilisateur.

   ![](assets/decision-scope-copy.png)

* **Configuration Edge :** pour plus d’informations, consultez la documentation sur la  [configuration ](../../fundamentals/edge-configuration.md) Edge.

* **Identité** : Pour plus d&#39;informations, veuillez lire cette documentation décrivant comment  [Platform Web SDK exploite Identity Service](../../identity/overview.md).

## Activation de l&#39;Offer decisioning

Pour activer l’Offer decisioning, vous devez effectuer les étapes suivantes :

1. Activation de Adobe Experience Platform dans votre configuration de bord [](../../fundamentals/edge-configuration.md) et cochez la case &quot;Offer decisioning&quot;
   ![offre-prise de décision-edge-config](./assets/offer-decisioning-edge-config.png)
2. Suivez les instructions pour [installer le SDK](../../fundamentals/installing-the-sdk.md) (le SDK peut être installé seul ou via [Adobe Experience Platform Launch](http://launch.adobe.com/fr). Voici un [guide de début rapide sur le Platform launch](https://docs.adobe.com/content/help/fr-FR/launch/using/intro/get-started/quick-start.html).
3. [Configurez le ](../../fundamentals/configuring-the-sdk.md) SDK pour l’Offer decisioning. D&#39;autres étapes spécifiques à l&#39;Offer decisioning sont présentées ci-dessous.
   * SDK installé autonome
      1. Configurez l&#39;action &quot;sendEvent&quot; avec votre `decisionScopes`

      ```javascript
      alloy("sendEvent", {
          ...
          "decisionScopes": [
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
          ]
      })
      ```
   * SDK platform launch installé
      1. [Création d’une propriété de Platform launch](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/admin/companies-and-properties.html)
      2. [Ajouter le code incorporé du Platform launch](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      3. Installez et configurez l&#39;extension Platform Web SDK avec la configuration Edge que vous venez de créer en sélectionnant la configuration dans la liste déroulante &quot;Edge Configuration&quot;. Documentation utile sur les [extensions](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/manage-resources/extensions/overview.html).
         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)
      4. Créez les [éléments de données](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/manage-resources/data-elements.translate.html) nécessaires. Au minimum, vous devrez créer une carte d&#39;identité du SDK Web de plate-forme et un élément de données d&#39;objet XDM SDK de plate-forme Web.
         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)
      5. Créez vos [règles](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/manage-resources/rules.translate.html).
         * Ajouter une action Envoyer le Événement d&#39;un SDK Web de plate-forme et ajouter le `decisionScopes` correspondant à la configuration de cette action
            ![send-événement-action-décisionScopes](./assets/send-event-action-decisionScopes.png)
      6. [Créez et publiez une ](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/publish/libraries.html) bibliothèque contenant toutes les règles, éléments de données et extensions appropriés que vous avez configurés.


## Exemples de demandes et de réponses

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
| `identityMap` | Oui | Consultez cette [documentation Identity Service](../../identity/overview.md). | Une identité par demande. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | Oui | Tableau de chaînes codées Base64 de JSON contenant les identifiants d’activité et de placement. | Maximum 30 `decisionScopes` par requête. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

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
| `scope` | Portée de la décision qui a abouti aux offres proposées. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | ID unique de l’activité d’offre. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | ID unique de l’emplacement de l’offre. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | ID de l’offre proposée. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Schéma du contenu associé à l&#39;offre proposée. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | ID de l’offre proposée. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Format du contenu associé à l&#39;offre proposée. | `"format": "text/html"` |
| `language` | Tableau de langues associées au contenu de l&#39;offre proposée. | `"language": [ "en-US" ]` |
| `content` | Contenu associé à l’offre proposée au format d’une chaîne. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenu de l’image associé à l’offre proposée au format d’une URL. | `"deliveryURL": "https://image.jpeg"` |
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
| `identityMap` | Oui | Consultez cette [documentation Identity Service](../../identity/overview.md). | Une identité par demande. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | Oui | Tableau de chaînes codées Base64 de JSON contenant les identifiants d’activité et de placement. | Maximum 30 `decisionScopes` par requête. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

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
| `scope` | Portée de la décision qui a abouti aux offres proposées. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | ID unique de l’activité d’offre. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | ID unique de l’emplacement de l’offre. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | ID de l’offre proposée. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | Schéma du contenu associé à l&#39;offre proposée. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | ID de l’offre proposée. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | Format du contenu associé à l&#39;offre proposée. | `"format": "text/text"` |
| `language` | Tableau de langues associées au contenu de l&#39;offre proposée. | `"language": [ "en-US" ]` |
| `content` | Contenu associé à l’offre proposée au format d’une chaîne. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenu de l’image associé à l’offre proposée au format d’une URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Caractéristiques associées à l’offre proposée au format d’un objet JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
