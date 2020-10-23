---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Principes fondamentaux des API d’Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: fac4b3d02a6e58a9d2c298f9b849fa7345e4fa93
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 59%

---


# Principes fondamentaux des API d’Adobe Experience Platform

Adobe Experience Platform APIs employ several underlying technologies and syntaxes that are important to understand in order to effectively manage JSON-based [!DNL Platform] resources. Ce document apporte un aperçu rapide de ces technologies ainsi que des liens vers de la documentation externe pour vous apporter de plus amples informations.

## JSON Pointer {#json-pointer}

JSON Pointer est une syntaxe de chaîne normalisée ([RFC 6901](https://tools.ietf.org/html/rfc6901)) qui permet d’identifier des valeurs spécifiques dans des documents JSON. Un pointeur JSON est une chaîne de jetons séparés par des caractères `/` qui précisent soit les clés d’objet soit les index de tableau ainsi que les jetons pouvant être une chaîne ou un nombre. JSON Pointer strings are used in many PATCH operations for [!DNL Platform] APIs, as described later in this document. Pour plus d’informations sur JSON Pointer, reportez-vous à la [documentation de présentation de JSON Pointer](https://rapidjson.org/md_doc_pointer.html).

### Exemple d’objet de schéma JSON

Le fichier JSON suivant représente un schéma XDM simplifié dont les champs peuvent être référencés à l’aide de chaînes de pointeur JSON. Notez que tous les champs qui ont été ajoutés à l’aide de mixins personnalisés ( `loyaltyLevel`par exemple) sont espacés de noms sous un `_{TENANT_ID}` objet, contrairement aux champs qui ont été ajoutés à l’aide de mixins principaux (par exemple `fullName`).

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:altId": "_{TENANT_ID}.schemas.85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Example schema",
  "type": "object",
  "description": "This is an example schema.",
  "properties": {
    "_{TENANT_ID}": {
      "type": "object",
      "properties": {
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "",
          "type": "string",
          "isRequired": false,
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ]
        }
      }
    },
    "person": {
      "title": "Person",
      "description": "An individual actor, contact, or owner.",
      "type": "object",
      "properties": {
        "name": {
          "title": "Full name",
          "description": "The person's full name.",
          "type": "object",
          "properties": {
            "fullName": {
              "title": "Full name",
              "type": "string",
              "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
            },
            "suffix": {
              "title": "Suffix",
              "type": "string",
              "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
          "meta:xdmField": "xdm:name"
        }
      }
    }
  }
}
```

### Exemple de pointeurs JSON basés sur l’objet de schéma

| JSON Pointer | Est résolu sur |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (Renvoie une référence au `fullName` champ, fournie par un mixin principal.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Renvoie une référence au `loyaltyLevel` champ, fournie par un mixin personnalisé.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>When dealing with the `xdm:sourceProperty` and `xdm:destinationProperty` attributes of [!DNL Experience Data Model] (XDM) descriptors, any `properties` keys must be **excluded** from the JSON Pointer string. See the [!DNL Schema Registry] API developer guide sub-guide on [descriptors](../xdm/api/descriptors.md) for more information.

## Correctif JSON

There are many PATCH operations for [!DNL Platform] APIs that accept JSON Patch objects for their request payloads. Le correctif JSON est un format standardisé ([RFC 6902](https://tools.ietf.org/html/rfc6902)) permettant de décrire les modifications apportées à un document JSON. Il vous permet de définir des mises à jour partielles vers JSON sans avoir besoin d’envoyer le document entier dans un corps de requête.

### Exemple d’un objet de correctif JSON

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op` : le type d’opération de correctif. While JSON Patch supports several different operation types, not all PATCH operations in [!DNL Platform] APIs are compatible with every operation type. Les types d’opérations disponibles sont :
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path` : la partie de la structure JSON mise à jour, identifiée grâce à la notation [JSON Pointer](#json-pointer).

En fonction du type d’opération indiqué dans `op`, l’objet du correctif JSON peut nécessiter des propriétés supplémentaires. Pour plus d’informations sur les différentes opérations de correctif JSON et leur syntaxe obligatoire, reportez-vous à la [documentation du correctif JSON](http://jsonpatch.com/).

## Schéma JSON

Le schéma JSON est un format utilisé pour décrire et valider la structure des données JSON. [Le modèle de données d’expérience (XDM)](../xdm/home.md) tire parti des fonctionnalités du schéma JSON pour imposer des contraintes sur la structure et le format des données d’expérience client ingérées. Pour plus d’informations sur le schéma JSON, consultez la [documentation officielle](https://json-schema.org/).

## Étapes suivantes

Ce document a présenté certaines des technologies et syntaxes impliquées dans la gestion des ressources basées sur JSON pour [!DNL Experience Platform]. For more information on working with [!DNL Platform] APIs, including best practices and answers to frequently asked questions, refer to the [Platform troubleshooting guide](troubleshooting.md).