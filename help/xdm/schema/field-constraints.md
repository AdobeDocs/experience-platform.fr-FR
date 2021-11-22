---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;groupe de champs;groupe de champs;groupes de champs;groupes de champs;type de données;types de données;types de données;type de données;conception de schéma;type de données;type de données;type de données;schémas;schémas;conception de schémas;mappage;carte;carte
solution: Experience Platform
title: Contraintes de type de champ XDM
topic-legacy: overview
description: Référence pour les contraintes de type de champ dans le modèle de données d’expérience (XDM), y compris les autres formats de sérialisation auxquels elles peuvent être mappées et comment définir vos propres types de champ dans l’API.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 684237122e7384f6c611e1c602c30af2518aba58
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 16%

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
| [!UICONTROL Entier] | Type : `INT32`<br>Annotation : `INT_32` | `IntegerType` | `java.lang.Integer` |
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
| [!UICONTROL Entier] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Court] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Octet] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Date] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Booléen] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Carte] | `Map` | (N/A) | `object` |

{style=&quot;table-layout:auto&quot;}

### MongoDB, Aerospike et Protobuf 2 {#mongo}

| Type XDM | MongoDB | Aerospike | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL Chaîne] | `string` | `String` | `string` |
| [!UICONTROL Double] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL Entier] | `int` | `Integer` | `int32` |
| [!UICONTROL Court] | `int` | `Integer` | `int32` |
| [!UICONTROL Octet] | `int` | `Integer` | `int32` |
| [!UICONTROL Date] | `date` | `Integer`<br>(millisecondes Unix) | `int64`<br>(millisecondes Unix) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(millisecondes Unix) | `int64`<br>(millisecondes Unix) |
| [!UICONTROL Booléen] | `bool` | `Integer`<br>(binaire 0/1) | `bool` |
| [!UICONTROL Carte] | `object` | `map` | `map<key_type, value_type>` |

{style=&quot;table-layout:auto&quot;}

## Définition des types de champ XDM dans l’API {#define-fields}

Tous les champs XDM sont définis à l’aide de la norme [Schéma JSON](https://json-schema.org/) contraintes qui s’appliquent à leur type de champ, avec des contraintes supplémentaires pour les noms de champ qui sont appliquées par [!DNL Experience Platform]. L’API Schema Registry vous permet de définir des types de champ supplémentaires à l’aide de formats et de contraintes facultatives. Les types de champ XDM sont exposés par l’attribut field-level, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` est une valeur générée par le système. Par conséquent, vous n’êtes pas obligé d’ajouter cette propriété au fichier JSON de votre champ lors de l’utilisation de l’API. La bonne pratique consiste à utiliser des types de schémas JSON (tels que `string` et `integer`) avec les contraintes min./max appropriées telles que définies dans le tableau ci-dessous.

Le tableau suivant décrit la mise en forme appropriée pour définir différents types de champs, y compris ceux avec des propriétés facultatives. Pour plus d’informations sur les propriétés facultatives et les mots-clés spécifiques au type, consultez la [documentation des schémas JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Pour commencer, recherchez le type de champ souhaité et utilisez l’exemple de code fourni pour créer votre requête API pour [création d’un groupe de champs](../api/field-groups.md#create) ou [création d’un type de données](../api/data-types.md#create).

<table style="table-layout:auto">
  <tr>
    <th>Type XDM</th>
    <th>Propriétés facultatives</th>
    <th>Exemple</th>
  </tr>
  <tr>
    <td>[!UICONTROL String]</td>
    <td>
      <ul>
        <li><code>pattern</code></li>
        <li><code>minLength</code></li>
        <li><code>maxLength</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
            "type": "string",
            "pattern": "^[A-Z]{2}$",
            "maxLength": 2
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "string",
          "format": "uri"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Enum]</td>
    <td>
      <ul>
        <li><code>default</code></li>
        <li><code>meta:enum</code></li>
      </ul>
    </td>
    <td>Les valeurs d’énumération contraintes sont fournies sous la variable <code>enum</code> , tandis que des étiquettes facultatives destinées aux clients pour chaque valeur peuvent être fournies sous <code>meta:enum</code>:
      <pre class="JSON language-JSON hljs">
"sampleField": {
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
}</pre>
    <br>Notez que la variable <code>meta:enum</code> la valeur est <strong>not</strong> déclarer une énumération ou piloter toute validation de données par elle-même. Dans la plupart des cas, les chaînes fournies sous <code>meta:enum</code> sont également fournis sous <code>enum</code> pour s’assurer que les données sont limitées. Cependant, il existe certains cas d’utilisation où <code>meta:enum</code> est fourni sans qu’un <code>enum</code> tableau. Voir le tutoriel sur <a href="../tutorials/extend-soft-enum.md">extension d’énumérations</a> pour plus d’informations.
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Number]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "number"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "integer",
          "minimum": -9007199254740992,
          "maximum": 9007199254740992
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Integer]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "integer",
          "minimum": -2147483648,
          "maximum": 2147483648
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Court]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "integer",
          "minimum": -32768,
          "maximum": 32768
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Byte]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "entier",
          "minimum": -128,
          "maximum": 128
  }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Booléen]</td>
    <td>
      <ul>
        <li><code>default</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "boolean",
          "default": false
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Date]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "string",
          "format": "date",
          "examples": ["2004-10-23"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "date-time", "examples" : ["2004-10-23T12:00:00-06:00"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Array]</td>
    <td></td>
    <td>Tableau de types scalaires de base (par exemple, chaînes) :
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "array",
          "items": {
            "type": "string"
  }
}</pre>
      Un tableau d’objets défini par un autre schéma :<br/>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "array", "items" : { "$ref": "https://ns.adobe.com/xdm/data/paymentitem" } }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Object]</td>
    <td></td>
    <td>Le <code>type</code> de chaque sous-champ défini sous <code>properties</code> peut être défini à l’aide de n’importe quel type scalaire :
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "object",
          "properties": {
            "field1": {
              "type": "string"
            },
            "field2": {
              "type": "number"
    }
  }
}</pre>
      Les champs de type objet peuvent être définis en référençant la variable <code>$id</code> d’un type de données :
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "$ref" : "https://ns.adobe.com/xdm/common/phoneinteraction" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>Une carte <strong>must not</strong> définissez les propriétés. It <strong>must</strong> définir une seule <code>additionalProperties</code> schéma pour décrire le type de valeurs contenues dans le mappage (chaque mappage ne peut contenir qu’un seul type de données). Les valeurs peuvent être tout XDM valide <code>type</code> ou une référence à un autre schéma à l’aide d’un <code>$ref</code> attribut.<br/><br/>Un champ map avec des valeurs de type chaîne :
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "object",
          "additionalProperties":{
            "type": "string"
  }
}</pre>
    Un champ map avec des tableaux de chaînes pour les valeurs :
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "object",
          "additionalProperties":{
            "type": "array",
            "items": {
              "type": "string"
    }
  }
}</pre>
    Un champ map qui fait référence à un autre type de données :
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "additionalProperties":{ "$ref": "https://ns.adobe.com/xdm/data/paymentitem" } }</pre>
    </td>
  </tr>
</table>
