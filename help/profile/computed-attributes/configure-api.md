---
keywords: Experience Platform ; profil ; profil client en temps réel ; dépannage ; API
title: Configuration d’un champ d’attribut calculé
topic: guide
type: Documentation
description: Les attributs calculés sont des fonctions utilisées pour agrégat des données au niveau du événement en attributs au niveau du profil. Pour configurer un attribut calculé, vous devez d’abord identifier le champ dans lequel la valeur d’attribut calculé sera conservée. Ce champ peut être créé à l'aide de l'API de registre de Schéma pour définir un schéma et un mixin personnalisé qui contiendra le champ d'attribut calculé.
translation-type: tm+mt
source-git-commit: 2a4fb8af8cd29254c499bfa6bfb8b316a4834526
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 18%

---


# (Alpha) Configurez un champ d&#39;attribut calculé à l&#39;aide de l&#39;API de registre de Schéma

>[!IMPORTANT]
>
>La fonctionnalité d’attribut calculé est actuellement en alpha et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Pour configurer un attribut calculé, vous devez d’abord identifier le champ dans lequel la valeur d’attribut calculé sera conservée. Ce champ peut être créé à l&#39;aide de l&#39;API de registre de Schéma pour définir un schéma et un mixin personnalisé qui contiendra le champ d&#39;attribut calculé. Il est recommandé de créer un schéma et un mixin &quot;Attributs calculés&quot; distincts dans lesquels votre entreprise peut ajouter des attributs à utiliser comme attributs calculés. Cela permet à votre entreprise de séparer clairement le schéma d&#39;attributs calculé des autres schémas utilisés pour l&#39;assimilation de données.

Le processus de ce document décrit comment utiliser l’API de registre de Schéma pour créer un schéma &quot;Attribut calculé&quot; compatible avec le Profil qui référence un mixin personnalisé. Ce document contient un exemple de code spécifique aux attributs calculés. Pour plus d&#39;informations sur la définition des mixins et des schémas à l&#39;aide de l&#39;API, consultez le [guide de l&#39;API de registre des Schémas](../../xdm/api/overview.md).

## Création d’un mixin d’attributs calculés

Pour créer un mixin à l’aide de l’API Schéma Registry, commencez par envoyer une requête de POST au point de terminaison `/tenant/mixins` et fournissez les détails du mixin dans le corps de la requête. Pour plus d&#39;informations sur l&#39;utilisation des mixins à l&#39;aide de l&#39;API de registre de Schéma, consultez le [guide du point de terminaison de l&#39;API de mixins](../../xdm/api/mixins.md).

**Format d’API**

```http
POST /tenant/mixins
```

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "title":"Computed Attributes Mixin",
        "description":"Description of the mixin.",
        "type":"object",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "definitions": {
          "computedAttributesMixin": {
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
            "$ref": "#/definitions/computedAttributesMixin"
          }
        ]
      }'
```

| Propriété | Description |
|---|---|
| `title` | Nom du mixin que vous créez. |
| `meta:intendedToExtend` | Classe XDM avec laquelle le mixin peut être utilisé. |

**Réponse**

Une requête réussie renvoie un état de réponse HTTP 201 (Created) avec un corps de réponse qui contient les détails du nouveau mixin, y compris les clés `$id`, `meta:altIt`, et `version`. Ces valeurs sont en lecture seule et sont attribuées par le registre des schémas.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Mixin",
  "type": "object",
  "description": "Description of the mixin.",
  "definitions": {
    "computedAttributesMixin": {
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
      "$ref": "#/definitions/computedAttributesMixin",
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

## Mise à jour du mixin avec des attributs calculés supplémentaires

À mesure que davantage d’attributs calculés sont nécessaires, vous pouvez mettre à jour le mélange d’attributs calculés avec des attributs supplémentaires en exécutant une requête de PUT vers le point de terminaison `/tenant/mixins`. Cette demande requiert que vous incluiez l’identifiant unique du mixin que vous avez créé dans le chemin d’accès et tous les nouveaux champs que vous souhaitez ajouter dans le corps.

Pour plus d&#39;informations sur la mise à jour d&#39;un mixin à l&#39;aide de l&#39;API de registre de Schéma, consultez le [guide du point de terminaison de l&#39;API de mixins](../../xdm/api/mixins.md).

**Format d’API**

```http
PUT /tenant/mixins/{MIXIN_ID}
```

**Requête**

Cette demande ajoute de nouveaux champs liés aux informations `purchaseSummary`.

>[!NOTE]
>
>Lors de la mise à jour d’un mixin via une requête de PUT, le corps doit inclure tous les champs requis lors de la création d’un mixin dans une requête de POST.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Mixin",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Description of mixin.",
        "definitions": {
          "computedAttributesMixin": {
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
            "$ref": "#/definitions/computedAttributesMixin"
          }
        ]
      }'
```

**Réponse**

Une réponse réussie renvoie les détails du mixin mis à jour.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Mixin",
  "type": "object",
  "description": "Description of mixin.",
  "definitions": {
    "computedAttributesMixin": {
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
      "$ref": "#/definitions/computedAttributesMixin",
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

## Création d’un schéma compatible avec les Profils

Pour créer un schéma à l’aide de l’API de registre de Schémas, commencez par envoyer une requête de POST au point de terminaison `/tenant/schemas` et fournissez les détails du schéma dans le corps de la requête. Le schéma doit également être activé pour [!DNL Profile] et apparaître dans le schéma d&#39;union de la classe de schéma.

Pour plus d&#39;informations sur les [!DNL Profile] schémas et schémas d&#39;union activés, consultez le [[!DNL Schema Registry] guide d&#39;API](../../xdm/api/overview.md) et la [documentation de base sur la composition de schéma](../../xdm/schema/composition.md).

**Format d’API**

```http
POST /tenants/schemas
```

**Requête**

La requête suivante crée un nouveau schéma qui référence le `computedAttributesMixin` créé précédemment dans ce document (à l&#39;aide de son identifiant unique) et est activé pour le schéma d&#39;union de Profil (à l&#39;aide du tableau `meta:immutableTags`). Pour obtenir des instructions détaillées sur la création d&#39;un schéma à l&#39;aide de l&#39;API de registre de Schémas, consultez le [guide du point de terminaison de l&#39;API de schémas](../../xdm/api/schemas.md).

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

Maintenant que vous avez créé un schéma et un mixin dans lequel vos attributs calculés seront stockés, vous pouvez créer l&#39;attribut calculé à l&#39;aide du point de terminaison de l&#39;API `/computedattributes`. Pour obtenir des instructions détaillées sur la création d&#39;un attribut calculé dans l&#39;API, suivez les étapes fournies dans le guide de point de terminaison de l&#39;API [attributs calculés](ca-api.md).