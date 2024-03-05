---
title: Utilisation d’Adobe Target avec le SDK Web pour la personnalisation
description: Découvrez comment effectuer le rendu du contenu personnalisé avec le SDK Web Experience Platform à l’aide d’Adobe Target
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 5%

---

# Utilisation [!DNL Adobe Target] et [!DNL Web SDK] personnalisation

[!DNL Adobe Experience Platform] [!DNL Web SDK] peut fournir et générer des expériences personnalisées gérées dans [!DNL Adobe Target] au canal web. Vous pouvez utiliser un éditeur WYSIWYG, appelé [Compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), ou une interface non visuelle, [Compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=fr), pour créer, activer et diffuser vos activités et expériences de personnalisation.

>[!IMPORTANT]
>
>Découvrez comment migrer votre mise en oeuvre Target vers le SDK Web Platform avec le [Migration de Target depuis at.js 2.x vers le SDK Web Platform](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=fr) tutoriel .
>
>Découvrez comment mettre en oeuvre Target pour la première fois avec le [Mise en oeuvre de Adobe Experience Cloud avec le SDK Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=fr) tutoriel . Pour plus d’informations spécifiques à Target, consultez la section du tutoriel intitulée [Configuration de Target avec le SDK Web de Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).


Les fonctionnalités suivantes ont été testées et sont actuellement prises en charge dans [!DNL Target]:

* [Tests A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [Rapports Impression et conversion A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=fr)
* [Activités Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Activités de ciblage d’expérience](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Tests multivariés (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Activités Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Création de rapports d’impression et de conversion Target natifs](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [Prise en charge de VEC](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Web SDK] diagramme de système

Le diagramme suivant vous aide à comprendre le workflow de [!DNL Target] et [!DNL Web SDK] prise de décision Edge.

![Diagramme de prise de décision Adobe Target Edge avec le SDK Web Platform](./assets/target-platform-web-sdk.png)

| L’appel | Détails |
| --- | --- |
| 1 | L’appareil charge la variable [!DNL Web SDK]. La variable [!DNL Web SDK] envoie une requête au réseau Edge avec des données XDM, l’identifiant d’environnement des flux de données, les paramètres transmis et l’identifiant du client (facultatif). La page (ou les conteneurs) est pré-masquée. |
| 2 | Le réseau Edge envoie la demande aux services Edge pour l’enrichir avec l’identifiant visiteur, le consentement et d’autres informations contextuelles sur le visiteur, telles que la géolocalisation et les noms conviviaux de l’appareil. |
| 3 | Le réseau Edge envoie la demande de personnalisation enrichie au [!DNL Target] Edge avec l’identifiant visiteur et les paramètres transmis. |
| 4 | Les scripts de profil s’exécutent, puis sont introduits dans [!DNL Target] stockage des profils. Le stockage des profils récupère les segments du [!UICONTROL Bibliothèque d’audiences] (par exemple, les segments partagés à partir de [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], la variable [!DNL Adobe Experience Platform]). |
| 5 | En fonction des paramètres de requête d’URL et des données de profil, [!DNL Target] détermine les activités et expériences à afficher pour le visiteur pour la page vue actuelle et pour les futures vues prérécupérées. [!DNL Target] renvoie ensuite cette information au réseau Edge. |
| 6 | a. Le réseau Edge renvoie la réponse de personnalisation à la page, y compris éventuellement les valeurs de profil pour une personnalisation supplémentaire. Le contenu personnalisé sur la page active est affiché aussi rapidement que possible sans scintillement du contenu par défaut.<br>b. Le contenu personnalisé pour les vues affichées à la suite d’actions de l’utilisateur dans une application d’une seule page (SPA) est mis en cache afin de pouvoir être appliqué instantanément sans appel au serveur supplémentaire lorsque les vues sont déclenchées. <br>. Le réseau Edge envoie l’identifiant visiteur et d’autres valeurs dans les cookies, telles que le consentement, l’ID de session, l’identité, la vérification de cookie et la personnalisation. |
| 7 | En amont du réseau Edge [!UICONTROL Analytics pour Target] (A4T) des détails (métadonnées d’activité, d’expérience et de conversion) sur la variable [!DNL Analytics] edge. |

## Activation [!DNL Adobe Target]

Pour activer [!DNL Target], procédez comme suit :

1. Activer [!DNL Target] dans votre [datastream](../../../datastreams/overview.md) avec le code client approprié.
1. Ajoutez la variable `renderDecisions` à vos événements.

Vous pouvez ensuite, éventuellement, ajouter les options suivantes :

* **`decisionScopes`**: récupérez des activités spécifiques (utiles pour les activités créées avec le compositeur d’après les formulaires) en ajoutant cette option à vos événements.
* **[Prémasquer le fragment de code](../manage-flicker.md)**: masquez uniquement certaines parties de la page.

## Utilisation du VEC d’Adobe Target

Pour utiliser le VEC avec une [!DNL Web SDK] implémentation, installez et activez l’une des options suivantes : [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) Extension d’assistance du compositeur d’expérience visuelle.

Pour plus d’informations, voir [Extension d’assistance du compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) dans le *Guide Adobe Target*.

## Rendu du contenu personnalisé

Voir [Rendu du contenu de personnalisation](../rendering-personalization-content.md) pour plus d’informations.

## Audiences dans XDM

Lors de la définition d’audiences pour votre [!DNL Target] les activités diffusées via l’ [!DNL Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr) doit être définie et utilisée. Après avoir défini des schémas XDM, des classes et des groupes de champs de schéma, vous pouvez créer un [!DNL Target] règle d’audience définie par les données XDM pour le ciblage. Within [!DNL Target], les données XDM s’affichent dans la variable [!UICONTROL Audience Builder] comme paramètre personnalisé. Le XDM est sérialisé à l’aide de la notation par points (par exemple, `web.webPageDetails.name`).

Si vous avez [!DNL Target] les activités avec des audiences prédéfinies qui utilisent des paramètres personnalisés ou un profil utilisateur ne sont pas diffusées correctement via le SDK. Au lieu d’utiliser des paramètres personnalisés pour le profil utilisateur, vous devez utiliser XDM à la place. Toutefois, des champs de ciblage d’audience d’usine sont pris en charge via le [!DNL Web SDK] qui ne nécessitent pas XDM. Ces champs sont disponibles dans la variable [!DNL Target] IU qui ne nécessite pas XDM :

* Bibliothèque Target
* Géo
* Réseau
* Système d’exploitation
* Pages du site
* Navigateur
* Sources de trafic
* Période

Pour plus d’informations, voir [Catégories d’audiences](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html) dans le *Guide Adobe Target*.

### Jetons de réponse

Les jetons de réponse sont utilisés pour envoyer des métadonnées à des tiers tels que Google ou Facebook. Les jetons de réponse sont renvoyés dans la variable `meta` champ dans `propositions` -> `items`. Voici un exemple :

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

Pour collecter les jetons de réponse, vous devez vous abonner à `alloy.sendEvent` promesse, itérer `propositions`, puis extrayez les détails de `items` -> `meta`.

Chaque `proposition` a une `renderAttempted` champ booléen indiquant si la variable `proposition` a été rendu ou non. Consultez l’exemple ci-dessous :

```js
alloy("sendEvent",
  {
    "renderDecisions": true,
    "decisionScopes": [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

Lorsque le rendu automatique est activé, le tableau de propositions contient :

#### Au chargement de la page :

* Compositeur d’après les formulaires `propositions` avec `renderAttempted` indicateur défini sur `false`
* Propositions basées sur le compositeur d’expérience visuelle `renderAttempted` indicateur défini sur `true`
* Propositions basées sur le compositeur d’expérience visuelle pour une application d’une seule page avec `renderAttempted` indicateur défini sur `true`

#### On View - change (pour les vues en mémoire cache) :

* Propositions basées sur le compositeur d’expérience visuelle pour une application d’une seule page avec `renderAttempted` indicateur défini sur `true`

Lorsque le rendu automatique est désactivé, le tableau de propositions contient :

#### Au chargement de la page :

* [!DNL Form-based Composer]-based `propositions` avec `renderAttempted` indicateur défini sur `false`
* [!DNL Visual Experience Composer]propositions basées sur les `renderAttempted` indicateur défini sur `false`
* [!DNL Visual Experience Composer]propositions basées sur une vue d’application d’une seule page avec `renderAttempted` indicateur défini sur `false`

#### On View - change (pour les vues en mémoire cache) :

* Propositions basées sur le compositeur d’expérience visuelle pour une application d’une seule page avec `renderAttempted` indicateur défini sur `false`

### Mise à jour d’un profil unique

La variable [!DNL Web SDK] permet de mettre à jour le profil vers la fonction [!DNL Target] et au [!DNL Web SDK] comme événement d’expérience.

Pour mettre à jour une [!DNL Target] , assurez-vous que les données de profil sont transmises avec les éléments suivants :

* Sous `"data {"`
* Sous `"__adobe.target"`
* Préfixe `"profile."`

| Clé | Type | Description |
| --- | --- | --- |
| `renderDecisions` | Booléen | Indique au composant de personnalisation s’il doit interpréter les actions DOM. |
| `decisionScopes` | Tableau `<String>` | Liste des portées pour lesquelles récupérer les décisions |
| `xdm` | Objet | Données formatées dans XDM qui se trouve dans le SDK Web en tant qu’événement d’expérience |
| `data` | Objet | Paires clé/valeur arbitraires envoyées à [!DNL Target] solutions sous la classe cible. |

Typique [!DNL Web SDK] Le code utilisant cette commande ressemble à ce qui suit :

**`sendEvent`avec données de profil**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**Comment envoyer des attributs de profil à Adobe Target :**

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Demande de recommandations

Le tableau suivant répertorie [!DNL Recommendations] les attributs et si chacun d’eux est pris en charge via l’ [!DNL Web SDK]:

| Catégorie | Attribut | État de la prise en charge |
| --- | --- | --- |
| Recommendations - Attributs d’entité par défaut | entity.id | Pris en charge |
|  | entity.name | Pris en charge |
|  | entity.categoryId | Pris en charge |
|  | entity.pageUrl | Pris en charge |
|  | entity.thumbnailUrl | Pris en charge |
|  | entity.message | Pris en charge |
|  | entity.value | Pris en charge |
|  | entity.inventory | Pris en charge |
|  | entity.brand | Pris en charge |
|  | entity.margin | Pris en charge |
|  | entity.event.detailsOnly | Pris en charge |
| Recommendations - Attributs d’entité personnalisés | entity.yourCustomAttributeName | Pris en charge |
| Recommendations : paramètres de mbox/page réservés | excludedIds | Pris en charge |
|  | cartIds | Pris en charge |
|  | productPurchasedId | Pris en charge |
| Page ou catégorie d’élément pour les affinités catégorielles | user.categoryId | Pris en charge |

**Comment envoyer des attributs Recommendations à Adobe Target :**

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## Débogage

mboxTrace et mboxDebug ont été abandonnés. Utilisation d’une méthode de [Débogage du SDK Web](/help/web-sdk/use-cases/debugging.md) au lieu de .

## Terminologie

__Propositions :__ Dans [!DNL Adobe Target], les propositions correspondent à l’expérience sélectionnée dans une activité.

__Schéma :__ Le schéma d’une décision est le type d’offre dans [!DNL Adobe Target].

__Portée :__ Portée de la décision. Dans [!DNL Adobe Target], la portée est la mBox. La mBox globale est la `__view__` portée.

__XDM :__ Le XDM est sérialisé en notation par points, puis placé dans [!DNL Adobe Target] comme paramètres mBox.
