---
title: 'Adobe Target et Adobe Experience Platform Web SDK. '
seo-title: Adobe Experience Platform Web SDK et utilisation de Adobe Target
description: Découvrez comment rendre du contenu personnalisé avec le SDK Web Experience Platform à l’aide d’Adobe Target
seo-description: Découvrez comment rendre du contenu personnalisé avec le SDK Web Experience Platform à l’aide d’Adobe Target
keywords: target;adobe target;xdm views; views;single page applications;SPA;SPA lifecycle;client-side;AB testing;AB;Experience targeting;XT;VEC
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 14%

---


# Mise en œuvre d’une application d’une seule page

Adobe Experience Platform Web SDK fournit des fonctionnalités riches qui permettent à votre entreprise d’exécuter la personnalisation sur des technologies de nouvelle génération côté client, telles que les applications d’une seule page (SPA).

Les sites Web traditionnels fonctionnaient sur des modèles de navigation « page à page », appelés également applications multi-pages dans lesquelles les conceptions de site Web étaient étroitement couplées à des URL et les transitions d’une page Web à une autre nécessitaient un chargement de page.

Les applications Web modernes, telles que les applications d’une seule page, ont au contraire adopté un modèle qui encourage l’utilisation rapide du rendu de l’interface utilisateur du navigateur, qui est souvent indépendant des rechargements de page. Ces expériences peuvent être déclenchées par des interactions client, telles que des défilés, des clics et des mouvements de curseur. À mesure que les paradigmes du Web moderne évoluent, la pertinence des événements génériques traditionnels, tels qu&#39;un chargement de page, pour déployer la personnalisation et l&#39;expérimentation ne fonctionne plus.

![](assets/spa-vs-traditional-lifecycle.png)

## Avantages de Platform Web SDK pour SPA

Voici quelques avantages à l’utilisation du SDK Web Adobe Experience Platform pour vos applications d’une seule page :

* Capacité à mettre en cache toutes les offres au chargement de la page afin de passer de plusieurs appels serveur à un seul appel serveur.
* Améliorez considérablement l’expérience des utilisateurs de votre site, car les offres sont affichées immédiatement par le cache sans délai lors des appels traditionnels au serveur.
* Une seule ligne de code et une seule configuration de développeur permettent aux spécialistes du marketing de créer et d’exécuter des activités A/B et de ciblage d’expérience (XT) via le compositeur d’expérience visuelle (VEC) sur votre SPA.

## Vues XDM et applications d’une seule page

Le VEC de Adobe Target pour les applications SPA tire profit d’un nouveau concept nommé Vues : un groupe logique d’éléments visuels qui, ensemble, forment une expérience pour application d’une seule page. Par conséquent, une application d’une seule page peut être considérée comme une transition par le biais de Vues, plutôt que d’URL, en fonction des interactions de l’utilisateur. Une Vue peut généralement représenter un site entier ou des éléments visuels regroupés dans un site.

Pour expliquer plus en détail les Vues, l&#39;exemple suivant utilise un site de commerce électronique en ligne hypothétique implémenté dans React pour explorer des exemples de Vues.

Après avoir accédé au site d&#39;accueil, une image de héros fait la promotion d&#39;une vente de Pâques ainsi que des produits les plus récents disponibles sur le site. Dans ce cas, une Vue peut être définie pour l’ensemble de l’écran d’accueil. Cette Vue pourrait simplement être appelée &quot;maison&quot;.

![](assets/example-views.png)

As the customer becomes more interested in the products that the business is selling, they decide to click the **Products** link. Comme pour le site d’accueil, l’intégralité du site de produits peut être définie comme une ue.V Cette Vue peut être nommée &quot;products-all&quot;.

![](assets/example-products-all.png)

Comme une Vue peut être définie comme un site entier ou un groupe d&#39;éléments visuels sur un site, les quatre produits affichés sur le site de produits peuvent être regroupés et considérés comme une Vue. Cette vue peut être nommée &quot;produits&quot;.

![](assets/example-products.png)

Lorsque le client décide de cliquer sur le bouton **Charger plus** pour explorer davantage de produits sur le site, l’URL du site Web ne change pas dans ce cas, mais une Vue peut être créée ici pour représenter uniquement la deuxième ligne de produits qui s’affiche. Le nom de la Vue peut être &quot;products-page-2&quot;.

![](assets/example-load-more.png)

Le client décide d&#39;acheter quelques produits sur le site et passe à l&#39;écran de passage en caisse. Sur le site de passage en caisse, le client dispose d&#39;options lui permettant de choisir une diffusion normale ou une diffusion express. Une Vue peut être n’importe quel groupe d’éléments visuels sur un site, de sorte qu’une Vue peut être créée pour les préférences de diffusion et être appelée &quot;Préférences de Diffusion&quot;.

![](assets/example-check-out.png)

Le concept de Vue peut être étendu bien plus loin que cela. Ce ne sont là que quelques exemples de Vues qui peuvent être définies sur un site.

## Implémentation de Vues XDM

Les Vues XDM peuvent être exploitées dans Adobe Target pour permettre aux spécialistes du marketing d’exécuter des tests A/B et XT sur SPA via le compositeur d’expérience visuelle. Pour ce faire, vous devez exécuter les étapes suivantes afin de terminer la configuration unique d’un développeur :

1. Install [Adobe Experience Platform Web SDK](../../fundamentals/installing-the-sdk.md)
2. Déterminez toutes les Vues XDM de votre application d&#39;une seule page que vous souhaitez personnaliser.
3. Après avoir défini les Vues XDM, afin de fournir des activités du compositeur d’expérience visuelle AB ou XT, implémentez la `sendEvent()` fonction avec `renderDecisions` la valeur `true` et la Vue XDM correspondante dans votre application d’une seule page. La Vue XDM doit être transmise `xdm.web.webPageDetails.viewName`. Cette étape permet aux spécialistes du marketing d’exploiter le compositeur d’expérience visuelle pour lancer les tests A/B et XT pour ces XDM.

   ```javascript
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
>Lors du premier `sendEvent()` appel, toutes les Vues XDM qui doivent être rendues à l’utilisateur final seront récupérées et mises en cache. Les `sendEvent()` appels suivants avec les Vues XDM transmises seront lus à partir du cache et rendus sans appel au serveur.

## `sendEvent()` exemples de fonctions

Cette section présente trois exemples illustrant comment appeler la `sendEvent()` fonction dans Réagir pour une SPA de commerce électronique hypothétique.

### Exemple 1 : Page d&#39;accueil de test A/B

L’équipe marketing souhaite exécuter des tests A/B sur toute la page d&#39;accueil.

![](assets/use-case-1.png)

Pour exécuter des tests A/B sur l’ensemble du site d’accueil, `sendEvent()` vous devez appeler avec XDM `viewName` défini sur `home`:

```jsx
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

### Exemple 2 : Produits personnalisés

L’équipe marketing souhaite personnaliser la deuxième ligne de produits en changeant la couleur de l’étiquette de prix en rouge lorsqu’un utilisateur clique sur **Charger plus**.

![](assets/use-case-2.png)

```jsx
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
      <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button> 
    ); 
  } 

  handleLoadMoreClicked() { 
    var page = this.state.page + 1; // assuming page number is derived from component’s state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### Exemple 3 : Préférences de la diffusion de test A/B

The marketing team want to run an A/B test to see whether changing the color of the button from blue to red when **Express Delivery** is selected can boost conversions (as opposed to keeping the button color blue for both delivery options).

![](assets/use-case-3.png)

Pour personnaliser le contenu du site en fonction des préférences de diffusion sélectionnées, une Vue peut être créée pour chaque préférence de diffusion. Lorsque la Diffusion **** normale est sélectionnée, la Vue peut être nommée &quot;checkout-normal&quot;. If **Express Delivery** is selected, the View can be named &quot;checkout-express&quot;.

```jsx
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

class Checkout extends Component { 

  render() { 
    return ( 
      <div onChange={this.onDeliveryPreferenceChanged}> 
        <label> 
          <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/> 
          <span> Normal Delivery (7-10 business days)</span> 
        </label> 
        <label> 
          <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/> 
          <span> Express Delivery* (2-3 business days)</span> 
        </label> 
      </div> 
    ); 
  } 

  onDeliveryPreferenceChanged(evt) { 
    var selectedPreferenceValue = evt.target.value; 
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## Utilisation du compositeur d’expérience visuelle pour un SPA

Une fois la définition de vos Vues XDM terminée et implémentée `sendEvent()` avec ces Vues XDM transmises, le compositeur d’expérience visuelle pourra détecter ces Vues et permettre aux utilisateurs de créer des actions et des modifications pour les activités A/B ou XT.

>[!NOTE]
>
>Pour utiliser le compositeur d’expérience visuelle pour votre SPA, vous devez installer et activer [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension.

### Panneau des modifications

Le panneau Modifications capture les actions créées pour une Vue particulière. Toutes les actions d’une Vue sont regroupées sous cette Vue.

![](assets/modifications-panel.png)

### Actions

Cliquer sur une action met en évidence l’élément de la page sur lequel cette action sera appliquée. Each VEC action created under a View has the following icons: **Information**, **Edit**, **Clone**, **Move**, and **Delete**. Ces icônes sont expliquées plus en détail dans le tableau qui suit.

![](assets/action-icons.png)

| Icône | Description |
|---|---|
| Informations | Affiche les détails de cette action. |
| Modifier | Permet de modifier directement les propriétés de cette action. |
| Dupliquer | Cloner l’action vers une ou plusieurs vues figurant dans le panneau Modifications ou vers une ou plusieurs vues que vous avez parcourues et auxquelles vous avez accédé dans le VEC. L’action n’a pas nécessairement besoin d’exister dans le panneau Modifications.<br/><br/>**Remarque :** Après une opération de clonage, vous devez accéder à la Vue du compositeur d’expérience visuelle via Parcourir pour vérifier si l’action clonée était une opération valide. Si l’action ne peut pas être appliquée à l’affichage, une erreur s’affiche. |
| Déplacer | Déplace l’action vers un événement de chargement de page ou tout autre vue existant dans le panneau Modifications.<br/><br/>**Événement de chargement de page :** Toutes les actions correspondant au événement de chargement de page sont appliquées au premier chargement de page de votre application Web. <br/><br/>**Remarque :** après une opération de déplacement, vous devez accéder à la Vue du compositeur d’expérience visuelle via Parcourir pour vérifier si le déplacement est une opération valide. Si l’action ne peut pas être appliquée à l’affichage, une erreur s’affiche. |
| Supprimer | Supprime l’action. |

## Utilisation du compositeur d’expérience visuelle pour SPA exemples

Cette section présente trois exemples d’utilisation du compositeur d’expérience visuelle pour créer des actions et des modifications pour les activités A/B ou XT.

### Exemple 1 : Mettre à jour la Vue &quot;accueil&quot;

Au début de ce document, une Vue nommée &quot;accueil&quot; a été définie pour l’ensemble du site d’accueil. L’équipe marketing souhaite maintenant mettre à jour la vue &quot;d’accueil&quot; de la manière suivante :

* Les boutons **Ajouter au panier** et **J’aime** sont remplacés par un bleu plus léger. Cela doit se produire pendant le chargement de la page, car cela implique de modifier les composants de l’en-tête.
* Change the **Latest Products for 2019** label to **Hottest Products for 2019** and change the text color to purple.

To make these updates in the VEC, select **Compose** and apply those changes to the &quot;home&quot; view.

![](assets/vec-home.png)

### Exemple 2 : Modifier les étiquettes de produits

Pour la Vue &quot;products-page-2&quot;, l’équipe marketing souhaite remplacer l’étiquette **Prix** par **Prix de vente** et modifier la couleur de l’étiquette en rouge.

Pour effectuer ces mises à jour dans le compositeur d’expérience visuelle, procédez comme suit :

1. Sélectionnez **Parcourir** dans le compositeur d’expérience visuelle.
2. Sélectionnez **Produits** dans la barre de navigation supérieure du site.
3. Select **Load More** once to view the second row of products.
4. Sélectionnez **Composer** dans le compositeur d’expérience visuelle.
5. Apply actions to change the text label to **Sale Price** and the color to red.

![](assets/vec-products-page-2.png)

### Exemple 3 : Personnaliser le style des préférences de diffusion

Les vues peuvent être définies à un niveau granulaire, tel qu’un état ou une option d’un bouton radio. Plus tôt dans ce document, les Vues ont été définies pour les préférences de diffusion, &quot;checkout-normal&quot; et &quot;checkout-express&quot;. L’équipe marketing souhaite remplacer la couleur du bouton par le rouge pour la Vue &quot;express&quot;.

Pour effectuer ces mises à jour dans le compositeur d’expérience visuelle, procédez comme suit :

1. Sélectionnez **Parcourir** dans le compositeur d’expérience visuelle.
2. Ajoutez des produits au panier sur le site.
3. Sélectionnez l’icône de panier dans le coin supérieur droit du site.
4. Sélectionnez **Paiement de votre commande**.
5. Sélectionnez le bouton radio **Express Diffusion** sous Préférences **de** Diffusion.
6. Sélectionnez **Composer** dans le compositeur d’expérience visuelle.
7. Remplacez la couleur rouge du bouton **Payer** par la couleur rouge.

>[!NOTE]
>
>La Vue &quot;express&quot; n&#39;apparaît pas dans le panneau Modifications tant que le bouton radio **Express Diffusion** n&#39;a pas été sélectionné. Cela est dû au fait que la`sendEvent()` fonction est exécutée lorsque le bouton radio **Express Diffusion** est sélectionné. Par conséquent, le compositeur d’expérience visuelle n’est pas au courant de la Vue &quot;express&quot; tant que le bouton radio n’est pas sélectionné.

![](assets/vec-delivery-preference.png)
