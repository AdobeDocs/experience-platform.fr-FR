---
title: Définition des champs XDM dans l’API Schema Registry
description: Découvrez comment définir différents champs lors de la création de ressources XDM (Experience Data Model) personnalisées dans l’API Schema Registry.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 1%

---

# Définition des champs XDM dans l’API Schema Registry

Tous les champs de modèle de données d’expérience (XDM) sont définis à l’aide des contraintes [Schéma JSON](https://json-schema.org/) standard qui s’appliquent à leur type de champ, avec des contraintes supplémentaires pour les noms de champ qui sont appliqués par Adobe Experience Platform. L’API Schema Registry vous permet de définir des champs personnalisés dans vos schémas à l’aide de formats et de contraintes facultatives. Les types de champ XDM sont exposés par l’attribut field-level, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` est une valeur générée par le système. Par conséquent, vous n’êtes pas obligé d’ajouter cette propriété au JSON de votre champ lors de l’utilisation de l’API (sauf lors de la [création de types de mappage personnalisés](#custom-maps)). La bonne pratique consiste à utiliser des types de schémas JSON (tels que `string` et `integer`) avec les contraintes min/max appropriées telles que définies dans le tableau ci-dessous.

Ce guide décrit la mise en forme appropriée pour définir différents types de champ, y compris ceux avec des propriétés facultatives. Pour plus d’informations sur les propriétés facultatives et les mots-clés spécifiques au type, consultez la [documentation des schémas JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Pour commencer, recherchez le type de champ souhaité et utilisez l’exemple de code fourni pour créer votre requête API pour [créer un groupe de champs](../api/field-groups.md#create) ou [créer un type de données](../api/data-types.md#create).

## [!UICONTROL Chaîne] {#string}

Les champs [!UICONTROL String] sont indiqués par `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

Vous pouvez éventuellement limiter les types de valeurs qui peuvent être saisis pour la chaîne au moyen des propriétés supplémentaires suivantes :

* `pattern` : modèle regex à contraindre.
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

Les champs [!UICONTROL URI] sont indiqués par `type: string` avec une propriété `format` définie sur `uri`. Aucune autre propriété n’est acceptée.

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

Vous pouvez éventuellement fournir des étiquettes destinées aux clients pour chaque valeur sous une propriété `meta:enum`, chaque étiquette étant indexée sur une valeur correspondante sous `enum`.

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
>La valeur `meta:enum` ne **pas** déclare une énumération ou exécute toute validation de données seule. Dans la plupart des cas, les chaînes fournies sous `meta:enum` sont également fournies sous `enum` pour s’assurer que les données sont limitées. Cependant, il existe certains cas d’utilisation où `meta:enum` est fourni sans tableau `enum` correspondant. Pour plus d’informations, consultez le tutoriel sur la [définition des valeurs suggérées](../tutorials/suggested-values.md) .

Vous pouvez éventuellement fournir une propriété `default` pour indiquer la valeur `enum` par défaut que le champ utilisera si aucune valeur n’est fournie.

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
>Si aucune valeur `default` n’est fournie et que le champ d’énumération est défini sur `required`, tout enregistrement ne disposant pas d’une valeur acceptée pour ce champ ne sera pas validé lors de l’ingestion.

## [!UICONTROL Number] {#number}

Les champs Nombre sont indiqués par `type: number` et ne possèdent aucune autre propriété requise.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>Les types `number` sont utilisés pour tout type numérique, qu’il s’agisse de nombres entiers ou de nombres à virgule flottante, tandis que les [`integer` types](#integer) sont utilisés pour les nombres entiers en particulier. Pour plus d’informations sur les cas d’utilisation de chaque type, consultez la [documentation du schéma JSON sur les types numériques](https://json-schema.org/understanding-json-schema/reference/numeric.html) .

## [!UICONTROL Entier] {#integer}

Les champs [!UICONTROL Entier] sont indiqués par `type: integer` et ne comportent aucun autre champ obligatoire.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>Bien que les types `integer` fassent spécifiquement référence aux nombres entiers, les [`number` types](#number) sont utilisés pour tout type numérique, qu’il s’agisse de nombres entiers ou de nombres à virgule flottante. Pour plus d’informations sur les cas d’utilisation de chaque type, consultez la [documentation du schéma JSON sur les types numériques](https://json-schema.org/understanding-json-schema/reference/numeric.html) .

Vous pouvez éventuellement limiter la plage de l’entier en ajoutant des propriétés `minimum` et `maximum` à la définition. Plusieurs autres types numériques pris en charge par l’interface utilisateur du Générateur de schémas ne sont que `integer` avec des contraintes `minimum` et `maximum` spécifiques, telles que [[!UICONTROL Long]](#long), [[!UICONTROL Short]](#short) et [[!UICONTROL Byte]](#byte).

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

L’équivalent d’un champ [!UICONTROL Long] créé via l’interface utilisateur du Générateur de schémas est un champ de type [`integer`](#integer) avec des valeurs `minimum` et `maximum` spécifiques (`-9007199254740992` et `9007199254740992`, respectivement).

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

L’équivalent d’un champ [!UICONTROL Court] créé via l’interface utilisateur du Générateur de schémas est un champ de type [`integer`](#integer) avec des valeurs `minimum` et `maximum` spécifiques (`-32768` et `32768`, respectivement).

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

L’équivalent d’un champ [!UICONTROL Byte] créé via l’interface utilisateur du Générateur de schémas est un champ de type [`integer`](#integer) avec des valeurs `minimum` et `maximum` spécifiques (`-128` et `128`, respectivement).

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 128
}
```

## [!UICONTROL Booléen] {#boolean}

Les champs [!UICONTROL Booléen] sont indiqués par `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

Vous pouvez éventuellement fournir une valeur `default` que le champ utilisera lorsqu’aucune valeur explicite n’est fournie pendant l’ingestion.

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
>Si aucune valeur `default` n’est fournie et que le champ booléen est défini sur `required`, tout enregistrement ne disposant pas d’une valeur acceptée pour ce champ ne sera pas validé lors de l’ingestion.

## [!UICONTROL Date] {#date}

Les champs [!UICONTROL Date] sont indiqués par `type: string` et `format: date`. Vous pouvez également éventuellement fournir un tableau de `examples` à exploiter lorsque vous souhaitez afficher un exemple de chaîne de date pour les utilisateurs qui saisissent les données manuellement.

```json
"sampleField": {
  "title": "Sample Date Field",
  "description": "An example date field with an example array item.",
  "type": "string",
  "format": "date",
  "examples": ["2004-10-23"]
}
```

## [!UICONTROL DateTime] {#date-time}

Les champs [!UICONTROL DateTime] sont indiqués par `type: string` et `format: date-time`. Vous pouvez également éventuellement fournir un tableau de `examples` à exploiter lorsque vous souhaitez afficher un exemple de chaîne de date et d’heure pour les utilisateurs qui saisissent les données manuellement.

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

Les champs [!UICONTROL Array] sont indiqués par `type: array` et un objet `items` qui définit le schéma des éléments que le tableau accepte.

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

Vous pouvez également définir les éléments du tableau en fonction d’un type de données existant en faisant référence à `$id` du type de données par le biais d’une propriété `$ref`. Voici un tableau d’objets [!UICONTROL payment Item] :

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

Chaque sous-champ défini sous `properties` peut être défini à l’aide de n’importe quel `type` primitif ou en référençant un type de données existant via une propriété `$ref` pointant vers le `$id` du type de données en question :

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

Vous pouvez également définir l’objet entier en faisant référence à un type de données, à condition que le type de données en question soit lui-même défini comme `type: object` :

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL Carte] {#map}

Un champ de mappage est essentiellement un champ de type [`object` ](#object) avec un ensemble de clés non limité. Comme les objets, les cartes ont une valeur `type` de `object`, mais leur `meta:xdmType` est explicitement défini sur `map`.

Une carte **ne doit pas** définir de propriétés. Il **must** définit un seul schéma `additionalProperties` pour décrire le type de valeurs contenu dans la carte (chaque carte ne peut contenir qu’un seul type de données). La valeur `type` doit être `string` ou `integer`.

Par exemple, un champ map avec des valeurs de type chaîne est défini comme suit :

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

Consultez la section ci-dessous pour plus d’informations sur la création de champs de mappage personnalisés.

### Création de types de mappage personnalisés {#custom-maps}

Afin de prendre en charge efficacement les données &quot;map-like&quot; dans XDM, les objets peuvent être annotés avec un `meta:xdmType` défini sur `map` pour indiquer clairement qu’un objet doit être géré comme si l’ensemble de clés n’était pas limité. Les données ingérées dans les champs de mappage doivent utiliser des clés de chaîne et uniquement des valeurs string ou integer (comme déterminé par `additionalProperties.type`).

XDM impose les restrictions suivantes à l’utilisation de cet indice de stockage :

* Les types de carte DOIVENT être de type `object`.
* Les types de carte NE DOIVENT PAS avoir de propriétés définies (en d’autres termes, ils définissent des objets &quot;vides&quot;).
* Les types de carte DOIVENT inclure un champ `additionalProperties.type` qui décrit les valeurs qui peuvent être placées dans le mappage, `string` ou `integer`.

Assurez-vous que vous utilisez uniquement des champs de type map lorsque cela est absolument nécessaire, car ils présentent les inconvénients suivants en termes de performances :

* Le temps de réponse de [Adobe Experience Platform Query Service](../../query-service/home.md) se dégrade de trois secondes à dix secondes pour 100 millions d’enregistrements.
* Les cartes doivent comporter moins de 16 clés, sinon elles risquent d’être détériorées.

L’interface utilisateur de Platform présente également des limites quant à la manière dont elle peut extraire les clés des champs de type map. Bien que les champs de type objet puissent être développés, les mappages s’affichent sous la forme d’un champ unique.

## Étapes suivantes

Ce guide explique comment définir différents types de champ dans l’API. Pour plus d’informations sur la mise en forme des types de champ XDM, consultez le guide sur les [contraintes de type de champ XDM](../schema/field-constraints.md).
