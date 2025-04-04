---
title: Définir des champs XDM dans l’API Schema Registry
description: Découvrez comment définir différents champs lors de la création de ressources de modèle de données d’expérience (XDM) personnalisées dans l’API Schema Registry.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 2%

---

# Définir des champs XDM dans l’API Schema Registry

Tous les champs de modèle de données d’expérience (XDM) sont définis à l’aide des contraintes standard [Schéma JSON](https://json-schema.org/) qui s’appliquent à leur type de champ, avec des contraintes supplémentaires pour les noms de champ appliqués par Adobe Experience Platform. L’API Schema Registry vous permet de définir des champs personnalisés dans vos schémas à l’aide de formats et de contraintes facultatives. Les types de champs XDM sont exposés par l’attribut field-level, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` est une valeur générée par le système. Vous n’êtes donc pas tenu d’ajouter cette propriété au fichier JSON pour votre champ lors de l’utilisation de l’API (sauf lors de la [création de types de mappage personnalisés](#custom-maps)). Une bonne pratique consiste à utiliser les types de schéma JSON (tels que `string` et `integer`) avec les contraintes min/max appropriées telles que définies dans le tableau ci-dessous.

Ce guide décrit la mise en forme appropriée pour définir différents types de champ, y compris ceux avec des propriétés facultatives. Pour plus d’informations sur les propriétés facultatives et les mots-clés spécifiques au type, consultez la [documentation des schémas JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Pour commencer, recherchez le type de champ souhaité et utilisez l’exemple de code fourni pour créer votre requête API pour [création d’un groupe de champs](../api/field-groups.md#create) ou [création d’un type de données](../api/data-types.md#create).

## [!UICONTROL Chaîne] {#string}

Les champs [!UICONTROL Chaîne] sont indiqués par `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

Vous pouvez éventuellement contraindre les types de valeurs qui peuvent être saisis pour la chaîne par le biais des propriétés supplémentaires suivantes :

* `pattern` : modèle RegEx à contraindre par.
* `minLength` : longueur minimale de la chaîne.
* `maxLength` : longueur maximale de la chaîne.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field with added constraints.",
  "type": "string",
  "pattern": "^[A-Z]{2}$",
  "maxLength": 2
}
```

## [!UICONTROL URI] {#uri}

Les champs [!UICONTROL URI] sont indiqués par des `type: string` avec une propriété `format` définie sur `uri`. Aucune autre propriété n’est acceptée.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL Enum] {#enum}

Les champs [!UICONTROL Enum] doivent utiliser `type: string`, avec les valeurs d’énumération elles-mêmes fournies sous un tableau `enum` :

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ]
}
```

Vous pouvez éventuellement fournir des libellés orientés client pour chaque valeur sous une propriété `meta:enum`, chaque libellé étant indexé à une valeur correspondante sous `enum`.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Value 1",
      "value2": "Value 2",
      "value3": "Value 3"
  }
}
```

>[!NOTE]
>
>La valeur `meta:enum` ne déclare **pas** d’énumération ni ne génère de validation de données seule. Dans la plupart des cas, les chaînes fournies sous `meta:enum` sont également fournies sous `enum` pour s’assurer que les données sont limitées. Cependant, il existe certains cas d’utilisation où `meta:enum` est fourni sans tableau de `enum` correspondant. Pour plus d’informations, consultez le tutoriel sur la [définition de valeurs suggérées](../tutorials/suggested-values.md).

Vous pouvez éventuellement fournir une propriété `default` pour indiquer la valeur de `enum` par défaut que le champ utilisera si aucune valeur n’est fournie.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels and a default value.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Value 1",
      "value2": "Value 2",
      "value3": "Value 3"
  },
  "default": "value1"
}
```

>[!IMPORTANT]
>
>Si aucune valeur de `default` n’est fournie et que le champ d’énumération est défini sur `required`, tout enregistrement ne disposant pas d’une valeur acceptée pour ce champ ne sera pas validé lors de l’ingestion.

## [!UICONTROL Nombre] {#number}

Les champs numériques sont indiqués par `type: number` et n’ont pas d’autres propriétés requises.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>Les types `number` sont utilisés pour tout type numérique, entier ou nombre à virgule flottante, tandis que les types [`integer` sont spécifiquement utilisés pour les nombres entiers](#integer) Pour plus d’informations sur les cas d’utilisation de chaque type](https://json-schema.org/understanding-json-schema/reference/numeric.html) reportez-vous à la documentation sur les types numériques du schéma [JSON.

## [!UICONTROL Entier] {#integer}

Les champs [!UICONTROL Entiers] sont indiqués par `type: integer` et n’ont pas d’autres champs obligatoires.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>Alors que les types `integer` font spécifiquement référence aux nombres entiers, les types [`number` sont utilisés pour n&#39;importe quel type numérique](#number) qu&#39;il s&#39;agisse de nombres entiers ou de nombres à virgule flottante. Pour plus d’informations sur les cas d’utilisation de chaque type](https://json-schema.org/understanding-json-schema/reference/numeric.html) reportez-vous à la documentation sur les types numériques du schéma [JSON.

Vous pouvez éventuellement contraindre la plage de l’entier en ajoutant les propriétés `minimum` et `maximum` à la définition. Plusieurs autres types numériques pris en charge par l’interface utilisateur du créateur de schémas sont simplement des types `integer` avec des contraintes de `minimum` et de `maximum` spécifiques, telles que [[!UICONTROL Long]](#long), [[!UICONTROL Court]](#short) et [[!UICONTROL Octet]](#byte).

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field with added constraints.",
  "type": "integer",
  "minimum": 1,
  "maximum": 100
}
```

## [!UICONTROL Long] {#long}

L’équivalent d’un champ [!UICONTROL Long] créé via l’interface utilisateur du créateur de schémas est un champ de type [`integer`](#integer) avec des valeurs `minimum` et `maximum` spécifiques (`-9007199254740992` et `9007199254740992`, respectivement).

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL Court] {#short}

L’équivalent d’un champ [!UICONTROL Court] créé via l’interface utilisateur du créateur de schémas est un champ de type [`integer`](#integer) avec des valeurs `minimum` et `maximum` spécifiques (`-32768` et `32768`, respectivement).

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32768
}
```

## [!UICONTROL Octet] {#byte}

L’équivalent d’un champ [!UICONTROL Octet] créé via l’interface utilisateur du créateur de schémas est un champ de type [`integer`](#integer) avec des valeurs `minimum` et `maximum` spécifiques (`-128` et `128`, respectivement).

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 128
}
```

## [!UICONTROL booléen] {#boolean}

Les champs [!UICONTROL booléens] sont indiqués par `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

Vous pouvez éventuellement fournir une valeur de `default` que le champ utilisera lorsqu’aucune valeur explicite n’est fournie lors de l’ingestion.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field with a default value.",
  "type": "boolean",
  "default": false
}
```

>[!IMPORTANT]
>
>Si aucune valeur de `default` n’est fournie et que le champ booléen est défini sur `required`, tout enregistrement ne disposant pas d’une valeur acceptée pour ce champ ne sera pas validé lors de l’ingestion.

## [!UICONTROL Date] {#date}

Les champs [!UICONTROL Date] sont indiqués par `type: string` et `format: date`. Vous pouvez également fournir un tableau d’`examples` à exploiter dans les cas où vous souhaitez afficher un exemple de chaîne de date pour les utilisateurs qui saisissent manuellement les données.

```json
"sampleField": {
  "title": "Sample Date Field",
  "description": "An example date field with an example array item.",
  "type": "string",
  "format": "date",
  "examples": ["2004-10-23"]
}
```

## [!UICONTROL DateHeure] {#date-time}

Les champs [!UICONTROL DateTime] sont indiqués par `type: string` et `format: date-time`. Vous pouvez également fournir un tableau des `examples` à exploiter dans les cas où vous souhaitez afficher un exemple de chaîne datetime pour les utilisateurs qui saisissent manuellement les données.

```json
"sampleField": {
  "title": "Sample Datetime Field",
  "description": "An example datetime field with an example array item.",
  "type": "string",
  "format": "date-time",
  "examples": ["2004-10-23T12:00:00-06:00"]
}
```

## [!UICONTROL Tableau] {#array}

Les champs [!UICONTROL Tableau] sont indiqués par `type: array` et un objet `items` qui définit le schéma des éléments que le tableau acceptera.

Vous pouvez définir des éléments de tableau à l’aide de types primitifs, tels qu’un tableau de chaînes :

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a primitive type.",
  "type": "array",
  "items": {
    "type": "string"
  }
}
```

Vous pouvez également définir les éléments de tableau en fonction d’un type de données existant en vous référant à la `$id` du type de données via une propriété `$ref`. Voici un tableau d&#39;objets [!UICONTROL Payment Item] :

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a data type reference.",
  "type": "array",
  "items": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}
```

## [!UICONTROL Objet] {#object}

Les champs [!UICONTROL Object] sont indiqués par `type: object` et un objet `properties` qui définit des sous-propriétés pour le champ de schéma.

Les différents sous-champs définis sous `properties` peuvent être définis à l’aide de n’importe quel `type` primitif ou en référençant un type de données existant par le biais d’une propriété `$ref` pointant vers le `$id` du type de données en question :

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field.",
  "type": "object",
  "properties": {
    "field1": {
      "type": "string"
    },
    "field2": {
      "$ref": "https://ns.adobe.com/xdm/common/measure"
    }
  }
}
```

Vous pouvez également définir l’objet entier via en faisant référence à un type de données, à condition que le type de données en question soit lui-même défini comme `type: object` :

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL Carte] {#map}

Un champ de mappage est essentiellement un champ de type [`object`](#object) avec un ensemble non contraint de clés. Comme les objets, les mappages ont une valeur `type` de `object`, mais leur `meta:xdmType` est explicitement définie sur `map`.

Un mappage **ne doit pas** définir de propriétés. Il **doit** définir un schéma de `additionalProperties` unique pour décrire le type de valeurs contenues dans le mappage (chaque mappage ne peut contenir qu’un seul type de données). La valeur `type` doit être `string` ou `integer`.

Par exemple, un champ de mappage avec des valeurs de type chaîne serait défini comme suit :

```json
"sampleField": {
  "title": "Sample Map Field",
  "description": "An example map field.",
  "type": "object",
  "meta:xdmType": "map",
  "additionalProperties": {
    "type": "string"
  }
}
```

Pour plus d’informations sur la création de champs de mappage personnalisés, consultez la section ci-dessous .

### Création de types de carte personnalisés {#custom-maps}

Pour prendre en charge efficacement les données « similaires à des mappages » dans XDM, les objets peuvent être annotés avec un jeu de `meta:xdmType` à `map` pour indiquer clairement qu’un objet doit être géré comme si le jeu de clés n’était pas contraint. Les données ingérées dans les champs de mappage doivent utiliser des clés de chaîne et uniquement des valeurs de chaîne ou entières (déterminées par `additionalProperties.type`).

XDM impose les restrictions suivantes à l’utilisation de cet indicateur de stockage :

* Les types de carte DOIVENT être de type `object`.
* Les propriétés des types de carte NE DOIVENT PAS ÊTRE définies (en d’autres termes, ils définissent des objets « vides »).
* Les types de mappage DOIVENT inclure un champ `additionalProperties.type` qui décrit les valeurs qui peuvent être placées dans le mappage, que ce soit `string` ou `integer`.

Assurez-vous d’utiliser uniquement des champs de type carte lorsqu’ils sont absolument nécessaires, car ils présentent les inconvénients de performance suivants :

* Le temps de réponse de [Adobe Experience Platform Query Service](../../query-service/home.md) passe de trois secondes à dix secondes pour 100 millions d’enregistrements.
* Les cartes doivent comporter moins de 16 clés, faute de quoi elles risquent d’être dégradées davantage.

L’interface utilisateur d’Experience Platform présente également des limites dans la façon dont elle peut extraire les clés des champs de type carte. Alors que les champs de type objet peuvent être développés, les mappages s’affichent sous la forme d’un seul champ à la place.

## Étapes suivantes

Ce guide explique comment définir différents types de champs dans l’API. Pour plus d’informations sur le formatage des types de champs XDM, consultez le guide sur les [ Contraintes de type de champ XDM ](../schema/field-constraints.md).
