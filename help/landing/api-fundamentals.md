---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Principes de base de l’API d’Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: c94f065a5d56ac495dd2d541531aaec94c187612

---


# Principes de base de l’API d’Adobe Experience Platform

Les API d’Adobe Experience Platform utilisent plusieurs technologies et syntaxes sous-jacentes qui sont importantes à comprendre pour gérer efficacement les ressources de plateformes JSON. Ce donne un bref aperçu de ces technologies, ainsi que des liens vers la documentation externe pour plus d’informations.

## Pointeur JSON {#json-pointer}

JSON Pointer est une syntaxe de chaîne standard ([RFC 6901](https://tools.ietf.org/html/rfc6901)) permettant d’identifier des valeurs spécifiques dans le  JSON. Un pointeur JSON est une chaîne de jetons séparés par `/` des caractères, qui spécifient des clés d’objet ou des index de tableau, et les jetons peuvent être une chaîne ou un nombre. Les chaînes de pointeur JSON sont utilisées dans de nombreuses opérations PATCH pour les API de plateforme, comme décrit plus loin dans cette  de. Pour plus d’informations sur le pointeur JSON, reportez-vous à la documentation [d’aperçu du pointeur](https://rapidjson.org/md_doc_pointer.html)JSON.

### Exemple d’objet  JSON

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

### Exemple de pointeurs JSON en fonction d’un objet 

| Pointeur JSON | Résout à |
|--- | ---|
| `"/title"` | &quot;Détails du membre de fidélité&quot; |
| `"/definitions/loyalty"` | (Renvoie le contenu de l’ `loyalty` objet) |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!Note] :
>Lorsque vous traitez des attributs `xdm:sourceProperty` et `xdm:destinationProperty` des descripteurs de modèle de données d’expérience (XDM), toutes les `properties` clés doivent être **exclues** de la chaîne de pointeur JSON. Pour plus d&#39;informations, reportez-vous au sous-guide du développeur d&#39;API de Registre  sur les [descripteurs](../xdm/api/descriptors.md) .

## Correctif JSON

Il existe de nombreuses opérations PATCH pour les API de plateforme qui acceptent les objets de correctif JSON pour leurs charges de requête. Le correctif JSON est un format normalisé ([RFC 6902](https://tools.ietf.org/html/rfc6902)) pour décrire les modifications apportées à un  JSON. Il vous permet de définir des mises à jour partielles de JSON sans avoir à envoyer l’ensemble du dans un corps de requête.

### Exemple d’objet de correctif JSON

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Type d’opération de correctif. Bien que le correctif JSON prenne en charge plusieurs types d’opérations différents, toutes les opérations PATCH dans les API de plateforme ne sont pas compatibles avec chaque type d’opération. Les types d’opération disponibles sont les suivants :
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: Partie de la structure JSON à mettre à jour, identifiée à l’aide de la notation Pointeur [](#json-pointer) JSON.

Selon le type d’opération indiqué dans `op`, l’objet JSON Patch peut nécessiter des propriétés supplémentaires. Pour plus d’informations sur les différentes opérations de correctif JSON et leur syntaxe requise, reportez-vous à la documentation [du correctif](http://jsonpatch.com/)JSON.

##  JSON

Le  JSON est un format utilisé pour décrire et valider la structure des données JSON. [Le modèle de données d’expérience (XDM)](../xdm/home.md) tire parti des  JSON pour imposer des contraintes sur la structure et le format des données d’expérience client assimilées. Pour plus d&#39;informations sur le  JSON, veuillez consulter la documentation [officielle](https://json-schema.org/).

## Étapes suivantes

Ce présente certaines des technologies et des syntaxes impliquées dans la gestion des ressources JSON pour Experience Platform. Pour plus d’informations sur l’utilisation des API de plateforme, y compris les meilleures pratiques et les réponses aux questions fréquentes, consultez le guide [de dépannage de](troubleshooting.md)plateforme.