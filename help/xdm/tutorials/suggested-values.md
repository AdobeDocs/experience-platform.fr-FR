---
title: Gestion des valeurs proposées dans l’API
description: Découvrez comment ajouter des valeurs suggérées à un champ de chaîne dans l’API Schema Registry.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: 19bd5d9c307ac6e1b852e25438ff42bf52a1231e
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 6%

---

# Gestion des valeurs suggérées dans l’API

Pour tout champ de chaîne dans le modèle de données d’expérience (XDM), vous pouvez définir une **enum** qui limite les valeurs que le champ peut ingérer à un jeu prédéfini. Si vous tentez d’ingérer des données dans un champ d’énumération et que la valeur ne correspond à aucune de celles définies dans sa configuration, l’ingestion sera refusée.

Contrairement aux énumérations, l’ajout de **valeurs suggérées** à un champ de chaîne ne limite pas les valeurs qu’il peut ingérer. Au lieu de cela, les valeurs suggérées affectent les valeurs prédéfinies disponibles dans la variable [Interface utilisateur de segmentation](../../segmentation/ui/overview.md) lors de l’inclusion du champ de chaîne en tant qu’attribut.

>[!NOTE]
>
>Il existe un délai d’environ cinq minutes pour que les valeurs suggérées d’un champ soient répercutées dans l’interface utilisateur de segmentation.

Ce guide explique comment gérer les valeurs suggérées à l’aide de la méthode [API Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Pour savoir comment procéder dans l’interface utilisateur de Adobe Experience Platform, reportez-vous à la section [Guide de l’interface utilisateur sur les énumérations et les valeurs suggérées](../ui/fields/enum.md).

## Conditions préalables

Ce guide suppose que vous connaissez les éléments de la composition des schémas dans XDM et que vous savez utiliser l’API Schema Registry pour créer et modifier des ressources XDM. Si vous avez besoin d’une introduction, reportez-vous à la documentation suivante :

* [Principes de base de la composition des schémas](../schema/composition.md)
* [Guide du registre des schémas API](../api/overview.md)

Il est également vivement recommandé de consulter la section [règles d’évolution pour les énumérations et les valeurs suggérées](../ui/fields/enum.md#evolution) si vous mettez à jour des champs existants. Si vous gérez des valeurs suggérées pour les schémas qui participent à une union, reportez-vous à la section [règles de fusion des énumérations et des valeurs proposées](../ui/fields/enum.md#merging).

## Composition

Dans l’API, les valeurs contraintes d’une **enum** est représenté par une `enum` tableau, lorsqu’un `meta:enum` fournit des noms d’affichage conviviaux pour ces valeurs :

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

Vous pouvez également définir un champ de chaîne qui ne contient pas de `enum` et utilise uniquement la variable `meta:enum` objet à indiquer **valeurs suggérées**:

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

Puisque la chaîne n’a pas de `enum` tableau pour définir des contraintes, son `meta:enum` peut être étendue pour inclure de nouvelles valeurs.

## Gestion des valeurs suggérées pour les champs standard

Pour les champs standard existants, vous pouvez : [ajouter des valeurs suggérées](#add-suggested-standard) ou [suppression des valeurs suggérées](#remove-suggested-standard).

### Ajout de valeurs suggérées {#add-suggested-standard}

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

### Supprimer les valeurs suggérées {#remove-suggested-standard}

Si un champ de chaîne standard comporte des valeurs suggérées prédéfinies, vous pouvez supprimer toutes les valeurs que vous ne souhaitez pas voir dans la segmentation. Pour ce faire, créez une [descripteur de nom convivial](../api/descriptors.md#friendly-name) pour le schéma qui comprend une `xdm:excludeMetaEnum` .

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante supprime les valeurs suggérées &quot;[!DNL Web Form Filled Out]&quot; et &quot;[!DNL Media ping]&quot; pour `eventType` dans un schéma basé sur la fonction [Classe XDM ExperienceEvent](../classes/experienceevent.md).

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

| Propriété | Description |
| --- | --- |
| `@type` | Le type de descripteur en cours de définition. Pour un descripteur de nom convivial, cette valeur doit être définie sur `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | L’URI `$id` du schéma dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du schéma source. |
| `xdm:sourceProperty` | Chemin d’accès à la propriété spécifique dont vous souhaitez gérer les valeurs suggérées. Le chemin doit commencer par une barre oblique (`/`) et ne pas se terminer par un. Ne pas inclure `properties` dans le chemin (par exemple, utilisez `/personalEmail/address` au lieu de `/properties/personalEmail/properties/address`). |
| `meta:excludeMetaEnum` | Objet décrivant les valeurs suggérées qui doivent être exclues pour le champ de la segmentation. La clé et la valeur de chaque entrée doivent correspondre à celles incluses dans l’original. `meta:enum` du champ pour que la saisie soit exclue. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Created) et les détails du nouveau descripteur. Les valeurs proposées incluses sous `xdm:excludeMetaEnum` sera désormais masqué dans l’interface utilisateur de segmentation.

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
```

## Gestion des valeurs proposées pour un champ personnalisé {#suggested-custom}

Pour gérer la variable `meta:enum` d’un champ personnalisé, vous pouvez mettre à jour la classe parent, le groupe de champs ou le type de données du champ par le biais d’une requête de PATCH.

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

Ce guide explique comment gérer les valeurs suggérées pour les champs de chaîne dans l’API Schema Registry. Consultez le guide sur la [définition de champs personnalisés dans l’API](./custom-fields-api.md) pour plus d’informations sur la création de différents types de champ.
