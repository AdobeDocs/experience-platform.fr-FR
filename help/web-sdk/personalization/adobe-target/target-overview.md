---
title: Utilisation d’Adobe Target avec Web SDK pour la personnalisation
description: Découvrez comment effectuer le rendu du contenu personnalisé avec Experience Platform Web SDK à l’aide d’Adobe Target
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 3%

---

# Utilisation de [!DNL Adobe Target] et [!DNL Web SDK] pour la personnalisation

[!DNL Adobe Experience Platform] [!DNL Web SDK] peut diffuser et générer des expériences personnalisées gérées dans [!DNL Adobe Target] au canal web. Vous pouvez utiliser un éditeur WYSIWYG, appelé [Compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=fr) (VEC), ou une interface non visuelle, le [Compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=fr), pour créer, activer et diffuser vos activités et expériences de personnalisation.

>[!IMPORTANT]
>
>Découvrez comment migrer votre implémentation Target vers Experience Platform Web SDK à l’aide du tutoriel [Migration de Target d’at.js 2.x vers Experience Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=fr).
>
>Découvrez comment mettre en œuvre Target pour la première fois à l’aide du tutoriel [Implémentation de Adobe Experience Cloud avec Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=fr). Pour plus d’informations spécifiques à Target, consultez la section du tutoriel intitulée [Configuration de Target avec Experience Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=fr).


Les fonctionnalités suivantes ont été testées et sont actuellement prises en charge dans [!DNL Target] :

* [Tests AB](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=fr)
* [Rapports d’impression et de conversion A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=fr)
* [Activités Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=fr)
* [Activités de ciblage d’expérience](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=fr)
* [Tests multivariés (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html?lang=fr)
* [Activités Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html?lang=fr)
* [Création de rapports native sur les impressions et les conversions de Target](https://experienceleague.adobe.com/docs/target/using/reports/reports.html?lang=fr)
* [Prise en charge du compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=fr)

## Diagramme système [!DNL Web SDK]

Le diagramme suivant vous aide à comprendre le workflow de la prise de décision [!DNL Target] et [!DNL Web SDK] Edge.

![Diagramme d’Adobe Target Edge Decisioning avec Experience Platform Web SDK](assets/target-platform-web-sdk-new.png)

| Appel | Détails |
| --- | --- |
| 1 | L’appareil charge le [!DNL Web SDK]. Le [!DNL Web SDK] envoie une requête à Edge Network avec les données XDM, l’identifiant d’environnement des flux de données, les paramètres transmis et l’identifiant client (facultatif). La page (ou les conteneurs) est prémasquée. |
| 2 | Edge Network envoie la requête aux services Edge pour l’enrichir avec l’identifiant visiteur, le consentement et d’autres informations contextuelles du visiteur, telles que la géolocalisation et les noms compatibles avec les appareils. |
| 3 | Edge Network envoie la demande de personnalisation enrichie à l’Edge de [!DNL Target] avec l’identifiant visiteur et les paramètres transmis. |
| 4 | Les scripts de profil s’exécutent, puis sont intégrés dans [!DNL Target] stockage de profil. Le stockage des profils récupère les segments de la [!UICONTROL Bibliothèque d’audiences] (par exemple, les segments partagés depuis [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], le [!DNL Adobe Experience Platform]). |
| 5 | En fonction des paramètres de requête d’URL et des données de profil, [!DNL Target] détermine les activités et expériences à afficher pour le visiteur pour la page vue actuelle et pour les vues prérécupérées futures. [!DNL Target] le renvoie ensuite à Edge Network. |
| 6 | a. L’Edge Network renvoie la réponse de personnalisation à la page, y compris éventuellement les valeurs de profil pour une personnalisation supplémentaire. Le contenu personnalisé sur la page active est révélé le plus rapidement possible sans scintillement du contenu par défaut.<br>b. Le contenu personnalisé des vues présentées à la suite d’actions de l’utilisateur dans une application d’une seule page (SPA) est mis en cache afin de pouvoir être appliqué instantanément sans appel au serveur supplémentaire lorsque les vues sont déclenchées. <br>c. Edge Network envoie l’identifiant visiteur et d’autres valeurs dans les cookies, telles que le consentement, l’identifiant de session, l’identité, la vérification des cookies et la personnalisation. |
| 7 | Le SDK Web envoie la notification de l’appareil vers Edge Network. |
| 8 | Edge Network transfère les détails [!UICONTROL Analytics for Target] (A4T) (métadonnées d’activité, d’expérience et de conversion) vers [!DNL Analytics] Edge. |

## Activation de [!DNL Adobe Target]

Pour [!DNL Target] activer, procédez comme suit :

1. Activez [!DNL Target] dans votre [flux de données](../../../datastreams/overview.md) avec le code client approprié.
1. Ajoutez l’option `renderDecisions` à vos événements.

Vous pouvez ensuite éventuellement ajouter les options suivantes :

* **`decisionScopes`** : récupérez les activités spécifiques (utiles pour les activités créées avec le compositeur basé sur les formulaires) en ajoutant cette option à vos événements.
* **[Masquage préalable du fragment de code](../manage-flicker.md)** : masquez uniquement certaines parties de la page.

## Utilisation du VEC d’Adobe Target

Pour utiliser le VEC avec une implémentation [!DNL Web SDK], installez et activez l’extension d’assistance du VEC [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak).

Pour plus d’informations, voir [Extension d’assistance du compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=fr) dans le guide *Adobe Target*.

## Rendu du contenu personnalisé

Pour plus d’informations, consultez [ Rendu de contenu de personnalisation ](../rendering-personalization-content.md) .

## Audiences dans XDM

Lors de la définition des audiences pour vos activités [!DNL Target] diffusées via le [!DNL Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr) doit être défini et utilisé. Après avoir défini des schémas, des classes et des groupes de champs de schéma XDM, vous pouvez créer une règle d’audience [!DNL Target] définie par les données XDM pour le ciblage. Dans [!DNL Target], les données XDM s’affichent dans le [!UICONTROL Audience Builder] sous la forme d’un paramètre personnalisé. Le fichier XDM est sérialisé à l’aide de la notation par points (par exemple, `web.webPageDetails.name`).

Si vous disposez d’activités [!DNL Target] avec des audiences prédéfinies qui utilisent des paramètres personnalisés ou un profil utilisateur, elles ne sont pas correctement diffusées via le SDK. Au lieu d’utiliser des paramètres personnalisés pour le profil utilisateur, vous devez utiliser XDM. Cependant, il existe des champs de ciblage d’audience prêts à l’emploi pris en charge via le [!DNL Web SDK] qui ne nécessitent pas XDM. Ces champs sont disponibles dans l’interface utilisateur de [!DNL Target] qui ne nécessitent pas XDM :

* Bibliothèque Target
* Géo
* Réseau
* Système d’exploitation
* Pages du site
* Navigateur
* Sources de trafic
* Période

Pour plus d’informations, voir [Catégories d’audiences](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=fr) dans le guide *Adobe Target*.

### Jetons de réponse

Les jetons de réponse sont utilisés pour envoyer des métadonnées à des tiers tels que Google ou Facebook. Des jetons de réponse sont renvoyés.
dans le champ `meta` dans `propositions` -> `items`. Voici un exemple :

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

Pour collecter les jetons de réponse, vous devez vous abonner à `alloy.sendEvent` promesse, effectuer une itération sur `propositions` et extraire les détails de `items` -> `meta`.

Chaque `proposition` comporte un champ booléen `renderAttempted` indiquant si le `proposition` a été rendu ou non. Voir l’exemple ci-dessous :

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

Lorsque le rendu automatique est activé, le tableau des propositions contient :

#### Au chargement de la page :

* `propositions` basé sur le compositeur basé sur les formulaires avec l’indicateur `renderAttempted` défini sur `false`
* Propositions basées sur le compositeur d’expérience visuelle avec `renderAttempted` indicateur défini sur `true`
* Propositions basées sur le compositeur d’expérience visuelle pour une vue d’application monopage avec `renderAttempted` indicateur défini sur `true`

#### En mode Modification (pour les vues mises en cache) :

* Propositions basées sur le compositeur d’expérience visuelle pour une vue d’application monopage avec `renderAttempted` indicateur défini sur `true`

Lorsque le rendu automatique est désactivé, le tableau des propositions contient :

#### Au chargement de la page :

* `propositions` basé sur des [!DNL Form-based Composer] avec indicateur `renderAttempted` défini sur `false`
* Propositions basées sur des [!DNL Visual Experience Composer] avec `renderAttempted` indicateur défini sur `false`
* Propositions basées sur des [!DNL Visual Experience Composer] pour une vue d’application monopage avec `renderAttempted` indicateur défini sur `false`

#### En mode Modification (pour les vues mises en cache) :

* Propositions basées sur le compositeur d’expérience visuelle pour une vue d’application monopage avec `renderAttempted` indicateur défini sur `false`

### Mise à jour de profil individuel

L’[!DNL Web SDK] vous permet de mettre à jour le profil vers le profil [!DNL Target] et vers le [!DNL Web SDK] en tant qu’événement d’expérience.

Pour mettre à jour un profil de [!DNL Target], assurez-vous que les données du profil sont transmises avec les éléments suivants :

* Sous `"data {"`
* Sous `"__adobe.target"`
* Préfixe `"profile."`

| Clé | Type | Description |
| --- | --- | --- |
| `renderDecisions` | Booléen | Indique au composant de personnalisation s’il doit interpréter les actions DOM. |
| `decisionScopes` | `<String>` de tableau | Une liste de portées pour lesquelles récupérer des décisions |
| `xdm` | Objet | Données formatées dans XDM qui arrivent dans Web SDK en tant qu’événement d’expérience |
| `data` | Objet | Paires clé/valeur arbitraires envoyées à des solutions [!DNL Target] sous la classe cible. |

<!--Typical [!DNL Web SDK] code using this command looks like the following:-->

**Retarder l’enregistrement des paramètres de profil ou d’entité jusqu’à ce que le contenu ait été affiché à l’utilisateur final**

Pour retarder l’enregistrement des attributs dans le profil jusqu’à ce que le contenu ait été affiché, définissez `data.adobe.target._save=false` dans votre requête.

Par exemple, votre site web contient trois portées de décision correspondant à trois liens de catégorie sur le site web (hommes, femmes et enfants) et vous souhaitez effectuer le suivi de la catégorie que l’utilisateur a finalement visitée. Envoyez ces requêtes avec l’indicateur de `__save` défini sur `false` pour éviter de conserver la catégorie au moment où le contenu est demandé. Une fois le contenu visualisé, envoyez la payload appropriée (y compris les `eventToken` et les `stateToken`) pour que les attributs correspondants soient enregistrés.

L’exemple ci-dessous envoie un message de style trackEvent, exécute des scripts de profil, enregistre des attributs et enregistre immédiatement l’événement.

```js
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": { /* Experience Event XDM data */ },
    "data": {
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
})
```

>[!NOTE]
>
>Si la directive `__save` est omise, l’enregistrement des attributs de profil et d’entité se produit immédiatement. La directive `__save` n’est pertinente que pour les attributs de profil et les détails d’entité.

## Recommandations de requêtes

Le tableau suivant répertorie [!DNL Recommendations] attributs et indique si chacun est pris en charge par le biais du [!DNL Web SDK] :

| Catégorie | Attribut | Statut de la prise en charge |
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
| Recommendations - Paramètres de mbox/page réservés | excludeIds | Pris en charge |
|  | cartIds | Pris en charge |
|  | productPurchasedId | Pris en charge |
| Catégorie de page ou d&#39;élément pour l&#39;affinité catégorielle | user.categoryId | Pris en charge |

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

L’exemple ci-dessous montre comment vous pouvez effectuer le suivi des conversions de mbox d’affichage et envoyer des paramètres de profil à Adobe Target, sans avoir à qualifier de contenu ou d’activité.

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
| `xdm._experience.decisioning.propositions[x].scope` | La portée à laquelle associer la mesure de succès (qui l’attribuera à une activité spécifique du côté Target). |
| `xdm._experience.decisioning.propositions[x].eventType` | Chaîne décrivant le type d’événement prévu. Définissez ce paramètre sur `"decisioning.propositionDisplay"` pour ce cas d’utilisation. |

## Débogage

mboxTrace et mboxDebug ont été rendus obsolètes. Utilisez plutôt une méthode de [débogage Web SDK](/help/web-sdk/use-cases/debugging.md).

## Terminologie

__Propositions :__ dans [!DNL Adobe Target], les propositions sont corrélées à l’expérience sélectionnée dans une activité.

__Schéma :__ le schéma d’une décision est le type d’offre dans [!DNL Adobe Target].

__Portée :__ portée de la décision. En [!DNL Adobe Target], la portée est la mBox. La mBox globale est la portée `__view__`.

__XDM:__ le XDM est sérialisé en notation par points, puis placé dans [!DNL Adobe Target] en tant que paramètres mBox.
