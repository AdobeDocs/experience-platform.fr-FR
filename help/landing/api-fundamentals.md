---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Principes fondamentaux des API d’Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: fa439ebb9d02d4a08c8ed92b18f2db819d089174
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 69%

---


# Principes fondamentaux des API d’Adobe Experience Platform

Adobe Experience Platform APIs employ several underlying technologies and syntaxes that are important to understand in order to effectively manage JSON-based [!DNL Platform] resources. Ce document apporte un aperçu rapide de ces technologies ainsi que des liens vers de la documentation externe pour vous apporter de plus amples informations.

## JSON Pointer {#json-pointer}

JSON Pointer est une syntaxe de chaîne normalisée ([RFC 6901](https://tools.ietf.org/html/rfc6901)) qui permet d’identifier des valeurs spécifiques dans des documents JSON. Un pointeur JSON est une chaîne de jetons séparés par des caractères `/` qui précisent soit les clés d’objet soit les index de tableau ainsi que les jetons pouvant être une chaîne ou un nombre. JSON Pointer strings are used in many PATCH operations for [!DNL Platform] APIs, as described later in this document. Pour plus d’informations sur JSON Pointer, reportez-vous à la [documentation de présentation de JSON Pointer](https://rapidjson.org/md_doc_pointer.html).

### Exemple d’objet de schéma JSON

```json
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Mixin.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "description": "The current loyalty program level to which the individual member belongs.",
                            "type": "string",
                            "enum": [
                                "platinum",
                                "gold",
                                "silver",
                                "bronze"
                            ],
                            "meta:enum": {
                                "platinum": "Platinum",
                                "gold": "Gold",
                                "silver": "Silver",
                                "bronze": "Bronze"
                            },
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    }
}
```

### Exemple de pointeurs JSON basés sur l’objet de schéma

| JSON Pointer | Est résolu sur |
|--- | ---|
| `"/title"` | &quot;Loyalty Member Details&quot; |
| `"/definitions/loyalty"` | (Renvoie le contenu de l’objet `loyalty`) |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

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