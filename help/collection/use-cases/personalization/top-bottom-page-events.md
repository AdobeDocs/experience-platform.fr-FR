---
title: Configurer les événements haut et bas de page dans Web SDK
description: Cet article explique comment utiliser les événements de haut et de bas de page dans Web SDK.
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: 8058ee470717b95d30269a8072b12385c920c85f
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 1%

---


# Configurer les événements haut et bas de page dans Web SDK

Lors de la diffusion d’expériences personnalisées, le temps de chargement d’une page web est essentiel. Pour réduire le temps d’attente d’un contenu personnalisé, Web SDK prend en charge la configuration des événements en haut et en bas de la page.

Les événements en haut et en bas de la page décrivent une méthode de chargement asynchrone de divers éléments dans la page tout en réduisant le temps de chargement de la page :

* L’événement haut de page demande une personnalisation dès que le chargement de la page commence.
* L’événement de bas de page enregistre une page vue lorsque le chargement de la page se termine.

Adobe Analytics ignore les événements du haut de la page, ce qui permet d’enregistrer des mesures plus précises, car un seul accès à la page est enregistré (événement du bas de la page).

Vous pouvez configurer les événements de haut et de bas de page de deux manières : en appelant directement la bibliothèque JavaScript Web SDK (`alloy()`) ou en utilisant l’extension de balise Web SDK dans l’interface utilisateur des balises Adobe Experience Platform. L’action [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) de l’extension de balise comprend une option « [!UICONTROL Use guided events] » qui préconfigure les valeurs de champ pour les scénarios « [!UICONTROL Request personalization] » (haut de la page) et « [!UICONTROL Collect analytics] » (bas de page). Chaque exemple ci-dessous montre les deux implémentations.

## Événement haut de page {#top-of-page}

L’exemple ci-dessous configure un événement en haut de la page qui demande une personnalisation, mais supprime les [événements d’affichage](display-events.md) pour les propositions générées automatiquement. Ces événements d’affichage sont envoyés avec l’événement de bas de page à la place.

>[!BEGINTABS]

>[!TAB Bibliothèque JavaScript]

```js
alloy("sendEvent", {
  type: "decisioning.propositionFetch",
  renderDecisions: true,
  personalization: {
    sendDisplayEvent: false
  }
});
```

| Paramètre | Obligatoire / Facultatif | Description |
| --- | --- | --- |
| `type` | Obligatoire | Définissez ce paramètre sur `decisioning.propositionFetch`. Ce type d’événement spécial indique à Adobe Analytics de supprimer cet événement. Lors de l’utilisation de Customer Journey Analytics, vous pouvez également configurer un filtre pour supprimer ces événements. Voir [Types d’événements Edge Network dans Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/hit-types) pour plus d’informations. |
| `renderDecisions` | Obligatoire | Définissez ce paramètre sur `true`. Ce paramètre indique à Web SDK de rendre les décisions renvoyées par Edge Network. |
| `personalization.sendDisplayEvent` | Obligatoire | Définissez ce paramètre sur `false`. Ce paramètre empêche l’envoi d’événements d’affichage. |

>[!TAB Extension de balise Web SDK]

Configurez une action [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) dans la règle qui se déclenche en haut de la page. Activez **[!UICONTROL Use guided events]**, puis sélectionnez **[!UICONTROL Request personalization]**. Cette option verrouille &#39;[!UICONTROL Type]&#39; sur &#39;[!UICONTROL Decisioning Proposition Fetch]&#39;, &#39;[!UICONTROL Render visual personalization decisions]&#39; sur activé et &#39;[!UICONTROL Automatically send a display event]&#39; sur désactivé.

Pour définir ces champs manuellement à la place, laissez **[!UICONTROL Use guided events]** désactivé et configurez chaque champ vous-même.

>[!ENDTABS]

## Exemples d’événements en bas de page {#bottom-of-page}

### Propositions rendues automatiquement {#bottom-auto-rendered}

L’exemple ci-dessous configure un événement de bas de page qui envoie des événements d’affichage pour les propositions qui ont été automatiquement rendues sur la page, mais supprimées dans l’événement [haut de page](#top-of-page).

>[!BEGINTABS]

>[!TAB Bibliothèque JavaScript]

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| Paramètre | Obligatoire / Facultatif | Description |
| --- | --- | --- |
| `personalization.includeRenderedPropositions` | Obligatoire | Définissez ce paramètre sur `true`. Ce paramètre permet l’envoi d’événements d’affichage qui ont été supprimés dans l’événement haut de page. |
| `xdm` | Facultatif | Utilisez cet objet pour inclure toutes les données souhaitées pour l’événement de bas de page. |

>[!TAB Extension de balise Web SDK]

Configurez une action [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) dans la règle qui se déclenche au bas de la page. Activez **[!UICONTROL Use guided events]**, puis sélectionnez **[!UICONTROL Collect analytics]**. Cette option verrouille &#39;[!UICONTROL Include rendered propositions]&#39; sur activé.

Pour définir ce champ manuellement à la place, laissez **[!UICONTROL Use guided events]** désactivé et activez-**[!UICONTROL Include rendered propositions]** directement. Vous pouvez éventuellement renseigner le champ **[!UICONTROL XDM]** avec un élément de données [objet XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) qui transporte les données de votre page.

>[!ENDTABS]

### Propositions rendues manuellement {#bottom-manually-rendered}

L’exemple ci-dessous configure un événement de bas de page qui envoie des événements d’affichage pour les propositions qui ont été rendues manuellement sur la page (c’est-à-dire pour les portées de décision ou les surfaces personnalisées).

>[!NOTE]
>
>Dans ce scénario, l’événement de bas de page doit attendre que l’événement de haut de page soit terminé, de sorte que les propositions puissent être rendues et enregistrées.

>[!BEGINTABS]

>[!TAB Bibliothèque JavaScript]

```js
alloy("sendEvent", {
  xdm: { 
    ... // Optional bottom of page event data
    _experience: {
      decisioning: {
        propositions: propositions.map(function(p) {
          return {
            id: p.id,
            scope: p.scope,
            scopeDetails: p.scopeDetails
          };
        }),
        propositionEventType: {
          display: 1
        }
      }
    }
  }
});
```

| Paramètre | Obligatoire / Facultatif | Description |
| --- | --- | --- |
| `xdm._experience.decisioning.propositions` | Obligatoire | Cette section définit les propositions générées manuellement. Vous devez inclure les `id` de proposition, les `scope` et les `scopeDetails`. Voir [Gérer les événements d’affichage](display-events.md) pour plus d’informations. Le contenu de personnalisation généré manuellement doit être inclus dans l’événement de bas de page. |
| `xdm._experience.decisioning.propositionEventType` | Obligatoire | Définissez ce paramètre sur `display: 1`. |
| `xdm` | Facultatif | Utilisez cet objet pour inclure toutes les données souhaitées pour l’événement de bas de page. |

>[!TAB Extension de balise Web SDK]

L&#39;option &#39;[!UICONTROL Use guided events]&#39; ne couvre pas ce scénario, configurez donc l&#39;action manuellement :

1. Créez un élément de données [objet XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) (ou [Variable](/help/tags/extensions/client/web-sdk/data-element-types.md#variable)) qui renseigne les `_experience.decisioning.propositions` avec les `id`, `scope` et `scopeDetails` de chaque proposition rendue et définit le `_experience.decisioning.propositionEventType.display` sur `1`. Voir [Gérer les événements d’affichage](display-events.md) pour plus d’informations.
1. Dans l’action [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) pour la règle de bas de page, laissez **[!UICONTROL Use guided events]** désactivé et référencez l’élément de données à partir du champ **[!UICONTROL XDM]** .

>[!ENDTABS]

## Application monopage avec événements en haut et en bas de page {#spa-example}

Dans une application d’une seule page, vous devez spécifier le nom de l’affichage à chaque modification d’affichage afin que Web SDK effectue le rendu de la personnalisation appropriée en haut de la page et enregistre l’affichage correct en bas de la page.

### Première page vue {#spa-first-view}

Dans cet exemple, `home` est la vue chargée lors du chargement initial de la page.

>[!BEGINTABS]

>[!TAB Bibliothèque JavaScript]

L’appel supérieur demande la personnalisation de la vue `home` sans enregistrer d’accès Analytics ni déclencher d’événements d’affichage. L’appel du bas enregistre la page vue et déclenche les événements d’affichage supprimés. Incluez la même `viewName` dans les deux appels afin que la vue soit enregistrée de manière cohérente.

```js
// Top of page, render decisions for the "home" view.
alloy("sendEvent", {
    type: "decisioning.propositionFetch",
    renderDecisions: true,
    personalization: {
        sendDisplayEvent: false
    },
    xdm: {
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});

// Bottom of page, send display events for the items that were rendered.
alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});
```

>[!TAB Extension de balise Web SDK]

1. Créez un élément de données [objet XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) qui `web.webPageDetails.viewName` au nom de la vue (par exemple, `home`).
1. Configurez une action de [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) en haut de la page : activez **[!UICONTROL Use guided events]**, sélectionnez **[!UICONTROL Request personalization]** et référencez l’élément de données dans le champ **[!UICONTROL XDM]** .
1. Configurez une action de **[!UICONTROL Send event]** en bas de page : activez **[!UICONTROL Use guided events]**, sélectionnez **[!UICONTROL Collect analytics]** et référencez le même élément de données dans le champ **[!UICONTROL XDM]** afin que le `viewName` corresponde dans les deux événements.

>[!ENDTABS]

### Deuxième page vue — option 1 {#spa-second-view-option-1}

Dans cet exemple, un seul événement est suffisant, car la personnalisation de la page a déjà été récupérée.

>[!BEGINTABS]

>[!TAB Bibliothèque JavaScript]

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    ...,
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```

>[!TAB Extension de balise Web SDK]

1. Créez un élément de données [objet XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) qui `web.webPageDetails.viewName` au nom de la nouvelle vue (par exemple, `cart`).
1. Lors de la modification de l’affichage, configurez une seule action [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) : laissez **[!UICONTROL Use guided events]** désactivé, activez l’**[!UICONTROL Render visual personalization decisions]** et référencez l’élément de données dans le champ **[!UICONTROL XDM]** .

>[!ENDTABS]

### Deuxième page vue — option 2 {#spa-second-view-option-2}

Utilisez cette approche lorsque vous devez retarder l’événement de bas de page (par exemple, lorsque les données d’analyse de la page ne sont pas prêtes au moment du changement d’affichage). Gérer le changement d&#39;affichage en deux étapes :

1. En haut de la page, effectuez le rendu des propositions déjà récupérées sans effectuer d’appel Edge Network.
1. Une fois que les données d’analyse sont prêtes, envoyez l’événement au bas de la page.

Incluez la même `viewName` dans les deux appels afin que la vue soit enregistrée de manière cohérente.

>[!BEGINTABS]

>[!TAB Bibliothèque JavaScript]

Appelez [`applyPropositions`](/help/collection/js/commands/applypropositions.md) en haut de la page pour effectuer le rendu des propositions mises en cache pour la nouvelle vue. Appelez ensuite `sendEvent` au bas de la page avec `includeRenderedPropositions: true` afin que les événements d’affichage supprimés se déclenchent.

```js
// Top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// Bottom of page, send display events for the items that were rendered.
alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
});
```

>[!TAB Extension de balise Web SDK]

1. Créez un élément de données [objet XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) qui `web.webPageDetails.viewName` au nom de la nouvelle vue (par exemple, `cart`).
1. Pour l’événement en haut de la page, configurez une action [[!UICONTROL Apply propositions]](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) et définissez le champ **[!UICONTROL View name]** sur le nom de la vue (par exemple, `cart`). Cette action effectue le rendu des propositions déjà récupérées sans contacter l’Edge Network.
1. Pour l’événement de bas de page, configurez une action de [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) : activez **[!UICONTROL Use guided events]**, sélectionnez **[!UICONTROL Collect analytics]** et référencez l’élément de données dans le champ **[!UICONTROL XDM]** .

>[!ENDTABS]

## Exemple GitHub {#github-sample}

L’[exemple en haut et en bas dans le référentiel d’échantillons d’alliages](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom) montre comment demander une personnalisation en haut de la page et envoyer des mesures d’analyse en bas. Téléchargez l’exemple et exécutez-le localement pour voir comment fonctionnent les événements en haut et en bas de la page. L’exemple utilise directement la bibliothèque JavaScript ; les mêmes modèles s’appliquent lorsque vous configurez des règles équivalentes dans l’extension de balise Web SDK.
