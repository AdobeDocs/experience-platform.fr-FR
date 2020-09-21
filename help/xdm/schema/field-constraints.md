---
keywords: Experience Platform;home;popular topics;schema;Schema;mixin;Mixin;Mixins;mixins;data type;data types;Data types;Data type;schema design;datatype;Datatype;data type;Data type;schemas;Schemas;Schema design;map;Map;
solution: Experience Platform
title: Contraintes de type de champ XDM
topic: overview
description: Référence pour les contraintes de type de champ XDM, y compris les autres formats de sérialisation auxquels elles peuvent être associées et comment définir vos propres types de champ dans l’API.
translation-type: tm+mt
source-git-commit: 19167f58fae6fac7d938deb74182d2e19960beb3
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 74%

---


# Contraintes de type de champ XDM

Les types de champs XDM que vous sélectionnez pour vos schémas limitent les types de données que ces champs peuvent contenir. Ce document fournit une vue d’ensemble de chaque type de champ principal, y compris les autres formats de sérialisation auxquels ils peuvent être mappés, ainsi que la manière de définir vos propres types de champ dans l’API afin d’appliquer différentes contraintes.

## Prise en main

Avant d&#39;utiliser ce guide, veuillez examiner les [bases de la composition](./composition.md) des schémas pour une introduction aux schémas, classes et mixins XDM.

Si vous prévoyez de définir vos propres types de champs, il est vivement recommandé de début avec le guide [de développement du registre des](../api/getting-started.md) Schémas pour savoir comment créer des mixins et des types de données pour inclure vos champs personnalisés dans.

## Faire correspondre les types XDM à d’autres formats

The table below describes the mapping between each XDM type (`meta:xdmType`) and other serialization formats.

| Type XDM<br>(meta:xdmType) | JSON<br>(schéma JSON) | Parquet<br>(type/annotation) | [!DNL Spark] SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aerospike | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | type : chaîne | BYTE_ARRAY/UTF8 | StringType | java.lang.String | Chaîne | System.String | Chaîne | string | Chaîne | string |
| nombre | type : nombre | DOUBLE | DoubleType | java.lang.Double | Double | System.Double | Nombre | double | Double | double |
| long | type : entier<br>maximum : 2^53+1<br>minimum : -2^53+1 | INT64 | LongType | java.lang.Long | Long | System.Int64 | Nombre | long | Entier | int64 |
| int | type : entier<br>maximum : 2^31<br>minimum : -2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Nombre | int | Entier | int32 |
| court | type : entier<br>maximum : 2^15<br>minimum : -2^15 | INT32/INT_16 | ShortType | java.lang.Short | Court | System.Int16 | Nombre | int | Entier | int32 |
| byte | type : entier<br>maximum : 2^7<br>minimum : -2^7 | INT32/INT_8 | ByteType | java.lang.Short | Octet | System.SByte | Nombre | int | Entier | int32 |
| boolean | type : booléen | BOOLEAN | BooleanType | java.lang.Boolean | Booléen | System.Boolean | Booléen | bool | Entier | Entier | bool |
| date | type : chaîne<br>format : date<br>(RFC 3339, section 5.6) | INT32/DATE | DateType | java.util.Date | java.util.Date | System.DateTime | Chaîne | date | Entier<br>(unix millis) | int64<br>(unix millis) |
| date-time | type : chaîne<br>format : date-time<br>(RFC 3339, section 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | Chaîne | timestamp | Entier<br>(unix millis) | int64<br>(unix millis) |
| map | objet | Groupe annoté MAP<br><br>&lt;<span>key_type</span>> DOIT être STRING<br><br>&lt;<span>value_type</span>> type de valeurs de correspondance | MapType<br><br>&quot;keyType&quot; DOIT être StringType<br><br>&quot;valueType&quot; est le type de valeurs de correspondance. | java.util.Map | Map | --- | objet | objet | map | map&lt;<span>key_type, value_type</span>> |

## Définition des types de champ XDM dans l’API

XDM schemas are defined using [JSON Schema](https://json-schema.org/) standards and basic field types, with additional constraints for field names which are enforced by [!DNL Experience Platform]. The [Schema Registry API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) allows you to define additional field types through the use of formats and optional constraints. XDM field types are exposed by the field-level attribute, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` est une valeur générée par le système, vous n’êtes donc pas obligé d’ajouter cette propriété au JSON de votre champ. Il est recommandé d’utiliser les types de schémas JSON (comme la chaîne et l’entier) avec les contraintes min/max appropriées définies dans le tableau ci-dessous.

Le tableau suivant souligne la mise en forme appropriée pour définir les types de champs scalaires et les types de champs plus spécifiques à l’aide de propriétés facultatives. Pour plus d’informations sur les propriétés facultatives et les mots-clés spécifiques au type, consultez la [documentation des schémas JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Pour commencer, recherchez le type de champ souhaité et utilisez l’exemple de code fourni pour générer votre demande d’API pour [créer un mixin](../api/create-mixin.md) ou [créer un type](../api/create-data-type.md)de données.

<table>
  <tr>
    <th>Type souhaité<br/>(meta:xdmType)</th>
    <th>JSON<br/>(schéma JSON)</th>
    <th>Exemple de code</th>
  </tr>
  <tr>
    <td>chaîne</td>
    <td>type : chaîne<br/><br/><strong>Propriétés facultatives :</strong><br/>
      <ul>
        <li>pattern</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
            "type": "string",
            "pattern": "^[A-Z]{2}$",
            "maxLength": 2
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>type : chaîne<br/>format : uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "format": "uri"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType: string)</td>
    <td>type : chaîne<br/><br/><strong>Propriété facultative :</strong><br/>
      <ul>
        <li>par défaut</li>
      </ul>
    </td>
    <td>Précisez les étiquettes d’option côté client à l’aide de « meta:enum » :
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
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>nombre</td>
    <td>type : nombre<br/>minimum : ±2,23×10^308<br/>maximum : ±1,80×10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "number"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>long</td>
    <td>type : entier<br/>maximum : 2^53+1<br>minimum : -2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimum": -9007199254740992,
          "maximum": 9007199254740992
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>type : entier<br/>maximum : 2^31<br>minimum : -2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimum": -2147483648,
          "maximum": 2147483648
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>court</td>
    <td>type : entier<br/>maximum : 2^15<br>minimum : -2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimum": -32768,
          "maximum": 32768
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>octet</td>
    <td>type : entier<br/>maximum : 2^7<br>minimum : -2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "entier",
          "minimum": -128,
          "maximum": 128
          }
      </pre>
    </td>
  </tr>
  <tr>
    <td>booléen</td>
    <td><br/>type : booléen<br/>{true, false}<br/><br/><strong>Propriété facultative :</strong><br/>
      <ul>
        <li>par défaut</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "boolean",
          "default": false
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>date</td>
    <td>type : chaîne<br/>format : date</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "format": "date",
          "examples": ["2004-10-23"]
        }
      </pre>
      Date définie par le <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, section 5.6</a>, où "full-date" = date-fullyear "-" date-month "-" date-mday (YYYY-MM-DD)
    </td>
  </tr>
  <tr>
    <td>date-time</td>
    <td>type : chaîne<br/>format : date-time</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "format": "date-time",
          "examples": ["2004-10-23T12:00:00-06:00"]
        }
      </pre>
      Date-Time définie par le <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, section 5.6</a>, où "date-time" = full-date "T" full-time:<br/>(YYYY-MM-DD'T'HH:MM:SS.SSSSX)
    </td>
  </tr>
  <tr>
    <td>tableau</td>
    <td>type : tableau</td>
    <td>Vous pouvez définir les items.type en utilisant n’importe quel type scalaire :
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      </pre>
      Tableau d’objets défini par un autre schéma :<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "array",
          "items": {
            "$ref": "id"
          }
        }
      </pre>
      où « id » désigne l’{id} du schéma de référence.
    </td>
  </tr>
  <tr>
    <td>objet</td>
    <td>type : propriétés</td>
    <td>d’objets.{field}.type en utilisant n’importe quel type scalaire :
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
        }
      </pre>
      Le champ de type « objet » défini par un schéma de référence :
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "$ref": "id"
        }
      </pre>
      où « id » désigne l’{id} du schéma de référence.
    </td>
  </tr>
  <tr>
    <td>map</td>
    <td>type : objet<br/><br/><strong>Remarque :</strong><br/>l’utilisation du type de données « map » est réservée à une utilisation par des schémas du secteur et des fournisseurs et n’est pas disponible à l’utilisation pour des champs définis par des clients. Ce type de données est utilisé dans des schémas standards lorsque les données sont représentées sous la forme de clés qui correspondent à certaines valeurs ou lorsque les clés ne peuvent pas raisonnablement être incluses dans un schéma statique et doivent être traitées comme valeur de données.</td>
    <td>Une « map » NE DOIT PAS définir de propriétés. Il DOIT définir un seul schéma "[!UICONTROL additionalProperties]" pour décrire le type de valeurs contenues dans la 'map'. Dans XDM, une « map » ne peut contenir qu’un seul type de données. Les valeurs peuvent être tout type de définitions de schéma XDM, y compris un tableau ou un objet, ou sous la forme d’une référence à un autre schéma (via $ref).<br/><br/>Faire correspond le champ avec des valeurs de type « champ » :
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "additionalProperties":{
            "type": "string"
          }
        }
      </pre>
    Faire correspondre le champ avec des valeurs sous la forme d’un tableau de chaînes :
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "additionalProperties":{
            "type": "array",
            "items": {
              "type": "string"
            }
          }
        }
      </pre>
    Faire correspondre un champ qui fait référence à un autre schéma :
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "additionalProperties":{
            "$ref": "id"
          }
        }
      </pre>
      où « id » désigne l’{id} du schéma de référence.
    </td>
  </tr>
</table>
