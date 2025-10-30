---
title: Extension de la couche de données Google
description: Découvrez l’extension de balise de la couche de données client Google dans Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 12%

---

# Extension de la couche de données Google

L’extension de couche de données Google vous permet d’utiliser une couche de données Google dans votre implémentation de balises. L’extension peut être utilisée indépendamment ou simultanément avec les solutions Google et avec Google open source [bibliothèque d’assistance de couche de données](https://github.com/google/data-layer-helper).

La bibliothèque d’assistance fournit des fonctionnalités pilotées par les événements similaires à la couche de données client (ACDL) Adobe. Les éléments de données, les règles et les actions de l’extension de la couche de données Google fournissent des fonctionnalités similaires à celles de l’extension [ACDL](../client-data-layer/overview.md).

## Installation

Pour installer l’extension, accédez au catalogue d’extensions dans l’interface utilisateur de collecte de données et sélectionnez **[!UICONTROL Google Data Layer]**.

Une fois installée, l’extension crée une couche de données ou y accède à chaque charge de la bibliothèque Adobe Experience Platform Tags.

## Vue d’extension

La configuration de l’extension peut être utilisée pour définir le nom de la couche de données utilisée par l’extension. Si aucune couche de données portant le nom configuré n’est présente lors du chargement de Adobe Experience Platform Tags, l’extension en crée une.

Le nom de couche de données par défaut est le nom Google par défaut `dataLayer`.

>[!NOTE]
>
>Peu importe que le code Google ou Adobe se charge en premier et crée la couche de données. Les deux systèmes se comportent de la même manière : créez la couche de données si elle n’est pas présente ou utilisez la couche de données existante.

## Événements

>[!NOTE]
>
>Le mot _event_ est surchargé lorsqu’une couche de données pilotée par un événement est utilisée dans Adobe Experience Platform Tags. Les _événements_ peuvent être les suivants :
>
> - Événements Adobe Experience Platform Tags (bibliothèque chargée, etc.).
> - Événements JavaScript.
> - Données transmises à la couche de données avec le mot-clé _event_.

L’extension vous offre la possibilité d’écouter les modifications apportées à la couche de données.

>[!NOTE]
>
>Il est important de comprendre l’utilisation du mot-clé _event_ lorsque des données sont transmises à une couche de données Google, de la même manière que la couche de données client Adobe. Le mot-clé _event_ modifie le comportement de la couche de données Google et, par conséquent, cette extension.\
> Veuillez lire la documentation de Google ou effectuer des recherches si vous n’êtes pas sûr de ce point.

### Types d’événements Google

Google prend en charge deux méthodes de publication d’événements : Google Tag Manager, utilisant la méthode `push()`, et Google Analytics 4, utilisant la méthode `gtag()`.

Les versions d’extension de la couche de données Google antérieures à la version 1.2.1 prenaient uniquement en charge les événements créés par `push()`, comme illustré dans les exemples de code sur cette page.

Les versions 1.2.1 et ultérieures prennent en charge les événements créés à l’aide de `gtag()`.  Cette option est facultative et peut être activée dans la boîte de dialogue Configuration de l’extension .

Pour plus d’informations sur les événements `push()` et `gtag()`, consultez la documentation de Google [&#128279;](https://developers.google.com/analytics/devguides/collection/ga4/reference/events?client_type=gtag).  Des informations sont également fournies dans les boîtes de dialogue de configuration et de règle de l’extension.

### Écouter toutes les notifications push vers la couche de données

Si vous sélectionnez cette option, votre écouteur d’événement écoute toute modification apportée à la couche de données.

### Écoute des notifications push en excluant les événements

Si vous sélectionnez cette option, votre écouteur d’événement écoute toute notification push de données vers la couche de données, à l’exclusion des événements.

L’exemple d’événement push suivant est suivi par l’écouteur :

```js
dataLayer.push({"data":"something"})
```

L’exemple d’événement push suivant ne serait pas suivi par l’écouteur :

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Écouter pour tous les événements

Si vous sélectionnez cette option, votre écouteur d’événement écoute tout événement transmis à la couche de données.

L’exemple d’événement push suivant est suivi par l’écouteur :

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

L’exemple d’événement push suivant ne serait pas suivi par l’écouteur :

```js
dataLayer.push({"data":"something"})
```

### Écoute d’un événement spécifique

Si vous spécifiez un événement, l’écouteur d’événement suit tout événement correspondant à une chaîne spécifique.

Par exemple, si vous définissez `myEvent` lors de l’utilisation de cette configuration, l’écouteur ne suit que l’événement push suivant :

```js
dataLayer.push({"event":"myEvent"})
```

Une expression régulière (ECMAScript / JavaScript) peut être utilisée pour faire correspondre les noms des événements.

Par exemple, la définition de « myEvent\d » permet d’effectuer le suivi des `myEvent` avec un chiffre (\d) :

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Actions

### Push to Data Layer (Envoi vers couche de données) {#push-to-data-layer}

L’extension vous fournit deux actions pour pousser le fichier JSON vers la couche de données : un champ de texte libre pour créer manuellement le fichier JSON à pousser et, à partir de la version 1.2.0, une boîte de dialogue à plusieurs champs clé-valeur.

#### JSON en texte libre

L’action de texte libre permet d’utiliser des éléments de données directement dans le fichier JSON. Dans l’éditeur JSON, les éléments de données doivent être référencés à l’aide de la notation de pourcentage. Par exemple : `%dataElementName%`.

```json
{
  "page": {
    "url": "%url%",
    "previous_url": "%previous_url%",
    "concatenated_values": "static string %dataElement%"
  }
}
```

#### Champ multiple clé-valeur

La nouvelle boîte de dialogue à plusieurs champs clé-valeur est une interface plus conviviale qui permet de configurer une notification push sans écrire manuellement de code JSON.

### Google DL Reset to Computed State

L’extension vous fournit une action pour réinitialiser la couche de données. Si elle est utilisée dans une règle qui traite une modification de couche de données Google, la couche de données est réinitialisée à l’état calculé de la couche de données au moment du déclenchement de la règle. Si l’action est utilisée dans une règle qui ne traite pas les modifications de couche de données Google, l’action vide la couche de données.

## Éléments de données

L’élément de données fourni peut être utilisé lors de l’exécution d’une règle déclenchée par un changement de couche de données Google (événement push) ou dans une règle non liée telle que Library Loaded (Bibliothèque chargée). Dans le premier cas, l’élément de données renvoie une valeur extraite de l’état calculé au moment du changement de la couche de données. Dans ce dernier cas, l’état calculé au moment de l’exécution de la règle est utilisé.

Le bouton (bascule) vous permet de choisir si l’élément de données doit renvoyer des valeurs de l’ensemble de l’état calculé ou uniquement à partir des informations d’événement (s’il est utilisé dans une règle déclenchée par un changement de couche de données).

L’élément de données peut donc renvoyer :

- Champ vide : état calculé de la couche de données.
- Champ avec clé (comme page.previous_url dans l’exemple ci-dessus) : valeur de la clé dans l’objet d’événement ou l’état calculé.

## Informations supplémentaires 

Les boîtes de dialogue d’élément de données et d’événement de l’extension contiennent des informations d’utilisation détaillées et des exemples.

Vous trouverez des informations générales supplémentaires dans la section [LISEZ-MOI du projet](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
