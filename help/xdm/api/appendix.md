---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Annexe destinée aux développeurs du registre des Schémas
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 6%

---


# Annexe

Ce document fournit des informations supplémentaires sur l&#39;utilisation de l&#39;API de registre de Schémas.

## Mode de compatibilité

Le modèle de données d’expérience (XDM) est une spécification publiquement documentée, pilotée par Adobe pour améliorer l’interopérabilité, l’expressivité et la puissance des expériences numériques. Adobe conserve le code source et les définitions XDM formelles dans un projet [open source sur GitHub](https://github.com/adobe/xdm/). Ces définitions sont écrites en Notation standard XDM, en utilisant JSON-LD (Notation d’objet JavaScript pour les données liées) et le Schéma JSON comme grammaire pour la définition de schémas XDM.

Lorsque vous consultez des définitions XDM formelles dans le référentiel public, vous pouvez constater que XDM standard diffère de ce que vous voyez dans l&#39;Adobe Experience Platform. Ce que vous voyez en Experience Platform s&#39;appelle le Mode de compatibilité, et il fournit une mise en correspondance simple entre le XDM standard et la façon dont il est utilisé dans Platform.

### Fonctionnement du mode de compatibilité

Le mode de compatibilité permet au modèle JSON-LD XDM de fonctionner avec l’infrastructure de données existante en modifiant les valeurs dans XDM standard tout en conservant la sémantique la même. Il utilise une structure JSON imbriquée, affichant les schémas sous forme d’arborescence.

La principale différence que vous remarquerez entre XDM standard et le mode de compatibilité est la suppression du préfixe &quot;xdm:&quot; pour les noms de champs.

Vous trouverez ci-dessous une comparaison côte à côte montrant les champs liés à l’anniversaire (avec la suppression des attributs &quot;description&quot;) en mode XDM standard et en mode de compatibilité. Notez que les champs Mode de compatibilité incluent une référence au champ XDM et à son type de données dans les attributs &quot;meta:xdmField&quot; et &quot;meta:xdmType&quot;.

<table>
  <th>XDM standard</th>
  <th>Mode de compatibilité</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        { "xdm:bornDate": { "title" : "Date de naissance", "type" : "string", "format" : "date", }, "xdm:bornDayAndMonth" : { "title" : "Date de naissance", "type" : "string", "pattern" : "[0-1][0-9]-[0-9][0-9]", }, "xdm:bornYear" : { "title" : "Année de naissance", "type" : "integer", "minimum" : 1, "maximum" : 32767 }
      </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        { "bornDate" : { "title" : "Date de naissance", "type" : "string", "format" : "date", "meta:xdmField" : "xdm:bornDate", "meta:xdmType" : "date" }, "bornDayAndMonth": { "title" : "Date de naissance", "type" : "string", "pattern" : "[0-1][0-9]-[0-9][0-9]", "meta:xdmField" : "xdm:bornDayAndMonth", "meta:xdmType" : "string" }, "bornYear" : { "title" : "Année de naissance", "type" : "integer", "minimum" : 1, "maximum" : 32767, "meta:xdmField" : "xdm:bornYear", "meta:xdmType" : "short" }
      </pre>
  </td>
  </tr>
</table>

### Pourquoi le mode de compatibilité est-il nécessaire ?

L&#39;Adobe Experience Platform est conçu pour fonctionner avec plusieurs solutions et services, chacun avec ses propres défis techniques et limites (par exemple, comment certaines technologies gèrent des caractères spéciaux). Afin de surmonter ces limitations, le mode de compatibilité a été développé.

La plupart des services Experience Platform, y compris Catalog, Data Lake et le Profil client en temps réel, utilisent le mode de compatibilité plutôt que le mode XDM standard. L&#39;API Schéma Registry utilise également le mode de compatibilité, et les exemples de ce document sont tous affichés à l&#39;aide du mode de compatibilité.

Il est intéressant de savoir qu&#39;un mappage a lieu entre XDM standard et la façon dont il est mis en oeuvre en Experience Platform, mais il ne devrait pas affecter votre utilisation des services Platform.

Le projet open source est à votre disposition, mais lorsqu&#39;il s&#39;agit d&#39;interagir avec des ressources via le Registre des Schémas, les exemples d&#39;API de ce document fournissent les meilleures pratiques que vous devez connaître et suivre.

## Définition des types de champs XDM dans l&#39;API {#field-types}

Les schémas XDM sont définis à l’aide des normes de Schéma JSON et des types de champs de base, avec des contraintes supplémentaires pour les noms de champs appliqués par l’Experience Platform. XDM vous permet de définir d&#39;autres types de champs en utilisant des formats et des contraintes facultatives. Les types de champ XDM sont exposés par l&#39;attribut de niveau champ `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` est une valeur générée par le système. Par conséquent, vous n’êtes pas tenu d’ajouter cette propriété au fichier JSON pour votre champ. Il est recommandé d’utiliser des types de Schéma JSON (chaînes et entiers, par exemple) avec les contraintes min/max appropriées, telles que définies dans le tableau ci-dessous.

Le tableau suivant décrit la mise en forme appropriée pour définir des types de champs scalaires et des types de champs plus spécifiques à l’aide de propriétés facultatives. Pour plus d’informations sur les propriétés facultatives et les mots-clés spécifiques au type, consultez la documentation [du Schéma](https://json-schema.org/understanding-json-schema/reference/type.html)JSON.

Pour commencer, recherchez le type de champ souhaité et utilisez l’exemple de code fourni pour générer votre requête d’API.

<table>
  <tr>
    <th>Type<br/>souhaité (meta:xdmType)</th>
    <th>JSON<br/>(Schéma JSON)</th>
    <th>Exemple de code</th>
  </tr>
  <tr>
    <td>chaîne</td>
    <td>type : Propriétés<br/><br/><strong>stringOptional :</strong><br/>
      <ul>
        <li>pattern</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "string", "pattern" : "^[A-Z]{2}$", "maxLength": 2 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>type : Format<br/>de chaîne : uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "string", "format" : "uri" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType: string)</td>
    <td>type :<br/><br/><strong>stringOptional, propriété :</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>Spécifiez des libellés d’option destinés aux clients à l’aide de "meta:enum" :
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "string", "enum" : [ "value1", "value2", "value3" ], "meta:enum" : { "value1": "Value 1", "value2" : "Value 2", "value3" : "Value 3" }, "default": "value1" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>nombre</td>
    <td>type :<br/>nombre minimum : ±2,23 × 10^308<br/>maximum : ±1,80 × 10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "number" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>long</td>
    <td>type :<br/>nombre maximal : 2^53+1<br>minimum : -2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "integer", "minimum" : -9007199254740992, "maximum" : 9007199254740992 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>type :<br/>maximal : 2^31<br>minimum : -2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "integer", "minimum" : -2147483648, "maximum" : 2147483648 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>short</td>
    <td>type :<br/>nombre maximal : 2^15<br>minimum : -2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "integer", "minimum" : -32768, "maximum" : 32768 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>byte</td>
    <td>type :<br/>nombre maximal : 2^7<br>minimum : -2^7</td>
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
    <td>type : Format<br/>de chaîne : date</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "string", "format" : "date", "exemples" : ["2004-10-23"] }
      </pre>
      Date définie par la <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, section 5.6</a>, où "date complète" = date-année complète "-" date-mois "-" date-mday (AAAA-MM-JJ)
    </td>
  </tr>
  <tr>
    <td>date-heure</td>
    <td>type : Format<br/>de chaîne : date-heure</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "string", "format" : "date-heure", "exemples" : ["2004-10-23T12:00:00-06:00"] }
      </pre>
      Date-Heure telle que définie par la <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, section 5.6</a>, où "date-time" = "T" à temps plein à date complète:<br/>(AAAA-MM-JJ'T'HH:MM:SS.SSSSX)
    </td>
  </tr>
  <tr>
    <td>tableau</td>
    <td>type : tableau</td>
    <td>items.type peut être défini à l’aide de n’importe quel type scalaire :
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "array", "items" : { "type" : "string" } }
      </pre>
      Tableau d'objets définis par un autre schéma :<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "array", "items" : { "$ref": "id" } }
      </pre>
      Où "id" correspond à {id} du schéma de référence.
    </td>
  </tr>
  <tr>
    <td>objet</td>
    <td>type : objet</td>
    <td>du média.{field}.type peut être défini à l'aide de n'importe quel type scalaire :
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "object", "properties" : { "field1" : { "type" : "string" }, "field2" : { "type" : "number" } } }
      </pre>
      Champ de type "objet" défini par un schéma de référence :
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "object", "$ref" : "id" }
      </pre>
      Où "id" correspond à {id} du schéma de référence.
    </td>
  </tr>
  <tr>
    <td>map</td>
    <td>type :<br/><br/><strong>objectNote :</strong><br/>L'utilisation du type de données "map" est réservée à l'utilisation du schéma du secteur industriel et du fournisseur et n'est pas disponible pour l'utilisation dans les champs définis par le client. Elle est utilisée dans les schémas standard lorsque les données sont représentées sous la forme de clés qui correspondent à une valeur ou lorsque les clés ne peuvent pas raisonnablement être incluses dans un schéma statique et doivent être traitées comme des valeurs de données.</td>
    <td>Un 'map' NE DOIT PAS définir de propriétés. Il DOIT définir un schéma "additionalProperties" unique pour décrire le type de valeurs contenues dans la "map". Un "mappage" dans XDM ne peut contenir qu'un seul type de données. Les valeurs peuvent être n'importe quelle définition de schéma XDM valide, y compris un tableau ou un objet, ou comme référence à un autre schéma (via $ref).<br/><br/>Champ de correspondance avec des valeurs de type "string" :
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "object", "additionalProperties":{ "type": "string" } }
      </pre>
    Mapper un champ dont les valeurs sont un tableau de chaînes :
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "object", "additionalProperties":{ "type": "array", "items" : { "type" : "string" } } }
      </pre>
    Champ de mappage qui référence un autre schéma :
      <pre class="JSON language-JSON hljs">
        "sampleField" : { "type" : "object", "additionalProperties":{ "$ref": "id" } }
      </pre>
      Où "id" correspond à {id} du schéma de référence.
    </td>
  </tr>
</table>


## Mappage de types XDM à d’autres formats

Le tableau ci-dessous décrit le mappage entre &quot;meta:xdmType&quot; et d’autres formats de sérialisation.

| Type<br>XDM (meta:xdmType) | JSON<br>(Schéma JSON) | Parquet<br>(type/annotation) | Spark SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aérospike | Protocole 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| chaîne | type:string | BYTE_ARRAY/UTF8 | StringType | java.lang.String | Chaîne | System.String | Chaîne | chaîne | Chaîne | chaîne |
| nombre | type:number | DOUBLE | DoubleType | java.lang.Double | Double | System.Double | Nombre | double | Double | double |
| long | type:<br>integermaximum:2^53+1<br>minimum:-2^53+1 | INT64 | LongType | java.lang.Long | Long | System.Int64 | Nombre | long | Entier | int64 |
| int | type:<br>integermaximum:2^31<br>minimum:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Nombre | int | Entier | int32 |
| short | type:<br>integermaximum:2^15<br>minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Court | System.Int16 | Nombre | int | Entier | int32 |
| byte | type:<br>integermaximum:2^7<br>minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Octet | System.SByte | Nombre | int | Entier | int32 |
| booléen | type:boolean | BOOLÉEN | BooleanType | java.lang.Boolean | Booléen | System.Boolean | Booléen | bool | Entier | Entier | bool |
| date | type:format<br>de chaîne:date<br>(RFC 3339, section 5.6) | INT32/DATE | DateType | java.util.Date | java.util.Date | System.DateTime | Chaîne | date | Entier<br>(unix millis) | int64<br>(unix millis) |
| date-heure | type:format<br>de chaîne:date-time<br>(RFC 3339, section 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | Chaîne | timestamp | Entier<br>(unix millis) | int64<br>(unix millis) |
| map | objet | MAP groupe<br><br>annoté &lt;<span>key_type</span>> DOIT être de type STRING<br><br>&lt;<span>value_type</span>> type de valeurs de mappage | MapType<br><br>&quot;keyType&quot; DOIT être StringType<br><br>&quot;valueType&quot; est un type de valeurs de mappage. | java.util.Map | Carte | --- | objet | objet | map | map&lt;<span>key_type, value_type</span>> |
