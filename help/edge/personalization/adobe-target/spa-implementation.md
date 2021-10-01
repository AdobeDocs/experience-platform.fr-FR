---
title: Mise en oeuvre d’applications d’une seule page pour le SDK Web de Adobe Experience Platform
description: Découvrez comment créer une implémentation d’application d’une seule page (SPA) du SDK Web de Adobe Experience Platform à l’aide d’Adobe Target.
keywords: target;adobe target;vues xdm; vues;applications d’une seule page;SPA;SPA cycle de vie;test AB;AB;ciblage d’expérience;XT;VEC
exl-id: cc48c375-36b9-433e-b45f-60e6c6ea4883
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 12%

---

# Implémentation d’applications d’une seule page

Le SDK Web de Adobe Experience Platform offre des fonctionnalités riches qui permettent à votre entreprise d’exécuter la personnalisation sur les technologies côté client de nouvelle génération, telles que les applications d’une seule page (SPA).

Les sites Web traditionnels fonctionnaient sur des modèles de navigation « page à page », appelés également applications multi-pages dans lesquelles les conceptions de site Web étaient étroitement couplées à des URL et les transitions d’une page Web à une autre nécessitaient un chargement de page.

Les applications web modernes, telles que les applications d’une seule page, ont adopté un modèle qui propulse l’utilisation rapide du rendu de l’interface utilisateur du navigateur, souvent indépendant des rechargements de page. Ces expériences peuvent être déclenchées par des interactions client, telles que des défilés, des clics et des mouvements de curseur. À mesure que les paradigmes du web moderne évoluent, la pertinence des événements génériques traditionnels, tels qu’un chargement de page, pour déployer la personnalisation et l’expérimentation ne fonctionne plus.

![](assets/spa-vs-traditional-lifecycle.png)

## Avantages du SDK Web Platform pour SPA

Voici quelques avantages de l’utilisation du SDK Web Adobe Experience Platform pour vos applications d’une seule page :

* Capacité à mettre en cache toutes les offres au chargement de la page afin de passer de plusieurs appels serveur à un seul appel serveur.
* Améliorez considérablement l’expérience utilisateur de votre site, car les offres sont immédiatement affichées via le cache sans délai intégré aux appels serveur traditionnels.
* Une seule ligne de code et une configuration de développeur unique permettent aux marketeurs de créer et d’exécuter des activités A/B et de ciblage d’expérience (XT) via le compositeur d’expérience visuelle (VEC) sur votre SPA.

## Vues XDM et applications d’une seule page

Le VEC d’Adobe Target pour SPA tire parti d’un concept appelé Vues : un groupe logique d’éléments visuels qui, ensemble, constituent une expérience SPA. Une application d’une seule page peut donc être considérée comme une transition entre les vues, au lieu des URL, selon les interactions de l’utilisateur. Une Vue peut généralement représenter un site entier ou des éléments visuels regroupés dans un site.

Pour expliquer plus en détail les vues, l’exemple suivant utilise un hypothétique site de commerce électronique en ligne implémenté dans React pour explorer les exemples de vues.

Après avoir accédé au site d’accueil, une image à forte identification fait la promotion d’une vente de Pâques ainsi que des produits les plus récents disponibles sur le site. Dans ce cas, une Vue peut être définie pour l’ensemble de l’écran d’accueil. Ce point de vue peut simplement être appelé &quot;accueil&quot;.

![](assets/example-views.png)

À mesure que le client s’intéresse davantage aux produits que l’entreprise vend, il décide de cliquer sur le lien **Produits** . Comme pour le site d’accueil, l’intégralité du site de produits peut être définie comme une ue.V Cette vue peut être nommée &quot;products-all&quot;.

![](assets/example-products-all.png)

Une Vue pouvant être définie comme un site entier ou un groupe d’éléments visuels sur un site, les quatre produits affichés sur le site de produits peuvent être regroupés et considérés comme une Vue. Cette vue peut être appelée &quot;produits&quot;.

![](assets/example-products.png)

Lorsque le client décide de cliquer sur le bouton **Charger plus** pour explorer d’autres produits sur le site, l’URL du site web ne change pas dans ce cas, mais une Vue peut être créée ici pour représenter uniquement la deuxième ligne de produits qui s’affichent. Le nom de la vue peut être &quot;products-page-2&quot;.

![](assets/example-load-more.png)

Le client décide d’acheter quelques produits sur le site et passe à l’écran de passage en caisse. Sur le site de paiement, le client dispose d’options lui permettant de choisir une diffusion normale ou express. Une Vue peut être n’importe quel groupe d’éléments visuels d’un site. Une Vue peut donc être créée pour les préférences de diffusion et appelée &quot;Préférences de diffusion&quot;.

![](assets/example-check-out.png)

Le concept de Vues peut être étendu beaucoup plus loin. Il ne s’agit que de quelques exemples de vues qui peuvent être définies sur un site.

## Implémentation des vues XDM

Les vues XDM peuvent être exploitées dans Adobe Target pour permettre aux marketeurs d’exécuter des tests A/B et XT sur SPA via le compositeur d’expérience visuelle. Pour effectuer une configuration de développeur unique, procédez comme suit :

1. Installer [SDK Web Adobe Experience Platform](../../fundamentals/installing-the-sdk.md)
2. Déterminez toutes les vues XDM de votre application d’une seule page que vous souhaitez personnaliser.
3. Après avoir défini les vues XDM, pour diffuser des activités AB ou XT VEC, implémentez la fonction `sendEvent()` avec `renderDecisions` défini sur `true` et la vue XDM correspondante dans votre application de page unique. La vue XDM doit être transmise dans `xdm.web.webPageDetails.viewName`. Cette étape permet aux marketeurs d’utiliser le compositeur d’expérience visuelle pour lancer des tests A/B et XT pour ces XDM.

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
>Lors du premier appel `sendEvent()`, toutes les vues XDM qui doivent être rendues à l’utilisateur final seront récupérées et mises en cache. Les appels `sendEvent()` suivants avec les vues XDM transmises seront lus à partir du cache et rendus sans appel au serveur.

## `sendEvent()` exemples de fonctions

Cette section présente trois exemples illustrant l’appel de la fonction `sendEvent()` dans React pour une hypothèse de SPA de commerce électronique.

### Exemple 1 : Page d’accueil du test A/B

L’équipe marketing souhaite exécuter des tests A/B sur l’ensemble de la page d’accueil.

![](assets/use-case-1.png)

Pour exécuter des tests A/B sur l’ensemble du site d’accueil, `sendEvent()` doit être appelé en définissant XDM `viewName` sur `home` :

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

L’équipe marketing souhaite personnaliser la deuxième ligne de produits en définissant la couleur du libellé du prix sur rouge après qu’un utilisateur a cliqué sur **Charger plus**.

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

### Exemple 3 : Préférences de diffusion du test A/B

L’équipe marketing souhaite exécuter un test A/B afin de déterminer si la modification de la couleur du bouton du bleu au rouge lorsque l’option **Livraison express** est sélectionnée peut augmenter les conversions (au lieu de conserver la couleur bleue du bouton pour les deux options de livraison).

![](assets/use-case-3.png)

Pour personnaliser le contenu du site en fonction des préférences de diffusion sélectionnées, une Vue peut être créée pour chaque préférence de diffusion. Lorsque **Livraison normale** est sélectionné, la vue peut être nommée &quot;checkout-normal&quot;. Si **Livraison express** est sélectionné, la vue peut être nommée &quot;Extraction-express&quot;.

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

Une fois que vous avez défini vos vues XDM et mis en oeuvre `sendEvent()` avec ces vues XDM transmises, le VEC peut détecter ces vues et permettre aux utilisateurs de créer des actions et des modifications pour les activités A/B ou XT.

>[!NOTE]
>
>Pour utiliser le compositeur d’expérience visuelle pour votre SPA, vous devez installer et activer l’extension d’assistance [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC.

### Panneau des modifications

Le panneau Modifications capture les actions créées pour une vue spécifique. Toutes les actions d’une vue sont regroupées sous cette vue.

![](assets/modifications-panel.png)

### Actions

Cliquer sur une action met en évidence l’élément de la page sur lequel cette action sera appliquée. Chaque action du VEC créée sous une vue comporte les icônes suivantes : **Informations**, **Modifier**, **Cloner**, **Déplacer** et **Supprimer**. Ces icônes sont expliquées plus en détail dans le tableau qui suit.

![](assets/action-icons.png)

| Icon | Description |
|---|---|
| Informations | Affiche les détails de cette action. |
| Modifier | Permet de modifier directement les propriétés de cette action. |
| Dupliquer | Cloner l’action vers une ou plusieurs vues figurant dans le panneau Modifications ou vers une ou plusieurs vues que vous avez parcourues et auxquelles vous avez accédé dans le VEC. L’action n’a pas nécessairement besoin d’exister dans le panneau Modifications.<br/><br/>**Remarque :** Une fois une opération de clonage effectuée, vous devez accéder à la vue dans le VEC via Parcourir pour vérifier si l’action clonée a été une opération valide. Si l’action ne peut pas être appliquée à l’affichage, une erreur s’affiche. |
| Déplacer | Déplace l’action vers un événement de chargement de page ou tout autre vue existant dans le panneau Modifications.<br/><br/>**Événement de chargement de page :** toutes les actions correspondant à l’événement de chargement de page sont appliquées au chargement initial de la page de votre application web. <br/><br/>**Remarque :** Une fois une opération de déplacement effectuée, vous devez accéder à la vue dans le VEC via Parcourir pour vérifier si le déplacement a été une opération valide. Si l’action ne peut pas être appliquée à l’affichage, une erreur s’affiche. |
| Supprimer | Supprime l’action. |

## Utilisation du compositeur d’expérience visuelle pour SPA exemples

Cette section présente trois exemples d’utilisation du compositeur d’expérience visuelle pour créer des actions et des modifications pour les activités A/B ou XT.

### Exemple 1 : Mettre à jour la vue &quot;accueil&quot;

Auparavant, dans ce document, une vue nommée &quot;accueil&quot; était définie pour l’ensemble du site d’accueil. L’équipe marketing souhaite maintenant mettre à jour la vue &quot;accueil&quot; de la manière suivante :

* Remplacez les boutons **Ajouter au panier** et **Comme** par un partage plus clair de bleu. Cela doit se produire lors du chargement de la page, car cela implique de modifier les composants de l’en-tête.
* Remplacez le libellé **Derniers produits pour 2019** par **Produits les plus chauds pour 2019** et remplacez la couleur du texte par le violet.

Pour effectuer ces mises à jour dans le VEC, sélectionnez **Composer** et appliquez ces modifications à la vue &quot;accueil&quot;.

![](assets/vec-home.png)

### Exemple 2 : Modification des étiquettes de produit

Pour la vue &quot;products-page-2&quot;, l’équipe marketing souhaite remplacer l’étiquette **Prix** par **Prix de vente** et changer la couleur du libellé en rouge.

Pour effectuer ces mises à jour dans le compositeur d’expérience visuelle, procédez comme suit :

1. Sélectionnez **Parcourir** dans le VEC.
2. Sélectionnez **Produits** dans la barre de navigation supérieure du site.
3. Sélectionnez **Charger plus** une fois pour afficher la deuxième ligne de produits.
4. Sélectionnez **Composer** dans le VEC.
5. Appliquez les actions pour remplacer le libellé du texte par **Prix de vente** et modifier la couleur en rouge.

![](assets/vec-products-page-2.png)

### Exemple 3 : Personnaliser le style des préférences de diffusion

Les vues peuvent être définies à un niveau granulaire, par exemple un état ou une option d’un bouton radio. Auparavant, dans ce document, les vues étaient définies pour les préférences de livraison, &quot;checkout-normal&quot; et &quot;checkout-express&quot;. L’équipe marketing souhaite remplacer la couleur du bouton par le rouge pour la vue &quot;express&quot;.

Pour effectuer ces mises à jour dans le compositeur d’expérience visuelle, procédez comme suit :

1. Sélectionnez **Parcourir** dans le VEC.
2. Ajoutez des produits au panier sur le site.
3. Sélectionnez l’icône de panier dans le coin supérieur droit du site.
4. Sélectionnez **Extraire votre commande**.
5. Sélectionnez le bouton radio **Livraison express** sous **Préférences de remise**.
6. Sélectionnez **Composer** dans le VEC.
7. Remplacez la couleur du bouton **Payer** par rouge.

>[!NOTE]
>
>La vue &quot;checkout-express&quot; n’apparaît pas dans le panneau Modifications tant que le bouton radio **Livraison express** n’a pas été sélectionné. Cela est dû au fait que la fonction `sendEvent()` est exécutée lorsque le bouton radio **Livraison express** est sélectionné. Par conséquent, le VEC ne connaît pas la vue &quot;checkout-express&quot; tant que le bouton radio n’a pas été sélectionné.

![](assets/vec-delivery-preference.png)
