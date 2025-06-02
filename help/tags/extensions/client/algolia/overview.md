---
title: Présentation de l’extension Algolia Tags
description: Découvrez l’extension Balises Algolia dans Adobe Experience Platform.
source-git-commit: 5b488a596472fe61b487f75ad62d741237caa820
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 2%

---

# Présentation de l’extension [!DNL Algolia] Tags

L’extension [!DNL Algolia] Tags permet aux spécialistes marketing de configurer facilement des règles qui envoient des données d’interaction utilisateur aux [!DNL Algolia], ce qui vous permet de proposer des expériences IA Search et Discovery plus personnalisées.

Cette extension est optimisée par une fonctionnalité clé :

* **[!DNL Algolia]Insights** : capture et envoie automatiquement les événements d’interaction utilisateur à [!DNL Algolia], ce qui permet des analyses puissantes, des expériences personnalisées et une pertinence de recherche améliorée.

## Conditions préalables {#prerequisites}

Vous devez disposer d’un compte [!DNL Algolia] valide pour utiliser cette extension. Accédez à la page [[!DNL Algolia] inscription](https://dashboard.algolia.com/users/sign_up) pour créer un compte si vous n’en avez pas déjà un.

### Collecter les détails de configuration requis {#configuration-details}

Pour vous connecter [!DNL Algolia] Adobe Experience Platform, vous aurez besoin des informations suivantes :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| ID de l’application | Votre ID d’application se trouve dans la section [ Clés API ](https://www.algolia.com/account/api-keys/all) de votre tableau de bord [!DNL Algolia]. | 0ABCDEFG12 |
| Clé API de recherche | Votre clé d’API de recherche se trouve dans la section [Clés d’API](https://www.algolia.com/account/api-keys/all) de votre tableau de bord de [!DNL Algolia]. | 1234a12345678901b1234567890c1ab1 |

## Installation et configuration de l’extension [!DNL Algolia] Insights {#install-configure}

Pour installer l’extension [!DNL Algolia] Insights, accédez à l’[!UICONTROL interface utilisateur de la collecte de données] et sélectionnez **[!UICONTROL Balises]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez-en une nouvelle.

Une fois la propriété sélectionnée ou créée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**. Recherchez la carte [!DNL Algolia] Insights , puis sélectionnez **[!UICONTROL Installer]**.

![](../../../images/extensions/client/algolia/install.png)

Dans la vue de configuration qui s’affiche, vous devez fournir les détails suivants :

| Propriété | Description |
| --- | --- |
| ID de l’application | Saisissez l’[!UICONTROL ID de l’application] que vous avez précédemment collecté dans la section [détails de la configuration](#configuration-details). |
| Clé API de recherche | Saisissez la [!UICONTROL clé API de recherche] que vous avez précédemment collectée dans la section [détails de configuration](#configuration-details). |
| Nom de l’index | Le [!UICONTROL Nom de l’index] contient les produits ou le contenu.  Cet index sera utilisé par défaut. |
| Élément de données Jeton d’utilisateur | L’élément de données qui renverra le jeton d’utilisateur. |
| Élément de données Jeton d’utilisateur authentifié | Définissez l’élément de données qui renverra le jeton d’utilisateur authentifié. |
| Devise | Sélectionnez un type de devise.  La valeur par défaut est définie sur `USD`. |

![](../../../images/extensions/client/algolia/configure.png)

## Types d’actions de l’extension [!DNL Algolia] Insights {#action-types}

[!DNL Algolia] prend en charge un ensemble d’événements standard prédéfinis, chacun avec des contextes et des propriétés spécifiques. Les actions disponibles dans l’extension [!DNL Algolia] s’alignent sur ces types d’événements, ce qui facilite la classification et la configuration des événements que vous envoyez à [!DNL Algolia] en fonction de leur type.

### Charger les informations {#load-insights}

>[!NOTE]
>
>Dans la plupart des cas, il est recommandé de charger [!DNL Algolia] Insights sur chaque page de votre site.

Ajoutez l’action **[!UICONTROL Charger les informations]** à votre règle de balise là où elle est le plus utile pour charger des informations [!DNL Algolia] en fonction du contexte de votre règle. Cette action charge la bibliothèque `search-insights.js` sur la page.

Créez une règle de balise ou ouvrez-en une existante. Définissez les conditions en fonction de vos besoins, puis sélectionnez **[!UICONTROL Algolie]** comme [!UICONTROL Extension] et sélectionnez **[!UICONTROL Charger les informations]** comme [!UICONTROL Type d’action].

| Propriété | Description |
| --- | --- |
| [!UICONTROL Version de la bibliothèque Insight] | Version d’[!DNL Algolia] Insights. La valeur par défaut est de `2.13.0`. |
| [!UICONTROL Élément De Données Opt-Out De L’Utilisateur] | L’élément de données qui capture la préférence de suivi de l’utilisateur. |
| [!UICONTROL Utiliser le cookie du jeton d’utilisateur] | Cochez cette case pour [!DNL Algolia] permettre de générer un cookie de jeton d’utilisateur. Par défaut, cette option est définie sur `false`. |

![](../../../images/extensions/client/algolia/load-insights.png)

### Cliqué {#clicked}

Ajoutez l’action **[!UICONTROL Clic]** à votre règle de balise pour envoyer les événements sur lesquels l’utilisateur a cliqué aux [!DNL Algolia]. Créez une règle de balise ou ouvrez-en une existante. Définissez les conditions en fonction de vos besoins, puis sélectionnez **[!UICONTROL Algolie]** comme [!UICONTROL Extension] et sélectionnez **[!UICONTROL Cliqué]** comme [!UICONTROL Type d’action].

| Propriété | Description |
| --- | --- |
| [!UICONTROL Nom de l’événement] | Nom de l’événement qui peut être utilisé pour affiner davantage cet événement de clic. |
| Élément de données Détails de l’événement | L’élément de données qui récupère les détails de l’événement, y compris `indexName`, `objectIDs` et éventuellement `queryID`, `position`. Si les `queryID` et les `position` sont inclus, l’événement est classé comme *ID d’objet sur lesquels l’utilisateur a cliqué après la recherche* sinon il est traité comme un événement *ID d’objet sur lesquels l’utilisateur a cliqué*. Si l’élément de données ne fournit pas de nom d’index, le nom d’index par défaut est utilisé lors de l’envoi de l’événement. |

![](../../../images/extensions/client/algolia/clicked.png)

### Converti {#converted}

Ajoutez l’action **[!UICONTROL Converti]** à votre règle de balise pour envoyer les événements convertis aux [!DNL Algolia]. Créez une règle de balise ou ouvrez-en une existante. Définissez les conditions en fonction de vos besoins, puis sélectionnez **[!UICONTROL Algolie]** comme [!UICONTROL Extension] et sélectionnez **[!UICONTROL Converti]** comme [!UICONTROL Type d’action].

| Propriété | Description |
| --- | --- |
| Nom de l’événement | Nom de l’événement qui sera utilisé pour affiner davantage cet événement **convert**. |
| Élément de données Détails de l’événement | L’élément de données qui récupère les détails de l’événement, y compris `indexName`, `objectId` et éventuellement `queryId`. Si l’élément de données contient des `queryId`, l’événement est classé comme *Converti après la recherche* sinon il est considéré comme une classe d’événement *Converti*. Si l’élément de données ne fournit pas de nom d’index, le nom d’index par défaut est utilisé lors de l’envoi de l’événement. |

![](../../../images/extensions/client/algolia/converted.png)

### Ajouté au panier {#added-to-cart}

Ajoutez l’action **[!UICONTROL Ajouté au panier]** à votre règle de balise pour envoyer les événements ajoutés au panier aux [!DNL Algolia]. Créez une règle de balise ou ouvrez-en une existante. Définissez les conditions en fonction de vos besoins, puis sélectionnez **[!UICONTROL Algolie]** comme [!UICONTROL Extension] et sélectionnez **[!UICONTROL Ajouté au panier]** comme [!UICONTROL Type d’action].

| Propriété | Description |
| --- | --- |
| Nom de l’événement | Nom de l’événement qui sera utilisé pour affiner davantage cet événement **convert**. |
| Élément de données Détails de l’événement | L’élément de données qui récupère les détails de l’événement, y compris `indexName`, `objectId` et éventuellement `queryId`, `objectData`. Si l’élément de données contient des `queryId`, l’événement est classé comme *Ajouté aux ID d’objet de panier après recherche* sinon il est considéré comme une classe d’événement *Ajouté aux ID d’objet de panier*. Si l’élément de données ne fournit pas de nom d’index, le nom d’index par défaut est utilisé lors de l’envoi de l’événement. |
| Devise | Spécifie le type de devise, par exemple `USD`. |

![](../../../images/extensions/client/algolia/added-to-cart.png)

### Purchased {#purchased}

Ajoutez l’action **[!UICONTROL Ajouté au panier]** à votre règle de balise pour envoyer les événements achetés à [!DNL Algolia]. Créez une règle de balise ou ouvrez-en une existante. Définissez les conditions en fonction de vos besoins, puis sélectionnez **[!UICONTROL Algolie]** comme [!UICONTROL Extension] et sélectionnez **[!UICONTROL Acheté]** comme [!UICONTROL Type d’action].

| Propriété | Description |
| --- | --- |
| Nom de l’événement | Nom de l’événement qui sera utilisé pour affiner davantage cet événement **achat**. |
| Élément de données Détails de l’événement | L’élément de données qui récupère les détails de l’événement, y compris `indexName`, `objectId` et éventuellement `queryId`. Si l’élément de données contient des `queryId`, l’événement est classé comme *ID d’objet achetés après recherche* sinon il est considéré comme une classe d’événement *ID d’objet achetés*. Si l’élément de données ne fournit pas de nom d’index, le nom d’index par défaut est utilisé lors de l’envoi de l’événement. |

![](../../../images/extensions/client/algolia/purchased.png)

### Consulté {#viewed}

Ajoutez l’action **[!UICONTROL Ajouté au panier]** à votre règle de balise pour envoyer les événements achetés à [!DNL Algolia]. Créez une règle de balise ou ouvrez-en une existante. Définissez les conditions en fonction de vos besoins, puis sélectionnez **[!UICONTROL Algolie]** comme [!UICONTROL Extension] et sélectionnez **[!UICONTROL Affiché]** comme [!UICONTROL Type d’action].

![](../../../images/extensions/client/algolia/viewed.png)

| Propriété | Description |
| --- | --- |
| Nom de l’événement | Nom de l’événement qui sera utilisé pour affiner davantage cet événement **vue**. |
| Élément de données Détails de l’événement | L’élément de données qui récupère les détails de l’événement, y compris les `indexName` et les `objectId`. Si `indexName` n’est pas disponible, le Nom d’index par défaut est utilisé lors de l’envoi des événements. |

## Éléments de données de l’extension [!DNL Algolia] Insights {#data-elements}

[!DNL Algolia] prend en charge un ensemble d’éléments de données prédéfinis, chacun avec des propriétés et des contextes spécifiques. Les sections suivantes décrivent les éléments de données disponibles dans l’extension [!DNL Algolia] Insights.

### DataSet {#dataset}

L’élément de données DataSet récupère les données associées aux éléments HTML, qui sont ensuite utilisées dans les actions [!DNL Algolia].

| Propriété | Description |
| --- | --- |
| Nom De Classe/Div De L’Élément D’Accès | Le nom de l’élément HTML et/ou le nom de classe CSS contenant les attributs du jeu de données, y compris `data-insights-object-id` et éventuellement`data-insights-query-id` et `data-insights-position` sur l’élément HTML. |
| Nom De L’Index Élément Div/Nom De Classe | Nom de l’élément HTML et/ou Nom de classe CSS qui contient les attributs de jeu de données (`data-indexname`) sur l’élément HTML. |

![](../../../images/extensions/client/algolia/dataset.png)

Cet élément de données renvoie :

```javascript
{
  timestamp,
    queryID,
    indexName,
    objectIDs,
    positions
}
```

Exemple d’HTML contenant un jeu de données :

```html
<div data-indexname="acme_master_default_products" class="instant-search-comp__hits">
  <div class="hit-card"
    data-insights-object-id="${hit.objectID}"
    data-insights-position="${hit.__position}"
    data-insights-query-id="${hit.__queryID}">
    <h4 class="hit-name">...</h4>   
  </div>
</div>
```

### Chaîne de requête {#query-string}

L’élément de données Chaîne de requête extrait les données de la chaîne de requête URL pour les utiliser dans des actions [!DNL Algolia].

| Propriété | Description |
| --- | --- |
| Nom du paramètre d’ID d’objet | Nom du paramètre de requête contenant l’ID d’objet. |
| Nom Du Paramètre D’Index (Facultatif) | Nom du paramètre de requête contenant le nom de l’index. |
| Nom du paramètre d’ID de requête (facultatif) | Nom du paramètre de requête contenant l’ID de requête. |
| Nom du paramètre de position (facultatif) | Nom du paramètre de requête contenant la position. |

![](../../../images/extensions/client/algolia/query-string.png)

Cet élément de données renvoie :

```javascript
{
  timestamp,
    queryID,
    indexName,
    objectIDs
}
```

Exemple d’HTML contenant des paramètres de requête.

```
<a href="product.html?objectID=${hit.objectID}&queryID=${hit.__queryID}&indexName=${indexName}&position=${hit.position}">Read More</a>
```

### Stockage {#storage}

L’élément de données de stockage récupère les données du stockage de session pour les utiliser dans des actions [!DNL Algolia].

Cet élément de données récupère les détails de l’événement à partir du stockage de session. Aucune configuration n’est requise. Les données sont automatiquement ajoutées pendant l’action d’événement *click* et supprimées pendant l’action d’événement *convert*.

![](../../../images/extensions/client/algolia/storage.png)

Cet élément de données renvoie ce qui est stocké dans le stockage de session.

```javascript
{
  timestamp,
    queryID,
    indexName,
    objectIDs
}
```

## Clic ou conversion après la recherche {#clicked-converted-after-search}

Les événements *Cliqué après la recherche* ou *Converti après la recherche* nécessitent un `queryId` et `position` est également requis pour les événements *Cliqué après la recherche*. Ces propriétés sont disponibles lorsque l’indicateur `insights` est activé dans les paramètres de requête InstantSearch et/ou Autocomplete. Reportez-vous aux ressources suivantes pour savoir comment configurer Insights pour votre site :

* [Configuration des informations sur la saisie semi-automatique](https://www.algolia.com/doc/ui-libraries/autocomplete/api-reference/autocomplete-js/autocomplete/#param-insights)
* [Configuration des informations sur InstantSearch.js](https://www.algolia.com/doc/guides/building-search-ui/events/js/#set-the-insights-option-to-true)
* [Prise en main des événements de clic et de conversion](https://www.algolia.com/doc/guides/sending-events/implementing/how-to/sending-events-backend/)
* [Envoi  [!DNL Algolia]  événements Insights](https://www.algolia.com/doc/ui-libraries/autocomplete/guides/sending-algolia-insights-events/)
* [[!DNL Algolia] Référentiel GitHub de l’extension Launch](https://github.com/algolia/algolia-launch-extension)
* [Documentation InstantSearch.js](https://www.algolia.com/doc/guides/building-search-ui/what-is-instantsearch/js/)
* [[!DNL Algolia]  Documentation de l’API Insights ](https://www.algolia.com/doc/rest-api/insights/)

## Étapes suivantes {#next-steps}

Ce guide explique comment envoyer des données à [!DNL Algolia] à l’aide de l’extension de balise [!DNL Algolia Insights]. Si vous prévoyez d’envoyer également des événements côté serveur à [!DNL Algolia], vous pouvez maintenant procéder à l’installation et à la configuration de l’extension de transfert d’événement [[!DNL Conversions API] event](../../server/algolia/overview.md).

Pour plus d’informations sur les balises dans Experience Platform, consultez la [présentation des balises](../../../home.md).
