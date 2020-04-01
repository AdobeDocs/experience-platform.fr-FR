---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Annexe du développeur du registre des '
topic: developer guide
translation-type: tm+mt
source-git-commit: f7c87cc86bfc5017ec5c712d05e39be5c14a7147

---


# Annexe

Ce fournit des informations supplémentaires relatives à l’utilisation de l’API de registre .

## Mode de compatibilité

Le modèle de données d’expérience (XDM) est une spécification publiquement documentée, conçue par Adobe pour améliorer l’interopérabilité, l’expressivité et la puissance des expériences numériques. Adobe conserve le code source et les définitions XDM formelles dans un projet [open source sur GitHub](https://github.com/adobe/xdm/). Ces définitions sont écrites dans la notation standard XDM, en utilisant JSON-LD (JavaScript Object Notation for Linked Data) et le  JSON comme grammaire pour la définition du XDM.

Lorsque vous examinez les définitions XDM formelles dans le référentiel public, vous constatez que le modèle XDM standard diffère de ce que vous voyez dans Adobe Experience Platform. Ce que vous voyez dans la plate-forme d’expérience s’appelle le mode de compatibilité, et il fournit un mappage simple entre XDM standard et la manière dont il est utilisé dans la plate-forme.

### Mode de compatibilité

Le mode de compatibilité permet au modèle JSON-LD XDM de fonctionner avec l’infrastructure de données existante en modifiant les valeurs dans XDM standard tout en conservant la même sémantique. Il utilise une structure JSON imbriquée, affichant des  de dans un format arborescent.

La principale différence que vous remarquerez entre XDM standard et le mode de compatibilité est la suppression du préfixe &quot;xdm:&quot; pour les noms de champ.

Voici une comparaison côte à côte montrant les champs liés à l’anniversaire (avec suppression des attributs &quot;description&quot;) dans le XDM standard et le mode de compatibilité. Les champs Mode de compatibilité contiennent une référence au champ XDM et à son type de données dans les attributs meta:xdmField et meta:xdmType.

<table>
  <th>XDM standard</th>
  <th>Mode de compatibilité</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        { "xdm:bornDate" : { "title" : "Date de naissance", "type" : "string", "format" : "date", }, "xdm:bornDayAndMonth" : { "title" : "Date de naissance", "type" : "string", "pattern" : "[0-1][0-9]-[0-9][0-9]", }, "xdm:bornYear" : { "title" : "Année de naissance", "type" : "integer", "minimum" : 1, "maximum" : 32767 }
      </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        { "bornDate" : { "title" : "Date de naissance", "type" : "string", "format" : "date", "meta:xdmField" : "xdm:bornDate", "meta:xdmType" : "date" }, "bornDayAndMonth" : { "title" : "Date de naissance", "type" : "string", "pattern" : "[0-1][0-9]-[0-9][0-9]", "meta:xdmField" : "xdm:bornDayAndMonth", "meta:xdmType" : "string" }, "bornYear" : { "title" : "Année de naissance", "type" : "integer", "minimum" : 1, "maximum" : 32767, "meta:xdmField" : "xdm:bornYear", "meta:xdmType" : "short" }
      </pre>
  </td>
  </tr>
</table>

### Pourquoi le mode de compatibilité est-il nécessaire ?

Adobe Experience Platform est conçu pour fonctionner avec plusieurs solutions et services, chacun avec ses propres défis techniques et ses propres limites (par exemple, la manière dont certaines technologies gèrent des caractères spéciaux). Afin de surmonter ces limitations, le mode de compatibilité a été développé.

La plupart des services Experience Platform, y compris les Catalog, Data Lake et Real-time Customer  utilisent le mode de compatibilité plutôt que le mode XDM standard. L&#39;API de Registre  utilise également le mode de compatibilité, et les exemples de ce  sont tous affichés en mode de compatibilité.

Il est intéressant de savoir qu’un mappage a lieu entre XDM standard et la manière dont il est opérationnel dans Experience Platform, mais il ne devrait pas affecter votre utilisation des services de Platform.

Le projet open source est à votre disposition, mais lorsqu&#39;il s&#39;agit d&#39;interagir avec des ressources via le Registre des , les exemples d&#39;API de ce  fournissent les meilleures pratiques que vous devez connaître et suivre.

## Définition des types de champs XDM dans l’API {#field-types}

Les  XDM sont définies à l’aide des normes JSON et des types de champs de base, avec des contraintes supplémentaires pour les noms de champs appliqués par Experience Platform. XDM vous permet de définir des types de champs supplémentaires à l’aide de formats et de contraintes facultatives. Les types de champs XDM sont exposés par l’attribut field-level `meta:xdmType`.

>[!NOTE] `meta:xdmType` est une valeur générée par le système. Par conséquent, vous n’êtes pas tenu d’ajouter cette propriété au fichier JSON pour votre champ. Il est recommandé d’utiliser les types de  JSON (chaînes et entiers, par exemple) avec les contraintes min/max appropriées, telles que définies dans le tableau ci-dessous.

Le tableau suivant décrit la mise en forme appropriée pour définir les types de champs scalaires et les types de champs plus spécifiques à l’aide de propriétés facultatives. Pour plus d’informations sur les propriétés facultatives et les mots-clés spécifiques au type, consultez la documentation [JSON](https://json-schema.org/understanding-json-schema/reference/type.html).

Pour commencer, recherchez le type de champ souhaité et utilisez l’exemple de code fourni pour créer votre requête d’API.

<table>
  <tr>
    <th>Type<br/>souhaité(meta:xdmType)</th>
    <th>JSON<br/>( JSON)</th>
    <th>Exemple de code</th>
  </tr>
  <tr>
    <td>chaîne</td>
    <td>type : Propriétés<br/><br/><strong>stringOptional :</strong><br/>
      <ul>
        <li>motif</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "string", "pattern" : "^[A-Z]{2}$", "maxLength" : 2 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>type : format<br/>de chaîne : uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "string", "format" : "uri" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType: string)</td>
    <td>type : Propriété<br/><br/><strong>stringOptional :</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>Spécifiez les libellés des options destinées aux clients à l’aide de "meta:enum" :
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "string", "enum" : [ "value1", "value2", "value3" ], "meta:enum" : { "value1" : "Value 1", "value2" : "Value 2", "value3" : "Value 3" }, "default" : "value1" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>nombre</td>
    <td>type :<br/>nombre minimal : ±2,23 × 10^308<br/>maximum : ±1,80 × 10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "number" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>long</td>
    <td>type :<br/>entier maximum : 2^53+1<br>minimum :-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "integer", "minimum" : -9007199254740992, "maximum": 9007199254740992 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>type :<br/>entier maximum:2^31<br>minimum:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "integer", "minimum" : -2147483648, "maximum" : 2147483648 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>short</td>
    <td>type :<br/>entier maximum:2^15<br>minimum:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "integer", "minimum" : -32768, "maximum" : 32768 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>byte</td>
    <td>type :<br/>entier maximum:2^7<br>minimum:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "integer", "minimum" : -128, "maximum" : 128 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>booléen</td>
    <td><br/>type : boolean<br/>{true, false}Propriété<br/><br/><strong>facultative :</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "boolean", "default" : false }
      </pre>
    </td>
  </tr>
  <tr>
    <td>date</td>
    <td>type : format<br/>de chaîne : date</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "string", "format" : "date", "exemples" : ["2004-10-23"] }
      </pre>
      Date définie par la <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, section 5.6</a>, où "date complète" = date-année complète "-" date-mois "-" date-mday (AAAA-MM-JJ)
    </td>
  </tr>
  <tr>
    <td>date-heure</td>
    <td>type : format<br/>de chaîne : date-heure</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "string", "format" : "date-heure", "exemples" : ["2004-10-23T12:00:00-06:00"] }
      </pre>
      Date-Heure, telle que définie par la <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, section 5.6</a>, où "date-Heure" = date-Heure complète "T" à temps plein:<br/>(AAAA-MM-JJ'T'HH:MM:SS.SSSSX)
    </td>
  </tr>
  <tr>
    <td>tableau</td>
    <td>type : tableau</td>
    <td>items.type peut être défini à l’aide de n’importe quel type scalaire :
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "array", "items" : { "type" : "string" } }
      </pre>
      Tableau d’objets défini par un autre  :<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "array", "items" : { "$ref" : "id" } }
      </pre>
      Où "id" est le {id} du  de référence.
    </td>
  </tr>
  <tr>
    <td>objet</td>
    <td>type : objet</td>
    <td>du média.{field}.type peut être défini à l’aide de n’importe quel type scalaire :
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "object", "properties" : { "field1" : { "type" : "string" }, "field2" : { "type" : "number" } } }
      </pre>
      Champ de type "object" défini par un de référence  :
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "object", "$ref" : "id" }
      </pre>
      Où "id" est le {id} du  de référence.
    </td>
  </tr>
  <tr>
    <td>map</td>
    <td>type :<br/><br/><strong>objectNote:L'</strong><br/>utilisation du type de données "map" est réservée à l'utilisation des  par le secteur industriel et le fournisseur et n'est pas disponible pour l'utilisation dans les champs définis par le client. Elle est utilisée dans les  standard lorsque les données sont représentées sous la forme de clés qui correspondent à une valeur ou lorsque les clés ne peuvent pas raisonnablement être incluses dans un statique et doivent être traitées comme des valeurs de données.</td>
    <td>Une carte NE DOIT PAS définir de propriétés. Il DOIT définir un seul "additionalProperties" pour décrire le type de valeurs contenues dans la "map". Un "map" dans XDM ne peut contenir qu’un seul type de données. Les valeurs peuvent être n’importe quelle définition de XDM valide, y compris un tableau ou un objet, ou comme référence à un autre  de (via $ref).<br/><br/>Champ de correspondance avec des valeurs de type "string" :
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "object", "additionalProperties":{ "type": "string" } }
      </pre>
    Champ de correspondance dont les valeurs sont un tableau de chaînes :
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "object", "additionalProperties":{ "type": "array", "items" : { "type" : "string" } } }
      </pre>
    Champ de mappage qui référence un autre  de :
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "object", "additionalProperties" :{ "$ref" : "id" } }
      </pre>
      Où "id" est le {id} du  de référence.
    </td>
  </tr>
</table>


## Mappage de types XDM avec d’autres formats

Le tableau ci-dessous décrit le mappage entre &quot;meta:xdmType&quot; et d’autres formats de sérialisation.

| Type<br>XDM (meta:xdmType) | JSON<br>( JSON) | Parquet<br>(type/annotation) | Spark SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aérospike | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| chaîne | type:string | BYTE_ARRAY/UTF8 | StringType | java.lang.String | Chaîne | System.String | Chaîne | chaîne | Chaîne | chaîne |
| nombre | type:number | DOUBLE | DoubleType | java.lang. | Double | System. | Nombre | double | Double | double |
| long | type:<br>entier maximum:2^53+1<br>minimum:-2^53+1 | INT64 | LongType | java.lang.Long | Long | System.Int64 | Nombre | long | Entier | int64 |
| int | type:<br>entier maximum:2^31<br>minimum:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Nombre | int | Entier | int32 |
| short | type:<br>entier maximum:2^15<br>minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Court | System.Int16 | Nombre | int | Entier | int32 |
| byte | type:<br>entier maximum:2^7<br>minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Octet | System.SByte | Nombre | int | Entier | int32 |
| booléen | type:boolean | BOOLÉEN | BooleanType | java.lang.Boolean | Booléen | System.Boolean | Booléen | bool | Entier | Entier | bool |
| date | type:<br>chaîne:date<br>(RFC 3339, section 5.6) | INT32/DATE | DateType | java.util.Date | java.util.Date | System.DateTime | Chaîne | date | Entier<br>(unix millis) | int64<br>(unix millis) |
| date-heure | type:<br>chaîne:date-time<br>(RFC 3339, section 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | Chaîne | timestamp | Entier<br>(unix millis) | int64<br>(unix millis) |
| map | objet | MAP annotated group<br><br>&lt;<span>key_type</span>> DOIT être de type STRING<br><br>&lt;<span>value_type</span>> type de valeurs de mappage | MapType<br><br>&quot;keyType&quot; DOIT être StringType<br><br>&quot;valueType&quot; est un type de valeurs de mappage. | java.util.Map | Carte | --- | objet | objet | map | map&lt;<span>key_type, value_type</span>> |
