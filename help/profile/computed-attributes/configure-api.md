---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Configuration d’un champ d’attribut calculé
topic-legacy: guide
type: Documentation
description: Les attributs calculés sont des fonctions utilisées pour regrouper des données au niveau de l’événement en attributs au niveau du profil. Pour configurer un attribut calculé, vous devez d’abord identifier le champ dans lequel la valeur d’attribut calculé sera conservée. Ce champ peut être créé à l’aide de l’API Schema Registry pour définir un schéma et un groupe de champs personnalisé qui contiendra le champ attribut calculé.
exl-id: 91c5d125-8ab5-4291-a974-48dd44c68a13
source-git-commit: e4bf5bb77ac4186b24580329699d74d653310d93
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 16%

---

# (Alpha) Configuration d’un champ attribut calculé à l’aide de l’API Schema Registry

>[!IMPORTANT]
>
>La fonctionnalité d’attribut calculé est actuellement en version alpha et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Pour configurer un attribut calculé, vous devez d’abord identifier le champ dans lequel la valeur d’attribut calculé sera conservée. Ce champ peut être créé à l’aide de l’API Schema Registry pour définir un schéma et un groupe de champs de schéma personnalisé qui contiendra le champ attribut calculé. Il est recommandé de créer un schéma et un groupe de champs &quot;Attributs calculés&quot; distincts dans lequel votre organisation peut ajouter tous les attributs à utiliser comme attributs calculés. Cela permet à votre organisation de séparer clairement le schéma d’attribut calculé des autres schémas utilisés pour l’ingestion de données.

Le workflow de ce document explique comment utiliser l’API Schema Registry pour créer un schéma &quot;Attribut calculé&quot; activé par Profile qui référence un groupe de champs personnalisé. Ce document contient un exemple de code spécifique aux attributs calculés. Pour plus d’informations sur la définition des groupes de champs et des schémas à l’aide de l’API, reportez-vous au [guide de l’API Schema Registry](../../xdm/api/overview.md).

## Création d’un groupe de champs Attributs calculés

Pour créer un groupe de champs à l’aide de l’API Schema Registry, commencez par envoyer une requête de POST au point de terminaison `/tenant/fieldgroups` et fournissez les détails du groupe de champs dans le corps de la requête. Pour plus d’informations sur l’utilisation des groupes de champs à l’aide de l’API Schema Registry, consultez le [guide de point de terminaison de l’API des groupes de champs](../../xdm/api/field-groups.md).

**Format d’API**

```http
POST /tenant/fieldgroups
```

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "title":"Computed Attributes Field Group",
        "description":"Description of the field group.",
        "type":"object",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "definitions": {
          "computedAttributesFieldGroup": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

| Propriété | Description |
|---|---|
| `title` | Nom du groupe de champs que vous créez. |
| `meta:intendedToExtend` | Classe XDM avec laquelle le groupe de champs peut être utilisé. |

**Réponse**

Une requête réussie renvoie un état de réponse HTTP 201 (Created) avec un corps de réponse qui contient les détails du nouveau groupe de champs, y compris `$id`, `meta:altIt` et `version`. Ces valeurs sont en lecture seule et sont attribuées par le registre des schémas.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of the field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesFieldGroup",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Mettre à jour le groupe de champs avec des attributs calculés supplémentaires

Au fur et à mesure que davantage d’attributs calculés sont nécessaires, vous pouvez mettre à jour le groupe de champs des attributs calculés avec des attributs supplémentaires en effectuant une requête de PUT sur le point de terminaison `/tenant/fieldgroups`. Cette requête nécessite que vous incluiez l’identifiant unique du groupe de champs que vous avez créé dans le chemin d’accès et tous les nouveaux champs que vous souhaitez ajouter dans le corps.

Pour plus d’informations sur la mise à jour d’un groupe de champs à l’aide de l’API Schema Registry, consultez le [guide de point de terminaison de l’API des groupes de champs](../../xdm/api/field-groups.md).

**Format d’API**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

**Requête**

Cette requête ajoute de nouveaux champs liés aux `purchaseSummary` informations.

>[!NOTE]
>
>Lors de la mise à jour d’un groupe de champs par le biais d’une requête de PUT, le corps doit inclure tous les champs requis lors de la création d’un groupe de champs dans une requête de POST.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Field Group",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Description of field group.",
        "definitions": {
          "computedAttributesFieldGroup": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  },
                  "purchaseSummary": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                      "totalSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      },
                      "countPurchases": {
                        "meta:xdmType": "int",
                        "type": "integer",
                        "minimum": -2147483648,
                        "maximum": 2147483647
                      },
                      "averageSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

**Réponse**

Une réponse réussie renvoie les détails du groupe de champs mis à jour.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            },
            "purchaseSummary": {
              "type": "object",
              "meta:xdmType": "object",
              "properties": {
                "totalSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                },
                "countPurchases": {
                  "meta:xdmType": "int",
                  "type": "integer",
                  "minimum": -2147483648,
                  "maximum": 2147483647
                },
                "averageSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                }
              }
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesFieldGroup",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Création d’un schéma activé par Profile

Pour créer un schéma à l’aide de l’API Schema Registry, commencez par envoyer une requête de POST au point de terminaison `/tenant/schemas` et fournissez les détails du schéma dans le corps de la requête. Le schéma doit également être activé pour [!DNL Profile] et s’afficher dans le cadre du schéma d’union pour la classe de schéma.

Pour plus d’informations sur les [!DNL Profile] schémas et schémas d’union activés, consultez le [[!DNL Schema Registry] guide de l’API](../../xdm/api/overview.md) et la [documentation de base sur la composition des schémas](../../xdm/schema/composition.md).

**Format d’API**

```http
POST /tenants/schemas
```

**Requête**

La requête suivante crée un nouveau schéma qui référence la balise `computedAttributesFieldGroup` créée précédemment dans ce document (à l’aide de son identifiant unique) et est activée pour le schéma d’union Profile (à l’aide du tableau `meta:immutableTags`). Pour obtenir des instructions détaillées sur la création d’un schéma à l’aide de l’API Schema Registry, consultez le [guide de point de terminaison de l’API des schémas](../../xdm/api/schemas.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Schema",
        "meta:extensible": false,
        "meta:abstract": false,
        "meta:immutableTags": [
          "union"
        ],
        "meta:extends": [
          "https://ns.adobe.com/xdm/context/profile",
          "https://ns.adobe.com/xdm/context/identitymap",
          "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
        ],
        "description": "Description of schema.",
        "definitions": {
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
          },
          {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
          },
          {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
          }
        ],
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
      }' 
```

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Créé) et un payload qui contient les détails du schéma créé, y compris le `$id`, l’`meta:altId` et la `version`. Ces valeurs sont en lecture seule et sont attribuées par le registre des schémas.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:altId": "_{TENANT}.schemas.699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Computed Attributes Schema",
  "type": "object",
  "description": "Description of schema.",
  "definitions": {},
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/identitymap",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612385766411,
    "repo:lastModifiedDate": 1612385766411,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "a9c6b5c25c109970ffa5eaeb3db2b47b59c696e1d9407fb39ccf7e48b74b558e",
    "meta:globalLibVersion": "1.18.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT}",
  "meta:immutableTags": [
    "union"
  ]
}
```

## Étapes suivantes

Maintenant que vous avez créé un schéma et un groupe de champs dans lesquels vos attributs calculés seront stockés, vous pouvez créer l’attribut calculé à l’aide du point d’entrée de l’API `/computedattributes`. Pour obtenir des instructions détaillées sur la création d’un attribut calculé dans l’API, suivez les étapes fournies dans le [guide de point d’entrée de l’API des attributs calculés](ca-api.md).
