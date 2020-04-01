---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Définir une relation entre deux  à l''aide de l''API de Registre '
topic: tutorials
translation-type: tm+mt
source-git-commit: 7e867ee12578f599c0c596decff126420a9aca01

---


# Définir une relation entre deux  à l&#39;aide de l&#39;API de Registre 


La capacité de comprendre les relations entre vos clients et leurs interactions avec votre marque dans divers  de est un élément important d’Adobe Experience Platform. La définition de ces relations au sein de la structure de votre de modèle de données d’expérience (XDM) vous permet d’obtenir des informations complexes sur vos données client.

Ce fournit un didacticiel pour la définition d’une relation de type &quot;un à un&quot; entre deux  définis par votre organisation à l’aide de l’API [de registre de l’](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)des .

## Prise en main

Ce didacticiel nécessite une compréhension pratique du modèle de données d’expérience (XDM) et du système XDM. Avant de commencer ce didacticiel, consultez la documentation suivante :

* [Système XDM dans la plate-forme](../home.md)d’expérience : Présentation de XDM et de son implémentation dans la plateforme d’expérience.
   * [Principes de base de la composition](../schema/composition.md)de  : Présentation des blocs de création de  XDM.
* [](../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
* [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Avant de commencer ce didacticiel, veuillez consulter le guide [du](../api/getting-started.md) développeur pour obtenir des informations importantes que vous devez connaître afin d&#39;effectuer des appels vers l&#39;API de Registre du . Cela inclut votre `{TENANT_ID}`, le concept de &quot;&quot; et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accept et à ses valeurs possibles).

## Définition d’un source et de destination {#define-schemas}

Vous devez avoir déjà créé les deux  de qui seront définies dans la relation. Ce didacticiel crée une relation entre les membres de l&#39;actuel de fidélité d&#39;une organisation (défini dans un &quot;Membres de fidélité&quot;) et leurs hôtels préférés (défini dans un &quot;Hôtels&quot;).

Les relations de  sont représentées par un **source** ayant un champ qui fait référence à un autre champ dans une **destination**. Dans les étapes qui suivent, &quot;Membres de la Fidélité&quot; sera la source du , tandis que &quot;Hôtels&quot; agira comme de destination .

Pour définir une relation entre deux  de, vous devez d’abord acquérir les `$id` valeurs des deux  de. Si vous connaissez les noms d’affichage (`title`) du  de, vous pouvez trouver leurs `$id` valeurs en envoyant une requête GET au `/tenant/schemas` point de terminaison dans l’API de Registre de.

**Format API**

```http
GET /tenant/schemas
```

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE] L’en-tête Accepter `application/vnd.adobe.xed-id+json` renvoie uniquement les titres, les ID et les versions du résultant.

**Réponse**

Une réponse réussie renvoie un  de  défini par votre organisation, y compris leur `name`, `$id`, `meta:altId`et `version`.

```json
{
    "results": [
        {
            "title": "Newsletter Subscriptions",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/192a66930afad02408429174c311ae73",
            "meta:altId": "_{TENANT_ID}.schemas.192a66930afad02408429174c311ae73",
            "version": "1.2"
        },
        {
            "title": "Loyalty Members",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
            "version": "1.5"
        },
        {
            "title": "Hotels",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
            "meta:altId": "_{TENANT_ID}.schemas.d4ad4b8463a67f6755f2aabbeb9e02c7",
            "version": "1.0"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform-stage.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

Enregistrez les `$id` valeurs des deux  vous souhaitez définir une relation entre eux. Ces valeurs seront utilisées ultérieurement.

## Définition des champs de référence pour les deux  de

Dans le registre des  de, les descripteurs de relation fonctionnent de la même manière que les clés étrangères dans les tables SQL : un champ dans le source agit comme une référence à un champ d’un  de destination. Lors de la définition d’une relation, chaque  d’doit disposer d’un champ dédié à utiliser comme référence à l’autre  de.

>[!IMPORTANT] Si le  de destination doit être activé pour une utilisation dans le [Client en temps](../../profile/home.md)réel, le champ de référence du **de destination doit être son identité** principale. Ce didacticiel explique plus en détail ce problème plus loin.

Si l’un des  n’a pas de champ à cet effet, vous devrez peut-être créer un mixin avec le nouveau champ et l’ajouter au  de. Ce nouveau champ doit avoir la `type` valeur &quot;string&quot;.

Pour les besoins de ce didacticiel, le de destination  &quot;Hôtels&quot; contient déjà un champ à cet effet : `hotelId`. Toutefois, le source  &quot;Membres de la loyauté&quot; n&#39;a pas de champ de ce type et doit se voir attribuer un nouveau mixin qui ajoute un nouveau champ, `favoriteHotel`, sous son `TENANT_ID` .

### Création d’un mixin

Pour ajouter un nouveau champ à un , il doit d’abord être défini dans un mixin. Vous pouvez créer un nouveau mixin en envoyant une requête POST au point de `/tenant/mixins` fin.

**Format API**

```http
POST /tenant/mixins
```

**Requête**

La requête suivante crée un nouveau mixin qui ajoute un `favoriteHotel` `TENANT_ID` champ sous le  de  de tout auquel il est ajouté.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel mixin for the Loyalty Members schema.",
        "definitions": {
            "favoriteHotel": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "favoriteHotel": {
                      "title": "Favorite Hotel",
                      "type": "string",
                      "description": "Favorite hotel for a Loyalty Member."
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
              "$ref": "#/definitions/favoriteHotel"
            }
        ]
      }'
```

**Réponse**

Une réponse réussie renvoie les détails du nouveau mixin.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220",
    "meta:altId": "_{TENANT_ID}.mixins.3387945212ad76ee59b6d2b964afb220",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "type": "object",
    "title": "Favorite Hotel",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Favorite hotel mixin for the Loyalty Members schema.",
    "definitions": {
        "favoriteHotel": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "favoriteHotel": {
                            "title": "Favorite Hotel",
                            "type": "string",
                            "description": "Favorite hotel for a Loyalty Member.",
                            "meta:xdmType": "string"
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
            "$ref": "#/definitions/favoriteHotel"
        }
    ],
    "meta:xdmType": "object",
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:registryMetadata": {
        "eTag": "quM2aMPyb2NkkEiZHNCs/MG34E4=",
        "palm:sandboxName": "prod"
    }
}
```

| Propriété | Description |
| --- | --- |
| `$id` | Le système générait un identifiant unique du nouveau mixin en lecture seule. Prend la forme d’un URI. |

Enregistrez l’ `$id` URI du mixin, à utiliser lors de l’étape suivante de l’ajout du mixin au source.

### Ajouter le mixin dans le source 

Une fois que vous avez créé un mixin, vous pouvez l’ajouter au source en faisant une requête PATCH au `/tenant/schemas/{SCHEMA_ID}` point de fin.

**Format API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | URI codé en URL `$id` ou `meta:altId` du source. |

**Requête**

La requête suivante ajoute le mixin &quot;Hôtel préféré&quot; au  &quot;Membres de la Fidélité&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    { 
      "op": "add", 
      "path": "/allOf/-", 
      "value":  {
        "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
      }
    }
  ]'
```

| Propriété | Description |
| --- | --- |
| `op` | Opération PATCH à effectuer. Cette requête utilise l’ `add` opération. |
| `path` | Chemin d’accès au champ de  du dans lequel la nouvelle ressource sera ajoutée. Lors de l’ajout de mixins aux , la valeur doit être `/allOf/-`. |
| `value.$ref` | Le `$id` mixin à ajouter. |

**Réponse**

Une réponse réussie renvoie les détails de la  mise à jour, qui inclut désormais la `$ref` valeur du mixin ajouté sous sa `allOf` matrice.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
    "meta:resourceType": "schemas",
    "version": "1.1",
    "type": "object",
    "title": "Loyalty Members",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
        }
    ],
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:tenantNamespace": "_{TENANT_ID}",
    "imsOrg": "{IMS_ORG}",
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3",
        "https://ns.adobe.com/{TENANT_ID}/mixins/61969bc646b66a6230a7e8840f4a4d33"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557525483804,
        "repo:lastModifiedDate": 1566419670915,
        "xdm:createdClientId": "{API_KEY}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "eTag": "ITNzu8BVTO5pw9wfCtTTpk6U4WY="
    }
}
```

## Définition des champs d&#39;identité principaux pour les deux 

>[!NOTE] Cette étape n’est requise que pour les  qui seront activés pour une utilisation dans le [client en temps](../../profile/home.md)réel. Si vous ne souhaitez pas que l’un ou l’autre des participe à un  de, ou si vos identités primaires sont déjà définies pour votre [, vous pouvez passer à l’étape suivante de la](#create-descriptor) création d’un descripteurd’identité de référence pour le de destination.

Pour que les  soient activés pour une utilisation dans le client en temps réel, une identité principale doit être définie. En outre, le de destination d’une relation doit utiliser son identité principale comme champ de référence.

Aux fins de ce didacticiel, l&#39; source a déjà une identité principale définie, mais pas l&#39; de destination. Vous pouvez marquer un champ de  de comme champ d’identité principal en créant un descripteur d’identité. Pour ce faire, vous devez envoyer une requête POST au point de `/tenant/descriptors` fin.

**Format API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante crée un nouveau descripteur d’identité qui définit le `hotelId` champ du de destination  &quot;Hôtels&quot; comme champ d’identité principal.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true
  }'
```

| Paramètre | Description |
| --- | --- |
| `@type` | Type de descripteur à créer. La `@type` valeur des descripteurs d’identité est `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | Valeur du  de destination, obtenue à l’étape `$id` [](#define-schemas)précédente. |
| `xdm:sourceVersion` | Numéro de version du . |
| `sourceProperty` | Chemin d’accès au champ spécifique qui servira d’identité  principale du. Ce chemin d’accès doit commencer par un &quot;/&quot; et ne pas se terminer par un, tout en excluant les &quot;propriétés&quot;   de. Par exemple, la requête ci-dessus utilise `/_{TENANT_ID}/hotelId` au lieu de `/properties/_{TENANT_ID}/properties/hotelId`. |
| `xdm:namespace` | L’identité  le  du champ d’identité. `hotelId` est une valeur ECID dans cet exemple. Par conséquent, le &quot;ECID&quot;  est utilisé. Pour obtenir un de l’ensemble [des](../../identity-service/home.md) desdisponibles, reportez-vous à la section Identité  vue d’ensemble du. |
| `xdm:isPrimary` | Propriété booléenne déterminant si le champ d’identité sera l’identité principale du . Puisque cette requête définit une identité principale, la valeur est définie sur true. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau descripteur d’identité créé.

```json
{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true,
    "meta:containerId": "tenant",
    "@id": "e3cfa302d06dc27080e6b54663511a02dd61316f"
}
```

## Création d’un descripteur d’identité de référence

Un descripteur d’identité de référence doit être appliqué aux champs  de référence s’ils sont utilisés comme référence par d’autres  dans une relation. Puisque le `favoriteHotel` champ &quot;Membres de la loyauté&quot; renvoie au `hotelId` champ &quot;Hôtels&quot;, `hotelId` doit recevoir un descripteur d&#39;identité de référence.

Créez un descripteur de référence pour le de destination en envoyant une requête POST au point de `/tenant/descriptors` fin.

**Format API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante crée un descripteur de référence pour le `hotelId` champ du de destination &quot;Hôtels&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID"
  }'
```

| Paramètre | Description |
| --- | --- |
| `xdm:sourceSchema` | URL `$id` du de destination . |
| `xdm:sourceVersion` | Numéro de version du de destination. |
| `sourceProperty` | Chemin d’accès au champ d’identité principal du de destination . |
| `xdm:identityNamespace` | L’identité  le  du champ de référence. `hotelId` est une valeur ECID dans cet exemple. Par conséquent, le &quot;ECID&quot;  est utilisé. Pour obtenir un de l’ensemble [des](../../identity-service/home.md) desdisponibles, reportez-vous à la section Identité  vue d’ensemble du. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau descripteur de référence créé pour le de destination.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Création d’un descripteur de relation {#create-descriptor}

Les descripteurs de relation établissent une relation de type &quot;un à un&quot; entre un  source et un  de destination. Vous pouvez créer un nouveau descripteur de relation en envoyant une requête POST au point de `/tenant/descriptors` fin.

**Format API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante crée un nouveau descripteur de relation, avec &quot;Membres de la fidélité&quot; comme source et &quot;Membres de la fidélité héritée&quot; comme de destination.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| Paramètre | Description |
| --- | --- |
| `@type` | Type de descripteur à créer. La `@type` valeur des descripteurs de relation est `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | URL `$id` du source. |
| `xdm:sourceVersion` | Numéro de version du source. |
| `sourceProperty` : | Chemin d’accès au champ de référence dans le  source. |
| `xdm:destinationSchema` | URL `$id` du de destination . |
| `xdm:destinationVersion` | Numéro de version du de destination. |
| `destinationProperty` : | Chemin d’accès au champ de référence dans le  de destination. |

### Réponse

Une réponse réussie renvoie les détails du nouveau descripteur de relation.

```json
{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId",
    "meta:containerId": "tenant",
    "@id": "76f6cc7105f4eaab7eb4a5e1cb4804cadc741669"
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à créer une relation de type &quot;un à un&quot; entre deux  de. Pour plus d&#39;informations sur l&#39;utilisation de descripteurs à l&#39;aide de l&#39;API de Registre , consultez le guide [du développeur du Registre de](../api/getting-started.md). Pour savoir comment définir les relations  dans l’interface utilisateur, consultez le didacticiel sur la [définition des relations  à l’aide de l’éditeur](relationship-ui.md)de  dedonnées.