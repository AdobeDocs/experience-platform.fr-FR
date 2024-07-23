---
title: Utilisation d’Adobe Target avec le SDK Web pour la personnalisation
description: Découvrez comment effectuer le rendu du contenu personnalisé avec le SDK Web Experience Platform à l’aide d’Adobe Target
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: b50ea35bf0e394298c0c8f0ffb13032aaa1ffafb
workflow-type: tm+mt
source-wordcount: '1364'
ht-degree: 3%

---

# Utiliser [!DNL Adobe Target] et [!DNL Web SDK] pour la personnalisation

[!DNL Adobe Experience Platform] [!DNL Web SDK] peut fournir et générer des expériences personnalisées gérées dans [!DNL Adobe Target] sur le canal web. Vous pouvez utiliser un éditeur WYSIWYG, appelé [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC), ou une interface non visuelle, le [compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=fr), pour créer, activer et diffuser vos activités et expériences de personnalisation.

>[!IMPORTANT]
>
>Découvrez comment migrer votre mise en oeuvre Target vers le SDK Web Platform avec le tutoriel [Migration de Target d’at.js 2.x vers le SDK Web Platform](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html).
>
>Découvrez comment mettre en oeuvre Target pour la première fois avec le tutoriel [Mise en oeuvre de Adobe Experience Cloud avec le SDK Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=fr) . Pour plus d’informations spécifiques à Target, consultez la section de tutoriel intitulée [Configuration de Target avec le SDK Web Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).


Les fonctionnalités suivantes ont été testées et sont actuellement prises en charge dans [!DNL Target] :

* [Tests A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [Rapports d’impression et de conversion A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Activités Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Activités de ciblage d’expérience](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Tests multivariés (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Activités Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [ Création de rapports d’impression et de conversion natifs pour Target ](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [Prise en charge du VEC](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## Diagramme système [!DNL Web SDK]

Le diagramme suivant vous aide à comprendre le processus de prise de décision en périphérie [!DNL Target] et [!DNL Web SDK].

![Diagramme de prise de décision Adobe Target Edge avec le SDK Web Platform](assets/target-platform-web-sdk-new.png)

| Appeler | Détails |
| --- | --- |
| 1 | L’appareil charge le [!DNL Web SDK]. [!DNL Web SDK] envoie une demande à l’Edge Network avec des données XDM, l’identifiant d’environnement des flux de données, les paramètres transmis et l’identifiant client (facultatif). La page (ou les conteneurs) est pré-masquée. |
| 2 | L’Edge Network envoie la demande aux services Edge pour l’enrichir avec l’identifiant visiteur, le consentement et d’autres informations contextuelles sur le visiteur, telles que la géolocalisation et les noms conviviaux de l’appareil. |
| 3 | L’Edge Network envoie la demande de personnalisation enrichie à la périphérie [!DNL Target] avec l’identifiant visiteur et les paramètres transmis. |
| 4 | Les scripts de profil s’exécutent, puis sont introduits dans l’enregistrement de profil [!DNL Target]. Le stockage des profils récupère les segments de la [!UICONTROL bibliothèque d’audiences] (par exemple, les segments partagés à partir de [!DNL Adobe Analytics], [!DNL Adobe Audience Manager] et [!DNL Adobe Experience Platform]). |
| 5 | En fonction des paramètres de requête d’URL et des données de profil, [!DNL Target] détermine les activités et expériences à afficher pour le visiteur pour la page vue actuelle et pour les futures vues prérécupérées. [!DNL Target] renvoie alors ceci à l’Edge Network. |
| 6 | a. L’Edge Network renvoie la réponse de personnalisation à la page, y compris éventuellement les valeurs de profil pour une personnalisation supplémentaire. Le contenu personnalisé sur la page active est affiché aussi rapidement que possible sans scintillement du contenu par défaut.<br>b. Le contenu personnalisé pour les vues affichées à la suite d’actions de l’utilisateur dans une application d’une seule page (SPA) est mis en cache afin de pouvoir être appliqué instantanément sans appel au serveur supplémentaire lorsque les vues sont déclenchées. <br>c. L’Edge Network envoie l’identifiant visiteur et d’autres valeurs dans des cookies, tels que le consentement, l’ID de session, l’identité, la vérification de cookie et la personnalisation. |
| 7 | Le SDK Web envoie la notification de l’appareil à l’Edge Network. |
| 8 | L’Edge Network transfère les détails [!UICONTROL Analytics for Target] (A4T) (métadonnées d’activité, d’expérience et de conversion) vers la périphérie [!DNL Analytics]. |

## Activation de [!DNL Adobe Target]

Pour activer [!DNL Target], procédez comme suit :

1. Activez [!DNL Target] dans votre [datastream](../../../datastreams/overview.md) avec le code client approprié.
1. Ajoutez l’option `renderDecisions` à vos événements.

Vous pouvez ensuite, éventuellement, ajouter les options suivantes :

* **`decisionScopes`** : récupérez des activités spécifiques (utiles pour les activités créées avec le compositeur basé sur les formulaires) en ajoutant cette option à vos événements.
* **[Prémasquer le fragment de code](../manage-flicker.md)** : masquez uniquement certaines parties de la page.

## Utilisation du VEC d’Adobe Target

Pour utiliser le VEC avec une mise en oeuvre [!DNL Web SDK], installez et activez l’extension d’assistance du VEC [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak).

Pour plus d’informations, voir [Extension d’assistance du compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) dans le *guide Adobe Target*.

## Rendu du contenu personnalisé

Voir [Rendu du contenu de personnalisation](../rendering-personalization-content.md) pour plus d’informations.

## Audiences dans XDM

Lors de la définition d’audiences pour vos activités [!DNL Target] diffusées via [!DNL Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr) doit être défini et utilisé. Après avoir défini les schémas XDM, les classes et les groupes de champs de schéma, vous pouvez créer une règle d’audience [!DNL Target] définie par les données XDM pour le ciblage. Dans [!DNL Target], les données XDM s’affichent dans [!UICONTROL Audience Builder] en tant que paramètre personnalisé. Le XDM est sérialisé à l’aide de la notation par points (par exemple, `web.webPageDetails.name`).

Si vous avez des activités [!DNL Target] avec des audiences prédéfinies qui utilisent des paramètres personnalisés ou un profil utilisateur, elles ne sont pas diffusées correctement via le SDK. Au lieu d’utiliser des paramètres personnalisés pour le profil utilisateur, vous devez utiliser XDM à la place. Cependant, il existe des champs de ciblage d’audience prêts à l’emploi pris en charge par le biais de [!DNL Web SDK] qui ne nécessitent pas XDM. Ces champs sont disponibles dans l’interface utilisateur [!DNL Target] qui ne nécessite pas XDM :

* Bibliothèque Target
* Géo
* Réseau
* Système d’exploitation
* Pages du site
* Navigateur
* Sources de trafic
* Période

Pour plus d’informations, voir [Catégories d’audiences](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html) dans le *guide Adobe Target*.

### Jetons de réponse

Les jetons de réponse sont utilisés pour envoyer des métadonnées à des tiers tels que Google ou Facebook. Les jetons de réponse sont renvoyés
dans le champ `meta` de `propositions` -> `items`. Voici un exemple :

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

Pour collecter les jetons de réponse, vous devez vous abonner à la promesse `alloy.sendEvent`, effectuer une itération sur `propositions` et extraire les détails de `items` -> `meta`.

Chaque `proposition` possède un champ booléen `renderAttempted` indiquant si le `proposition` a été rendu ou non. Consultez l’exemple ci-dessous :

```js
alloy("sendEvent",
  {
    "renderDecisions": true,
    "decisionScopes": [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

Lorsque le rendu automatique est activé, le tableau de propositions contient :

#### Au chargement de la page :

* Compositeur basé sur les formulaires `propositions` avec indicateur `renderAttempted` défini sur `false`
* Propositions basées sur le compositeur d’expérience visuelle avec l’indicateur `renderAttempted` défini sur `true`
* Propositions basées sur le compositeur d’expérience visuelle pour une vue d’application d’une seule page avec l’indicateur `renderAttempted` défini sur `true`

#### On View - change (pour les vues en mémoire cache) :

* Propositions basées sur le compositeur d’expérience visuelle pour une vue d’application d’une seule page avec l’indicateur `renderAttempted` défini sur `true`

Lorsque le rendu automatique est désactivé, le tableau de propositions contient :

#### Au chargement de la page :

* [!DNL Form-based Composer] basé sur `propositions` avec l’indicateur `renderAttempted` défini sur `false`
* Propositions basées sur [!DNL Visual Experience Composer] avec indicateur `renderAttempted` défini sur `false`
* [!DNL Visual Experience Composer] propositions basées sur une vue d’application d’une seule page avec l’indicateur `renderAttempted` défini sur `false`

#### On View - change (pour les vues en mémoire cache) :

* Propositions basées sur le compositeur d’expérience visuelle pour une vue d’application d’une seule page avec l’indicateur `renderAttempted` défini sur `false`

### Mise à jour d’un profil unique

[!DNL Web SDK] vous permet de mettre à jour le profil vers le profil [!DNL Target] et vers le [!DNL Web SDK] en tant qu’événement d’expérience.

Pour mettre à jour un profil [!DNL Target], vérifiez que les données de profil sont transmises avec les éléments suivants :

* Sous `"data {"`
* Sous `"__adobe.target"`
* Préfixe `"profile."`

| Clé | Type | Description |
| --- | --- | --- |
| `renderDecisions` | Booléen | Indique au composant de personnalisation s’il doit interpréter les actions DOM. |
| `decisionScopes` | Tableau `<String>` | Liste des portées pour lesquelles récupérer les décisions |
| `xdm` | Objet | Données formatées dans XDM qui se trouve dans le SDK Web en tant qu’événement d’expérience |
| `data` | Objet | Paires clé/valeur arbitraires envoyées aux solutions [!DNL Target] sous la classe cible. |

<!--Typical [!DNL Web SDK] code using this command looks like the following:-->

**Retarder l&#39;enregistrement des paramètres de profil ou d&#39;entité jusqu&#39;à ce que le contenu soit affiché pour l&#39;utilisateur final**

Pour retarder l’enregistrement des attributs dans le profil jusqu’à l’affichage du contenu, définissez `data.adobe.target._save=false` dans votre requête.

Par exemple, votre site web contient trois portées de décision correspondant à trois liens de catégorie sur le site web (Hommes, Femmes et Enfants) et vous souhaitez effectuer le suivi de la catégorie que l’utilisateur a finalement visitée. Envoyez ces requêtes avec l’indicateur `__save` défini sur `false` pour éviter de conserver la catégorie au moment de la demande du contenu. Une fois le contenu visualisé, envoyez la charge utile appropriée (y compris `eventToken` et `stateToken`) pour que les attributs correspondants soient enregistrés.

L’exemple ci-dessous envoie un message de style trackEvent, exécute des scripts de profil, enregistre des attributs et enregistre immédiatement l’événement.

```js
alloy("sendEvent", {
    "renderDecisions": true,
    "data": {
        "xdm": { // Experience Event XDM data },
            "__adobe": {
                "target": {
                    " __save": true|false,
                    //defaults to true if omitted 
                    "profile.gender": "female",
                    "profile.age": 30,
                    "entity.name": "T-shirt",
                    "entity.id": "1234"
                }
            }
        }
    }
})
```

>[!NOTE]
>
>Si la directive `__save` est omise, l’enregistrement des attributs de profil et d’entité se produit immédiatement. La directive `__save` n’est pertinente que pour les attributs de profil et les détails d’entité.

## Demande de recommandations

Le tableau suivant répertorie les attributs [!DNL Recommendations] et indique si chacun est pris en charge via [!DNL Web SDK] :

| Catégorie | Attribut | État de la prise en charge |
| --- | --- | --- |
| Recommendations - Attributs d’entité par défaut | entity.id | Pris en charge |
|  | entity.name | Pris en charge |
|  | entity.categoryId | Pris en charge |
|  | entity.pageUrl | Pris en charge |
|  | entity.thumbnailUrl | Pris en charge |
|  | entity.message | Pris en charge |
|  | entity.value | Pris en charge |
|  | entity.inventory | Pris en charge |
|  | entity.brand | Pris en charge |
|  | entity.margin | Pris en charge |
|  | entity.event.detailsOnly | Pris en charge |
| Recommendations - Attributs d’entité personnalisés | entity.yourCustomAttributeName | Pris en charge |
| Recommendations : paramètres de mbox/page réservés | excludedIds | Pris en charge |
|  | cartIds | Pris en charge |
|  | productPurchasedId | Pris en charge |
| Page ou catégorie d’élément pour les affinités catégorielles | user.categoryId | Pris en charge |

**Comment envoyer des attributs Recommendations à Adobe Target :**

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## Affichage des mesures de conversion de mbox {#display-mbox-conversion-metrics}

L’exemple ci-dessous montre comment effectuer le suivi des conversions des mbox d’affichage et envoyer des paramètres de profil à Adobe Target, sans avoir à être admissible pour un contenu ou une activité.

```js
alloy("sendEvent", {
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [{
                    "scope": "conversion-step-1" //example scope name
                }],
                "propositionEventType": {
                    "display": 1
                }
            }
        },
        "eventType": "decisioning.propositionDisplay"
    }
});
```


| Propriété | Description |
|---------|----------|
| `xdm._experience.decisioning.propositions[x].scope` | Portée à laquelle associer la mesure de succès (qui l’attribuera à une activité spécifique du côté cible). |
| `xdm._experience.decisioning.propositions[x].eventType` | Chaîne décrivant le type d’événement prévu. Définissez-le sur `"decisioning.propositionDisplay"` pour ce cas d’utilisation. |

## Débogage

mboxTrace et mboxDebug ont été abandonnés. Utilisez plutôt une méthode de [débogage du SDK Web](/help/web-sdk/use-cases/debugging.md) .

## Terminologie

__Propositions :__ Dans [!DNL Adobe Target], les propositions correspondent à l’expérience sélectionnée dans une activité.

__Schéma :__ Le schéma d’une décision est le type d’offre dans [!DNL Adobe Target].

__Portée :__ Portée de la décision. Dans [!DNL Adobe Target], la portée est la mBox. La mBox globale est la portée `__view__`.

__XDM :__ Le XDM est sérialisé en notation par point, puis placé dans [!DNL Adobe Target] en tant que paramètres mBox.
