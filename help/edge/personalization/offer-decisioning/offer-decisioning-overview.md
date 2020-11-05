---
title: Présentation d’Offer Decisioning
seo-title: Offer Decisioning et Adobe Experience Platform Web SDK
description: Le Adobe Experience Platform Web SDK peut fournir et générer des offres personnalisées gérées dans Offer Decisioning. Vous pouvez créer vos offres et d’autres objets associés à l’aide de l’interface utilisateur ou de l’API Offer Decisioning.
seo-description: Le Adobe Experience Platform Web SDK peut fournir et générer des offres personnalisées gérées dans Offer Decisioning. Vous pouvez créer vos offres et d’autres objets associés à l’aide de l’interface utilisateur ou de l’API Offer Decisioning.
keywords: offer decisioning;decisioning;Web SDK;Platform Web SDK;personalized offers;deliver offers;offer delivery;offer personalization;
translation-type: tm+mt
source-git-commit: 86d819daf26eaf1b46afe76054d475e61720dd27
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 10%

---


# [!DNL Offer Decisioning] Présentation

>[!NOTE]
>
>L’utilisation de Offer Decisioning dans Adobe Experience Platform Web SDK est actuellement disponible en accès rapide pour certains utilisateurs. Cette fonctionnalité n&#39;est pas disponible pour toutes les organisations IMS.

Le Adobe Experience Platform [!DNL Web SDK] peut fournir et générer des offres personnalisées qui sont gérées dans Offer Decisioning. Vous pouvez créer vos offres et d’autres objets associés à l’aide de l’interface utilisateur ou des API Offer Decisioning.

## Prérequis

* L&#39;organisation IMS est activée pour la prise de décision d&#39;arête
* Offres, Activités créées
* Edge config est publié

## Terminologie

Il est important de comprendre la terminologie suivante lorsque vous travaillez avec Offer Decisioning. Pour plus d&#39;informations et pour vue des termes supplémentaires, veuillez visiter le glossaire [](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html?lang=en#get-started)Offer Decisioning.

* **Conteneur :** Un conteneur est un mécanisme d&#39;isolation qui permet de séparer les différentes préoccupations. L’ID de conteneur est le premier élément de chemin d’accès pour toutes les API du référentiel. Tous les objets de prise de décision résident dans un conteneur.

* **Etendues de décision :** Pour Offer Decisioning, il s’agit des chaînes codées Base64 de JSON contenant les identifiants d’activité et de placement que vous souhaitez que le service de prise de décision d’offre utilise pour proposer des offres.

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
   >Vous pouvez copier la valeur de la portée de la décision depuis la page Aperçu **de l’** Activité de l’interface utilisateur.

   ![](assets/decision-scope-copy.png)

* **Configuration Edge :** Pour plus d&#39;informations, consultez la documentation sur la configuration [des](../../fundamentals/edge-configuration.md) bords.

* **Identité**: Pour plus d&#39;informations, veuillez lire cette documentation décrivant comment [Platform Web SDK exploite Identity Service](../../identity/overview.md).

## Activation de Offer Decisioning

Pour activer Offer Decisioning, vous devez effectuer les étapes suivantes :

1. Activation de Adobe Experience Platform dans votre configuration [de](../../fundamentals/edge-configuration.md) bord et cochez la case &quot;Offer Decisioning&quot;
   ![offre-prise de décision-edge-config](./assets/offer-decisioning-edge-config.png)
2. Suivez les instructions pour [installer le SDK](../../fundamentals/installing-the-sdk.md) (le SDK peut être installé seul ou via [Adobe Experience Platform Launch](http://launch.adobe.com/fr). Voici un guide de début [rapide pour le lancement](https://docs.adobe.com/content/help/fr-FR/launch/using/intro/get-started/quick-start.html)de plateformes.
3. [Configurez le SDK](../../fundamentals/configuring-the-sdk.md) pour Offer Decisioning. D&#39;autres étapes spécifiques à Offer Decisioning sont présentées ci-dessous.
   * SDK installé autonome
      1. Configurez l’action &quot;sendEvent&quot; avec votre `decisionScopes`

      ```javascript
      alloy("sendEvent", {
          ...
          "decisionScopes": [
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
          ]
      })
      ```
   * Kit SDK installé pour le lancement de plate-forme
      1. [Créer une propriété de lancement de plate-forme](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/admin/companies-and-properties.html)
      2. [Ajouter le code incorporé de lancement de plateforme](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      3. Installez et configurez l’extension Adobe Experience Platform Web SDK avec la configuration Edge que vous venez de créer en sélectionnant la configuration dans la liste déroulante &quot;Edge Configuration&quot;. Documentation utile sur les [extensions](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/manage-resources/extensions/overview.html).
         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)
      4. Créez les éléments [de](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/manage-resources/data-elements.translate.html)données nécessaires. Au minimum, vous devrez créer une carte d&#39;identité du SDK Web de plate-forme et un élément de données d&#39;objet XDM SDK de plate-forme Web.
         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)
      5. Créez vos [règles](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/manage-resources/rules.translate.html).
         * Ajouter une action Envoyer le Événement d&#39;un SDK Web de plate-forme et ajouter les éléments appropriés `decisionScopes` à la configuration de cette action
            ![send-événement-action-décisionScopes](./assets/send-event-action-decisionScopes.png)
      6. [Créez et publiez une bibliothèque](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/publish/libraries.html) contenant toutes les règles, éléments de données et extensions appropriés que vous avez configurés.


## Exemples de demandes et de réponses

### Une `decisionScopes` valeur

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
| `identityMap` | Oui | Reportez-vous à cette documentation [du service](../../identity/overview.md)d&#39;identité. | Une identité par demande. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | Oui | Tableau de chaînes codées Base64 de JSON contenant les identifiants d’activité et de placement. | Maximum 30 `decisionScopes` par demande. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

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
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
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
| `items.id` | ID de l’offre proposée. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Schéma du contenu associé à l&#39;offre proposée. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | ID de l’offre proposée. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Format du contenu associé à l&#39;offre proposée. | `"format": "text/html"` |
| `language` | Tableau de langues associées au contenu de l&#39;offre proposée. | `"language": [ "en-US" ]` |
| `content` | Contenu associé à l’offre proposée au format d’une chaîne. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenu de l’image associé à l’offre proposée au format d’une URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Caractéristiques associées à l’offre proposée au format d’un objet JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### Plusieurs `decisionScopes` valeurs

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
| `identityMap` | Oui | Reportez-vous à cette documentation [du service](../../identity/overview.md)d&#39;identité. | Une identité par demande. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | Oui | Tableau de chaînes codées Base64 de JSON contenant les identifiants d’activité et de placement. | Maximum 30 `decisionScopes` par demande. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

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
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p style="color:red;">20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
          "items": [
            {
              "id": "xcore:personalized-offer:235fe313094cdb75",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "data": {
                "id": "xcore:personalized-offer:235fe313094cdb75",
                "format": "text/text",
                "language": [
                  "en-US"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2",
                  "foo3": "bar3"
                }
              }
            }
          ]
        }
      ],
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ==",
          "items": [
            {
              "id": "xcore:personalized-offer:312de312095cda65",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "data": {
                "id": "xcore:personalized-offer:312de312095cda65",
                "format": "image/png",
                "language": [
                  "en-US"
                ],
                "deliveryURL": "https://image.jpeg"
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
| `items.id` | ID de l’offre proposée. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Schéma du contenu associé à l&#39;offre proposée. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | ID de l’offre proposée. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Format du contenu associé à l&#39;offre proposée. | `"format": "text/html"` |
| `language` | Tableau de langues associées au contenu de l&#39;offre proposée. | `"language": [ "en-US" ]` |
| `content` | Contenu associé à l’offre proposée au format d’une chaîne. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenu de l’image associé à l’offre proposée au format d’une URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Caractéristiques associées à l’offre proposée au format d’un objet JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |