---
title: Configurer les événements haut et bas de page dans Web SDK
description: Cet article explique comment utiliser les événements de haut et de bas de page dans Web SDK.
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 2%

---


# Configurer les événements haut et bas de page dans Web SDK

Lorsque vous souhaitez offrir des expériences personnalisées à vos clients et clientes, le temps de chargement d’une page web est essentiel.

Pour optimiser les temps de chargement et fournir une personnalisation aussi rapidement que possible, Web SDK prend en charge la configuration des événements en haut et en bas de page.

Les événements en haut et en bas de la page décrivent une méthode de chargement asynchrone de divers éléments dans la page, tout en réduisant le temps de chargement de la page.

Cette configuration réduit le temps d’attente nécessaire à l’utilisateur ou à l’utilisatrice avant le chargement du contenu personnalisé.

En termes de précision des mesures, Adobe Analytics peut ignorer les événements situés en haut de la page, ce qui permet d’enregistrer des mesures plus précises, car un seul accès à la page est enregistré (événement situé en bas de la page).

## Cas d’utilisation {#use-cases}

Un retailer de vêtements de sport souhaite offrir des expériences personnalisées à ses clients, tout en réduisant le frottement des utilisateurs et utilisatrices lors de leur visite sur son site web, tout en étant en mesure de collecter avec précision les mesures des visiteurs et visiteuses.

En utilisant les événements en haut et en bas de page dans Web SDK, l’équipe marketing peut configurer sa diffusion de personnalisation de la manière la plus optimale :

* Web SDK envoie une demande de personnalisation qui est chargée dès que le chargement de la page commence. Il s’agit d’un événement en haut de la page.
* Lorsque le chargement de la page se termine, un événement de page vue est enregistré. Cela se produit ultérieurement au cours du processus de chargement de la page. Il s’agit d’un événement de bas de page.

## Exemple d’événement en haut de page {#top-of-page}

L’exemple de code ci-dessous illustre une configuration d’événement en haut de page qui demande une personnalisation, mais n’[ pas d’événements d’affichage](../personalization/display-events.md#send-sendEvent-calls) pour les propositions générées automatiquement. Les [événements d’affichage](../personalization/display-events.md#send-sendEvent-calls) sont envoyés dans le cadre de l’événement du bas de page.

>[!BEGINTABS]

>[!TAB Événement haut de page]

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
|---|---|---|
| `type` | Obligatoire | Définissez ce paramètre sur `decisioning.propositionFetch`. Ce type d’événement spécial indique à Adobe Analytics de supprimer cet événement. Lors de l’utilisation de Customer Journey Analytics, vous pouvez également configurer un filtre pour supprimer ces événements. |
| `renderDecisions` | Obligatoire | Définissez ce paramètre sur `true`. Ce paramètre indique à Web SDK de rendre les décisions renvoyées par Edge Network. |
| `personalization.sendDisplayEvent` | Obligatoire | Définissez ce paramètre sur `false`. Cela empêche l’envoi d’événements d’affichage. |

>[!ENDTABS]

## Exemples d’événements en bas de page {#bottom-of-page}

>[!BEGINTABS]

>[!TAB Propositions rendues automatiquement]

L’exemple de code ci-dessous illustre une configuration d’événement de bas de page qui envoie des événements d’affichage pour les propositions qui ont été automatiquement rendues sur la page, mais pour lesquelles les événements d’affichage ont été supprimés dans l’événement [haut de la page](#top-of-page).

>[!NOTE]
>
>Dans ce scénario, vous devez appeler l’événement de bas de page _après_ le haut de la page un. Cependant, l’événement de bas de page n’a pas besoin d’attendre que le haut de la page un soit terminé.

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| Paramètre | Obligatoire / Facultatif | Description |
|---|---|---|
| `personalization.includeRenderedPropositions` | Obligatoire | Définissez ce paramètre sur `true`. Cela permet d’envoyer les événements d’affichage qui ont été supprimés dans l’événement haut de page. |
| `xdm` | Facultatif | Utilisez cette section pour inclure toutes les données dont vous avez besoin pour l’événement de bas de page. |

>[!TAB Propositions rendues manuellement]

L’exemple de code ci-dessous illustre une configuration d’événement en bas de page qui envoie des événements d’affichage pour les propositions qui ont été rendues manuellement sur la page (c’est-à-dire pour les portées de décision ou les surfaces personnalisées).

>[!NOTE]
>
>Dans ce scénario, l’événement de bas de page doit attendre que l’événement de haut de page soit terminé pour effectuer le rendu des propositions et enregistrer l’événement de bas de page.

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
|---|---|---|
| `xdm._experience.decisioning.propositions` | Obligatoire | Cette section définit les propositions générées manuellement. Vous devez inclure les `ID` de proposition, les `scope` et les `scopeDetails`. Voir [Gérer les événements d’affichage](display-events.md) pour plus d’informations. Le contenu de personnalisation généré manuellement doit être inclus au bas de l’accès à la page. |
| `xdm._experience.decisioning.propositionEventType` | Obligatoire | Définissez ce paramètre sur `display: 1`. |
| `xdm` | Facultatif | Utilisez cette section pour inclure toutes les données dont vous avez besoin pour l’événement de bas de page. |

>[!ENDTABS]


## Application monopage avec accès aux pages supérieure et inférieure {#spa-example}


>[!BEGINTABS]

>[!TAB  Première page vue ]

L’exemple ci-dessous inclut l’ajout du paramètre `xdm.web.webPageDetails.viewName` obligatoire. C’est ce qui en fait une application d’une seule page. La `viewName` dans cet exemple est la vue qui est chargée au chargement de la page.

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
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.

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

>[!TAB Deuxième page vue (option 1)]

Dans cet exemple, il n’est pas nécessaire d’effectuer un partage haut/bas de page, car la personnalisation de la page a déjà été récupérée.

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


>[!TAB Deuxième page vue (option 2)]

Si vous devez toujours retarder l’accès au bas de la page, vous pouvez utiliser `applyPropositions` pour l’accès au haut de la page. Étant donné qu’aucune personnalisation ne doit être récupérée et qu’aucune donnée Analytics ne doit être enregistrée, il n’est pas nécessaire d’adresser une requête à Edge Network.

```js
// top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// bottom of page, send display events for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.
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

>[!ENDTABS]

## Exemple GitHub {#github-sample}

L’exemple figurant à l’adresse [cette adresse](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom) montre comment utiliser Experience Platform et Web SDK pour demander une personnalisation en haut de la page et envoyer des mesures d’analyse en bas. Vous pouvez télécharger l’exemple et l’exécuter localement pour comprendre comment fonctionnent les événements en haut et en bas de la page.
