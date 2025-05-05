---
title: Implémentation d’applications monopages
description: Découvrez comment mettre en oeuvre SPA vues dans Adobe Journey Optimizer
exl-id: 1883251b-2d59-46d3-ac74-b8657edd0325
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 77%

---

# Implémenter des applications monopages (SPA) {#web-spa-implementation}

Le SDK Web de Adobe Experience Platform offre des fonctionnalités riches qui permettent à votre entreprise d’exécuter la personnalisation sur les technologies côté client de nouvelle génération, telles que les applications d’une seule page (SPA).

Les sites web traditionnels fonctionnaient sur des modèles de navigation « page à page », appelés également applications multi-pages dans lesquelles les conceptions de site web étaient étroitement couplées à des URL et les transitions d’une page web à une autre nécessitaient un chargement de page.

Les applications web modernes, comme les applications monopages, adoptent plutôt un modèle qui projette rapidement le rendu de l’interface utilisateur du navigateur, ce qui est souvent indépendant des rechargements de page. Ces expériences peuvent être déclenchées par des interactions client, comme faire défiler, cliquer et faire bouger le curseur. À mesure de l’évolution des paradigmes du Web moderne, la pertinence des événements génériques traditionnels, comme le chargement des pages, pour déployer la personnalisation et les expériences ne fonctionnent plus.

![ Diagramme de cycle de vie de page.](assets/web-spa-vs-traditional-lifecycle.png)

## Avantages du SDK Web pour SPA {#web-spa-benefits}

Voici quelques avantages de l’utilisation du SDK Web pour vos applications d’une seule page :

* Capacité à mettre en cache toutes les offres au chargement de la page afin de passer de plusieurs appels au serveur à un seul appel au serveur.
* Améliorez considérablement l’expérience utilisateur de votre site, car les offres sont immédiatement affichées via le cache, sans délai intégré aux appels serveur traditionnels.
* La configuration unique des développeurs et développeuses permet aux spécialistes du marketing de créer et d’exécuter des activités de personnalisation et d’expérimentation via l’éditeur visuel web Adobe Journey Optimizer sur votre SPA.

## Vues XDM et applications monopages {#web-spa-xdm}

L’éditeur web de Journey Optimizer tire parti d’un concept appelé _views_.

Les vues sont un groupe logique d’éléments visuels qui, ensemble, constituent une expérience SPA. Une application monopage peut donc être considérée comme une transition entre les vues (et pas entre les URL) basée sur les interactions des utilisateurs et utilisatrices. Une vue peut généralement représenter un site entier, une seule page ou des éléments visuels regroupés dans une page.

Pour montrer plus de détails sur les vues, l’exemple suivant utilise un hypothétique site d’e-commerce.

* Après avoir accédé au site d’accueil, une image principale fait la promotion de collections saisonnières ainsi que des différents catalogues de produits disponibles sur le site. Dans ce cas, une vue peut être définie pour la totalité de l’écran d’accueil. Cette vue pourrait simplement être nommée « accueil ».

  ![Exemple d&#39;image de site web montrant une page d&#39;accueil.](assets/web-spa-home.png)

* À mesure que le client ou la cliente s’intéresse de plus en plus aux produits de l’entreprise, il ou elle décide de cliquer sur le lien **Hommes**. Comme pour la page d’accueil, l’intégralité de la page **Hommes** peut être définie comme une vue. Cette vue pourrait être nommée « hommes ».

  ![Exemple d&#39;image de site web montrant une vue spécifique.](assets/web-spa-men.png)

* Étant donné qu’une vue peut être définie comme un site entier ou un groupe d’éléments visuels sur un site, les quatre produits affichés sur le site de produits peuvent être regroupés et considérés comme une vue. Cette vue pourrait être nommée « produits ».

  ![Exemple d&#39;image de site web montrant une vue spécifique.](assets/web-spa-men-products.png)

* Lorsque le client ou la cliente décide de cliquer sur le bouton **TOUS LES PRODUITS POUR HOMMES** pour voir d’autres produits sur le site, l’URL du site web ne change pas dans ce cas, mais une vue peut être créée ici pour représenter uniquement la deuxième ligne des produits affichés. Le nom de la vue pourrait être « page-produits-2 ».

* Le client ou la cliente décide d’acheter quelques produits sur le site et passe à l’écran de passage en caisse. L’écran du panier lui-même peut être associé à une vue nommée « panier ». Vous pouvez également disposer d’une vue différente dans l’écran de passage en caisse pour afficher les produits recommandés en dessous.

  ![Exemple d&#39;image de site web montrant une vue spécifique.](assets/web-spa-cart.png)

Le concept de vues peut être étendu bien plus loin. Ce ne sont que quelques exemples de vues qui peuvent être définies sur un site.

## Implémentation des vues XDM {#implement-xdm-views}

Les vues XDM peuvent être exploitées dans Adobe Journey Optimizer pour permettre aux marketeurs d’exécuter des campagnes de personnalisation et d’expérimentation web sur SPA, via l’éditeur visuel web Journey Optimizer.

Pour effectuer une configuration de développeur ou développeuse unique, procédez comme suit :

1. Installez [Adobe Experience Platform Web SDK](/help/web-sdk/install/overview.md) et vérifiez la page [conditions préalables requises pour le canal web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/configure-web-channel/web-prerequisites.html?lang=fr).

2. Déterminez toutes les vues XDM de votre application monopage que vous souhaitez personnaliser.

3. Après avoir défini les vues XDM, vous devez implémenter la fonction `sendEvent()` avec `renderDecisions` défini sur `true` et la vue XDM correspondante dans votre application monopage pour leur diffuser du contenu. La vue XDM doit être transmise dans `xdm.web.webPageDetails.viewName`. Cette étape permet aux spécialistes du marketing de découvrir ces vues dans l’éditeur web de Journey Optimizer et d’y appliquer des modifications de contenu :

```js
 alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
   "web": {
    "webPageDetails": {
    "viewName":"home"
   }
  }
 }
});
```

>[!NOTE]
>
>Au premier appel `sendEvent()`, toutes les vues XDM qui doivent être rendues à l’utilisateur ou l’utilisatrice finale seront récupérées et mises en cache. Les appels `sendEvent()` suivants avec des vues XDM transmises seront lus à partir du cache et rendus sans appel au serveur.

## Exemples de fonctions `sendEvent()`

Cette section présente deux exemples montrant comment invoquer la fonction `sendEvent()` dans React pour une application monopage hypothétique d’e-commerce.

### Exemple 1 : page d’accueil du test A/B {#web-spa-sample-1}

L’équipe marketing souhaite exécuter des tests A/B sur l’ensemble de la page d’accueil.

![Exemple de page d’application d’une seule page.](assets/web-spa-home.png)

Pour exécuter des tests A/B sur l’ensemble du site d’accueil, `sendEvent()` doit être appelé avec `viewName` XDM défini sur `home` :

```js
function onViewChange() {

  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash

  viewName = viewName || 'home'; // view name cannot be empty

  // Sanitize viewName to get rid of any trailing symbols derived from URL

  if (viewName.startsWith('#') || viewName.startsWith('/')) {
    viewName = viewName.substr(1);
  }

  alloy("sendEvent", {
    "renderDecisions": true,

    "xdm": {
      "web": {
        "webPageDetails": {
          "viewName":"home"
        }
      }
    }
  });
}

// react router v4

const history = syncHistoryWithStore(createBrowserHistory(), store);

history.listen(onViewChange);

// react router v3

<Router history={hashHistory} onUpdate={onViewChange} >
```

### Exemple 2 : produits personnalisés {#web-spa-sample-2}

L’équipe marketing souhaite personnaliser la deuxième ligne de produits en définissant la couleur du libellé du prix en rouge après qu’un utilisateur ou une utilisatrice a cliqué pour afficher tous les produits Hommes.

![Exemple de page d’application d’une seule page avec des produits personnalisés.](assets/web-spa-men-products.png)

```js
function onViewChange(viewName) {

    alloy("sendEvent", {
        "renderDecisions": true,
        "xdm": {
            "web": {
                "webPageDetails": {
                    "viewName": viewName
                }
            }
        }
    });
}

class Products extends Component {

    render() {
        return (

            <
            button type = "button"
            onClick = {
                this.handleLoadMoreClicked
            } > All Men 's Products</button>
        );
    }

    handleLoadMoreClicked() {
        var page = this.state.page + 1; // assuming page number is derived from component's state
        this.setState({
            page: page
        });
        onViewChange('PRODUCTS-PAGE-' + page);
    }
}
```
