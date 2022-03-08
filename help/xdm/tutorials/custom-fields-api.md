---
title: Définition des champs XDM dans l’API Schema Registry
description: Découvrez comment définir différents champs lors de la création de ressources XDM (Experience Data Model) personnalisées dans l’API Schema Registry.
source-git-commit: af4c345819d3e293af4e888c9cabba6bd874583b
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 14%

---

# Définition des champs XDM dans l’API Schema Registry

Tous les champs de modèle de données d’expérience (XDM) sont définis à l’aide de la norme [Schéma JSON](https://json-schema.org/) contraintes qui s’appliquent à leur type de champ, avec des contraintes supplémentaires pour les noms de champ qui sont appliqués par Adobe Experience Platform. L’API Schema Registry vous permet de définir des champs personnalisés dans vos schémas à l’aide de formats et de contraintes facultatives. Les types de champ XDM sont exposés par l’attribut field-level, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` est une valeur générée par le système. Par conséquent, vous n’êtes pas obligé d’ajouter cette propriété au fichier JSON de votre champ lors de l’utilisation de l’API (sauf lorsque [création de types de mappage personnalisés](#maps)). La bonne pratique consiste à utiliser des types de schémas JSON (tels que `string` et `integer`) avec les contraintes min./max appropriées telles que définies dans le tableau ci-dessous.

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
    <td>Un champ de type map est essentiellement un champ de type objet avec un ensemble non limité de clés. Comme les objets, les cartes ont une <code>type</code> valeur de <code>object</code>, mais leur <code>meta:xdmType</code> est explicitement défini sur <code>map</code>.<br><br>Une carte <strong>must not</strong> définissez les propriétés. It <strong>must</strong> définir une seule <code>additionalProperties</code> schéma pour décrire le type de valeurs contenues dans le mappage (chaque mappage ne peut contenir qu’un seul type de données). Le <code>type</code> doit être définie sur <code>string</code> ou <code>integer</code>.<br/><br/>Un champ map avec des valeurs de type chaîne :
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "meta:xdmType" : "map", "additionalProperties":{ "type": "string" } }</pre>
    Consultez la section ci-dessous pour plus d’informations sur la création de types de mappage personnalisés dans XDM.
    </td>
  </tr>
</table>

## Création de types de mappage personnalisés {#maps}

Afin de prendre en charge efficacement les données &quot;de type carte&quot; dans XDM, les objets peuvent être annotés avec un `meta:xdmType` défini sur `map` pour indiquer clairement qu’un objet doit être géré comme si l’ensemble de clés n’était pas contraint. XDM impose les restrictions suivantes à l’utilisation de cet indice de stockage :

* Les types de carte DOIVENT être de type `object`
* Les types de carte NE DOIVENT PAS avoir de propriétés définies (en d’autres termes, ils définissent des objets &quot;vides&quot;)
* Les types de mappage DOIVENT inclure une seule `additionalProperties` schéma qui décrit les valeurs qui peuvent être placées dans le mappage

Assurez-vous que vous utilisez uniquement des champs de type map lorsque cela est absolument nécessaire, car ils présentent les inconvénients suivants en termes de performances :

* Le temps de réponse de Adobe Experience Platform Query Service passe de trois secondes à dix secondes pour 100 millions d’enregistrements.
* Les cartes doivent comporter moins de 16 clés, sinon elles risquent d’être détériorées.

L’interface utilisateur de Platform présente également des limites quant à la manière dont elle peut extraire les clés des champs de type map. Bien que les champs de type objet puissent être développés, les mappages s’affichent sous la forme d’un champ unique.

## Étapes suivantes

Ce guide explique comment définir différents types de champ dans l’API. Pour plus d’informations sur la mise en forme des types de champ XDM, consultez le guide sur [Contraintes de type de champ XDM](../schema/field-constraints.md).
