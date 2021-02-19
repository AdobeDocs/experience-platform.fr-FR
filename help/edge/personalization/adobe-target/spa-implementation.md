---
title: Implémentation d'applications page unique pour le kit de développement Adobe Experience Platform Web SDK
description: Découvrez comment créer une mise en oeuvre d’application d’une seule page (SPA) du kit de développement Web Adobe Experience Platform à l’aide de Adobe Target.
keywords: target ; adobe target ; vues xdm ; vues ; applications d'une seule page ; SPA ; SPA cycle de vie ; côté client ; test AB ; AB ; Ciblage d'expérience ; XT ; VEC
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 12%

---


# Mise en oeuvre d’applications d’une page

Adobe Experience Platform Web SDK offre de riches fonctionnalités qui permettent à votre entreprise d’exécuter la personnalisation sur des technologies côté client de nouvelle génération, telles que les applications d’une page (SPA).

Les sites Web traditionnels fonctionnaient sur des modèles de navigation « page à page », appelés également applications multi-pages dans lesquelles les conceptions de site Web étaient étroitement couplées à des URL et les transitions d’une page Web à une autre nécessitaient un chargement de page.

Les applications Web modernes, telles que les applications d’une seule page, ont au contraire adopté un modèle qui encourage l’utilisation rapide du rendu de l’interface utilisateur du navigateur, qui est souvent indépendant des rechargements de page. Ces expériences peuvent être déclenchées par des interactions client, telles que des défilés, des clics et des mouvements de curseur. À mesure que les paradigmes du Web moderne évoluent, la pertinence des événements génériques traditionnels, tels qu&#39;un chargement de page, pour déployer la personnalisation et l&#39;expérimentation ne fonctionne plus.

![](assets/spa-vs-traditional-lifecycle.png)

## Avantages de Platform Web SDK pour SPA

Voici quelques avantages à l’utilisation du SDK Web Adobe Experience Platform pour vos applications d’une seule page :

* Capacité à mettre en cache toutes les offres au chargement de la page afin de passer de plusieurs appels serveur à un seul appel serveur.
* Améliorez considérablement l’expérience des utilisateurs de votre site, car les offres sont affichées immédiatement par le cache sans délai lors des appels traditionnels au serveur.
* Une seule ligne de code et une seule configuration de développeur permettent aux spécialistes du marketing de créer et d’exécuter des activités A/B et de ciblage d’expérience (XT) via le compositeur d’expérience visuelle (VEC) sur votre SPA.

## Vues XDM et applications d’une seule page

Le Adobe Target VEC pour SPA tire parti d&#39;un concept appelé Vues : un groupe logique d’éléments visuels qui forment ensemble une expérience SPA. Par conséquent, une application d’une seule page peut être considérée comme une transition par le biais de Vues, plutôt que d’URL, en fonction des interactions de l’utilisateur. Une Vue peut généralement représenter un site entier ou des éléments visuels regroupés dans un site.

Pour expliquer plus en détail ce que sont les vues, l&#39;exemple suivant utilise un hypothétique site de commerce électronique en ligne mis en place dans Réaction pour explorer l&#39;exemple de vues.

Après avoir visité le site d&#39;accueil, une image d&#39;héros fait la promotion d&#39;une vente de Pâques ainsi que des produits les plus récents disponibles sur le site. Dans ce cas, une Vue peut être définie pour l’ensemble de l’écran d’accueil. Ce point de vue pourrait simplement être appelé &quot;maison&quot;.

![](assets/example-views.png)

À mesure que le client s’intéresse de plus en plus aux produits que l’entreprise vend, il décide de cliquer sur le lien **Produits**. Comme pour le site d’accueil, l’intégralité du site de produits peut être définie comme une ue.V Cette vue peut être nommée &quot;product-all&quot;.

![](assets/example-products-all.png)

Étant donné qu&#39;une vue peut être définie comme un site entier ou un groupe d&#39;éléments visuels sur un site, les quatre produits affichés sur le site de produits peuvent être regroupés et considérés comme une vue. Cette vue peut être appelée &quot;produits&quot;.

![](assets/example-products.png)

Lorsque le client décide de cliquer sur le bouton **Charger plus** pour explorer d’autres produits sur le site, l’URL du site Web ne change pas dans ce cas, mais une vue peut être créée ici pour représenter uniquement la deuxième ligne de produits qui s’affiche. Le nom de la vue peut être &quot;products-page-2&quot;.

![](assets/example-load-more.png)

Le client décide d&#39;acheter quelques produits sur le site et de passer à l&#39;écran d&#39;extraction. Sur le site de paiement, le client dispose d&#39;options pour choisir la livraison normale ou la livraison express. Une vue peut être n’importe quel groupe d’éléments visuels sur un site, de sorte qu’une vue peut être créée pour les préférences de livraison et être appelée &quot;Préférences de livraison&quot;.

![](assets/example-check-out.png)

Le concept de vues peut être étendu bien plus loin que cela. Ce ne sont que quelques exemples de vues qui peuvent être définis sur un site.

## Implémentation de vues XDM

Les vues XDM peuvent être exploitées dans Adobe Target pour permettre aux spécialistes du marketing d’exécuter des tests A/B et XT sur SPA via le compositeur d’expérience visuelle. Pour ce faire, vous devez effectuer les étapes suivantes afin de terminer une configuration de développeur unique :

1. Installer [Adobe Experience Platform Web SDK](../../fundamentals/installing-the-sdk.md)
2. Déterminez toutes les vues XDM de votre application d’une seule page que vous souhaitez personnaliser.
3. Après avoir défini les vues XDM, afin de livrer les activités AB ou XT VEC, implémentez la fonction `sendEvent()` avec `renderDecisions` défini sur `true` et la vue XDM correspondante dans votre application Une seule page. La vue XDM doit être transmise dans `xdm.web.webPageDetails.viewName`. Cette étape permet aux spécialistes du marketing de tirer parti du compositeur d’expérience visuelle pour lancer des tests A/B et XT pour ces XDM.

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
>Lors du premier appel `sendEvent()`, toutes les vues XDM qui doivent être rendues à l&#39;utilisateur final seront récupérées et mises en cache. Les appels `sendEvent()` suivants avec les vues XDM transmises seront lus à partir du cache et rendus sans appel de serveur.

## `sendEvent()` exemples de fonctions

Cette section présente trois exemples illustrant comment appeler la fonction `sendEvent()` dans Réagir pour une SPA de commerce électronique hypothétique.

### Exemple 1 : Page d&#39;accueil du test A/B

L’équipe marketing souhaite exécuter des tests A/B sur l’ensemble de la page d’accueil.

![](assets/use-case-1.png)

Pour exécuter des tests A/B sur l&#39;ensemble du site d&#39;accueil, `sendEvent()` doit être appelé avec la valeur `viewName` de XDM définie sur `home` :

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

L’équipe marketing souhaite personnaliser la deuxième ligne de produits en définissant la couleur du libellé de prix sur rouge après qu’un utilisateur ait cliqué sur **Charger plus**.

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

### Exemple 3 : Préférences de livraison des tests A/B

L’équipe marketing souhaite exécuter un test A/B pour déterminer si le changement de couleur du bouton du bleu au rouge alors que **la Diffusion Express** est sélectionnée peut augmenter les conversions (contrairement à ce qui se produit lorsque la couleur du bouton est bleue pour les deux options de diffusion).

![](assets/use-case-3.png)

Pour personnaliser le contenu du site en fonction des préférences de diffusion sélectionnées, une Vue peut être créée pour chaque préférence de diffusion. Lorsque **Livraison normale** est sélectionné, la vue peut être nommée &quot;Retrait normal&quot;. Si **Diffusion express** est sélectionné, la Vue peut être nommée &quot;express&quot;.

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

Une fois que vous avez terminé de définir vos vues XDM et mis en oeuvre `sendEvent()` avec ces vues XDM transmises, le VEC pourra détecter ces vues et permettre aux utilisateurs de créer des actions et des modifications pour les activités A/B ou XT.

>[!NOTE]
>
>Pour utiliser le VEC pour votre SPA, vous devez installer et activer l’extension d’assistance [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC.

### Panneau des modifications

Le panneau Modifications capture les actions créées pour une Vue particulière. Toutes les actions d’une Vue sont regroupées sous cette Vue.

![](assets/modifications-panel.png)

### Actions

Cliquer sur une action met en évidence l’élément de la page sur lequel cette action sera appliquée. Chaque action du compositeur d’expérience visuelle créée sous une Vue comporte les icônes suivantes : **Informations**, **Modifier**, **Clone**, **Déplacer** et **Supprimer**. Ces icônes sont expliquées plus en détail dans le tableau qui suit.

![](assets/action-icons.png)

| Icône | Description |
|---|---|
| Informations | Affiche les détails de cette action. |
| Modifier | Permet de modifier directement les propriétés de cette action. |
| Dupliquer | Cloner l’action vers une ou plusieurs vues figurant dans le panneau Modifications ou vers une ou plusieurs vues que vous avez parcourues et auxquelles vous avez accédé dans le VEC. L’action n’a pas nécessairement besoin d’exister dans le panneau Modifications.<br/><br/>**Remarque :** après une opération de clonage, vous devez accéder à la Vue du compositeur d’expérience visuelle via Parcourir pour vérifier si l’action clonée était une opération valide. Si l’action ne peut pas être appliquée à l’affichage, une erreur s’affiche. |
| Déplacer | Déplace l’action vers un événement de chargement de page ou tout autre vue existant dans le panneau Modifications.<br/><br/>**Événement de chargement de page :** toutes les actions correspondant au événement de chargement de page sont appliquées au chargement initial de page de votre application Web. <br/><br/>**Remarque :** après une opération de déplacement, vous devez accéder à la Vue du compositeur d’expérience visuelle via Parcourir pour vérifier si le déplacement est une opération valide. Si l’action ne peut pas être appliquée à l’affichage, une erreur s’affiche. |
| Supprimer | Supprime l’action. |

## Utilisation de la VEC pour SPA exemples

Cette section présente trois exemples d’utilisation du compositeur d’expérience visuelle pour créer des actions et des modifications pour les activités A/B ou XT.

### Exemple 1 : Mettre à jour la vue &quot;Accueil&quot;

Auparavant, une vue nommée &quot;Accueil&quot; était définie pour l’ensemble du site d’accueil. Désormais, l’équipe marketing souhaite mettre à jour la vue &quot;Accueil&quot; de l’une des façons suivantes :

* Remplacez les boutons **Ajouter au panier** et **Aimer** par une part plus claire de bleu. Cela doit se produire lors du chargement de la page, car cela implique de modifier les composants de l’en-tête.
* Remplacez le libellé **Derniers produits pour 2019** par **Produits les plus chauds pour 2019** et remplacez la couleur du texte par le violet.

Pour effectuer ces mises à jour dans le compositeur d’expérience visuelle, sélectionnez **Composer** et appliquez ces modifications à la vue &quot;d’accueil&quot;.

![](assets/vec-home.png)

### Exemple 2 : Modification des étiquettes de produits

Pour la vue &quot;products-page-2&quot;, l’équipe marketing souhaite remplacer l’étiquette **Prix** par **Prix de vente** et remplacer la couleur de l’étiquette par rouge.

Pour effectuer ces mises à jour dans le VEC, les étapes suivantes sont requises :

1. Sélectionnez **Parcourir** dans le VEC.
2. Sélectionnez **Produits** dans la barre de navigation supérieure du site.
3. Sélectionnez **Charger plus** une fois pour vue à la deuxième ligne de produits.
4. Sélectionnez **Composer** dans la VEC.
5. Appliquez des actions pour remplacer le libellé de texte par **Prix de vente** et la couleur par le rouge.

![](assets/vec-products-page-2.png)

### Exemple 3 : Personnalisation du style des préférences de livraison

Les vues peuvent être définies à un niveau granulaire, tel qu’un état ou une option d’un bouton radio. Auparavant, dans ce document, les vues étaient définies pour les préférences de livraison, &quot;checkout-normal&quot; et &quot;checkout-express&quot;. L&#39;équipe marketing veut changer la couleur du bouton en rouge pour la vue &quot;Extraction express&quot;.

Pour effectuer ces mises à jour dans le VEC, les étapes suivantes sont requises :

1. Sélectionnez **Parcourir** dans le VEC.
2. Ajoutez des produits au panier sur le site.
3. Sélectionnez l’icône de panier dans le coin supérieur droit du site.
4. Sélectionnez **Extraire votre commande**.
5. Sélectionnez le bouton radio **Livraison express** sous **Préférences de livraison**.
6. Sélectionnez **Composer** dans la VEC.
7. Définissez la couleur rouge du bouton **Payer**.

>[!NOTE]
>
>La vue &quot;Extraction-express&quot; n&#39;apparaît pas dans le panneau Modifications tant que le bouton radio **Livraison express** n&#39;est pas sélectionné. Ceci est dû au fait que la fonction `sendEvent()` est exécutée lorsque le bouton radio **Livraison express** est sélectionné. Par conséquent, le VEC n&#39;est pas au courant de la vue &quot;Extraction express&quot; tant que le bouton radio n&#39;est pas sélectionné.

![](assets/vec-delivery-preference.png)
