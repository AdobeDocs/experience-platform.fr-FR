---
title: 'Adobe Target et Adobe Experience Platform Web SDK. '
seo-title: Adobe Experience Platform Web SDK et utilisation de Adobe Target
description: Découvrez comment rendre du contenu personnalisé avec le SDK Web Experience Platform à l’aide d’Adobe Target
seo-description: Découvrez comment rendre du contenu personnalisé avec le SDK Web Experience Platform à l’aide d’Adobe Target
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisionScopes;prehiding snippet;vec;Form-Based Experience Composer;xdm;audiences;decisions;scope;schema;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 5%

---


# [!DNL Target] Présentation

Adobe Experience Platform [!DNL Web SDK] peut fournir et rendre des expériences personnalisées gérées à Adobe Target sur le canal Web. Vous pouvez utiliser un éditeur WYSIWYG, appelé compositeur [d’expérience](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) visuelle (VEC), ou une interface non visuelle, le compositeur d’expérience [basé sur les](https://docs.adobe.com/content/help/fr-FR/target/using/experiences/form-experience-composer.html)formulaires, pour créer, activer et diffuser vos activités et expériences de personnalisation.

## Activation de Adobe Target

Pour l’activer [!DNL Target], vous devez effectuer les opérations suivantes :

1. Activez la cible dans votre configuration [](../../fundamentals/edge-configuration.md) Edge avec le code client approprié.
1. Ajoutez l’ `renderDecisions` option à vos événements.

Ensuite, vous pouvez également :

* Ajoutez `decisionScopes` vos événements pour récupérer des activités spécifiques (utiles pour les activités créées avec le compositeur basé sur les formulaires).
* Ajoutez le fragment de code [](../manage-flicker.md) caché pour masquer uniquement certaines parties de la page.

## Utilisation du compositeur d’expérience visuelle Adobe Target

Pour utiliser le compositeur d’expérience visuelle avec une implémentation du SDK Web de plate-forme, vous devez installer et activer l’extension d’assistance [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC.

## Activités du compositeur d’expérience visuelle à rendu automatique

Adobe Experience Platform Web SDK permet à vos utilisateurs de rendre automatiquement sur le Web vos expériences définies via le compositeur d’expérience visuelle d’Adobe Target. Pour indiquer au Adobe Experience Platform Web SDK de générer automatiquement des activités du compositeur d’expérience visuelle, envoyez un événement avec `renderDecisions = true`:

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

Le compositeur d’expérience d’après les formulaires est une interface non visuelle qui s’avère utile pour configurer des tests A/B, [!DNL Experience Targeting]Automated Personalization et des activités Recommendations avec différents types de réponse, tels que JSON, HTML, Image, etc. En fonction du type de réponse ou de la décision renvoyée par Adobe Target, votre logique métier de base peut être exécutée. Pour récupérer les décisions relatives à vos activités de compositeur d’après les formulaires, envoyez un événement contenant toutes les &quot;étendues de décision&quot; pour lesquelles vous souhaitez récupérer une décision.

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

## Etendues de décision

`decisionScopes` définit les sections, les emplacements ou les parties de vos pages dans lesquelles vous souhaitez générer une expérience personnalisée. Il `decisionScopes` s’agit de personnalisables et définies par l’utilisateur. Pour les [!DNL Target] clients actuels, `decisionScopes` sont également appelés &quot;mbox&quot;. Dans l’ [!DNL Target] interface utilisateur, `decisionScopes` apparaissent les &quot;emplacements&quot;.

## La `__view__` portée

Adobe Experience Platform Web SDK fournit une fonctionnalité qui vous permet de récupérer les actions du compositeur d’expérience visuelle sans vous reposer sur le kit SDK pour effectuer le rendu des actions du compositeur d’expérience visuelle. Envoie un événement avec `__view__` défini comme `decisionScopes`un.

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

Lors de la définition d’Audiences pour vos activités de Cible qui seront distribuées via Adobe Experience Platform Web SDK, [XDM](https://docs.adobe.com/content/help/fr-FR/experience-platform/xdm/home.html) doit être défini et utilisé. Après avoir défini des schémas XDM, des classes et des mixins, vous pouvez créer une règle d’audience de Cible définie par les données XDM pour le ciblage. Dans la Cible, les données XDM s’affichent dans le créateur d’Audiences sous la forme d’un paramètre personnalisé. Le XDM est sérialisé à l’aide de la notation par point (par exemple, `web.webPageDetails.name`).

Si vous disposez d’activités de Cible avec des audiences prédéfinies qui utilisent des paramètres personnalisés ou un profil utilisateur, n’oubliez pas qu’elles ne seront pas diffusées correctement par le biais du SDK. Au lieu d&#39;utiliser des paramètres personnalisés ou le profil utilisateur, vous devez utiliser XDM à la place. Cependant, il existe des champs de ciblage d’audience prêts à l’emploi pris en charge par le SDK Web Adobe Experience Platform qui ne nécessitent pas XDM. Il s’agit des champs disponibles dans l’interface utilisateur de la Cible qui ne nécessitent pas XDM :

* Bibliothèque Target
* Géo
* Réseau
* Operating System
* Pages du site
* Browser
* Sources de trafic
* Période

## Terminologie

__Décisions :__ Dans [!DNL Target]ce cas, elles sont corrélées à l’expérience sélectionnée dans une Activité.

__Schéma :__ Le schéma d&#39;une décision est le type d&#39;offre dans [!DNL Target].

__Portée :__ Portée de la décision. Dans [!DNL Target], voici la mBox. La mBox globale est la `__view__` portée.

__XDM :__ Le fichier XDM est sérialisé en notation de point, puis placé dans [!DNL Target] des paramètres mBox.
