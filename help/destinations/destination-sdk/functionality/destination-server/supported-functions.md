---
description: Experience Platform Destination SDK utilise des modèles Pebble, ce qui vous permet de transformer les données exportées d’Experience Platform au format demandé par la destination.
title: Fonctions de transformation prises en charge dans Destination SDK
exl-id: 36f761c7-9d76-41fe-b05f-d4cad655ddd2
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 100%

---

# Fonctions de transformation prises en charge dans Destination SDK

Experience Platform Destination SDK utilise des modèles [[!DNL Pebble] ](https://pebbletemplates.io/), ce qui vous permet de transformer les données exportées d’Experience Platform au format demandé par la destination.

L’implémentation [!DNL Pebble] d’Experience Platform comporte quelques modifications par rapport à la version prête à l’emploi fournie par [!DNL Pebble]. En outre, en plus des fonctions prêtes à l’emploi fournies par [!DNL Pebble], Adobe a créé des fonctions supplémentaires que vous pouvez utiliser avec Destination SDK.

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Lieu d’utilisation {#where-to-use}

Utilisez les fonctions prises en charge répertoriées ci-dessous sur cette page au moment de la [création d’un modèle de transformation de message](../../testing-api/streaming-destinations/create-template.md) pour les données exportées depuis Experience Platform vers la destination.

Le modèle de transformation des messages est utilisé dans la [configuration du serveur de destination](templating-specs.md) pour les destinations de diffusion en streaming.

## Conditions préalables {#prerequisites}

Pour comprendre les concepts et les fonctions de cette page de référence, commencez par consulter le document relatif au [format du message](message-format.md). Vous devez comprendre la [structure d’un profil](message-format.md#profile-structure) dans Experience Platform avant de pouvoir utiliser les modèles [!DNL Pebble] à transformer et les données exportées.

Avant d’accéder aux fonctions décrites ci-dessous, consultez les exemples de modèle dans la section [Utiliser un langage de modèle pour les transformations d’identité, d’attributs et d’appartenance à une audience](message-format.md#using-templating). Ces exemples commencent très simplement et se complexifient au fur et à mesure.

## Fonction [!DNL Pebble] prise en charge {#supported-functions}

Dans la section de balise [!DNL Pebble], Destination SDK ne prend en charge que les éléments suivants :

* [filtrer](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [set](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>L’utilisation de `for` est différente quand il s’agit de parcourir les éléments d’un *tableau* ou d’une *map* dans un modèle. Quand vous parcourez un tableau, vous pouvez obtenir l’élément directement. Quand vous parcourez une map, vous obtenez chaque entrée de map qui comporte une paire clé-valeur.
>
> * Pour obtenir un exemple d’élément de tableau, pensez aux identités d’un espace de nom [identityMap](message-format.md#identities), où vous pouvez parcourir des éléments tels que `identityMap.gaid`, `identityMap.email` ou similaires.
> * Pour obtenir un exemple d’élément map, pensez à [segmentMembership](message-format.md#segment-membership).

Dans la section de filtre [!DNL Pebble], Destination SDK prend en charge toutes les fonctions. Un exemple ci-dessous montre comment la fonction `date` peut être utilisée dans Destination SDK.

Dans la section de fonction [!DNL Pebble], Adobe *ne prend pas* en charge la fonction de [plage](https://pebbletemplates.io/wiki/function/range/).

## Exemple de la manière dont la fonction `date` est utilisée {#date-function}

Pour illustrer comment les fonctions [!DNL Pebble] sont utilisées dans Destination SDK, consultez ci-dessous la manière dont la fonction de date ([lien dans la documentation Pebble](https://pebbletemplates.io/wiki/filter/date/)) est utilisée pour transformer le format d’une date et heure.

### Cas d’utilisation

Vous souhaitez modifier la date et l’heure `lastQualificationTime` de la valeur [ISO 8601](https://fr.wikipedia.org/wiki/ISO_8601) par défaut qu’Experience Platform exporte par une autre valeur préférée par la destination.

### Exemple

#### Entrée

```json
{
"lastQualificationTime": "2022-02-08T18:34:24.000+0000"
}
```

#### Format

```java
{{ lastQualificationTime | date(existingFormat="yyyy-MM-dd'T'HH:mm:sss.SSSX", format="yyyy-MM-dd'T'HH:mm:ssX") }}
```

#### Sortie

```json
{
"lastQualificationTime": "2022-02-21T18:34:24Z"
}
```

## Fonctions ajoutées par Adobe {#functions-added-by-adobe}

Outre les fonctions prêtes à l’emploi fournies par [!DNL Pebble], consultez ci-dessous les fonctions supplémentaires créées par Adobe que vous pouvez utiliser pour vos exportations de données.

### Fonctions `addedSegments` et `removedSegments` {#addedsegments-removedsegments-functions}

#### Cas d’utilisation

Ces fonctions peuvent être utilisées pour obtenir la liste des audiences qui ont été ajoutées ou supprimées d’un profil.

#### Exemple

##### Entrée

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Format

```java
added: {% for s in addedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}; removed: {% for s in removedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}
```

##### Sortie

```json
added: <111111><333333>; removed: <222222>
```

<!--

### Added and removed audiences filters {#added-and-removed-segmnts-filters}

#### Use case {#use-case}

These filters are similar to `addedSegments` and `removedSegments`, described above. The only difference is that they are implemented as filters as opposed to functions.

#### Example {#example}

##### Input {#input}

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Format {#format}

```java
added: {% for s in input.profile.segmentMembership.ups | added %}<{{s.key}}>{% endfor %};|removed: {% for s in input.profile.segmentMembership.ups | removed %}<{{s.key}}>{% endfor %};
```

##### Output {#output}

```json
added: <111111><333333>;|removed: <222222>;
```

-->

## Étapes suivantes {#next-steps}

Vous savez quelles fonctions [!DNL Pebble] sont prises en charge dans Destination SDK, ainsi que la manière de les utiliser pour ajuster le format des données exportées selon vos besoins. Vous devez à présent consulter les pages suivantes :

* [Création et test d’un modèle de transformation de message](../../testing-api/streaming-destinations/create-template.md)
* [Opérations de l’API de modèle de rendu](../../testing-api/streaming-destinations/render-template-api.md)
