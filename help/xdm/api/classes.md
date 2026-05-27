---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre de classes;registre de schémas;classe;classe;classes;classes;créer
solution: Experience Platform
title: Point d’entrée de l’API Classes
description: Le point d’entrée /classes de l’API Schema Registry vous permet de gérer les classes XDM par programmation dans votre application d’expérience.
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
TQID: https://experienceleague.adobe.com/4nnZ3Opf259QCj1n-1VfZmOifXUzEB5SPyDvIUHRhCA
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 1524
ht-degree: 21%

---

# Point d’entrée des classes

Tous les schémas de modèle de données d’expérience (XDM) doivent être basés sur une classe . Une classe détermine la structure de base des propriétés communes que tous les schémas basés sur cette classe doivent contenir, ainsi que les groupes de champs de schéma éligibles à l’utilisation dans ces schémas. En outre, la classe d’un schéma détermine les aspects comportementaux des données qu’un schéma contiendra, qui peuvent être de deux types :

* **[!UICONTROL Record]** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **[!UICONTROL Time-series]** : fournit un instantané du système au moment où une action a été entreprise directement ou indirectement par un objet d’enregistrement.

>[!NOTE]
>
>Pour plus d’informations sur les classes de comportements de données et leur impact sur la composition des schémas, reportez-vous à la section [principes de base de la composition des schémas](../schema/composition.md).

Le point d’entrée `/classes` de l’API [!DNL Schema Registry] vous permet de gérer par programmation les classes de votre application d’expérience.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de l’API ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). [[!DNL Schema Registry] Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Récupération d’une liste de classes {#list}

Vous pouvez répertorier toutes les classes sous le conteneur `global` ou `tenant` en effectuant une requête GET à `/global/classes` ou `/tenant/classes`, respectivement.

>[!NOTE]
>
>Lors de l’énumération des ressources, le registre des schémas limite les jeux de résultats à 300 éléments. Pour renvoyer des ressources au-delà de cette limite, vous devez utiliser des paramètres de pagination. Il est également recommandé d’utiliser des paramètres de requête supplémentaires pour filtrer les résultats et réduire le nombre de ressources renvoyées. Pour plus d’informations, consultez la section sur les [paramètres de requête](./appendix.md#query) dans le document annexe.

**Format d’API**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Conteneur à partir duquel vous souhaitez récupérer des classes : `global` pour les classes créées par Adobe ou `tenant` pour les classes appartenant à votre organisation. |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs en fonction desquels filtrer les résultats. Voir le [document annexe](./appendix.md#query) pour obtenir une liste des paramètres disponibles. |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère une liste de classes à partir du conteneur de `tenant`, à l’aide d’un paramètre de requête `orderby` pour trier les classes en fonction de leur attribut `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Le format de la réponse dépend de l’en-tête `Accept` envoyé dans la requête. Les en-têtes `Accept` suivants sont disponibles pour répertorier les classes :

| En-tête `Accept` | Description |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Renvoie un bref résumé de chaque ressource. Il s’agit de l’en-tête recommandé pour répertorier les ressources. (Limite : 300) |
| `application/vnd.adobe.xed+json` | Renvoie une classe JSON complète pour chaque ressource, avec les `$ref` et `allOf` d’origine inclus. (Limite : 300) |

{style="table-layout:auto"}

**Réponse**

La requête ci-dessus a utilisé l’en-tête `application/vnd.adobe.xed-id+json` `Accept`. Par conséquent, la réponse inclut uniquement les attributs `title`, `$id`, `meta:altId` et `version` pour chaque classe. L’utilisation de l’autre en-tête `Accept` (`application/vnd.adobe.xed+json`) renvoie tous les attributs de chaque classe. Sélectionnez l’en-tête de `Accept` approprié en fonction des informations dont vous avez besoin dans votre réponse.

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

## Recherche d’une classe {#lookup}

Vous pouvez rechercher une classe spécifique en incluant l’identifiant de la classe dans le chemin d’accès d’une requête GET.

**Format d’API**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Conteneur qui contient la classe à récupérer : `global` pour une classe créée par Adobe ou `tenant` pour une classe appartenant à votre organisation. |
| `{CLASS_ID}` | `$id` codée en `meta:altId` ou en URL de la classe que vous souhaitez rechercher. |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère une classe en fonction de sa valeur `meta:altId` fournie dans le chemin d’accès .

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Le format de la réponse dépend de l’en-tête `Accept` envoyé dans la requête. Toutes les requêtes de recherche nécessitent qu’un `version` soit inclus dans l’en-tête `Accept`. Les en-têtes `Accept` suivants sont disponibles :

| En-tête `Accept` | Description |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Brut avec `$ref` et `allOf`, contient des titres et des descriptions. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` et `allOf` résolus, contient des titres et des descriptions. |
| `application/vnd.adobe.xed-notext+json; version=1` | Brut avec `$ref` et `allOf`, ne contient aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` et `allOf` résolus, ne contient aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` et `allOf` résolus, contient des descripteurs. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails de la classe . Les champs renvoyés dépendent de l’en-tête `Accept` envoyé dans la requête. Testez différents en-têtes `Accept` pour comparer les réponses et déterminer l’en-tête le mieux adapté à votre cas d’utilisation.

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
  "imsOrg":"{ORG_ID}",
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

Vous pouvez définir une classe personnalisée sous le conteneur `tenant` en effectuant une requête POST.

>[!IMPORTANT]
>
>Lors de la composition d’un schéma basé sur une classe personnalisée que vous définissez, vous ne pourrez pas utiliser de groupes de champs standard. Chaque groupe de champs définit les classes avec lesquelles ils sont compatibles dans leur attribut `meta:intendedToExtend`. Une fois que vous avez commencé à définir des groupes de champs compatibles avec votre nouvelle classe (en utilisant la `$id` de votre nouvelle classe dans le champ `meta:intendedToExtend` du groupe de champs ), vous pourrez réutiliser ces groupes de champs chaque fois que vous définissez un schéma qui implémente la classe que vous avez définie. Pour plus d’informations](./field-groups.md#create) reportez-vous aux sections [création de groupes de champs et [création de schémas](./schemas.md#create) dans leurs guides de point d’entrée respectifs.
>
>Si vous prévoyez d’utiliser des schémas basés sur des classes personnalisées dans le profil client en temps réel, il est également important de garder à l’esprit que les schémas d’union ne sont construits que sur la base de schémas partageant la même classe. Si vous souhaitez inclure un schéma de classe personnalisée dans l’union pour une autre classe telle que [!UICONTROL XDM Individual Profile] ou [!UICONTROL XDM ExperienceEvent], vous devez établir une relation avec un autre schéma qui utilise cette classe. Pour plus d’informations, consultez le tutoriel sur [l’établissement d’une relation entre deux schémas dans l’API](../tutorials/relationship-api.md).

**Format d’API**

```http
POST /tenant/classes
```

**Requête**

La requête de création (POST) d’une classe doit inclure un attribut `allOf` contenant un `$ref` d’une de ces deux valeurs : `https://ns.adobe.com/xdm/data/record` ou `https://ns.adobe.com/xdm/data/time-series`. Ces valeurs représentent le comportement sur lequel la classe est basée (enregistrement ou série temporelle, respectivement). Pour plus d’informations sur les différences entre les données d’enregistrement et les données de série temporelle, consultez la section sur les types de comportements dans les [principes de base de la composition des schémas](../schema/composition.md).

Lorsque vous définissez une classe, vous pouvez également inclure des groupes de champs ou des champs personnalisés dans la définition de classe. Cela entraîne l’inclusion des groupes de champs et des champs ajoutés dans tous les schémas qui implémentent la classe . L’exemple de requête suivant définit une classe intitulée « Propriété » qui capture les informations concernant différentes propriétés détenues et exploitées par une société. Elle inclut un champ `propertyId` à ajouter chaque fois que la classe est utilisée.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `_{TENANT_ID}` | L’espace de noms `TENANT_ID` pour votre organisation. Toutes les ressources créées par votre organisation doivent inclure cette propriété pour éviter les conflits avec d’autres ressources du [!DNL Schema Registry]. |
| `allOf` | Une liste des ressources dont les propriétés doivent être héritées par la nouvelle classe. L’un des objets `$ref` au sein du tableau définit le comportement de la classe. Dans cet exemple, la classe hérite du comportement « enregistrement ». |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Created) et un payload contenant les détails de la classe que vous venez de créer, notamment `$id`, `meta:altId` et `version`. Ces trois valeurs sont en lecture seule et sont attribuées par le [!DNL Schema Registry].

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
  "imsOrg": "{ORG_ID}",
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

L’exécution d’une requête GET pour [répertorier toutes les classes](#list) dans le conteneur de `tenant` inclut désormais la classe Property. Vous pouvez également [effectuer une requête de recherche (GET)](#lookup) à l’aide du `$id` codé URL pour afficher directement la nouvelle classe.

## Mise à jour d’une classe {#put}

Vous pouvez remplacer une classe entière par une opération PUT, ce qui revient essentiellement à réécrire la ressource. Lors de la mise à jour d’une classe par le biais d’une requête PUT, le corps doit inclure tous les champs qui sont requis lors de la [création d’une classe](#create) dans une requête POST.

>[!NOTE]
>
>Si vous ne souhaitez mettre à jour qu’une partie d’une classe au lieu de la remplacer entièrement, consultez la section sur la [mise à jour d’une partie d’une classe](#patch).

**Format d’API**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CLASS_ID}` | `$id` codée en `meta:altId` ou en URL de la classe que vous souhaitez réécrire. |

{style="table-layout:auto"}

**Requête**

La requête suivante réécrit une classe existante, modifiant son `description` et la `title` de l’un de ses champs.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  "imsOrg": "{ORG_ID}",
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

## Mise à jour d’une partie d’une classe {#patch}

Vous pouvez mettre à jour une partie d’une classe à l’aide d’une requête PATCH. Le [!DNL Schema Registry] prend en charge toutes les opérations standard JSON Patch, notamment `add`, `remove` et `replace`. Pour plus d’informations sur le correctif JSON, voir [Guide de base des API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Si vous souhaitez remplacer une ressource entière par de nouvelles valeurs au lieu de mettre à jour des champs individuels, consultez la section sur le [remplacement d’une classe à l’aide d’une opération PUT](#put).

**Format d’API**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{CLASS_ID}` | L’URI `$id` encodé URL ou le `meta:altId` de la classe que vous souhaitez mettre à jour. |

{style="table-layout:auto"}

**Requête**

L’exemple de requête ci-dessous met à jour la `description` d’une classe existante et la `title` de l’un de ses champs.

Le corps de la requête se présente sous la forme d’un tableau, où chaque objet répertorié représente une modification spécifique apportée à un champ individuel. Chaque objet inclut l’opération à effectuer (`op`), le champ sur lequel l’opération doit être effectuée (`path`) et les informations à inclure dans cette opération (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**Réponse**

La réponse montre que les deux opérations ont été réalisées avec succès. La `description` a été mise à jour, ainsi que la `title` du champ `propertyId` .

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
  "imsOrg": "{ORG_ID}",
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

## Suppression d’une classe {#delete}

Il peut parfois être nécessaire de supprimer une classe du registre des schémas. Pour ce faire, il suffit d’effectuer une requête DELETE avec l’identifiant de classe fourni dans le chemin d’accès .

**Format d’API**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CLASS_ID}` | L’URI de `$id` codé URL ou le `meta:altId` de la classe que vous souhaitez supprimer. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un statut HTTP 204 (Pas de contenu) et un corps vide.

Vous pouvez confirmer la suppression en tentant d’exécuter une [requête de recherche (GET)](#lookup) pour la classe . Vous devez inclure un en-tête `Accept` dans la requête, mais vous devriez recevoir le statut HTTP 404 (Not Found), car la classe a été supprimée du registre des schémas.
