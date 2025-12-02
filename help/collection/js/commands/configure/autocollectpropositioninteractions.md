---
title: autoCollectPropositionInteractions
description: Collecter automatiquement des données lorsqu’un utilisateur clique sur un lien.
exl-id: c70db76a-3f2f-45a6-86ab-36efcb18d20f
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# `autoCollectPropositionInteractions`

La propriété `autoCollectPropositionInteractions` est un paramètre facultatif qui détermine si le SDK Web collecte automatiquement les interactions de proposition. La valeur est une carte des fournisseurs de décision, chacun avec une valeur indiquant la manière dont les interactions de proposition automatiques doivent être traitées.

Lorsque vous activez le suivi automatique des interactions de propositions, tous les clics dans un élément de proposition rendu au DOM sont automatiquement collectés par le SDK Web. Cette collection comprend toutes les expériences automatiquement rendues au DOM par le SDK Web et les expériences rendues au DOM à l’aide de la commande [`applyPropositions`](../applypropositions.md).

Si vous omettez cette propriété lors de la configuration de Web SDK, elle est définie par défaut sur `{"AJO": "always", "TGT": "never"}`. Si vous préférez ne pas suivre automatiquement les interactions de proposition, définissez la valeur sur `{"AJO": "never", "TGT": "never"}`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "autoCollectPropositionInteractions": {
    "AJO": "always",
    "TGT": "never"
  }
});
```

Les propriétés prises en charge dans cet objet sont les suivantes :

| Propriété | Description |
| --- | --- |
| **`AJO`** | Adobe Journey Optimizer. |
| **`TGT`** | Adobe Target. |

Les valeurs possibles pour chaque propriété sont les suivantes :

| Valeur | Description |
| --- | --- |
| **`always`** | Collectez toujours automatiquement les événements `interact` pour les éléments associés à une proposition. |
| **`never`** | Ne collectez jamais automatiquement les événements `interact` pour les éléments associés à une proposition. |
| **`decoratedElementsOnly`** | Collecter automatiquement les événements `interact` pour les éléments associés à une proposition si l&#39;élément inclut des attributs de données spécifiant un libellé ou un jeton. |

## Attributs de données {#data-attributes}

Vous pouvez utiliser des attributs de données sur les éléments pour ajouter de la spécificité à une interaction.

| Nom | Attribut de données | Description |
| --- | --- | --- |
| **[!UICONTROL Label]** | `data-aep-click-label` | Lorsque l’attribut de données de libellé est présent sur un élément sur lequel l’utilisateur a cliqué, il est inclus dans les détails d’interaction envoyés à Edge Network. Le SDK Web recherche un attribut de données de libellé commençant par l’élément sur lequel l’utilisateur a cliqué et remontant l’arborescence DOM. Le SDK Web utilise le premier libellé trouvé. |
| **[!UICONTROL Token]** | `data-aep-click-token` | Utilisez ce jeton lors de l’utilisation des politiques de décision dans les campagnes basées sur le code [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/code-based-experience/get-started-code-based). Vous pouvez utiliser le jeton pour distinguer l’élément de politique de décision sur lequel l’utilisateur a cliqué. Lorsque l’attribut de données de jeton est présent sur un élément sur lequel l’utilisateur a cliqué, il est inclus dans les détails d’interaction envoyés à Edge Network. Le SDK Web recherche un attribut de données de jeton commençant par l’élément sur lequel l’utilisateur a cliqué et remontant l’arborescence DOM. Le SDK Web utilise le premier jeton qu’il trouve. |
| **[!UICONTROL Interact ID]** | `data-aep-interact-id` | Le SDK Web ajoute automatiquement cet identifiant unique aux éléments de conteneur lors du rendu des propositions. Le SDK Web utilise cet identifiant pour corréler les éléments DOM aux propositions. Comme il s’agit d’un identifiant requis par le SDK Web, vous ne devez pas le modifier du tout. Vous pouvez l’ignorer en toute sécurité. |

## Exemple

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/alpha.jpg" class="poster" />
    <h2>Example Movie Alpha</h2>
    <p class="description"> A lighthearted story about exploration and friendship set on a distant world. Follow a curious rover who discovers that small actions can lead to big changes.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Alpha">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/bravo.jpg" class="poster" />
    <h2>Example Movie Bravo</h2>
    <p class="description">An uplifting tale of a determined chef who overcomes unlikely odds to create culinary masterpieces in a bustling city bistro.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Bravo">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/charlie.jpg" class="poster" />
    <h2>Example Movie Charlie</h2>
    <p class="description">A vibrant adventure following a young musician who journeys into a fantastical realm to find the true meaning of family and tradition.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Charlie">View details</button>
    </p>
  </div>
</div>
```

### Utilisation de `autoCollectPropositionInteractions` avec la commande `applyPropositions` {#apply-propositions}

La commande [`applyPropositions`](../applypropositions.md) est un moyen pratique de rendre des propositions dans le DOM. Cependant, dans le cas de campagnes basées sur du code avec JSON, vous pouvez utiliser cette commande pour corréler un élément DOM existant (ou celui que le code de votre application a rendu à l’écran en fonction des valeurs JSON) à une proposition.

Cette corrélation active le suivi automatique des interactions pour cet élément et attribue à cet élément la proposition appropriée. Pour ce faire, définissez la `actionType` sur `track`.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://example.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://example.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## Configuration des interactions de proposition automatiques pour l&#39;extension de balise Web SDK

Les deux menus déroulants suivants lors de la configuration de l’extension de balise Web SDK sont l’équivalent de balise de cet objet :

* [[!UICONTROL Auto click collection for Adobe Journey Optimizer]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-journey-optimizer)
* [[!UICONTROL Auto click collection for Adobe Target]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-target)
