---
title: Définition des champs XDM dans l’API Schema Registry
description: Découvrez comment définir différents champs lors de la création de ressources XDM (Experience Data Model) personnalisées dans l’API Schema Registry.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 6277725cd69bc94325d3584177742df1a7fd4f95
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 3%

---

# Définition des champs XDM dans l’API Schema Registry

Tous les champs de modèle de données d’expérience (XDM) sont définis à l’aide de la norme [Schéma JSON](https://json-schema.org/) contraintes qui s’appliquent à leur type de champ, avec des contraintes supplémentaires pour les noms de champ qui sont appliqués par Adobe Experience Platform. L’API Schema Registry vous permet de définir des champs personnalisés dans vos schémas à l’aide de formats et de contraintes facultatives. Les types de champ XDM sont exposés par l’attribut field-level, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` est une valeur générée par le système. Par conséquent, vous n’êtes pas obligé d’ajouter cette propriété au fichier JSON de votre champ lors de l’utilisation de l’API (sauf lorsque [création de types de mappage personnalisés](#custom-maps)). La bonne pratique consiste à utiliser des types de schémas JSON (tels que `string` et `integer`) avec les contraintes min./max appropriées telles que définies dans le tableau ci-dessous.

Ce guide décrit la mise en forme appropriée pour définir différents types de champ, y compris ceux avec des propriétés facultatives. Pour plus d’informations sur les propriétés facultatives et les mots-clés spécifiques au type, consultez la [documentation des schémas JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Pour commencer, recherchez le type de champ souhaité et utilisez l’exemple de code fourni pour créer votre requête API pour [création d’un groupe de champs](../api/field-groups.md#create) ou [création d’un type de données](../api/data-types.md#create).

## [!UICONTROL Chaîne] {#string}

[!UICONTROL Chaîne] les champs indiqués par `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

Vous pouvez éventuellement limiter les types de valeurs qui peuvent être saisis pour la chaîne au moyen des propriétés supplémentaires suivantes :

* `pattern`: Un modèle d’expression régulière à contraindre.
* `minLength`: Longueur minimale de la chaîne.
* `maxLength`: Longueur maximale de la chaîne.

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

[!UICONTROL URI] les champs indiqués par `type: string` avec un `format` définie sur `uri`. Aucune autre propriété n’est acceptée.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL Énumération] {#enum}

[!UICONTROL Enum] Les champs doivent être utilisés `type: string`, avec les valeurs d’énumération elles-mêmes fournies sous une `enum` tableau :

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

Vous pouvez éventuellement fournir des étiquettes destinées aux clients pour chaque valeur sous une `meta:enum` , avec chaque libellé associé à une valeur correspondante sous `enum`.

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
>Le `meta:enum` la valeur est **not** déclarer une énumération ou piloter toute validation de données par elle-même. Dans la plupart des cas, les chaînes fournies sous `meta:enum` sont également fournis sous `enum` pour s’assurer que les données sont limitées. Cependant, il existe certains cas d’utilisation où `meta:enum` est fourni sans qu’un `enum` tableau. Voir le tutoriel sur [définition des valeurs proposées](../tutorials/suggested-values.md) pour plus d’informations.

Vous pouvez éventuellement fournir un `default` pour indiquer la propriété par défaut `enum` valeur que le champ utilisera si aucune valeur n’est fournie.

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
>Si non `default` est fournie et le champ enum est défini sur `required`, toute valeur acceptée de ce champ n’est pas validée lors de l’ingestion.

## [!UICONTROL Nombre] {#number}

Les champs Nombre sont indiqués par `type: number` et ne comportent aucune autre propriété requise.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` Les types sont utilisés pour tout type numérique, qu’il s’agisse de nombres entiers ou de nombres à virgule flottante, alors que [`integer` types](#integer) sont spécifiquement utilisés pour les nombres entiers. Reportez-vous à la section [Documentation du schéma JSON sur les types numériques](https://json-schema.org/understanding-json-schema/reference/numeric.html) pour plus d’informations sur les cas d’utilisation de chaque type.

## [!UICONTROL Nombre entier] {#integer}

[!UICONTROL Entier] les champs indiqués par `type: integer` et ne comportent aucun autre champ requis.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>while `integer` les types font spécifiquement référence aux nombres entiers, [`number` types](#number) sont utilisés pour tout type numérique, qu’il s’agisse de nombres entiers ou de nombres à virgule flottante. Reportez-vous à la section [Documentation du schéma JSON sur les types numériques](https://json-schema.org/understanding-json-schema/reference/numeric.html) pour plus d’informations sur les cas d’utilisation de chaque type.

Vous pouvez éventuellement limiter la plage de l’entier en ajoutant `minimum` et `maximum` propriétés de la définition. Plusieurs autres types numériques pris en charge par l’interface utilisateur du Créateur de schémas sont simplement `integer` types spécifiques `minimum` et `maximum` des contraintes, telles que [[!UICONTROL Long]](#long), [[!UICONTROL Court]](#short), et [[!UICONTROL Octet]](#byte).

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

L’équivalent d’un [!UICONTROL Long] le champ créé via l’interface utilisateur du Créateur de schémas est une [`integer` champ de type](#integer) avec des `minimum` et `maximum` valeurs (`-9007199254740992` et `9007199254740992`, respectivement).

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

L’équivalent d’un [!UICONTROL Court] le champ créé via l’interface utilisateur du Créateur de schémas est une [`integer` champ de type](#integer) avec des `minimum` et `maximum` valeurs (`-32768` et `32768`, respectivement).

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

L’équivalent d’un [!UICONTROL Octet] le champ créé via l’interface utilisateur du Créateur de schémas est une [`integer` champ de type](#integer) avec des `minimum` et `maximum` valeurs (`-128` et `128`, respectivement).

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

[!UICONTROL Booléen] les champs indiqués par `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

Vous pouvez éventuellement fournir un `default` valeur que le champ utilisera lorsqu’aucune valeur explicite n’est fournie pendant l’ingestion.

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
>Si non `default` est fournie et le champ booléen est défini sur `required`, toute valeur acceptée de ce champ n’est pas validée lors de l’ingestion.

## [!UICONTROL Date] {#date}

[!UICONTROL Date] les champs indiqués par `type: string` et `format: date`. Vous pouvez également fournir un tableau de `examples` pour tirer parti des cas où vous souhaitez afficher un exemple de chaîne de date pour les utilisateurs qui saisissent les données manuellement.

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

[!UICONTROL DateTime] les champs indiqués par `type: string` et `format: date-time`. Vous pouvez également fournir un tableau de `examples` pour tirer parti des cas où vous souhaitez afficher un exemple de chaîne datetime pour les utilisateurs qui saisissent les données manuellement.

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

[!UICONTROL Tableau] les champs indiqués par `type: array` et un `items` qui définit le schéma des éléments que le tableau acceptera.

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

Vous pouvez également définir les éléments du tableau en fonction d’un type de données existant en faisant référence au `$id` du type de données par le biais d’une `$ref` . Voici un tableau de [!UICONTROL Élément de paiement] objets :

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

[!UICONTROL Objet] les champs indiqués par `type: object` et un `properties` qui définit des sous-propriétés pour le champ de schéma.

Chaque sous-champ défini sous `properties` peut être défini à l’aide de n’importe quel primitif. `type` ou en référençant un type de données existant via un `$ref` pointant vers la propriété `$id` du type de données en question :

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

Vous pouvez également définir l’objet entier en faisant référence à un type de données, à condition que le type de données en question soit lui-même défini comme `type: object`:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL Carte] {#map}

Un champ de carte est essentiellement un [`object`Champ de type](#object) avec un ensemble de clés non limité. Comme les objets, les cartes ont une `type` valeur de `object`, mais leur `meta:xdmType` est explicitement défini sur `map`.

Une carte **must not** définissez les propriétés. It **must** définir une seule `additionalProperties` schéma pour décrire le type de valeurs contenues dans le mappage (chaque mappage ne peut contenir qu’un seul type de données). Le `type` doit être définie sur `string` ou `integer`.

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

Afin de prendre en charge efficacement les données &quot;de type carte&quot; dans XDM, les objets peuvent être annotés avec un `meta:xdmType` défini sur `map` pour indiquer clairement qu’un objet doit être géré comme si l’ensemble de clés n’était pas contraint. Les données ingérées dans les champs de mappage doivent utiliser des clés de chaîne et uniquement des valeurs string ou integer (telles que déterminées par `additionalProperties.type`).

XDM impose les restrictions suivantes à l’utilisation de cet indice de stockage :

* Les types de carte DOIVENT être de type `object`.
* Les types de carte NE DOIVENT PAS avoir de propriétés définies (en d’autres termes, ils définissent des objets &quot;vides&quot;).
* Les types de carte DOIVENT inclure un `additionalProperties.type` qui décrit les valeurs qui peuvent être placées dans le mappage, soit `string` ou `integer`.

Assurez-vous que vous utilisez uniquement des champs de type map lorsque cela est absolument nécessaire, car ils présentent les inconvénients suivants en termes de performances :

* Temps de réponse de [Adobe Experience Platform Query Service](../../query-service/home.md) se dégrade de trois secondes à dix secondes pour 100 millions d&#39;enregistrements.
* Les cartes doivent comporter moins de 16 clés, sinon elles risquent d’être détériorées.

L’interface utilisateur de Platform présente également des limites quant à la manière dont elle peut extraire les clés des champs de type map. Bien que les champs de type objet puissent être développés, les mappages s’affichent sous la forme d’un champ unique.

## Étapes suivantes

Ce guide explique comment définir différents types de champ dans l’API. Pour plus d’informations sur la mise en forme des types de champ XDM, consultez le guide sur [Contraintes de type de champ XDM](../schema/field-constraints.md).
