---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Principes de base de l’API d’Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: 2e5668a8b1d5fb831188fbd4e453b9f4aa7474df
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 3%

---


# Principes de base de l’API d’Adobe Experience Platform

Les API d’Adobe Experience Platform utilisent plusieurs technologies et syntaxes sous-jacentes qui sont importantes à comprendre pour gérer efficacement les [!DNL Platform] ressources JSON. Ce document présente un bref aperçu de ces technologies, ainsi que des liens vers la documentation externe pour plus d&#39;informations.

## Pointeur JSON {#json-pointer}

JSON Pointer est une syntaxe de chaîne standard ([RFC 6901](https://tools.ietf.org/html/rfc6901)) permettant d’identifier des valeurs spécifiques dans les documents JSON. Un pointeur JSON est une chaîne de jetons séparés par `/` des caractères qui spécifient des clés d’objet ou des index de tableau, et les jetons peuvent être une chaîne ou un nombre. Les chaînes de pointeur JSON sont utilisées dans de nombreuses opérations PATCH pour [!DNL Platform] les API, comme décrit plus loin dans ce document. Pour plus d’informations sur le pointeur JSON, reportez-vous à la documentation [d’aperçu du pointeur](https://rapidjson.org/md_doc_pointer.html)JSON.

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

### Exemple de pointeurs JSON basés sur un objet schéma

| Pointeur JSON | Résout à |
|--- | ---|
| `"/title"` | &quot;Détails du membre de fidélité&quot; |
| `"/definitions/loyalty"` | (Renvoie le contenu de l’ `loyalty` objet) |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!Note] :
>Lors de l’utilisation des `xdm:sourceProperty` attributs et `xdm:destinationProperty` des descripteurs [!DNL Experience Data Model] (XDM), toutes les `properties` clés doivent être **exclues** de la chaîne JSON Pointer. Pour plus d&#39;informations, consultez le sous-guide du développeur d&#39;API de registre de Schéma sur les [descripteurs](../xdm/api/descriptors.md) .

## Correctif JSON

Il existe de nombreuses opérations PATCH pour [!DNL Platform] les API qui acceptent les objets de correctif JSON pour leurs charges utiles de demande. Le correctif JSON est un format normalisé ([RFC 6902](https://tools.ietf.org/html/rfc6902)) qui décrit les modifications apportées à un document JSON. Il vous permet de définir des mises à jour partielles de JSON sans avoir à envoyer l’ensemble du document dans un corps de requête.

### Exemple d’objet Patch JSON

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Type d&#39;opération de correctif. Bien que le correctif JSON prenne en charge plusieurs types d’opérations différents, toutes les opérations PATCH dans [!DNL Platform] les API ne sont pas compatibles avec chaque type d’opération. Les types d&#39;opération disponibles sont les suivants :
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: Partie de la structure JSON à mettre à jour, identifiée à l’aide de la notation Pointeur [](#json-pointer) JSON.

Selon le type d’opération indiqué dans `op`, l’objet Patch JSON peut nécessiter des propriétés supplémentaires. Pour plus d’informations sur les différentes opérations de correctif JSON et leur syntaxe requise, consultez la documentation [sur le correctif](http://jsonpatch.com/)JSON.

## Schéma JSON

Le Schéma JSON est un format utilisé pour décrire et valider la structure des données JSON. [Le modèle de données d’expérience (XDM)](../xdm/home.md) utilise les capacités de Schéma JSON pour imposer des contraintes sur la structure et le format des données d’expérience client imbriquées. Pour plus d&#39;informations sur le Schéma JSON, veuillez consulter la documentation [](https://json-schema.org/)officielle.

## Étapes suivantes

Ce document a introduit certaines des technologies et syntaxes impliquées dans la gestion des ressources JSON pour [!DNL Experience Platform]. Pour plus d’informations sur l’utilisation des [!DNL Platform] API, y compris les meilleures pratiques et les réponses aux questions fréquentes, consultez le guide [de dépannage de](troubleshooting.md)Platform.