---
description: Experience Platform Destination SDK utilise des modèles de bulle, ce qui vous permet de transformer les données exportées d’Experience Platform au format requis par votre destination.
title: Fonctions de transformation prises en charge dans Destination SDK
source-git-commit: 840404741da06ba1593b227c7d6ba459b5f43110
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 6%

---

# Fonctions de transformation prises en charge dans Destination SDK

## Présentation {#overview}

La Destination SDK Experience Platform utilise [[!DNL Pebble] templates](https://pebbletemplates.io/), ce qui vous permet de transformer les données exportées d’Experience Platform au format requis par votre destination.

L’Experience Platform [!DNL Pebble] La mise en oeuvre comporte quelques modifications par rapport à la version prête à l’emploi fournie par [!DNL Pebble]. En outre, en plus des fonctions d’usine fournies par [!DNL Pebble], Adobe a créé des fonctions supplémentaires que vous pouvez utiliser avec Destination SDK.

## Où utiliser {#where-to-use}

Utilisez les fonctions prises en charge répertoriées ci-dessous dans cette page lorsque [création d&#39;un modèle de transformation de message](./create-template.md) pour les données exportées depuis l’Experience Platform vers votre destination. Le modèle de transformation des messages est utilisé dans la variable [configuration du serveur de destination](./server-and-template-configuration.md) pour les destinations de diffusion en continu.

## Conditions préalables {#prerequisites}

Pour comprendre les concepts et les fonctions de cette page de référence, lisez le [format du message](/help/destinations/destination-sdk/message-format.md) document en premier. Vous devez comprendre le [structure d&#39;un profil](/help/destinations/destination-sdk/message-format.md#profile-structure) dans Experience Platform avant de pouvoir utiliser [!DNL Pebble] modèles à transformer et les données exportées.

Avant d’accéder aux fonctions décrites ci-dessous, consultez les exemples de modèle dans la section . [Utilisation d’une langue de modèle pour les transformations d’identité, d’attributs et d’appartenance aux segments](/help/destinations/destination-sdk/message-format.md#using-templating). Les exemples dans ce cas commencent très simplement et augmentent la complexité.

## Pris en charge [!DNL Pebble] fonctions {#supported-functions}

Dans la [!DNL Pebble] section balises, Destination SDK ne prend en charge que les éléments suivants :
* [filtrer](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [définie](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>Utilisation `for` est différent lors de l’itération *tableau* ou *map* dans un modèle. Lorsque vous effectuez une itération sur un tableau, vous pouvez obtenir l’élément directement. Lorsque vous effectuez une itération sur une carte, vous obtenez chaque entrée de carte, qui comporte une paire clé-valeur.
>
> * Pour un exemple d’élément de tableau, pensez aux identités d’un [identityMap](./message-format.md#identities) espace de noms, où vous pouvez effectuer une itération sur des éléments tels que `identityMap.gaid`, `identityMap.email`ou similaire.
> * Pour un exemple d’élément map, pensez à [segmentMembership](./message-format.md#segment-membership).


Dans la [!DNL Pebble] filtre , Destination SDK prend en charge toutes les fonctions. Un exemple ci-dessous montre comment la fonction `date` peut être utilisée dans Destination SDK.

Dans la [!DNL Pebble] section fonctions, l’Adobe fait *not* la prise en charge de [range](https://pebbletemplates.io/wiki/function/range/) fonction .

## Exemple de la manière dont la variable `date` fonction utilisée {#date-function}

Pour illustrer comment [!DNL Pebble] Les fonctions sont utilisées dans Destination SDK, voir ci-dessous la manière dont la fonction de date ([lien dans la documentation sur les bulles](https://pebbletemplates.io/wiki/filter/date/)) est utilisé pour transformer le format d’un horodatage.

### Cas d’utilisation

Vous souhaitez modifier la variable `lastQualificationTime` horodatage de la valeur par défaut [ISO 8601](https://fr.wikipedia.org/wiki/ISO_8601) valeur que l’Experience Platform exporte vers une autre valeur préférée par votre destination.

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

Outre les fonctions d’usine fournies par [!DNL Pebble], voir ci-dessous les fonctions supplémentaires créées par Adobe que vous pouvez utiliser pour vos exportations de données.

### `addedSegments` et `removedSegments` fonctions {#addedsegments-removedsegments-functions}

#### Cas d’utilisation

Ces fonctions peuvent être utilisées pour obtenir la liste des segments qui ont été ajoutés ou supprimés d’un profil.

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

### Added and removed segments filters {#added-and-removed-segmnts-filters}

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

Vous savez lequel [!DNL Pebble] Les fonctions sont prises en charge dans Destination SDK, ainsi que la manière de les utiliser pour ajuster le format des données exportées selon vos besoins. Vous devez ensuite consulter les pages suivantes :

* [Créer et tester un modèle de transformation de message](/help/destinations/destination-sdk/create-template.md)
* [Opérations de l’API pour le rendu du modèle](/help/destinations/destination-sdk/render-template-api.md)