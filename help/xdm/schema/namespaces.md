---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;xdm;modèle de données d’expérience;espace de noms;espaces de noms;mode de compatibilité;xed;
solution: Experience Platform
title: Espace de noms dans le modèle de données d’expérience (XDM)
description: Découvrez comment l’espace de noms dans le modèle de données d’expérience (XDM) vous permet d’étendre vos schémas et d’empêcher les collisions de champs lorsque différents composants de schéma sont rassemblés.
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 1%

---

# Espace de noms dans le modèle de données d’expérience (XDM)

>[!IMPORTANT]
>
>Dans XDM, l’espace de noms (rubrique de cette page) est utilisé pour distinguer les champs d’un schéma. Cela diffère du concept d’espace de noms d’identité dans Identity Service, où l’espace de noms est utilisé pour distinguer les valeurs d’identité. Pour plus d’informations, consultez la documentation sur [l’espace de noms dans Identity Service](../../identity-service/features/namespaces.md).

Tous les champs des schémas de modèle de données d’expérience (XDM) sont associés à un espace de noms . Ces espaces de noms vous permettent d’étendre vos schémas et d’empêcher les collisions de champs lorsque différents composants de schéma sont rassemblés. Ce document présente les espaces de noms dans XDM et leur représentation dans l’[API Schema Registry](../api/overview.md).

L’espace de noms vous permet de définir un champ dans un espace de noms comme étant différent du même champ dans un autre espace de noms. En pratique, l’espace de noms d’un champ indique qui a créé le champ (par exemple, XDM standard (Adobe), un fournisseur ou votre organisation).

Prenons l’exemple d’un schéma XDM qui utilise le groupe de champs [[!UICONTROL Coordonnées personnelles] ](../field-groups/profile/demographic-details.md), qui comporte un champ `mobilePhone` standard existant dans l’espace de noms `xdm`. Dans le même schéma, vous êtes également libre de créer un champ de `mobilePhone` distinct sous un autre espace de noms (votre [identifiant client](../api/getting-started.md#know-your-tenant_id)). Ces deux champs peuvent coexister tout en ayant des significations ou des contraintes sous-jacentes différentes.

## Syntaxe de l’espace de noms

Les sections suivantes montrent comment les espaces de noms sont attribués dans la syntaxe XDM.

### XDM standard {#standard}

La syntaxe XDM standard fournit à insight la manière dont les espaces de noms sont représentés dans les schémas (y compris [leur traduction dans Adobe Experience Platform](#compatibility)).

Le XDM standard utilise la syntaxe [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts) pour affecter des espaces de noms aux champs. Cet espace de noms se présente sous la forme d’un URI (comme `https://ns.adobe.com/xdm` pour l’espace de noms `xdm`) ou d’un préfixe abrégé configuré dans l’attribut `@context` d’un schéma.

Voici un exemple de schéma pour un produit dans la syntaxe XDM standard. À l’exception de `@id` (l’identifiant unique tel que défini par la spécification JSON-LD ), chaque champ sous `properties` commence par un espace de noms et se termine par le nom du champ. Si vous utilisez un préfixe court défini sous `@context`, l’espace de noms et le nom du champ sont séparés par le caractère deux-points (`:`). Si vous n’utilisez pas de préfixe, l’espace de noms et le nom du champ sont séparés par une barre oblique (`/`).

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
| `@context` | Objet définissant les préfixes courts qui peuvent être utilisés au lieu d’un URI d’espace de noms complet sous `properties`. |
| `@id` | Identifiant unique de l’enregistrement tel que défini par la [spécification JSON-LD](https://www.w3.org/TR/json-ld11/#node-identifiers). |
| `xdm:sku` | Exemple de champ qui utilise un préfixe court pour indiquer un espace de noms. Dans ce cas, `xdm` est l’espace de noms (`https://ns.adobe.com/xdm`) et `sku` est le nom du champ. |
| `https://ns.adobe.com/xdm/channels/application` | Exemple de champ qui utilise l’URI d’espace de noms complet. Dans ce cas, `https://ns.adobe.com/xdm/channels` est l’espace de noms et `application` est le nom du champ. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Les champs fournis par les ressources fournisseur utilisent leurs propres espaces de noms uniques. Dans cet exemple, `https://ns.adobe.com/vendorA/product` est l’espace de noms du fournisseur et `stockNumber` est le nom du champ. |
| `tenantId:internalSku` | Les champs définis par votre organisation utilisent votre identifiant client unique comme espace de noms. Dans cet exemple, `tenantId` est l’espace de noms du client (`https://ns.adobe.com/tenantId`) et `internalSku` est le nom du champ. |

{style="table-layout:auto"}

### Mode de compatibilité {#compatibility}

Dans Adobe Experience Platform, les schémas XDM sont représentés dans la syntaxe [Mode de compatibilité](../api/appendix.md#compatibility) qui n’utilise pas la syntaxe JSON-LD pour représenter les espaces de noms. Au lieu de cela, Experience Platform convertit l’espace de noms en champ parent (en commençant par un trait de soulignement) et imbrique les champs en dessous.

Par exemple, le `repo:createdDate` XDM standard est converti en `_repo.createdDate` et s’affiche sous la structure suivante en mode de compatibilité :

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

Les champs qui utilisent l’espace de noms `xdm` apparaissent comme des champs racine sous `properties` et déposent le préfixe `xdm:` qui apparaîtrait dans [syntaxe XDM standard](#standard). Par exemple, `xdm:sku` est simplement répertorié comme `sku`.

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

Ce guide présente les espaces de noms XDM et leur représentation dans JSON. Pour plus d’informations sur la configuration des schémas XDM à l’aide de l’API, consultez le guide [API Schema Registry](../api/overview.md).
