---
title: Gestion des valeurs proposées dans l’API
description: Découvrez comment ajouter des valeurs suggérées à un champ de chaîne dans l’API Schema Registry.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---

# Gestion des valeurs suggérées dans l’API

Pour tout champ de chaîne dans le modèle de données d’expérience (XDM), vous pouvez définir une **énumération** qui limite les valeurs que le champ peut ingérer à un ensemble prédéfini. Si vous tentez d’ingérer des données dans un champ d’énumération et que la valeur ne correspond à aucune de celles définies dans sa configuration, l’ingestion sera refusée.

Contrairement aux énumérations, l’ajout de **valeurs suggérées** à un champ de chaîne ne limite pas les valeurs qu’il peut ingérer. Au lieu de cela, les valeurs suggérées affectent les valeurs prédéfinies disponibles dans l’ [interface utilisateur de segmentation](../../segmentation/ui/overview.md) lors de l’inclusion du champ de chaîne en tant qu’attribut.

>[!NOTE]
>
>Il existe un délai d’environ cinq minutes pour que les valeurs suggérées d’un champ soient répercutées dans l’interface utilisateur de segmentation.

Ce guide explique comment gérer les valeurs suggérées à l’aide de l’ [API Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Pour savoir comment procéder dans l’interface utilisateur de Adobe Experience Platform, consultez le [guide de l’interface utilisateur sur les énumérations et les valeurs suggérées](../ui/fields/enum.md).

## Conditions préalables

Ce guide suppose que vous connaissez les éléments de la composition des schémas dans XDM et que vous savez utiliser l’API Schema Registry pour créer et modifier des ressources XDM. Si vous avez besoin d’une introduction, reportez-vous à la documentation suivante :

* [Principes de base de la composition des schémas](../schema/composition.md)
* [Guide du registre des schémas API](../api/overview.md)

Il est également vivement recommandé de consulter les [règles d’évolution pour les énumérations et les valeurs suggérées](../ui/fields/enum.md#evolution) si vous mettez à jour des champs existants. Si vous gérez des valeurs suggérées pour les schémas qui participent à une union, consultez les [ règles de fusion des énumérations et des valeurs suggérées](../ui/fields/enum.md#merging).

## Composition

Dans l’API, les valeurs contraintes d’un champ **enum** sont représentées par un tableau `enum`, tandis qu’un objet `meta:enum` fournit des noms d’affichage conviviaux pour ces valeurs :

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

Pour les champs d’énumération, le registre des schémas ne permet pas d’étendre `meta:enum` au-delà des valeurs fournies sous `enum`, car toute tentative d’ingestion de valeurs de chaîne en dehors de ces contraintes ne serait pas validée.

Vous pouvez également définir un champ de chaîne qui ne contient pas de tableau `enum` et n’utilise que l’objet `meta:enum` pour représenter les **valeurs suggérées** :

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

Comme la chaîne ne dispose pas d’un tableau `enum` pour définir des contraintes, sa propriété `meta:enum` peut être étendue pour inclure de nouvelles valeurs.

<!-- ## Manage suggested values for standard fields

For existing standard fields, you can [add suggested values](#add-suggested-standard) or [remove suggested values](#remove-suggested-standard). -->

## Ajout de valeurs suggérées à un champ standard {#add-suggested-standard}

Pour étendre le `meta:enum` d’un champ de chaîne standard, vous pouvez créer un [descripteur de nom convivial](../api/descriptors.md#friendly-name) pour le champ en question dans un schéma particulier.

>[!NOTE]
>
>Les valeurs proposées pour les champs de chaîne ne peuvent être ajoutées qu’au niveau du schéma. En d’autres termes, étendre le `meta:enum` d’un champ standard dans un schéma n’affecte pas les autres schémas qui utilisent le même champ standard.

La requête suivante ajoute des valeurs suggérées au champ `eventType` standard (fourni par la [classe XDM ExperienceEvent](../classes/experienceevent.md)) pour le schéma identifié sous `sourceSchema` :

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>```json
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

<!-- ### Remove suggested values {#remove-suggested-standard}

If a standard string field has predefined suggested values, you can remove any values that you do not wish to see in segmentation. This is done through by creating a [friendly name descriptor](../api/descriptors.md#friendly-name) for the schema that includes an `xdm:excludeMetaEnum` property.

**API format**

```http
POST /tenant/descriptors
```

**Request**

The following request removes the suggested values "[!DNL Web Form Filled Out]" and "[!DNL Media ping]" for `eventType` in a schema based on the [XDM ExperienceEvent class](../classes/experienceevent.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/xdm:eventType",
        "xdm:excludeMetaEnum": {
          "web.formFilledOut": "Web Form Filled Out",
          "media.ping": "Media ping"
        }
      }'
```

| Property | Description |
| --- | --- |
| `@type` | The type of descriptor being defined. For a friendly name descriptor, this value must be set to `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | The `$id` URI of the schema where the descriptor is being defined. |
| `xdm:sourceVersion` | The major version of the source schema. |
| `xdm:sourceProperty` | The path to the specific property whose suggested values you want to manage. The path should begin with a slash (`/`) and not end with one. Do not include `properties` in the path (for example, use `/personalEmail/address` instead of `/properties/personalEmail/properties/address`). |
| `meta:excludeMetaEnum` | An object that describes the suggested values that should be excluded for the field in segmentation. The key and value for each entry must match those included in the original `meta:enum` of the field in order for the entry to be excluded.  |

{style="table-layout:auto"}

**Response**

A successful response returns HTTP status 201 (Created) and the details of the newly created descriptor. The suggested values included under `xdm:excludeMetaEnum` will now be hidden from the Segmentation UI.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out"
  },
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
``` -->

## Gestion des valeurs proposées pour un champ personnalisé {#suggested-custom}

Pour gérer l’ `meta:enum` d’un champ personnalisé, vous pouvez mettre à jour la classe parent, le groupe de champs ou le type de données du champ par le biais d’une requête de PATCH.

>[!WARNING]
>
>Contrairement aux champs standard, la mise à jour de `meta:enum` d’un champ personnalisé affecte tous les autres schémas qui utilisent ce champ. Si vous ne souhaitez pas que les modifications se propagent entre les schémas, envisagez plutôt de créer une ressource personnalisée :
>
>* [Créer une classe personnalisée](../api/classes.md#create)
>* [Créer un groupe de champs personnalisé](../api/field-groups.md#create)
>* [ Créez un type de données personnalisé ](../api/data-types.md#create)

La requête suivante met à jour le `meta:enum` d’un champ &quot;niveau de fidélité&quot; fourni par un type de données personnalisé :

```curl
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Ce guide explique comment gérer les valeurs suggérées pour les champs de chaîne dans l’API Schema Registry. Pour plus d’informations sur la création de différents types de champs, consultez le guide sur la [définition de champs personnalisés dans l’API](./custom-fields-api.md) .
