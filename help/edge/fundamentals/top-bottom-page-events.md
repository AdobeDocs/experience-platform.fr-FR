---
title: Utilisation des événements de haut et de bas de page
description: Cet article explique comment utiliser les événements de haut et de bas de page dans le SDK Web.
source-git-commit: 5322156774388a19788529aee554424b2fb5d91b
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 2%

---


# Utilisation des événements de haut et de bas de page dans le SDK Web

Lorsque vous souhaitez diffuser des expériences personnalisées à vos clients, le temps de chargement d’une page web est essentiel.

Pour optimiser les temps de chargement et fournir une personnalisation aussi rapidement que possible, le SDK Web prend en charge la configuration des événements de haut et de bas de page.

Les haut et bas des événements de page décrivent une méthode de chargement asynchrone de divers éléments dans la page, tout en maintenant le temps de chargement de la page au minimum.

Cette configuration réduit le temps d’attente d’un utilisateur jusqu’au chargement du contenu personnalisé.

En termes de précision des mesures, Adobe Analytics peut ignorer les événements de haut de page, ce qui entraîne un enregistrement des mesures plus précis, puisqu’un seul accès à la page est enregistré (le bas de l’événement de page).

## Cas d’utilisation {#use-cases}

Un détaillant de vêtements de sport souhaite offrir des expériences personnalisées à ses clients, tout en réduisant les frictions des utilisateurs lorsqu’ils visitent son site web, tout en étant en mesure de collecter précisément les mesures des visiteurs.

En utilisant les événements de haut et de bas de page dans le SDK Web, l’équipe marketing peut configurer leur diffusion de personnalisation de la manière la plus optimale :

* Le SDK Web envoie une demande de personnalisation qui est chargée dès que la page commence à se charger. Il s’agit d’un événement haut de page.
* Lorsque le chargement de la page se termine, un événement de page vue est enregistré. Cela se produit plus tard dans le processus de chargement de page. Il s’agit du bas de l’événement de page.

## Exemple d’événement haut de page {#top-of-page}

L’exemple de code ci-dessous illustre une configuration d’événement haut de page qui demande une personnalisation, mais n’envoie pas de notifications d’affichage pour les propositions générées automatiquement. Les notifications d’affichage seront envoyées dans le cadre de l’événement du bas de page.

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
| `type` | Obligatoire | Définissez ce paramètre sur `decisioning.propositionFetch`. Ce type d’événement spécial indique à Adobe Analytics de déposer cet événement. Lors de l’utilisation de Customer Journey Analytics, vous pouvez également configurer un filtre pour supprimer ces événements. |
| `renderDecisions` | Obligatoire | Définissez ce paramètre sur `true`. Ce paramètre indique au SDK Web de rendre les décisions renvoyées par le réseau Edge. |
| `personalization.sendDisplayEvent` | Obligatoire | Définissez ce paramètre sur `false`. Cela empêche l’envoi des notifications. |

>[!ENDTABS]

## Bas d’exemples d’événement de page {#bottom-of-page}

>[!BEGINTABS]

>[!TAB Propositions générées automatiquement]

L’exemple de code ci-dessous illustre une configuration d’événement de page inférieure qui envoie des notifications d’affichage pour les propositions qui sont automatiquement générées sur la page, mais pour lesquelles les notifications d’affichage ont été supprimées dans [haut de la page](#top-of-page) .

>[!NOTE]
>
>Dans ce scénario, vous devez appeler le bas de l’événement de page. _after_ en haut de la première page. Toutefois, il n’est pas nécessaire d’attendre que le haut de la page 1 soit terminé.

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
| `personalization.includeRenderedPropositions` | Obligatoire | Définissez ce paramètre sur `true`. Cela permet d’envoyer des notifications d’affichage qui ont été supprimées en haut de l’événement de page. |
| `xdm` | Facultatif | Utilisez cette section pour inclure toutes les données dont vous avez besoin pour l’événement du bas de la page. |

>[!TAB Propositions générées manuellement]

L’exemple de code ci-dessous illustre une configuration d’événement de page inférieure qui envoie des notifications d’affichage pour les propositions générées manuellement sur la page (c’est-à-dire pour les portées de décision ou les surfaces personnalisées).

>[!NOTE]
>
>Dans ce scénario, l’événement du bas de la page doit attendre que l’événement du haut de la page soit terminé pour générer les propositions et enregistrer l’événement du bas de la page.

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
| `xdm._experience.decisioning.propositions` | Obligatoire | Cette section définit les propositions générées manuellement. Vous devez inclure la proposition `ID`, `scope`, et `scopeDetails`. Consultez la documentation sur la manière de [personnalisation du rendu manuel](../personalization/rendering-personalization-content.md#manually) pour plus d’informations sur l’enregistrement des notifications d’affichage pour le contenu généré manuellement. Le contenu de personnalisation rendu manuellement doit être inclus dans l’accès au bas de la page. |
| `xdm._experience.decisioning.propositionEventType` | Obligatoire | Définissez ce paramètre sur `display: 1`. |
| `xdm` | Facultatif | Utilisez cette section pour inclure toutes les données dont vous avez besoin pour l’événement du bas de la page. |

>[!ENDTABS]


## Application d’une seule page avec accès aux pages supérieure et inférieure {#spa-example}


>[!BEGINTABS]

>[!TAB Première page vue]

L’exemple ci-dessous inclut l’ajout de la variable `xdm.web.webPageDetails.viewName` . C’est ce qui en fait une application d’une seule page. La variable `viewName` dans cet exemple, est la vue chargée au chargement de la page.

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

// Bottom of page, send display notifications for the items that were rendered.
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

>[!TAB Deuxième page vue (Option 1)]

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


>[!TAB Deuxième page vue (Option 2)]

Si vous devez toujours retarder l’accès au bas de la page, vous pouvez utiliser `applyPropositions` pour l’accès en haut de la page. Puisqu’aucune personnalisation ne doit être récupérée et qu’aucune donnée Analytics ne doit être enregistrée, il n’est pas nécessaire d’adresser une requête au réseau Edge.

```js
// top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// bottom of page, send display notifications for the items that were rendered.
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

L’exemple trouvé à l’adresse [cette adresse](https://github.com/adobe/alloy-samples/tree/main/top-and-bottom) montre comment utiliser Experience Platform et le SDK Web pour demander de la personnalisation en haut de la page et envoyer des mesures d’analyse en bas de la page. Vous pouvez télécharger l’exemple et l’exécuter localement pour comprendre le fonctionnement des événements de haut et de bas de page.
