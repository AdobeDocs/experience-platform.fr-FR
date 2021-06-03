---
title: Utilisation d’Adobe Target avec le SDK Web Platform
description: Découvrez comment effectuer le rendu du contenu personnalisé avec le SDK Web Experience Platform à l’aide d’Adobe Target
keywords: target;adobe target;activity.id;experience.id;renderDecisions;DecisionScopes;fragment de code de prémasquage;vec;compositeur d’expérience d’après les formulaires;xdm;audiences;décisions;portée;schéma;
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 202a77e4f9e8c7d5515ea0a5004b1c339f1d58ba
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 3%

---

# Utilisation de [!DNL Adobe Target] avec la balise [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] peut fournir et générer des expériences personnalisées gérées dans  [!DNL Adobe Target] sur le canal web. Vous pouvez utiliser un éditeur WYSIWYG, appelé [compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), ou une interface non visuelle, le [compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), pour créer, activer et diffuser vos activités et expériences de personnalisation.

Les fonctionnalités suivantes ont été testées et sont actuellement prises en charge dans [!DNL Target] :

* [Tests A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [Rapports d’impression et de conversion A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Activités Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Activités de ciblage d’expérience](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Tests multivariés (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Création de rapports d’impression et de conversion Target natifs](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [Prise en charge du compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

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

## Rendu automatique des activités du VEC

La fonction [!DNL Adobe Experience Platform Web SDK] peut rendre automatiquement vos expériences définies via le compositeur d’expérience visuelle de [!DNL Adobe Target] sur le web pour vos utilisateurs. Pour indiquer à [!DNL Experience Platform Web SDK] d’effectuer le rendu automatique des activités du VEC, envoyez un événement avec `renderDecisions = true` :

```javascript
alloy
("sendEvent", 
  { 
  "renderDecisions": true, 
  "xdm": {
    "commerce": { 
      "order": {
        "purchaseID": "a8g784hjq1mnp3", 
         "purchaseOrderNumber": "VAU3123", 
         "currencyCode": "USD", 
         "priceTotal": 999.98 
         } 
      } 
    }
  }
);
```

## Utilisation du compositeur d’après les formulaires

Le [compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) est une interface non visuelle utile pour configurer les [!UICONTROL tests A/B], [!UICONTROL ciblage d’expérience], [!UICONTROL Automated Personalization] et les activités [!UICONTROL Recommendations] avec différents types de réponse, tels que JSON, HTML, etc. Selon le type de réponse ou la décision renvoyé par [!DNL Target], votre logique métier principale peut être exécutée. Pour récupérer les décisions pour vos activités de compositeur d’après les formulaires, envoyez un événement avec tous les &quot;périmètres de décision&quot; pour lesquels vous souhaitez récupérer une décision.

```javascript
alloy
  ("sendEvent", { 
    decisionScopes: [
      "foo", "bar"], 
      "xdm": {
        "commerce": { 
          "order": { 
            "purchaseID": "a8g784hjq1mnp3", 
            "purchaseOrderNumber": "VAU3123", 
            "currencyCode": "USD", 
            "priceTotal": 999.98 
          } 
        } 
      } 
    }
  );
```

## Portées de décision

`decisionScopes` définissez des sections, des emplacements ou des parties de vos pages dans lesquelles vous souhaitez effectuer le rendu d’une expérience personnalisée. Ces `decisionScopes` sont personnalisables et définies par l’utilisateur. Pour les clients [!DNL Target] actuels, `decisionScopes` sont également appelés &quot;mbox&quot;. Dans l’interface utilisateur [!DNL Target], `decisionScopes` apparaît comme &quot;emplacements&quot;.

## Portée `__view__`

[!DNL Experience Platform Web SDK] fournit la fonctionnalité permettant de récupérer les actions du VEC sans compter sur le SDK pour effectuer le rendu des actions du VEC pour vous. Envoyez un événement avec `__view__` défini comme `decisionScopes`.

```javascript
alloy("sendEvent", {
      "decisionScopes": ["__view__", "foo", "bar"], 
      "xdm": { 
        "web": { 
          "webPageDetails": { 
            "name": "Home Page"
          }
        } 
      }
    }
  ).then(function(results) {
    for (decision of results.decisions) {
      if (decision.decisionScope === "__view__") {
        console.log(decision.content)
      }
    }
  });
```

## Audiences dans XDM

Lors de la définition d’audiences pour vos activités [!DNL Target] diffusées via [!DNL Platform Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr) doit être défini et utilisé. Après avoir défini les schémas XDM, les classes et les groupes de champs de schéma, vous pouvez créer une règle d’audience [!DNL Target] définie par les données XDM pour le ciblage. Dans [!DNL Target], les données XDM s’affichent dans [!UICONTROL Audience Builder] en tant que paramètre personnalisé. Le XDM est sérialisé à l’aide de la notation par points (par exemple, `web.webPageDetails.name`).

Si vous avez des activités [!DNL Target] avec des audiences prédéfinies qui utilisent des paramètres personnalisés ou un profil utilisateur, elles ne sont pas diffusées correctement via le SDK. Au lieu d’utiliser des paramètres personnalisés pour le profil utilisateur, vous devez utiliser XDM à la place. Cependant, il existe des champs de ciblage d’audience prêts à l’emploi pris en charge par le biais de [!DNL Platform Web SDK] qui ne nécessitent pas XDM. Ces champs sont disponibles dans l’interface utilisateur [!DNL Target] qui ne nécessite pas XDM :

* Bibliothèque Target
* Géo
* Réseau
* Operating System
* Pages du site
* Browser
* Sources de trafic
* Période

Pour plus d’informations, voir [Catégories d’audiences](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) dans le *guide Adobe Target*.

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
   data: { // Freeform stuff (event & profile) }
});
```

**Exemple de code**

```
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    device: {
      screenWidth: 9999
    }
  },
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
}) 
.then(console.log);
```

## Terminologie

__Décisions :__ dans  [!DNL Target], les décisions sont corrélées à l’expérience sélectionnée à partir d’une activité.

__Schéma :__ le schéma d’une décision est le type d’offre dans  [!DNL Target].

__Portée :__ la portée de la décision. Dans [!DNL Target], la portée est la mBox. La mBox globale est la portée `__view__`.

__XDM :__ le XDM est sérialisé en notation par point, puis placé dans  [!DNL Target] en tant que paramètres mBox.
