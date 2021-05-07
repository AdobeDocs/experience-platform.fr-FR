---
title: Utilisation de Adobe Target avec la plate-forme Web SDK
description: Découvrez comment rendre du contenu personnalisé avec le SDK Web Experience Platform à l’aide d’Adobe Target
keywords: cible;adobe cible;activité.id;experience.id;renderDecision;DecisionScopes;prehide snippet;vec;Form-Based Experience Composer;xdm;audiences;Decision;scope;schéma;
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
translation-type: tm+mt
source-git-commit: e12b1337c44095ee8731f99c5829ab83bba14889
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 5%

---

# Utilisation de Adobe Target avec la plate-forme Web SDK

Adobe Experience Platform [!DNL Web SDK] peut fournir et générer des expériences personnalisées gérées dans Adobe Target sur le canal Web. Vous pouvez utiliser un éditeur WYSIWYG, appelé [compositeur d’expérience visuelle](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) (VEC), ou une interface non visuelle, le [compositeur d’expérience d’après les formulaires](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html), pour créer, activer et fournir vos activités et expériences de personnalisation.

Les fonctionnalités suivantes ont été testées et sont actuellement prises en charge dans Cible :

* Tests A/B
* Rapports d’impression et de conversion A4T
* Automated Personalization
* Ciblage d’expérience
* Tests multivariés
* Rapports d’impression et de conversion des Cibles natives
* Prise en charge de VEC

## Activation de Adobe Target

Pour activer [!DNL Target], procédez comme suit :

1. Activez la cible dans votre configuration [edge](../../fundamentals/edge-configuration.md) avec le code client approprié.
1. Ajoutez l&#39;option `renderDecisions` à vos événements.

Ensuite, vous pouvez également ajouter les options suivantes :

* `decisionScopes`: Récupérez des activités spécifiques (utiles pour les activités créées avec le compositeur d’après les formulaires) en ajoutant cette option à vos événements.
* [Extrait prémasqué](../manage-flicker.md) : Ne masquez que certaines parties de la page.

## Utilisation du compositeur d’expérience visuelle Adobe Target

Pour utiliser le compositeur d’expérience visuelle avec une implémentation du SDK Web de plate-forme, installez et activez l’extension d’assistance du compositeur d’expérience visuelle [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak).

## Activités du compositeur d’expérience visuelle à rendu automatique

Adobe Experience Platform Web SDK permet à vos utilisateurs de rendre automatiquement sur le Web vos expériences définies via le compositeur d’expérience visuelle d’Adobe Target. Pour indiquer au Adobe Experience Platform Web SDK de générer automatiquement des activités du compositeur d’expérience visuelle, envoyez un événement avec `renderDecisions = true` :

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

Le compositeur d’expérience d’après les formulaires est une interface non visuelle utile pour configurer les tests A/B, [!DNL Experience Targeting], Automated Personalization et les activités Recommendations avec différents types de réponse, tels que JSON, HTML, Image, etc. En fonction du type de réponse ou de la décision renvoyée par Adobe Target, votre logique métier de base peut être exécutée. Pour récupérer les décisions relatives à vos activités de compositeur d’après les formulaires, envoyez un événement contenant toutes les &quot;étendues de décision&quot; pour lesquelles vous souhaitez récupérer une décision.

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

`decisionScopes` définit les sections, les emplacements ou les parties de vos pages dans lesquelles vous souhaitez générer une expérience personnalisée. Ces `decisionScopes` sont personnalisables et définies par l&#39;utilisateur. Pour les clients [!DNL Target] actuels, `decisionScopes` sont également appelés &quot;mbox&quot;. Dans l&#39;interface utilisateur [!DNL Target], `decisionScopes` apparaît comme &quot;emplacements&quot;.

## Portée `__view__`

Adobe Experience Platform Web SDK fournit une fonctionnalité qui vous permet de récupérer les actions du compositeur d’expérience visuelle sans vous reposer sur le kit SDK pour effectuer le rendu des actions du compositeur d’expérience visuelle. Envoyer un événement avec `__view__` défini comme `decisionScopes`.

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

Lors de la définition d’Audiences pour vos activités de Cible fournies par le SDK Web Adobe Experience Platform, [XDM](https://docs.adobe.com/content/help/fr-FR/experience-platform/xdm/home.html) doit être défini et utilisé. Après avoir défini des schémas XDM, des classes et des groupes de champs de schéma, vous pouvez créer une règle d&#39;audience de Cible définie par les données XDM pour le ciblage. Dans la Cible, les données XDM s’affichent dans le créateur d’Audiences sous la forme d’un paramètre personnalisé. Le XDM est sérialisé à l’aide de la notation par point (par exemple, `web.webPageDetails.name`).

Si vous disposez d’activités de Cible avec des audiences prédéfinies qui utilisent des paramètres personnalisés ou un profil utilisateur, elles ne sont pas correctement distribuées par le biais du SDK. Au lieu d&#39;utiliser des paramètres personnalisés ou le profil utilisateur, vous devez utiliser XDM à la place. Cependant, il existe des champs de ciblage d’audience prêts à l’emploi pris en charge par le SDK Web Adobe Experience Platform qui ne nécessitent pas XDM. Ces champs sont disponibles dans l’interface utilisateur de la Cible et ne nécessitent pas XDM :

* Bibliothèque Target
* Géo
* Réseau
* Operating System
* Pages du site
* Browser
* Sources de trafic
* Période

## Terminologie

__Décisions :__ Dans  [!DNL Target], les décisions sont corrélées à l’expérience sélectionnée dans une Activité.

__Schéma :__ Le schéma d&#39;une décision est le type d&#39;offre dans  [!DNL Target].

__Portée :__ Portée de la décision. Dans [!DNL Target], la portée est la mBox. La mBox globale est la portée `__view__`.

__XDM :__ le fichier XDM est sérialisé en notation de point, puis placé  [!DNL Target] sous forme de paramètres mBox.
