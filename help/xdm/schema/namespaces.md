---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;xdm;modèle de données d’expérience;espace de noms;espace de noms;mode de compatibilité;xed;
solution: Experience Platform
title: Espace de noms dans le modèle de données d’expérience (XDM)
description: Découvrez comment l’espace de noms dans le modèle de données d’expérience (XDM) vous permet d’étendre vos schémas et d’empêcher les collisions de champs lorsque différents composants de schéma sont rassemblés.
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: d26a0586a992948e1b278bae91a985fe3d9f1ee8
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 1%

---

# Espace de noms dans le modèle de données d’expérience (XDM)

>[!IMPORTANT]
>
>Dans XDM, l’espace de noms (la rubrique de cette page) est utilisé pour distinguer les champs d’un schéma. Cela diffère du concept d’espace de noms d’identité dans Identity Service, où l’espace de noms est utilisé pour distinguer les valeurs d’identité. Lisez la documentation sur [Espace de noms dans Identity Service](../../identity-service/features/namespaces.md) pour plus d’informations.

Tous les champs des schémas de modèle de données d’expérience (XDM) sont associés à un espace de noms. Ces espaces de noms vous permettent d’étendre vos schémas et d’empêcher les collisions de champs lorsque différents composants de schéma sont rassemblés. Ce document fournit un aperçu des espaces de noms dans XDM et de leur représentation dans la variable [API Schema Registry](../api/overview.md).

L’espace de noms permet de définir un champ dans un espace de noms comme signifiant quelque chose de différent du même champ dans un autre espace de noms. En pratique, l’espace de noms d’un champ indique qui a créé le champ (par exemple, XDM standard (Adobe), un fournisseur ou votre organisation).

Prenons l’exemple d’un schéma XDM qui utilise la variable [[!UICONTROL Détails du contact personnel] groupe de champs](../field-groups/profile/demographic-details.md), qui possède une `mobilePhone` qui existe dans le champ `xdm` espace de noms. Dans le même schéma, vous pouvez également créer une `mobilePhone` sous un autre espace de noms (votre [identifiant du client](../api/getting-started.md#know-your-tenant_id)). Ces deux domaines peuvent coexister tout en ayant des significations ou des contraintes sous-jacentes différentes.

## Syntaxe des espaces de noms

Les sections suivantes montrent comment les espaces de noms sont affectés dans la syntaxe XDM.

### XDM standard {#standard}

La syntaxe XDM standard fournit des informations sur la représentation des espaces de noms dans les schémas (y compris [comment ils sont traduits dans Adobe Experience Platform](#compatibility)).

Utilisations XDM standard [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts) pour affecter des espaces de noms aux champs. Cet espace de noms prend la forme d’un URI (tel que `https://ns.adobe.com/xdm` pour le `xdm` ) ou sous la forme d’un préfixe short configuré dans la variable `@context` d’un schéma.

Voici un exemple de schéma pour un produit dans la syntaxe XDM standard. À l’exception de `@id` (l’identifiant unique tel que défini par la spécification JSON-LD), chaque champ sous `properties` commence par un espace de noms et se termine par le nom du champ. Si vous utilisez un préfixe de raccourci défini sous `@context`, l’espace de noms et le nom du champ sont séparés par deux points (`:`). Si vous n’utilisez pas de préfixe, l’espace de noms et le nom du champ sont séparés par une barre oblique (`/`).

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
| `@context` | Objet qui définit le raccourci et les préfixes qui peuvent être utilisés à la place d’un URI d’espace de noms complet sous `properties`. |
| `@id` | Identifiant unique de l’enregistrement tel que défini par la variable [Spécification JSON-LD](https://www.w3.org/TR/json-ld11/#node-identifiers). |
| `xdm:sku` | Exemple de champ qui utilise un préfixe abrégé pour désigner un espace de noms. Dans ce cas, `xdm` est l’espace de noms (`https://ns.adobe.com/xdm`), et `sku` est le nom du champ. |
| `https://ns.adobe.com/xdm/channels/application` | Exemple de champ qui utilise l’URI d’espace de noms complet. Dans ce cas, `https://ns.adobe.com/xdm/channels` est l’espace de noms, et `application` est le nom du champ. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Les champs fournis par les ressources du fournisseur utilisent leurs propres espaces de noms uniques. Dans cet exemple, `https://ns.adobe.com/vendorA/product` est l’espace de noms du fournisseur ; et `stockNumber` est le nom du champ. |
| `tenantId:internalSku` | Les champs définis par votre organisation utilisent votre identifiant de client unique comme espace de noms. Dans cet exemple, `tenantId` est l’espace de noms du client (`https://ns.adobe.com/tenantId`), et `internalSku` est le nom du champ. |

{style="table-layout:auto"}

### Mode de compatibilité {#compatibility}

Dans Adobe Experience Platform, les schémas XDM sont représentés dans [Mode de compatibilité](../api/appendix.md#compatibility) qui n’utilise pas la syntaxe JSON-LD pour représenter les espaces de noms. Plutôt, Platform convertit l’espace de noms en un champ parent (en commençant par un trait de soulignement) et imbrique les champs en dessous.

Par exemple, le XDM standard `repo:createdDate` est converti en `_repo.createdDate` et apparaît sous la structure suivante en mode de compatibilité :

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

Champs qui utilisent la variable `xdm` L’espace de noms apparaît comme champs racine sous `properties` et déposez le `xdm:` préfixe qui apparaît dans [syntaxe XDM standard](#standard). Par exemple : `xdm:sku` est simplement répertorié comme `sku` au lieu de .

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

Ce guide fournit un aperçu des espaces de noms XDM et de leur représentation dans JSON. Pour plus d’informations sur la configuration des schémas XDM à l’aide de l’API, voir la section [Guide de l’API Schema Registry](../api/overview.md).
