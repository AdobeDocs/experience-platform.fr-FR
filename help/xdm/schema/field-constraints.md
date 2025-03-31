---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;groupe de champs;Groupe de champs;Groupes de champs;groupes de champs;type de données;types de données;types de données;type de données;conception de schéma;type de données;type de données;type de données;type de données;schémas;Schémas;conception de schéma;mapper;Mapper;
solution: Experience Platform
title: Contraintes de type de champ XDM
description: Référence pour les contraintes de type de champ dans le modèle de données d’expérience (XDM), y compris les autres formats de sérialisation auxquels ils peuvent être mappés et comment définir vos propres types de champ dans l’API.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: ca8859c7b71d1b0aad30880ff066d2b4b33b0a35
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 7%

---

# Contraintes des types de champs XDM

Dans les schémas de modèle de données d’expérience (XDM), le type d’un champ limite le type de données que le champ peut contenir. Ce document fournit un aperçu de chaque type de champ principal, y compris des autres formats de sérialisation auxquels ils peuvent être mappés et de la manière de définir vos propres types de champs dans l’API afin d’appliquer différentes contraintes.

## Commencer

Avant d’utiliser ce guide, consultez les [principes de base de la composition des schémas](./composition.md) pour une présentation des schémas, classes et groupes de champs de schéma XDM.

Si vous prévoyez de définir vos propres types de champs dans l’API, il est vivement recommandé de commencer par le guide de développement du [registre des schémas](../api/getting-started.md) pour savoir comment créer des groupes de champs et des types de données afin d’inclure vos champs personnalisés dans . Si vous utilisez l’interface utilisateur d’Experience Platform pour créer vos schémas, consultez le guide sur la [définition de champs dans l’interface utilisateur](../ui/fields/overview.md) pour savoir comment implémenter des contraintes sur les champs que vous définissez dans des groupes de champs et des types de données personnalisés.

## Structure de base et exemples {#basic-types}

XDM repose sur le schéma JSON. Par conséquent, les champs XDM héritent d’une syntaxe similaire lors de la définition de leur type. Comprendre comment différents types de champs sont représentés dans le schéma JSON peut vous aider à indiquer les contraintes de base de chaque type. Les noms des champs personnalisés ne respectent pas la casse et doivent porter des noms différents au même niveau dans votre schéma.

>[!NOTE]
>
>Pour plus d’informations sur le schéma JSON et les autres technologies sous-jacentes dans les API Platform](../../landing/api-fundamentals.md#json-schema) consultez le [ guide des principes de base des API .

Le tableau suivant décrit la manière dont chaque type XDM est représenté dans le schéma JSON, ainsi qu’un exemple de valeur conforme au type :

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
{« type »: « string »}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Number]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{« type »: « number »}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  « type » : « integer »,
  « maximum » : 9007199254740991,
  « minimum » : -9007199254740991
}</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  « type » : « integer »,
  « maximum » : 2147483648,
  « minimum » : -2147483648
}</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  « type » : « integer »,
  « maximum » : 32768,
  « minimum » : -32768
}</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  « type » : « integer »,
  « maximum » : 128
  « minimum » : -128
}</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Date]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  « type »: « string »,
  « format »: « date »
}</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  « type »: « string »,
  « format » : « date-heure »
}</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Boolean]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{« type »: « boolean »}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**Toutes les chaînes formatées en date doivent être conformes à la norme ISO 8601 ([RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Faire correspondre les types XDM à d’autres formats

Les sections ci-dessous décrivent comment chaque type XDM correspond à d’autres formats de sérialisation courants :

* [Parquet, Spark SQL et Java](#parquet)
* [Scala, .NET et CosmosDB](#scala)
* [MongoDB, Aerospike et Protobuf 2](#mongo)

>[!NOTE]
>
>Parmi les types XDM standard répertoriés dans les tableaux ci-dessous, le type [!UICONTROL Map] est également inclus. Les mappages sont utilisés dans les schémas standard lorsque les données sont représentées sous la forme de clés qui correspondent à certaines valeurs, ou lorsque les clés ne peuvent raisonnablement pas être incluses dans un schéma statique et doivent être traitées comme des valeurs de données.
>
>De nombreux composants XDM standard utilisent des types de mappage. Vous pouvez également [définir des champs de mappage personnalisés](../tutorials/custom-fields-api.md#custom-maps) si vous le souhaitez. L’inclusion du type de mappage dans les tableaux ci-dessous est destinée à vous aider à déterminer comment mapper vos données existantes à XDM si elles sont actuellement stockées dans l’un des formats répertoriés ci-dessous.

### Parquet, Spark SQL et Java {#parquet}

| Type XDM | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL Chaîne] | Type : `BYTE_ARRAY`<br>Annotation : `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Nombre] | Type : `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Long] | Type : `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Entier] | Type : `INT32`<br>Annotation : `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Court] | Type : `INT32`<br>Annotation : `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Octet] | Type : `INT32`<br>Annotation : `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Date] | Type : `INT32`<br>Annotation : `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateHeure] | Type : `INT64`<br>Annotation : `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL booléen] | Type : `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Carte] | Groupe `MAP`-annoté <br><br>(`<key-type>` doit être `STRING`) | `MapType`<br><br>(`keyType` doit être `StringType`) | `java.util.Map` |

{style="table-layout:auto"}

### Scala, .NET et CosmosDB {#scala}

| Type XDM | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL Chaîne] | `String` | `System.String` | `String` |
| [!UICONTROL Nombre] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Long] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Entier] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Court] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Octet] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Date] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateHeure] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL booléen] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Carte] | `Map` | (S/O) | `object` |

{style="table-layout:auto"}

### MongoDB, Aerospike et Protobuf 2 {#mongo}

| Type XDM | MongoDB | Aerospike | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL Chaîne] | `string` | `String` | `string` |
| [!UICONTROL Nombre] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL Entier] | `int` | `Integer` | `int32` |
| [!UICONTROL Court] | `int` | `Integer` | `int32` |
| [!UICONTROL Octet] | `int` | `Integer` | `int32` |
| [!UICONTROL Date] | `date` | `Integer`<br> (Unix millisecondes) | `int64`<br> (Unix millisecondes) |
| [!UICONTROL DateHeure] | `timestamp` | `Integer`<br> (Unix millisecondes) | `int64`<br> (Unix millisecondes) |
| [!UICONTROL booléen] | `bool` | `Integer`<br>(0/1 binaire) | `bool` |
| [!UICONTROL Carte] | `object` | `map` | `map<key_type, value_type>` |

{style="table-layout:auto"}

## Définir des types de champs XDM dans l’API {#define-fields}

L’API Schema Registry vous permet de définir des champs personnalisés à l’aide de formats et de contraintes facultatives. Pour plus d’informations, consultez le guide sur la [définition de champs personnalisés dans l’API Schema Registry](../tutorials/custom-fields-api.md).
