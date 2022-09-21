---
title: Extension de couche de données Google
description: Découvrez l’extension de balise de la couche de données client Google dans Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 8%

---

# Extension de la couche de données Google (bêta)

>[!IMPORTANT]
>
>Cette extension est actuellement en version bêta et n’a pas été entièrement testée en production.

L’extension de la couche de données Google vous permet d’utiliser une couche de données Google lorsque vous implémentez des balises. L’extension peut être utilisée indépendamment ou simultanément avec les solutions Google et avec Google open source [Bibliothèque d’assistance de couche de données](https://github.com/google/data-layer-helper).

La bibliothèque d’assistance fournit des fonctionnalités similaires, pilotées par des événements, au lecteur de données client Adobe (ACDL). Les éléments de données, les règles et les actions de l’extension de la couche de données Google fournissent des fonctionnalités similaires à celles du [Extension ACDL](../client-data-layer/overview.md).

## Maturité

La version 1.0.x de l’extension est une version bêta. Cette extension n’a pas été entièrement testée en production.

## Installation

Pour installer l’extension, accédez au catalogue d’extensions dans l’interface utilisateur Experience Platform ou l’interface utilisateur de collecte de données, puis sélectionnez **Couche de données Google**.

Une fois installée, l’extension crée ou accède à une couche de données chaque fois que la bibliothèque de balises se charge sur votre site web.

## Affichage de l’extension

Lors de la configuration de l’extension (lors de l’installation de l’extension ou en sélectionnant **[!UICONTROL Configurer]** dans le catalogue d’extensions) vous devez définir le nom de la couche de données utilisée par l’extension. Si aucune couche de données avec le nom configuré n’est présente lors du chargement de la bibliothèque, l’extension en crée une à la place.

>[!NOTE]
>
>Peu importe que le code Google ou Adobe se charge en premier et crée la couche de données. Les deux systèmes créent la couche de données s’ils ne sont pas présents ou utilisent la couche de données existante.

Par défaut, la couche de données utilise le nom Google par défaut. `dataLayer`.

## Événements

L’extension vous permet d’écouter les modifications (événements) dans la couche de données. Un événement peut être l’un des suivants :

* Balisage des événements (par exemple, une bibliothèque en cours de chargement)
* Événements JavaScript
* Données transmises à la couche de données avec la variable `event` mot-clé.

Il est important de comprendre l’utilisation de la variable [`event` keyword](https://developers.google.com/tag-platform/devguides/datalayer#use_a_data_layer_with_event_handlers) lorsque des données sont transmises à une couche de données Google, de la même manière que la couche de données client Adobe. Le `event` Le mot-clé modifie le comportement de la couche de données Google et, par conséquent, le comportement de l’extension se met à jour en conséquence.

Les sections ci-dessous décrivent les différents types d’événements que l’extension peut écouter.

### Prêtez attention à toutes les transmissions vers la couche de données

Si vous sélectionnez cette option, l’extension écoute toute modification apportée à la couche de données.

### Écoute des publications excluant des événements

Si vous sélectionnez cette option, l’extension écoute tout élément transmis à la couche de données, à l’exception des événements.

L’exemple d’événement push suivant est suivi par l’écouteur :

```js
dataLayer.push({"data":"something"})
```

L’exemple d’événement push suivant ne serait pas suivi par l’écouteur :

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Écoute de tous les événements

Si vous sélectionnez cette option, l’extension écoute tous les événements transmis à la couche de données.

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

Si vous souhaitez écouter un événement spécifique, sélectionnez cette option afin que le récepteur d’événements effectue le suivi des événements correspondant à une chaîne spécifique.

Par exemple, si vous définissez `myEvent` lors de l’utilisation de cette configuration, l’écouteur ne suit que l’événement push suivant :

```js
dataLayer.push({"event":"myEvent"})
```

Vous pouvez également utiliser une chaîne regex pour faire correspondre les noms d’événement. Par exemple, la définition de `myEvent\d` effectuent le suivi des événements commençant par `myEvent` suivi d’un chiffre :

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Actions

Les sections ci-dessous décrivent les différentes actions que l’extension peut effectuer lorsqu’elle est incluse dans une [règle](../../../ui/managing-resources/rules.md).

### Push to Data Layer (Envoi vers couche de données) {#push-to-data-layer}

Cette action envoie le contenu JSON à la couche de données elle-même, ce qui permet d’utiliser des éléments de données directement dans les payloads JSON. Dans l’éditeur JSON fourni, vous pouvez référencer des éléments de données à l’aide de la notation de pourcentage (par exemple, `%dataElementName%`).

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

### Réinitialisation du langage DL Google à l’état calculé

>[!NOTE]
>
>Cette action est disponible à partir de la version 1.0.5.

Cette action réinitialise la couche de données. Si elle est utilisée dans une règle qui traite une modification de couche de données Google, la couche de données est réinitialisée à l’état calculé de la couche de données au moment où la règle a été déclenchée. Si l’action est utilisée dans une règle qui ne traite pas de modification de couche de données Google, l’action vide la couche de données.

## Éléments de données

L’extension fournit un élément de données unique qui accède à la couche de données à l’aide d’une clé (par exemple, `page.url` dans le [extrait de code ci-dessus](#push-to-data-layer)).

L’élément de données peut fournir les éléments suivants :

* Une valeur spécifique de la couche de données (par exemple, `page.url`)
* Le tableau de couche de données entier (champ de clé vide)
* Valeurs d’un événement de couche de données à l’aide de la clé (si la variable `event` a été utilisé)
* Objet d’événement entier (champ de clé vide)

L’extension donne toujours la priorité aux informations d’événement. Si une couche de données `event` est en cours de traitement, les valeurs sont toujours lues à partir de cet événement. Si `event` n’est pas présent, les valeurs sont lues à partir de la couche de données directe à la place.

## Informations supplémentaires 

Des informations supplémentaires sont disponibles dans la section [project README](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md) et dans les boîtes de dialogue d’élément de données et d’événement de l’extension.
