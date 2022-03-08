---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;groupe de champs;groupe de champs;groupes de champs;groupes de champs;type de données;types de données;types de données;type de données;conception de schéma;type de données;type de données;type de données;schémas;schémas;conception de schémas;mappage;carte;carte
solution: Experience Platform
title: Contraintes de type de champ XDM
topic-legacy: overview
description: Référence pour les contraintes de type de champ dans le modèle de données d’expérience (XDM), y compris les autres formats de sérialisation auxquels elles peuvent être mappées et comment définir vos propres types de champ dans l’API.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 279a1d90be82188ad6fd9d2bb9123354d0046b0d
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 12%

---

# Contraintes de type de champ XDM

Dans les schémas de modèle de données d’expérience (XDM), le type d’un champ restreint le type de données que le champ peut contenir. Ce document fournit un aperçu de chaque type de champ principal, y compris les autres formats de sérialisation auxquels ils peuvent être mappés et comment définir vos propres types de champ dans l’API afin d’appliquer différentes contraintes.

## Prise en main

Avant d’utiliser ce guide, veuillez consulter la section [principes de base de la composition des schémas](./composition.md) pour une introduction aux schémas XDM, aux classes et aux groupes de champs de schéma.

Si vous prévoyez de définir vos propres types de champ dans l’API, il est vivement recommandé de commencer par la variable [Guide de développement du registre des schémas](../api/getting-started.md) pour savoir comment créer des groupes de champs et des types de données pour inclure vos champs personnalisés dans . Si vous utilisez l’interface utilisateur de l’Experience Platform pour créer vos schémas, consultez le guide sur la [définition des champs dans l’interface utilisateur](../ui/fields/overview.md) pour découvrir comment implémenter des contraintes sur les champs que vous définissez dans des groupes de champs personnalisés et des types de données.

## Structure de base et exemples

XDM repose sur le schéma JSON. Par conséquent, les champs XDM héritent d’une syntaxe similaire lors de la définition de leur type. Comprendre comment différents types de champ sont représentés dans le schéma JSON peut aider à indiquer les contraintes de base de chaque type.

>[!NOTE]
>
>Voir [Guide de base des API](../../landing/api-fundamentals.md#json-schema) pour plus d’informations sur le schéma JSON et d’autres technologies sous-jacentes dans les API Platform.

Le tableau suivant décrit la représentation de chaque type XDM dans le schéma JSON, ainsi qu’un exemple de valeur conforme au type :

<table style="table-layout:auto">
  <thead>
    <tr>
      <th>Type XDM</th>
      <th>Schéma JSON</th>
      <th>Exemple</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[!UICONTROL String]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Double]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "number"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 9007199254740991, "minimum" : -9007199254740991 }</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 2147483648, "minimum" : -2147483648 }</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Court]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 32768, "minimum" : -32768 }</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 128, "minimum" : -128 }</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Date]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "string", "format": "date" }</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "string", "format": "date-time" }</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Booléen]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**Toutes les chaînes au format date doivent être conformes à la norme ISO 8601 ([RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Faire correspondre les types XDM à d’autres formats

Les sections ci-dessous décrivent comment chaque type XDM est mappé à d’autres formats de sérialisation courants :

* [Parquet, Spark SQL et Java](#parquet)
* [Scala, .NET et CosmosDB](#scala)
* [MongoDB, Aerospike et Protobuf 2](#mongo)

>[!IMPORTANT]
>
>Parmi les types XDM standard répertoriés dans les tableaux ci-dessous, la variable [!UICONTROL Carte] est également inclus. Les cartes sont utilisées dans les schémas standard lorsque les données sont représentées sous la forme de clés qui mappent à certaines valeurs ou lorsque les clés ne peuvent pas raisonnablement être incluses dans un schéma statique et doivent être traitées comme des valeurs de données.
>
>Les champs de type map sont réservés à l’utilisation des schémas du secteur et des fournisseurs et ne peuvent donc pas être utilisés dans les ressources personnalisées que vous définissez. L’inclusion du type de mappage dans les tableaux ci-dessous est uniquement destinée à vous aider à déterminer comment mapper vos données existantes à XDM si elles sont actuellement stockées dans l’un des formats répertoriés ci-dessous.

### Parquet, Spark SQL et Java {#parquet}

| Type XDM | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL Chaîne] | Type : `BYTE_ARRAY`<br>Annotation : `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Double] | Type : `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Long] | Type : `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Nombre entier] | Type : `INT32`<br>Annotation : `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Court] | Type : `INT32`<br>Annotation : `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Octet] | Type : `INT32`<br>Annotation : `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Date] | Type : `INT32`<br>Annotation : `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Type : `INT64`<br>Annotation : `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Booléen] | Type : `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Carte] | `MAP`-groupe annoté<br><br>(`<key-type>` must `STRING`) | `MapType`<br><br>(`keyType` must `StringType`) | `java.util.Map` |

{style=&quot;table-layout:auto&quot;}

### Scala, .NET et CosmosDB {#scala}

| Type XDM | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL Chaîne] | `String` | `System.String` | `String` |
| [!UICONTROL Double] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Long] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Nombre entier] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Court] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Octet] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Date] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Booléen] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Carte] | `Map` | (S/O) | `object` |

{style=&quot;table-layout:auto&quot;}

### MongoDB, Aerospike et Protobuf 2 {#mongo}

| Type XDM | MongoDB | Aerospike | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL Chaîne] | `string` | `String` | `string` |
| [!UICONTROL Double] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL Nombre entier] | `int` | `Integer` | `int32` |
| [!UICONTROL Court] | `int` | `Integer` | `int32` |
| [!UICONTROL Octet] | `int` | `Integer` | `int32` |
| [!UICONTROL Date] | `date` | `Integer`<br>(millisecondes Unix) | `int64`<br>(millisecondes Unix) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(millisecondes Unix) | `int64`<br>(millisecondes Unix) |
| [!UICONTROL Booléen] | `bool` | `Integer`<br>(binaire 0/1) | `bool` |
| [!UICONTROL Carte] | `object` | `map` | `map<key_type, value_type>` |

{style=&quot;table-layout:auto&quot;}

## Définition des types de champ XDM dans l’API {#define-fields}

L’API Schema Registry vous permet de définir des champs personnalisés à l’aide de formats et de contraintes facultatives. Consultez le guide sur la [définition de champs personnalisés dans l’API Schema Registry](../tutorials/custom-fields-api.md) pour plus d’informations.
