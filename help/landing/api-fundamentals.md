---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Principes fondamentaux des API d’Experience Platform
description: Ce document présente brièvement certaines des technologies et syntaxes sous-jacentes impliquées dans les API d’Experience Platform.
role: Developer
feature: API
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 50%

---

# Principes fondamentaux des API d’Experience Platform

Les API Adobe Experience Platform utilisent plusieurs technologies et syntaxes sous-jacentes importantes à comprendre pour gérer efficacement les ressources [!DNL Experience Platform] basées sur JSON. Ce document apporte un aperçu rapide de ces technologies ainsi que des liens vers de la documentation externe pour vous apporter de plus amples informations.

## JSON Pointer {#json-pointer}

JSON Pointer est une syntaxe de chaîne normalisée ([RFC 6901](https://tools.ietf.org/html/rfc6901)) qui permet d’identifier des valeurs spécifiques dans des documents JSON. Un pointeur JSON est une chaîne de jetons séparés par des caractères `/` qui précisent soit les clés d’objet soit les index de tableau ainsi que les jetons pouvant être une chaîne ou un nombre. Les chaînes de pointeurs JSON sont utilisées dans de nombreuses opérations PATCH pour les API [!DNL Experience Platform], comme décrit plus loin dans ce document. Pour plus d’informations sur JSON Pointer, reportez-vous à la [documentation de présentation de JSON Pointer](https://rapidjson.org/md_doc_pointer.html).

### Exemple d’objet de schéma JSON

Le fichier JSON suivant représente un schéma XDM simplifié dont les champs peuvent être référencés à l’aide de chaînes de pointeurs JSON. Notez que tous les champs qui ont été ajoutés à l’aide de groupes de champs de schéma personnalisés (tels que `loyaltyLevel`) ont un espace de noms sous un objet `_{TENANT_ID}`, contrairement aux champs qui ont été ajoutés à l’aide de groupes de champs de base (tels que `fullName`).

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
| `"/properties/person/properties/name/properties/fullName"` | (Renvoie une référence au champ `fullName`, fourni par un groupe de champs principaux.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Renvoie une référence au champ `loyaltyLevel`, fourni par un groupe de champs personnalisés.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Lors de l’utilisation des attributs `xdm:sourceProperty` et `xdm:destinationProperty` des descripteurs [!DNL Experience Data Model] (XDM), toutes les clés `properties` doivent être **exclues** de la chaîne du pointeur JSON. Pour plus d’informations, consultez la sous-partie du guide de développement de l’API [!DNL Schema Registry] sur les [descripteurs](../xdm/api/descriptors.md).

## Correctif JSON {#json-patch}

Il existe de nombreuses opérations PATCH pour les API [!DNL Experience Platform] qui acceptent les objets Correctif JSON pour leurs payloads de requête. Le correctif JSON est un format standardisé ([RFC 6902](https://tools.ietf.org/html/rfc6902)) permettant de décrire les modifications apportées à un document JSON. Il vous permet de définir des mises à jour partielles vers JSON sans avoir besoin d’envoyer le document entier dans un corps de requête.

### Exemple d’un objet de correctif JSON

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op` : le type d’opération de correctif. Bien que le correctif JSON prenne en charge plusieurs types d’opérations différents, toutes les opérations PATCH dans les API [!DNL Experience Platform] ne sont pas compatibles avec chaque type d’opération. Les types d’opérations disponibles sont :
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path` : la partie de la structure JSON mise à jour, identifiée grâce à la notation [JSON Pointer](#json-pointer).

En fonction du type d’opération indiqué dans `op`, l’objet du correctif JSON peut nécessiter des propriétés supplémentaires. Pour plus d’informations sur les différentes opérations de correctif JSON et leur syntaxe obligatoire, reportez-vous à la [documentation du correctif JSON](https://datatracker.ietf.org/doc/html/rfc6902).

## Schéma JSON {#json-schema}

Le schéma JSON est un format utilisé pour décrire et valider la structure des données JSON. [Le modèle de données d’expérience (XDM)](../xdm/home.md) tire parti des fonctionnalités du schéma JSON pour imposer des contraintes sur la structure et le format des données d’expérience client ingérées. Pour plus d’informations sur le schéma JSON, consultez la [documentation officielle](https://json-schema.org/).

## Étapes suivantes

Ce document a présenté certaines des technologies et syntaxes impliquées dans la gestion des ressources basées sur JSON pour [!DNL Experience Platform]. Pour plus d’informations sur l’utilisation des API Experience Platform, y compris les bonnes pratiques](api-guide.md) consultez le [ guide de prise en main . Pour obtenir des réponses aux questions fréquentes, reportez-vous au guide de dépannage d’[Experience Platform](troubleshooting.md).
