---
title: Utilisation d’Adobe Target avec le SDK Web Platform
description: Découvrez comment effectuer le rendu du contenu personnalisé avec le SDK Web Experience Platform à l’aide d’Adobe Target
keywords: target;adobe target;activity.id;experience.id;renderDecisions;champ de décision;fragment de code de masquage préalable;vec;compositeur d’expérience d’après les formulaires;xdm;audiences;décisions;portée;schéma;schéma;diagramme système;diagramme
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 930756b4e10c42edf2d58be16c51d71df207d1af
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 6%

---

# Utilisation de [!DNL Adobe Target] avec la balise [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] peut fournir et générer des expériences personnalisées gérées dans  [!DNL Adobe Target] sur le canal web. Vous pouvez utiliser un éditeur WYSIWYG, appelé [compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), ou une interface non visuelle, le [compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), pour créer, activer et diffuser vos activités et expériences de personnalisation.

>[!IMPORTANT]
>
>La [documentation Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/aep-implementation/aep-web-sdk.html?lang=en) comprend des rubriques contenant des informations spécifiques au SDK Web Platform en ce qui concerne les fonctionnalités et fonctionnalités de Target.

Les fonctionnalités suivantes ont été testées et sont actuellement prises en charge dans [!DNL Target] :

* [Tests A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [Rapports d’impression et de conversion A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=fr)
* [Activités Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Activités de ciblage d’expérience](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Tests multivariés (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Les activités Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Création de rapports d’impression et de conversion Target natifs](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [Prise en charge du compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] diagramme de système

Le diagramme suivant vous aide à comprendre le processus de [!DNL Target] et de [!DNL Platform Web SDK] prise de décision en périphérie.

![Diagramme de prise de décision Adobe Target Edge avec le SDK Web Platform](./assets/target-platform-web-sdk.png)

| Appel | Détails |
| --- | --- |
| 1 | L’appareil charge la balise [!DNL Platform Web SDK]. [!DNL Platform Web SDK] envoie une requête au réseau Edge avec des données XDM, l’identifiant d’environnement des flux de données, les paramètres transmis et l’identifiant du client (facultatif). La page (ou les conteneurs) est pré-masquée. |
| 2 | Le réseau Edge envoie la demande aux services Edge pour l’enrichir avec l’identifiant visiteur, le consentement et d’autres informations contextuelles sur le visiteur, telles que la géolocalisation et les noms conviviaux de l’appareil. |
| 3 | Le réseau Edge envoie la demande de personnalisation enrichie à la périphérie [!DNL Target] avec l’identifiant visiteur et les paramètres transmis. |
| 4 | Les scripts de profil s’exécutent, puis sont introduits dans le stockage des profils [!DNL Target]. Le stockage des profils récupère les segments de la [!UICONTROL bibliothèque d’audiences] (par exemple, les segments partagés à partir de [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], la [!DNL Adobe Experience Platform]). |
| 5 | Selon les paramètres de requête d’URL et les données de profil, [!DNL Target] détermine les activités et expériences à afficher pour le visiteur pour la page vue actuelle et pour les futures vues prérécupérées. [!DNL Target] renvoie ensuite à edge network. |
| 6 | a. Le réseau Edge renvoie la réponse de personnalisation à la page, y compris éventuellement les valeurs de profil pour une personnalisation supplémentaire. Le contenu personnalisé sur la page active est affiché aussi rapidement que possible sans scintillement du contenu par défaut.<br>b. Le contenu personnalisé pour les vues affichées à la suite d’actions de l’utilisateur dans une application d’une seule page (SPA) est mis en cache afin de pouvoir être appliqué instantanément sans appel au serveur supplémentaire lorsque les vues sont déclenchées. <br>c. Le réseau Edge envoie l’identifiant visiteur et d’autres valeurs dans les cookies, telles que le consentement, l’ID de session, l’identité, la vérification de cookies, la personnalisation, etc. |
| 7 | Le réseau Edge transfère [!UICONTROL Analytics for Target] (A4T) les détails (métadonnées d’activité, d’expérience et de conversion) vers le serveur [!DNL Analytics] Edge. |

## Activation de [!DNL Adobe Target]

Pour activer [!DNL Target], procédez comme suit :

1. Activez [!DNL Target] dans votre [flux de données](../../fundamentals/datastreams.md) avec le code client approprié.
1. Ajoutez l’option `renderDecisions` à vos événements.

Vous pouvez ensuite, éventuellement, ajouter les options suivantes :

* **`decisionScopes`**: Récupérez des activités spécifiques (utiles pour les activités créées avec le compositeur basé sur les formulaires) en ajoutant cette option à vos événements.
* **[Fragment](../manage-flicker.md)** de prémasquage : Masquez uniquement certaines parties de la page.

## Utilisation du VEC d’Adobe Target

Pour utiliser le compositeur d’expérience visuelle avec une mise en oeuvre [!DNL Platform Web SDK], installez et activez [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) l’extension d’assistance du compositeur d’expérience visuelle.

Pour plus d’informations, voir [Extension d’assistance du compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) dans le *guide Adobe Target*.

## Rendu du contenu personnalisé

Voir [Rendu du contenu de personnalisation](../rendering-personalization-content.md) pour plus d’informations.

## Audiences dans XDM

Lors de la définition d’audiences pour vos activités [!DNL Target] diffusées via [!DNL Platform Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr) doit être défini et utilisé. Après avoir défini les schémas XDM, les classes et les groupes de champs de schéma, vous pouvez créer une règle d’audience [!DNL Target] définie par les données XDM pour le ciblage. Dans [!DNL Target], les données XDM s’affichent dans [!UICONTROL Audience Builder] en tant que paramètre personnalisé. Le XDM est sérialisé à l’aide de la notation par points (par exemple, `web.webPageDetails.name`).

Si vous avez des activités [!DNL Target] avec des audiences prédéfinies qui utilisent des paramètres personnalisés ou un profil utilisateur, elles ne sont pas diffusées correctement via le SDK. Au lieu d’utiliser des paramètres personnalisés pour le profil utilisateur, vous devez utiliser XDM à la place. Cependant, il existe des champs de ciblage d’audience prêts à l’emploi pris en charge par le biais de [!DNL Platform Web SDK] qui ne nécessitent pas XDM. Ces champs sont disponibles dans l’interface utilisateur [!DNL Target] qui ne nécessite pas XDM :

* Bibliothèque Target
* Géo
* Réseau
* Operating System
* Pages du site
* Navigateur
* Sources de trafic
* Période

Pour plus d’informations, voir [Catégories d’audiences](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) dans le *guide Adobe Target*.

### Jetons de réponse

Les jetons de réponse sont principalement utilisés pour envoyer des métadonnées à des tiers tels que Google, Facebook, etc. Les jetons de réponse sont renvoyés.
dans le champ `meta` dans `propositions` -> `items`. Voici un exemple :

```
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

Pour collecter les jetons de réponse, vous devez vous abonner à la promesse `alloy.sendEvent`, effectuer une itération sur `propositions`
et extrayez les détails à partir de `items` -> `meta`. Chaque `proposition` a un champ booléen `renderAttempted`
indiquant si `proposition` a été rendu ou non. Consultez l’exemple ci-dessous :

```
alloy("sendEvent",
  {
    renderDecisions: true,
    decisionScopes: [
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

* Compositeur d’après les formulaires basé sur `propositions` avec indicateur `renderAttempted` défini sur `false`
* Propositions basées sur le compositeur d’expérience visuelle avec l’indicateur `renderAttempted` défini sur `true`
* Propositions basées sur le compositeur d’expérience visuelle pour une vue d’application d’une seule page avec l’indicateur `renderAttempted` défini sur `true`

#### On View - change (pour les vues en mémoire cache) :

* Propositions basées sur le compositeur d’expérience visuelle pour une vue d’application d’une seule page avec l’indicateur `renderAttempted` défini sur `true`

Lorsque le rendu automatique est désactivé, le tableau de propositions contient :

#### Au chargement de la page :

* Compositeur d’après les formulaires basé sur `propositions` avec indicateur `renderAttempted` défini sur `false`
* Propositions basées sur le compositeur d’expérience visuelle avec l’indicateur `renderAttempted` défini sur `false`
* Propositions basées sur le compositeur d’expérience visuelle pour une vue d’application d’une seule page avec l’indicateur `renderAttempted` défini sur `false`

#### On View - change (pour les vues en mémoire cache) :

* Propositions basées sur le compositeur d’expérience visuelle pour une vue d’application d’une seule page avec l’indicateur `renderAttempted` défini sur `false`

### Mise à jour d’un profil unique

[!DNL Platform Web SDK] permet de mettre à jour le profil vers le profil [!DNL Target] et vers le [!DNL Platform Web SDK] en tant qu’événement d’expérience.

Pour mettre à jour un profil [!DNL Target], vérifiez que les données de profil sont transmises avec les éléments suivants :

* Sous `“data {“`
* Sous `“__adobe.target”`
* Préfixe `“profile.”` par exemple, comme ci-dessous

| Clé | Type | Description |
| --- | --- | --- |
| `renderDecisions` | Booléen | Indique au composant de personnalisation s’il doit interpréter les actions DOM. |
| `decisionScopes` | Tableau `<String>` | Liste des portées pour lesquelles récupérer les décisions |
| `xdm` | Objet | Données formatées dans XDM qui se trouvent dans le SDK Web Platform en tant qu’événement d’expérience |
| `data` | Objet | Paires clé/valeur arbitraires envoyées aux solutions [!DNL Target] sous la classe cible. |

Le code [!DNL Platform Web SDK] type utilisant cette commande ressemble à ce qui suit :

**`sendEvent`avec données de profil**

```
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**Comment envoyer des attributs de profil à Adobe Target :**

```
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Demande de recommandations

Le tableau suivant répertorie les attributs [!DNL Recommendations] et indique si chacun est pris en charge via [!DNL Platform Web SDK] :

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

```
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id" : "123",
        "entity.genre" : "Drama"
      }
    }
  }
});
```

## Débogage

mboxTrace et mboxDebug ont été abandonnés. Utilisez [[!DNL Platform Web SDK] le débogage](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## Terminologie

__Propositions :__ dans  [!DNL Target], les propositions correspondent à l’expérience sélectionnée dans une activité.

__Schéma :__ le schéma d’une décision est le type d’offre dans  [!DNL Target].

__Portée :__ la portée de la décision. Dans [!DNL Target], la portée est la mBox. La mBox globale est la portée `__view__`.

__XDM :__ le XDM est sérialisé en notation par point, puis placé dans  [!DNL Target] en tant que paramètres mBox.
