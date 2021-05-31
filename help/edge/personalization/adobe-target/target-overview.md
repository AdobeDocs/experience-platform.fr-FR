---
title: Utilisation d’Adobe Target avec le SDK Web Platform
description: Découvrez comment effectuer le rendu du contenu personnalisé avec le SDK Web Experience Platform à l’aide d’Adobe Target
keywords: target;adobe target;activity.id;experience.id;renderDecisions;DecisionScopes;fragment de code de prémasquage;vec;compositeur d’expérience d’après les formulaires;xdm;audiences;décisions;portée;schéma;
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 3%

---

# Utilisation d’Adobe Target avec le SDK Web Platform

Adobe Experience Platform [!DNL Web SDK] peut diffuser et générer des expériences personnalisées gérées dans Adobe Target sur le canal web. Vous pouvez utiliser un éditeur WYSIWYG, appelé [compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), ou une interface non visuelle, le [compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), pour créer, activer et diffuser vos activités et expériences de personnalisation.

Les fonctionnalités suivantes ont été testées et sont actuellement prises en charge dans Target :

* Tests A/B
* Rapports d’impression et de conversion A4T
* Automated Personalization
* Ciblage d’expérience
* Tests multivariés
* Création de rapports d’impression et de conversion Target natifs
* Prise en charge du compositeur d’expérience visuelle

## Activation d’Adobe Target

Pour activer [!DNL Target], procédez comme suit :

1. Activez Target dans votre [flux de données](../../fundamentals/datastreams.md) avec le code client approprié.
1. Ajoutez l’option `renderDecisions` à vos événements.

Vous pouvez ensuite, éventuellement, ajouter les options suivantes :

* `decisionScopes`: Récupérez des activités spécifiques (utiles pour les activités créées avec le compositeur basé sur les formulaires) en ajoutant cette option à vos événements.
* [Fragment](../manage-flicker.md) de prémasquage : Masquez uniquement certaines parties de la page.

## Utilisation du VEC d’Adobe Target

Pour utiliser le VEC avec une mise en oeuvre du SDK Web Platform, installez et activez l’extension d’assistance [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC.

## Rendu automatique des activités du VEC

Le SDK Web de Adobe Experience Platform permet à vos utilisateurs de rendre automatiquement vos expériences définies via le VEC d’Adobe Target sur le web. Pour indiquer au SDK Web de Adobe Experience Platform d’effectuer le rendu automatique des activités du VEC, envoyez un événement avec `renderDecisions = true` :

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

Le compositeur d’expérience d’après les formulaires est une interface non visuelle qui s’avère utile pour configurer les activités de tests A/B, [!DNL Experience Targeting], Automated Personalization et Recommendations avec différents types de réponse, tels que JSON, HTML, Image, etc. Selon le type de réponse ou la décision renvoyé par Adobe Target, votre logique métier de base peut être exécutée. Pour récupérer les décisions pour vos activités de compositeur d’après les formulaires, envoyez un événement avec tous les &quot;périmètres de décision&quot; pour lesquels vous souhaitez récupérer une décision.

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

`decisionScopes` définit les sections, les emplacements ou les parties de vos pages dans lesquelles vous souhaitez effectuer le rendu d’une expérience personnalisée. Ces `decisionScopes` sont personnalisables et définies par l’utilisateur. Pour les clients [!DNL Target] actuels, `decisionScopes` sont également appelés &quot;mbox&quot;. Dans l’interface utilisateur [!DNL Target], `decisionScopes` apparaît comme &quot;emplacements&quot;.

## Portée `__view__`

Le SDK Web de Adobe Experience Platform fournit une fonctionnalité permettant de récupérer les actions du VEC sans compter sur le SDK pour effectuer le rendu des actions du VEC pour vous. Envoyez un événement avec `__view__` défini comme `decisionScopes`.

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

Lors de la définition des audiences pour vos activités Target diffusées via le SDK Web Adobe Experience Platform, [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr) doit être défini et utilisé. Après avoir défini des schémas XDM, des classes et des groupes de champs de schéma, vous pouvez créer une règle d’audience Target définie par des données XDM pour le ciblage. Dans Target, les données XDM s’affichent dans Audience Builder sous la forme d’un paramètre personnalisé. Le XDM est sérialisé à l’aide de la notation par points (par exemple, `web.webPageDetails.name`).

Si vous disposez d’activités Target avec des audiences prédéfinies qui utilisent des paramètres personnalisés ou un profil utilisateur, elles ne sont pas correctement diffusées via le SDK. Au lieu d’utiliser des paramètres personnalisés pour le profil utilisateur, vous devez utiliser XDM à la place. Cependant, il existe des champs de ciblage d’audience prêts à l’emploi pris en charge par le biais du SDK Web Adobe Experience Platform qui ne nécessitent pas XDM. Ces champs sont disponibles dans l’interface utilisateur de Target qui ne nécessite pas XDM :

* Bibliothèque Target
* Géo
* Réseau
* Operating System
* Pages du site
* Browser
* Sources de trafic
* Période

## Terminologie

__Décisions :__ dans  [!DNL Target], les décisions sont corrélées à l’expérience sélectionnée à partir d’une activité.

__Schéma :__ le schéma d’une décision est le type d’offre dans  [!DNL Target].

__Portée :__ la portée de la décision. Dans [!DNL Target], la portée est la mBox. La mBox globale est la portée `__view__`.

__XDM :__ le XDM est sérialisé en notation par point, puis placé dans  [!DNL Target] en tant que paramètres mBox.
