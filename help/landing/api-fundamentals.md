---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Principes de base de l’API Experience Platform
topic-legacy: getting started
description: Ce document donne un bref aperçu de certaines technologies et syntaxes sous-jacentes impliquées dans les API Experience Platform.
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 54%

---

# Principes de base de l’API Experience Platform

Les API Adobe Experience Platform utilisent plusieurs technologies et syntaxes sous-jacentes qui sont importantes à comprendre pour gérer efficacement les ressources [!DNL Platform] JSON. Ce document apporte un aperçu rapide de ces technologies ainsi que des liens vers de la documentation externe pour vous apporter de plus amples informations.

## JSON Pointer {#json-pointer}

JSON Pointer est une syntaxe de chaîne normalisée ([RFC 6901](https://tools.ietf.org/html/rfc6901)) qui permet d’identifier des valeurs spécifiques dans des documents JSON. Un pointeur JSON est une chaîne de jetons séparés par des caractères `/` qui précisent soit les clés d’objet soit les index de tableau ainsi que les jetons pouvant être une chaîne ou un nombre. Les chaînes de pointeur JSON sont utilisées dans de nombreuses opérations de PATCH pour les API [!DNL Platform], comme décrit plus loin dans ce document. Pour plus d’informations sur JSON Pointer, reportez-vous à la [documentation de présentation de JSON Pointer](https://rapidjson.org/md_doc_pointer.html).

### Exemple d’objet de schéma JSON

Le fichier JSON suivant représente un schéma XDM simplifié dont les champs peuvent être référencés à l’aide de chaînes de pointeur JSON. Notez que tous les champs qui ont été ajoutés à l’aide de mixins personnalisés (tels que `loyaltyLevel`) sont espacés par nom sous un objet `_{TENANT_ID}`, contrairement aux champs qui ont été ajoutés à l’aide de mixins principaux (tels que `fullName`).

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
| `"/properties/person/properties/name/properties/fullName"` | (Renvoie une référence au champ `fullName`, fourni par un mixin principal.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Renvoie une référence au champ `loyaltyLevel`, fourni par un mixin personnalisé.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Lorsque vous utilisez les attributs `xdm:sourceProperty` et `xdm:destinationProperty` des descripteurs [!DNL Experience Data Model] (XDM), toute clé `properties` doit être **exclue** de la chaîne JSON Pointer. Pour plus d&#39;informations, consultez le [!DNL Schema Registry] sous-guide du développeur d&#39;API sur les [descripteurs](../xdm/api/descriptors.md).

## Correctif JSON {#json-patch}

De nombreuses opérations de PATCH pour les API [!DNL Platform] acceptent les objets de correctif JSON pour leurs charges utiles de demande. Le correctif JSON est un format standardisé ([RFC 6902](https://tools.ietf.org/html/rfc6902)) permettant de décrire les modifications apportées à un document JSON. Il vous permet de définir des mises à jour partielles vers JSON sans avoir besoin d’envoyer le document entier dans un corps de requête.

### Exemple d’un objet de correctif JSON

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op` : le type d’opération de correctif. Bien que le correctif JSON prenne en charge plusieurs types d’opérations différents, toutes les opérations de PATCH dans les API [!DNL Platform] ne sont pas compatibles avec chaque type d’opération. Les types d’opérations disponibles sont :
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path` : la partie de la structure JSON mise à jour, identifiée grâce à la notation [JSON Pointer](#json-pointer).

En fonction du type d’opération indiqué dans `op`, l’objet du correctif JSON peut nécessiter des propriétés supplémentaires. Pour plus d’informations sur les différentes opérations de correctif JSON et leur syntaxe obligatoire, reportez-vous à la [documentation du correctif JSON](http://jsonpatch.com/).

## Schéma JSON {#json-schema}

Le schéma JSON est un format utilisé pour décrire et valider la structure des données JSON. [Le modèle de données d’expérience (XDM)](../xdm/home.md) tire parti des fonctionnalités du schéma JSON pour imposer des contraintes sur la structure et le format des données d’expérience client ingérées. Pour plus d’informations sur le schéma JSON, consultez la [documentation officielle](https://json-schema.org/).

## Étapes suivantes

Ce document a présenté certaines des technologies et syntaxes impliquées dans la gestion des ressources basées sur JSON pour [!DNL Experience Platform]. Consultez le [guide de prise en main](api-guide.md) pour plus d&#39;informations sur l&#39;utilisation des API de plateformes, y compris les meilleures pratiques. Pour obtenir des réponses aux questions fréquentes, consultez le [Guide de dépannage de la plate-forme](troubleshooting.md).
