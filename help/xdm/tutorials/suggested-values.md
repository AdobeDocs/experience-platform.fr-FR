---
title: Ajout de valeurs proposées à un champ
description: Découvrez comment ajouter des valeurs suggérées à un champ de chaîne dans l’API Schema Registry.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: 4ce9e53ec420a8c9ba07cdfd75e66d854989f8d2
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---

# Ajout de valeurs suggérées à un champ

Dans le modèle de données d’expérience (XDM), un champ d’énumération représente un champ de chaîne limité à un sous-ensemble prédéfini de valeurs. Les champs d’énumération peuvent fournir une validation pour s’assurer que les données ingérées sont conformes à un ensemble de valeurs acceptées. Cependant, vous pouvez également définir un ensemble de valeurs suggérées pour un champ de chaîne sans les appliquer en tant que contraintes.

Dans le [API Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/), les valeurs contraintes d’un champ d’énumération sont représentées par une `enum` tableau, lorsqu’un `meta:enum` fournit des noms d’affichage conviviaux pour ces valeurs :

```json
"exampleStringField": {
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
}
```

Pour les champs d’énumération, le registre des schémas n’autorise pas `meta:enum` à étendre au-delà des valeurs fournies sous `enum`, puisque toute tentative d’ingestion de valeurs de chaîne en dehors de ces contraintes ne serait pas validée.

Vous pouvez également définir un champ de chaîne qui ne contient pas de `enum` et utilise uniquement la variable `meta:enum` pour indiquer les valeurs suggérées :

```json
"exampleStringField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

Puisque la chaîne n’a pas de `enum` tableau pour définir des contraintes, son `meta:enum` peut être étendue pour inclure de nouvelles valeurs. Ce tutoriel explique comment ajouter des valeurs suggérées à des champs de chaîne standard et personnalisés dans l’API Schema Registry.

## Conditions préalables

Ce guide suppose que vous connaissez les éléments de la composition des schémas dans XDM et que vous savez utiliser l’API Schema Registry pour créer et modifier des ressources XDM. Si vous avez besoin d’une introduction, reportez-vous à la documentation suivante :

* [Principes de base de la composition des schémas](../schema/composition.md)
* [Guide de l’API Schema Registry](../api/overview.md)

## Ajout de valeurs suggérées à un champ standard

Pour étendre la variable `meta:enum` d’un champ de chaîne standard, vous pouvez créer une [descripteur de nom convivial](../api/descriptors.md#friendly-name) pour le champ en question dans un schéma particulier.

>[!NOTE]
>
>Les valeurs proposées pour les champs de chaîne ne peuvent être ajoutées qu’au niveau du schéma. En d’autres termes, l’extension de la variable `meta:enum` d’un champ standard dans un schéma n’affecte pas les autres schémas qui utilisent le même champ standard.

La requête suivante ajoute les valeurs suggérées à la norme `eventType` (fourni par la fonction [Classe XDM ExperienceEvent](../classes/experienceevent.md)) pour le schéma identifié sous `sourceSchema`:

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "sourceProperty": "/eventType",
        "title": {
            "en_us": "Enum Event Type"
        },
        "description": {
            "en_us": "Event type field with soft enum values"
        },
        "meta:enum": {
          "eventA": {
            "en_us": "Event Type A"
          },
          "eventB": {
            "en_us": "Event Type B"
          }
        }
      }'
```

Après l’application du descripteur, le registre des schémas répond avec ce qui suit lors de la récupération du schéma (réponse tronquée pour l’espace) :

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "eventType": {
      "type":"string",
      "title": "Enum Event Type",
      "description": "Event type field with soft enum values.",
      "meta:enum": {
        "customEventA": "Custom Event Type A",
        "customEventB": "Custom Event Type B"
      }
    }
  }
}
```

>[!NOTE]
>
>Si le champ standard contient déjà des valeurs sous `meta:enum`, les nouvelles valeurs du descripteur ne remplacent pas les champs existants et sont ajoutées à la place :
>
>
```json
>"standardField": {
>   "type":"string",
>   "title": "Example standard enum field",
>   "description": "Standard field with existing enum values.",
>   "meta:enum": {
>       "standardEventA": "Standard Event Type A",
>       "standardEventB": "Standard Event Type B",
>       "customEventA": "Custom Event Type A",
>       "customEventB": "Custom Event Type B"
>   }
>}
>```

## Ajout de valeurs suggérées à un champ personnalisé

Pour étendre la variable `meta:enum` d’un champ personnalisé, vous pouvez mettre à jour la classe parent, le groupe de champs ou le type de données du champ par le biais d’une requête de PATCH.

>[!WARNING]
>
>Contrairement aux champs standard, la mise à jour de la variable `meta:enum` d’un champ personnalisé affecte tous les autres schémas qui utilisent ce champ. Si vous ne souhaitez pas que les modifications se propagent entre les schémas, envisagez plutôt de créer une ressource personnalisée :
>
>* [Création d’une classe personnalisée](../api/classes.md#create)
>* [Création d’un groupe de champs personnalisé](../api/field-groups.md#create)
>* [Création d’un type de données personnalisé](../api/data-types.md#create)


La requête suivante met à jour la variable `meta:enum` d’un champ &quot;niveau de fidélité&quot; fourni par un type de données personnalisé :

```curl
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/loyaltyLevel/meta:enum",
          "value": {
            "ultra-platinum": "Ultra Platinum",
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          }
        }
      ]'
```

Après avoir appliqué la modification, le registre des schémas répond avec ce qui suit lors de la récupération du schéma (réponse tronquée pour l’espace) :

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "loyaltyLevel": {
      "type":"string",
      "title": "Loyalty Level",
      "description": "The loyalty program tier that this customer qualifies for.",
      "meta:enum": {
        "ultra-platinum": "Ultra Platinum",
        "platinum": "Platinum",
        "gold": "Gold",
        "silver": "Silver",
        "bronze": "Bronze"
      }
    }
  }
}
```

## Étapes suivantes

Ce guide explique comment ajouter des valeurs suggérées à des champs de chaîne dans l’API Schema Registry. Consultez le guide sur la [définition de champs personnalisés dans l’API](./custom-fields-api.md) pour plus d’informations sur la création de différents types de champ.
