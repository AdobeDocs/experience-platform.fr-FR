---
keywords: Experience Platform ; accueil ; rubriques populaires ; api ; API ; XDM ; système XDM ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données ; modèle de données ; modèle de données ; registre de classes ; registre de Schémas ; classe ; classes ; classes ; créer
solution: Experience Platform
title: Point de terminaison de l'API Classes
description: Le point de terminaison /classes de l'API Schéma Registry vous permet de gérer par programmation les classes XDM dans votre application d'expérience.
topic-legacy: developer guide
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 23%

---

# Point de terminaison des classes

Tous les schémas de modèle de données d’expérience (XDM) doivent être basés sur une classe. Une classe détermine la structure de base des propriétés communes que tous les schémas basés sur cette classe doivent contenir, ainsi que les mixins qui peuvent être utilisés dans ces schémas. En outre, une classe de schéma détermine les aspects comportementaux des données qu&#39;un schéma contiendra, dont il existe deux types :

* **[!UICONTROL Enregistrer]** : Fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **[!UICONTROL Série]** chronologique : Fournit un instantané du système au moment où une action a été entreprise directement ou indirectement par un sujet d&#39;enregistrement.

>[!NOTE]
>
>Pour plus d&#39;informations sur les comportements des données en termes d&#39;impact sur la composition des schémas, consultez les [bases de la composition des schémas](../schema/composition.md).

Le point de terminaison `/classes` de l&#39;API [!DNL Schema Registry] vous permet de gérer par programmation les classes dans votre application d&#39;expérience.

## Prise en main

Le point de terminaison utilisé dans ce guide fait partie de l&#39;[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation connexe, un guide de lecture des exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API Experience Platform.

## Récupérer une liste de classes {#list}

Vous pouvez liste toutes les classes sous le conteneur `global` ou `tenant` en adressant une demande de GET à `/global/classes` ou `/tenant/classes`, respectivement.

>[!NOTE]
>
>Lors de la mise en vente de ressources, le Registre des Schémas limite les résultats à 300 éléments. Pour renvoyer des ressources au-delà de cette limite, vous devez utiliser des paramètres de pagination. Il est également recommandé d’utiliser des paramètres de requête supplémentaires pour filtrer les résultats et réduire le nombre de ressources renvoyées. Pour plus d&#39;informations, consultez la section [Paramètres de requête](./appendix.md#query) dans le document de l&#39;annexe.

**Format d’API**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Conteneur à partir duquel vous souhaitez récupérer des classes : `global` pour les classes créées par Adobe ou `tenant` pour les classes détenues par votre organisation. |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs en fonction desquels filtrer les résultats. Pour obtenir une liste des paramètres disponibles, consultez l&#39;[document ](./appendix.md#query) de l&#39;appendice. |

**Requête**

La requête suivante récupère une liste de classes du conteneur `tenant`, en utilisant un paramètre de requête `orderby` pour trier les classes selon leur attribut `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Le format de réponse dépend de l&#39;en-tête `Accept` envoyé dans la demande. Les en-têtes `Accept` suivants sont disponibles pour répertorier les classes :

| En-tête `Accept` | Description |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Renvoie un bref résumé de chaque ressource. Il s’agit de l’en-tête recommandé pour la liste des ressources. (Limite : 300) |
| `application/vnd.adobe.xed+json` | Renvoie la classe JSON complète pour chaque ressource, avec les valeurs d’origine `$ref` et `allOf` incluses. (Limite : 300) |

**Réponse**

La requête ci-dessus utilisait l&#39;en-tête `application/vnd.adobe.xed-id+json` `Accept`. Par conséquent, la réponse ne comprend que les attributs `title`, `$id`, `meta:altId` et `version` pour chaque classe. L&#39;utilisation de l&#39;autre en-tête `Accept` (`application/vnd.adobe.xed+json`) renvoie tous les attributs de chaque classe. Sélectionnez l&#39;en-tête `Accept` approprié en fonction des informations que vous souhaitez obtenir dans votre réponse.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
      "meta:altId": "_{TENANT_ID}.classes.01b7b1745e8ac4ed1e8784ec91b6afa7",
      "version": "1.0",
      "title": "Hotel"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/d43b86253676af50da3f671ecdd26ff9",
      "meta:altId": "_{TENANT_ID}.classes.d43b86253676af50da3f671ecdd26ff9",
      "version": "1.1",
      "title": "Property"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/366f015dbfea802455fbc46c3b27f771",
      "meta:altId": "_{TENANT_ID}.classes.366f015dbfea802455fbc46c3b27f771",
      "version": "1.0",
      "title": "Subscription"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/classes"
    }
  }
}
```

## Rechercher une classe {#lookup}

Vous pouvez rechercher une classe spécifique en incluant son identifiant dans le chemin d&#39;une demande de GET.

**Format d’API**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Conteneur qui héberge la classe que vous souhaitez récupérer : `global` pour une classe créée par un Adobe ou `tenant` pour une classe appartenant à votre organisation. |
| `{CLASS_ID}` | `meta:altId` ou `$id` de la classe que vous souhaitez rechercher, codés URL. |

**Requête**

La requête suivante récupère une classe par sa valeur `meta:altId` fournie dans le chemin d&#39;accès.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Le format de réponse dépend de l&#39;en-tête `Accept` envoyé dans la demande. Toutes les requêtes de recherche nécessitent l&#39;inclusion de `version` dans l&#39;en-tête `Accept`. Les en-têtes `Accept` suivants sont disponibles :

| En-tête `Accept` | Description |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Brut avec `$ref` et `allOf`, contient des titres et des descriptions. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` et `allOf` résolus, contient des titres et des descriptions. |
| `application/vnd.adobe.xed-notext+json; version=1` | Brut avec `$ref` et `allOf`, ne contient aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` et `allOf` résolus, ne contient aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` et `allOf` résolus, contient des descripteurs. |

**Réponse**

Une réponse réussie renvoie les détails de la classe. Les champs renvoyés dépendent de l&#39;en-tête `Accept` envoyé dans la demande. Testez différents en-têtes `Accept` pour comparer les réponses et déterminer l&#39;en-tête qui convient le mieux à votre cas d&#39;utilisation.

```json
{
  "$id":"https://ns.adobe.com/{TENANT_ID}/classes/f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:altId":"_{TENANT_ID}.classes.f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:resourceType":"classes",
  "version":"1.1",
  "title":"Hotel",
  "type":"object",
  "description":"Base class for the Hotels schema",
  "definitions":{
    "customFields":{
      "type":"object",
      "properties":{
        "_{TENANT_ID}":{
          "type":"object",
          "properties":{
            "Address":{
              "title":"Address",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/common/address",
              "type":"object",
              "meta:xdmType":"object"
            },
            "phoneNumber":{
              "title":"Phone Number",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/context/phonenumber",
              "type":"object",
              "meta:xdmType":"object"
            },
            "brand":{
              "title":"Brand",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            },
            "hotelId":{
              "title":"Hotel ID",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            }
          },
          "meta:xdmType":"object"
        }
      },
      "meta:xdmType":"object"
    }
  },
  "allOf":[
    {
      "$ref":"https://ns.adobe.com/xdm/data/record",
      "type":"object",
      "meta:xdmType":"object"
    },
    {
      "$ref":"#/definitions/customFields",
      "type":"object",
      "meta:xdmType":"object"
    }
  ],
  "imsOrg":"{IMS_ORG}",
  "meta:extensible":true,
  "meta:abstract":true,
  "meta:extends":[
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:xdmType":"object",
  "meta:registryMetadata":{
    "repo:createdDate":1593643258779,
    "repo:lastModifiedDate":1597246362579,
    "xdm:createdClientId":"{CLIENT_ID}",
    "xdm:lastModifiedClientId":"{CLIENT_ID}",
    "xdm:createdUserId":"{USER_ID}",
    "xdm:lastModifiedUserId":"{USER_ID}",
    "eTag":"502f89ee16b8ab2e6b4ea09ecf0ab1e5614907db755051c1f3c65a273001d725",
    "meta:globalLibVersion":"1.15.4"
  },
  "meta:containerId":"tenant",
  "meta:tenantNamespace":"_{TENANT_ID}"
}
```

## Création d’une classe {#create}

Vous pouvez définir une classe personnalisée sous le conteneur `tenant` en faisant une demande de POST.

>[!IMPORTANT]
>
>Lors de la composition d’un schéma basé sur une classe personnalisée que vous définissez, vous ne pourrez pas utiliser de mixins standard. Chaque mixin définit les classes avec lesquelles il est compatible dans l’attribut `meta:intendedToExtend`. Lorsque vous commencez à définir des mixins compatibles avec votre nouvelle classe (en utilisant le `$id` de votre nouvelle classe dans le champ `meta:intendedToExtend` du mixin), vous pourrez réutiliser ces mixins chaque fois que vous définissez un schéma qui met en œuvre la classe que vous avez définie. Pour plus d’informations, consultez les sections [création de mixins](./mixins.md#create) et [création de schémas](./schemas.md#create) dans leurs guides de points de terminaison respectifs.
>
>Si vous prévoyez d’utiliser des schémas basés sur des classes personnalisées dans le Profil client en temps réel, il est également important de garder à l’esprit que les schémas d’union ne sont construits que sur la base de schémas partageant la même classe. Si vous souhaitez inclure un schéma de classe personnalisée dans l&#39;union pour une autre classe telle que [!UICONTROL XDM Profil individuel] ou [!UICONTROL XDM ExperienceEvent], vous devez établir une relation avec un autre schéma qui emploie cette classe. Pour plus d&#39;informations, consultez le didacticiel [établissant une relation entre deux schémas dans l&#39;API](../tutorials/relationship-api.md).

**Format d’API**

```http
POST /tenant/classes
```

**Requête**

La requête de création (POST) d’une classe doit inclure un attribut `allOf` contenant un `$ref` d’une de ces deux valeurs : `https://ns.adobe.com/xdm/data/record` ou `https://ns.adobe.com/xdm/data/time-series`. Ces valeurs représentent le comportement sur lequel la classe est basée (enregistrement ou série temporelle, respectivement). Pour plus d’informations sur les différences entre les données d’enregistrement et les données de série temporelle, consultez la section sur les types de comportements dans les [principes de base de la composition des schémas](../schema/composition.md).

Lorsque vous définissez une classe, vous pouvez également inclure des mixins ou des champs personnalisés au sein de la définition de la classe. De cette manière, les mixins et les champs ajoutés seront inclus dans tous les schémas qui mettent en œuvre la classe. L’exemple de requête suivant définit une classe intitulée « Propriété » qui capture les informations concernant différentes propriétés détenues et exploitées par une société. Elle inclut un champ `propertyId` à ajouter chaque fois que la classe est utilisée.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| Propriété | Description |
| --- | --- |
| `_{TENANT_ID}` | L’espace de noms `TENANT_ID` pour votre organisation. Toutes les ressources créées par votre organisation doivent inclure cette propriété pour éviter toute collision avec d&#39;autres ressources dans [!DNL Schema Registry]. |
| `allOf` | Une liste des ressources dont les propriétés doivent être héritées par la nouvelle classe. L’un des objets `$ref` au sein du tableau définit le comportement de la classe. Dans cet exemple, la classe hérite du comportement « enregistrement ». |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Created) et un payload contenant les détails de la classe que vous venez de créer, notamment `$id`, `meta:altId` et `version`. Ces trois valeurs sont en lecture seule et sont affectées par [!DNL Schema Registry].

```JSON
{
  "title": "Property",
  "description": "Properties owned and operated by the company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property Identification Number",
                  "type": "string",
                  "description": "Unique Property identification number",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

L&#39;exécution d&#39;une demande de GET à [liste de toutes les classes](#list) dans le conteneur `tenant` inclurait désormais la classe Property. Vous pouvez également [exécuter une requête de recherche (GET)](#lookup) à l&#39;aide de l&#39;URL codée `$id` pour vue directement la nouvelle classe.

## Mettre à jour une classe {#put}

Vous pouvez remplacer une classe entière par le biais d&#39;une opération de PUT, en réécrivant essentiellement la ressource. Lors de la mise à jour d&#39;une classe par le biais d&#39;une requête de PUT, le corps doit inclure tous les champs qui seraient requis lorsque [la création d&#39;une nouvelle classe](#create) dans une requête de POST.

>[!NOTE]
>
>Si vous souhaitez uniquement mettre à jour une partie d&#39;une classe au lieu de la remplacer entièrement, consultez la section [mettant à jour une partie d&#39;une classe](#patch).

**Format d’API**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CLASS_ID}` | `meta:altId` ou `$id` de la classe que vous souhaitez réécrire. |

**Requête**

La requête suivante réécrit une classe existante, en modifiant sa `description` et la `title` de l&#39;un de ses champs.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property",
        "description": "Base class for properties operated by a company.",
        "type": "object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property ID",
                        "type": "string",
                        "description": "Unique Property ID string."
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

**Réponse**

Une réponse réussie renvoie les détails de la classe mise à jour.

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## Mettre à jour une partie d&#39;une classe {#patch}

Vous pouvez mettre à jour une partie d&#39;une classe à l&#39;aide d&#39;une requête de PATCH. [!DNL Schema Registry] prend en charge toutes les opérations de correctif JSON standard, y compris `add`, `remove` et `replace`. Pour plus d’informations sur le correctif JSON, consultez le [guide des fondamentaux de l’API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Si vous souhaitez remplacer une ressource entière par de nouvelles valeurs au lieu de mettre à jour des champs individuels, reportez-vous à la section [remplacement d&#39;une classe à l&#39;aide d&#39;une opération de PUT](#put).

**Format d’API**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{CLASS_ID}` | URI `$id` ou `meta:altId` codés URL de la classe à mettre à jour. |

**Requête**

L&#39;exemple de requête ci-dessous met à jour `description` d&#39;une classe existante et `title` de l&#39;un de ses champs.

Le corps de la requête prend la forme d&#39;un tableau, chaque objet répertorié représentant une modification spécifique à un champ individuel. Chaque objet comprend l’opération à exécuter (`op`), le champ sur lequel l’opération doit être exécutée (`path`) et les informations à inclure dans cette opération (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**Réponse**

La réponse montre que les deux opérations ont été réalisées avec succès. Le `description` a été mis à jour, ainsi que le champ `title` de `propertyId`.

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## Supprimer une classe {#delete}

Il peut parfois être nécessaire de supprimer une classe du registre des Schémas. Pour ce faire, il effectue une demande de DELETE avec l’ID de classe fourni dans le chemin d’accès.

**Format d’API**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CLASS_ID}` | URI `$id` ou `meta:altId` codés URL de la classe à supprimer. |

**Requête**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.

Vous pouvez confirmer la suppression en tentant une requête de recherche [recherche (GET)](#lookup) pour la classe. Vous devez inclure un en-tête `Accept` dans la requête, mais vous devez recevoir l&#39;état HTTP 404 (Non trouvé) car la classe a été supprimée du Registre du Schéma.
