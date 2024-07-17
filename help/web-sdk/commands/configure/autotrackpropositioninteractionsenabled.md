---
title: autoTrackPropositionInteractionsEnabled
description: Découvrez comment configurer le SDK Web Experience Platform pour collecter automatiquement les données de lien.
source-git-commit: ec5fd1c8228388ced96f58476e0174c8a0ff00df
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---


# `autoTrackPropositionInteractionsEnabled`

La propriété `autoTrackPropositionInteractionsEnabled` est un paramètre facultatif qui détermine si le SDK Web doit automatiquement collecter les interactions de proposition.

La valeur est une carte des fournisseurs de décision, chacun avec une valeur qui indique comment les interactions automatiques de proposition doivent être gérées.

## Valeurs compatibles {#supported-values}

Par défaut, les interactions de proposition automatique sont _always_ collectées pour Adobe Journey Optimizer (`AJO`) et _never_ collectées pour Adobe Target (`TGT`).

La valeur par défaut de `autoTrackPropositionInteractions` est illustrée ci-dessous.

```json
{
  "AJO": "always",
  "TGT": "never"
}
```

Reportez-vous au tableau ci-dessous pour connaître les valeurs de configuration prises en charge pour chaque fournisseur de décision.

| Valeur | Description |
| --- | --- |
| `always` | [!DNL Web SDK] collectera toujours automatiquement les événements `interact` pour tous les éléments associés à une proposition. |
| `never` | [!DNL Web SDK] ne collectera jamais automatiquement les événements `interact` pour les éléments associés à une proposition. |
| `decoratedElementsOnly` | [!DNL Web SDK] collectera automatiquement les événements `interact` pour les éléments associés à une proposition, mais uniquement si l’élément comprend des attributs de données spécifiant un libellé ou un jeton. |

## Suivi automatique des interactions avec les propositions {#logic}

Lorsque vous activez le suivi automatique des interactions de propositions, tous les clics au sein d’un élément de proposition rendu au DOM sont automatiquement collectés par le [!DNL Web SDK]. Cela inclut toutes les expériences automatiquement rendues au DOM par [!DNL Web SDK] et les expériences rendues au DOM à l’aide de la commande [`applyPropositions`](../applypropositions.md).

### Attributs de données {#data-attributes}

Vous pouvez utiliser des attributs de données sur les éléments pour ajouter une spécificité à une interaction.

| Nom | Attribut de données | Description |
| --- | --- | --- |
| [!DNL Label] | `data-aep-click-label` | Lorsque l’attribut de données de libellé est présent sur un élément sur lequel l’utilisateur a cliqué, il est inclus avec les détails de l’interaction envoyés à l’élément [!DNL Edge Network]. [!DNL Web SDK] recherche un attribut de données de libellé commençant par l’élément sur lequel l’utilisateur a cliqué et remontant l’arborescence DOM. Le [!DNL Web SDK] utilise le premier libellé qu’il trouve. |
| [!DNL Token] | `data-aep-click-token` | Utilisez ce jeton lorsque vous utilisez des stratégies de décision dans [des campagnes basées sur du code Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based). Vous pouvez utiliser le jeton pour distinguer l’élément de stratégie de décision ayant fait l’objet d’un clic. Lorsque l’attribut de données de jeton est présent sur un élément sur lequel l’utilisateur a cliqué, il est inclus avec les détails de l’interaction envoyés à l’Edge Network. [!DNL Web SDK] recherche un attribut de données de jeton commençant par l’élément sur lequel l’utilisateur a cliqué et remontant l’arborescence DOM. [!DNL Web SDK] utilise le premier jeton trouvé. |
| [!DNL Interact ID] | `data-aep-interact-id` | Le [!DNL Web SDK] ajoute automatiquement cet identifiant unique aux éléments de conteneur lors du rendu des propositions. Le SDK Web utilise cet identifiant pour mettre en relation les éléments [!DNL DOM] avec les propositions. Comme il s&#39;agit d&#39;un identifiant requis par le [!DNL Web SDK], vous ne devez pas le modifier de quelque manière que ce soit. Vous pouvez l’ignorer en toute sécurité. |

**Exemple**

Reportez-vous au fragment de code ci-dessous pour voir un exemple d’utilisation des attributs de données.

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/walle.jpg" class="poster" />
    <h2>WALL·E</h2>
    <p class="description"> In a distant, but not so unrealistic, future where mankind has abandoned earth because it has become covered with trash from products sold by the powerful multi-national Buy N Large corporation, WALL-E, a garbage collecting robot has been left to clean up the mess. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-WALL·E"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/ratatouille.jpg" class="poster" />
    <h2>Ratatouille</h2>
    <p class="description"> A rat named Remy dreams of becoming a great French chef despite his family's wishes and the obvious problem of being a rat in a decidedly rodent-phobic profession. When fate places Remy in the sewers of Paris, he finds himself ideally situated beneath a restaurant made famous by his culinary hero, Auguste Gusteau. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Ratatouille"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/coco.jpg" class="poster" />
    <h2>Coco</h2>
    <p class="description"> Despite his family's baffling generations-old ban on music, Miguel dreams of becoming an accomplished musician like his idol, Ernesto de la Cruz. Desperate to prove his talent, Miguel finds himself in the stunning and colorful Land of the Dead following a mysterious chain of events. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Coco"> View details >> </button>
    </p>
  </div>
</div>
```

### La commande `applyPropositions` {#apply-propositions}

Consultez la documentation [`applyPropositions`](../applypropositions.md) pour découvrir le fonctionnement de cette commande.

La commande `applyPropositions` est un moyen pratique d’effectuer le rendu des propositions vers [!DNL DOM]. Cependant, dans le cas de campagnes basées sur du code avec `JSON`, vous pouvez utiliser cette commande pour corréler un élément [!DNL DOM] existant (ou celui que votre code d&#39;application rendu à l&#39;écran en fonction des valeurs `JSON`) avec une proposition.

Cette corrélation active le suivi automatique des interactions pour cet élément et affecte à cet élément la proposition appropriée. Pour ce faire, définissez `actionType` sur `track`.

**Exemple**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://mywebsite.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://mywebsite.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## Activation du suivi automatique des clics des propositions et interactions via l’extension de balise SDK Web {#tag-extension}

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
2. Accédez à **Collecte de données** > **Balises**.
3. Sélectionnez la propriété de balise de votre choix.
4. Accédez à **Extensions**, puis sélectionnez **Configurer** dans la carte SDK Web Adobe Experience Platform.
5. Faites défiler l’écran jusqu’à la section **[!UICONTROL Collecte de données]**, puis cochez la case **Activer les propositions et le suivi des liens d’interaction**.
6. Sélectionnez **Enregistrer**, puis publiez vos modifications.

## Activation du suivi automatique des propositions et interactions via la bibliothèque JavaScript du SDK Web {#library}

Le suivi des propositions est activé par défaut dans [!DNL Web SDK]. Cependant, vous pouvez le configurer davantage à l’aide de la valeur `autoTrackPropositionInteractionsEnabled` lors de l’exécution de la commande [`configure`](../configure/overview.md).

Si vous omettez cette propriété lors de la configuration du SDK Web, elle est définie par défaut sur `{"AJO": "always", "TGT": "never"}`. Si vous préférez ne pas suivre automatiquement les interactions de proposition, définissez la valeur sur `{"AJO": "never", "TGT": "never"}`.

```javascript
alloy("configure", {
   "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
   "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
   "autoTrackPropositionInteractionsEnabled": {"AJO": "always", "TGT": "never"}
});
```
