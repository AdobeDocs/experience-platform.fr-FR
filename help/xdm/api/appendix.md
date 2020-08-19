---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Annexe de développement du registre des schémas
topic: developer guide
translation-type: tm+mt
source-git-commit: cb5df9b44486bda84f08805f1077d6097e3666e2
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 87%

---


# Annexe

This document provides supplemental information related to working with the [!DNL Schema Registry] API.

## Mode de compatibilité

[!DNL Experience Data Model] (XDM) est une spécification documentée publiquement, pilotée par l&#39;Adobe pour améliorer l&#39;interopérabilité, l&#39;expressivité et la puissance des expériences numériques. Adobe conserve le code source et les définitions formelles XDM dans un [projet open source sur GitHub](https://github.com/adobe/xdm/). Ces définitions sont écrites dans la notation standard XDM, et utilisent JSON-LD (JavaScript Object Notation for Linked Data) et le schéma JSON comme grammaire de définition des schémas XDM.

Lorsque vous examinez les définitions XDM formelles dans le référentiel public, vous pouvez voir que le XDM standard est différent de ce que vous voyez dans Adobe Experience Platform. What you are seeing in [!DNL Experience Platform] is called Compatibility Mode, and it provides a simple mapping between standard XDM and the way it is used within [!DNL Platform].

### Fonctionnement du mode de compatibilité

Le mode de compatibilité permet au modèle XDM JSON-LD de fonctionner avec une infrastructure de données existante en modifiant les valeurs du XDM standard tout en conservant la même sémantique. Il utilise une structure JSON imbriquée en affichant les schémas dans un format de type arbre.

La principale différence que vous noterez entre le XDM standard et le mode de compatibilité est la suppression du préfixe « xdm: » devant les noms des champs.

Le tableau ci-dessous contient une comparaison côte à côte affichant les champs associés à la date de naissance (dont les attributs « description » ont été supprimés) aux formats XDM standard et Mode de compatibilité. Notez que les champs Mode de compatibilité incluent une référence au champ XDM et à son type de données dans les attributs « meta:xdmField » et « meta:xdmType ».

<table>
  <th>XDM standard</th>
  <th>Mode de compatibilité</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "xdm:birthDate": {
              "title": "Birth Date",
              "type": "string",
              "format": "date",
          },
          "xdm:birthDayAndMonth": {
              "title": "Birth Date",
              "type": "string",
              "pattern": "[0-1][0-9]-[0-9][0-9]",
          },
          "xdm:birthYear": {
              "title": "Birth year",
              "type": "integer",
              "minimum": 1,
              "maximum": 32767
        }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "birthDate": {
              "title": "Birth Date",
              "type": "string",
              "format": "date",
              "meta:xdmField": "xdm:birthDate",
              "meta:xdmType": "date"
          },
          "birthDayAndMonth": {
              "title": "Birth Date",
              "type": "string",
              "pattern": "[0-1][0-9]-[0-9][0-9]",
              "meta:xdmField": "xdm:birthDayAndMonth",
              "meta:xdmType": "string"
          },
          "birthYear": {
              "title": "Birth year",
              "type": "integer",
              "minimum": 1,
              "maximum": 32767,
              "meta:xdmField": "xdm:birthYear",
              "meta:xdmType": "short"
        }
      </pre>
  </td>
  </tr>
</table>

### Pourquoi le mode de compatibilité est-il nécessaire ?

Adobe Experience Platform est conçu de manière à fonctionner avec plusieurs solutions et services possédant chacun leurs propres défis et limitations techniques (par exemple, la manière dont certaines technologies traitent les caractères spéciaux). Le mode de compatibilité a été développé dans le but de surpasser ces limites.

La plupart des [!DNL Experience Platform] services, y compris [!DNL Catalog]les services, [!DNL Data Lake]et [!DNL Real-time Customer Profile] , sont utilisés [!DNL Compatibility Mode] à la place de XDM standard. L’ [!DNL Schema Registry] API utilise également [!DNL Compatibility Mode]et les exemples de ce document s’affichent tous à l’aide [!DNL Compatibility Mode].

It is worthwhile to know that a mapping takes place between standard XDM and the way it is operationalized in [!DNL Experience Platform], but it should not affect your use of [!DNL Platform] services.

The open source project is available to you, but when it comes to interacting with resources through the [!DNL Schema Registry], the API examples in this document provide the best practices you should know and follow.

## Définition des types de champ XDM dans l’API {#field-types}

Les schémas XDM sont définis à l’aide des normes du schéma JSON et les types de champ de base avec des contraintes supplémentaires pour les noms de champ qui sont appliqués par [!DNL Experience Platform]. XDM vous permet de définir des types de champ supplémentaires par l’utilisation de formats et de contraintes facultatives. Les types de champ XDM sont exposés par l’attribut field-level, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` est une valeur générée par le système, vous n’êtes donc pas obligé d’ajouter cette propriété au JSON de votre champ. Il est recommandé d’utiliser les types de schémas JSON (comme la chaîne et l’entier) avec les contraintes min/max appropriées définies dans le tableau ci-dessous.

Le tableau suivant souligne la mise en forme appropriée pour définir les types de champs scalaires et les types de champs plus spécifiques à l’aide de propriétés facultatives. Pour plus d’informations sur les propriétés facultatives et les mots-clés spécifiques au type, consultez la [documentation des schémas JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Pour commencer, trouvez le type de champ souhaité et utilisez le code d’échantillon fourni pour créer votre requête API.

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


## Faire correspondre les types XDM à d’autres formats

Le tableau ci-dessous décrit le mappage entre « meta:xdmType » et d’autres formats de sérialisation.

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
