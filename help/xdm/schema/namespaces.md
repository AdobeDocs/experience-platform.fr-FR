---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; xdm ; modèle de données d’expérience ; espace de nommage ; espaces de nommage ; mode de compatibilité ; xed ;
solution: Experience Platform
title: Espace de noms dans le modèle de données d’expérience (XDM)
topic-legacy: overviews
description: Découvrez comment l’espacement des noms dans le modèle de données d’expérience (XDM) vous permet d’étendre vos schémas et d’éviter les collisions de champs lorsque différents composants de schéma sont réunis.
source-git-commit: b4c4f8f7e428d27f389bff5591a03925b6afa6d8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---


# Espace de noms dans le modèle de données d’expérience (XDM)

Tous les champs des schémas de modèle de données d’expérience (XDM) sont associés à un espace de nommage. Ces espaces de nommage vous permettent d&#39;étendre vos schémas et d&#39;éviter les collisions de champs lorsque différents composants de schéma sont réunis. Ce document présente un aperçu des espaces de nommage de la section
XDM et comment ils sont représentés dans l&#39;[API de registre de Schéma](../api/overview.md).

L’espace de noms permet de définir un champ dans un espace de nommage comme signifiant quelque chose de différent du même champ dans un espace de nommage différent. En pratique, l’espace de nommage d’un champ indique qui a créé le champ (par exemple, XDM (Adobe) standard, un fournisseur ou votre organisation).

Prenons l’exemple d’un schéma XDM qui utilise le groupe de champs [[!UICONTROL Détails du contact personnel]](../field-groups/profile/demographic-details.md), dont le champ `mobilePhone` standard existe dans l’espace de nommage `xdm`. Dans le même schéma, vous pouvez également créer un champ `mobilePhone` distinct sous un autre espace de nommage (votre [ID de client](../api/getting-started.md#know-your-tenant_id)). Ces deux domaines peuvent coexister tout en ayant des significations ou des contraintes sous-jacentes différentes.

## Syntaxe Namespacing

Les sections suivantes montrent comment les espaces de nommage sont affectés dans la syntaxe XDM.

### XDM standard {#standard}

La syntaxe XDM standard permet de comprendre comment les espaces de nommage sont représentés dans les schémas (y compris [comment ils sont traduits dans Adobe Experience Platform](#compatibility)).

XDM standard utilise la syntaxe [JSON-LD](https://json-ld.org/) pour affecter des espaces de nommage aux champs. Cet espace de nommage se présente sous la forme d&#39;un URI (tel que `https://ns.adobe.com/xdm` pour l&#39;espace de nommage `xdm`) ou sous la forme d&#39;un préfixe abrégé configuré dans l&#39;attribut `@context` d&#39;un schéma.

Voici un exemple de schéma pour un produit dans la syntaxe XDM standard. À l’exception de `@id` (l’identifiant unique défini par la spécification JSON-LD), chaque champ situé sous `properties` début avec un espace de nommage et se termine par le nom du champ. Si vous utilisez un préfixe abrégé défini sous `@context`, l’espace de nommage et le nom du champ sont séparés par deux points (`:`). Si vous n’utilisez pas de préfixe, l’espace de nommage et le nom du champ sont séparés par une barre oblique (`/`).

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "@context": {
    "xdm": "https://ns.adobe.com/xdm",
    "repo": "http://ns.adobe.com/adobecloud/core/1.0/",
    "schema": "http://schema.org",
    "tenantId": "https://ns.adobe.com/tenantId"
  },
  "properties": {
    "@id": {
      "type": "string"
    },
    "xdm:sku": {
      "type": "string"
    },
    "xdm:name": {
      "type": "string"
    },
    "repo:createdDate": {
      "type": "string",
      "format": "datetime"
    },
    "https://ns.adobe.com/xdm/channels/application": {
      "type": "string"
    },
    "schema:latitude": {
      "type": "number"
    },
    "https://ns.adobe.com/vendorA/product/stockNumber": {
      "type": "string"
    },
    "tenantId:internalSku": {
      "type": "number"
    }
  }
}
```

| Propriété | Description |
| --- | --- |
| `@context` | Objet qui définit les préfixes abrégés qui peuvent être utilisés à la place d&#39;un URI d&#39;espace de nommage complet sous `properties`. |
| `@id` | Identificateur unique de l’enregistrement tel que défini par la [spécification JSON-LD](https://json-ld.org/spec/latest/json-ld/#node-identifiers). |
| `xdm:sku` | Exemple de champ qui utilise un préfixe abrégé pour désigner un espace de nommage. Dans ce cas, `xdm` est l’espace de nommage (`https://ns.adobe.com/xdm`) et `sku` est le nom du champ. |
| `https://ns.adobe.com/xdm/channels/application` | Exemple d’un champ qui utilise l’URI d’espace de nommage complet. Dans ce cas, `https://ns.adobe.com/xdm/channels` est l’espace de nommage et `application` est le nom du champ. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Les champs fournis par les ressources fournisseur utilisent leurs propres espaces de nommage uniques. Dans cet exemple, `https://ns.adobe.com/vendorA/product` est l’espace de nommage fournisseur et `stockNumber` est le nom du champ. |
| `tenantId:internalSku` | Les champs définis par votre organisation utilisent votre identifiant de client unique comme espace de nommage. Dans cet exemple, `tenantId` est l’espace de nommage locataire (`https://ns.adobe.com/tenantId`) et `internalSku` est le nom du champ. |

{style=&quot;table-layout:auto&quot;}

### Mode de compatibilité {#compatibility}

Dans Adobe Experience Platform, les schémas XDM sont représentés dans la syntaxe [Mode de compatibilité](../api/appendix.md#compatibility), qui n’utilise pas la syntaxe JSON-LD pour représenter les espaces de nommage. Plate-forme convertit l’espace de nommage en un champ parent (en commençant par un trait de soulignement) et imbrique les champs situés en dessous.

Par exemple, le XDM standard `repo:createdDate` est converti en `_repo.createdDate` et apparaîtra sous la structure suivante en mode de compatibilité :

```json
"_repo": {
  "type": "object",
  "properties": {
    "createdDate": {
      "type": "string",
      "format": "datetime"
    }
  }
}
```

Les champs qui utilisent l&#39;espace de nommage `xdm` apparaissent sous la forme de champs racine sous `properties` et déposez le préfixe `xdm:` qui apparaîtra dans la syntaxe XDM standard [](#standard). Par exemple, `xdm:sku` est simplement répertorié comme `sku`.

Le fichier JSON suivant représente la manière dont l’exemple de syntaxe XDM standard illustré ci-dessus est traduit en mode de compatibilité.

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "properties": {
    "_id": {
      "type": "string"
    },
    "sku": {
      "type": "string"
    },
    "name": {
      "type": "string"
    },
    "_repo": {
      "type": "object",
      "properties": {
        "createdDate": {
          "type": "string",
          "format": "datetime"
        }
      }
    },
    "_channels": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_schema": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_vendorA": {
      "type": "object",
      "properties": {
        "product": {
          "type": "object",
          "properties": {
            "stockNumber": {
              "type": "string"
            }
          }
        }
      }
    },
    "_tenantId": {
      "type": "object",
      "properties": {
        "internalSku": {
          "type": "number"
        }
      }
    }
  }
}
```

## Étapes suivantes

Ce guide présente un aperçu des espaces de nommage XDM et de leur représentation dans JSON. Pour plus d&#39;informations sur la configuration des schémas XDM à l&#39;aide de l&#39;API, consultez le [Guide de l&#39;API de registre de Schéma](../api/overview.md).
