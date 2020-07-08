---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Définir une relation entre deux schémas à l'aide de l'API de registre de Schéma
topic: tutorials
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1504'
ht-degree: 2%

---


# Définir une relation entre deux schémas à l&#39;aide de l&#39;API de registre de Schéma


La capacité de comprendre les relations entre vos clients et leurs interactions avec votre marque sur différents canaux est un élément important de l&#39;Adobe Experience Platform. La définition de ces relations au sein de la structure de vos schémas de modèle de données d’expérience (XDM) vous permet d’obtenir des informations complexes sur vos données client.

Ce document fournit un didacticiel pour la définition d&#39;une relation de type &quot;un à un&quot; entre deux schémas définis par votre organisation à l&#39;aide de l&#39;API [de registre des](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)Schémas.

## Prise en main

Ce didacticiel nécessite une bonne compréhension du modèle de données d’expérience (XDM) et du système XDM. Avant de commencer ce didacticiel, consultez la documentation suivante :

* [Système XDM en Experience Platform](../home.md): Présentation de XDM et de son implémentation en Experience Platform.
   * [Principes de base de la composition](../schema/composition.md)des schémas : Présentation des blocs de construction des schémas XDM.
* [Profil](../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance Platform unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Avant de commencer ce didacticiel, veuillez consulter le guide [du](../api/getting-started.md) développeur pour obtenir des informations importantes que vous devez connaître pour pouvoir invoquer l&#39;API de registre de Schéma. Cela inclut votre `{TENANT_ID}`nom, le concept de &quot;conteneurs&quot; et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accepter et à ses valeurs possibles).

## Définir un schéma source et de destination {#define-schemas}

Il est prévu que vous ayez déjà créé les deux schémas qui seront définis dans la relation. Ce didacticiel crée une relation entre les membres du programme de fidélité actuel d&#39;une organisation (défini dans un schéma &quot;Membres fidèles&quot;) et leurs hôtels favoris (défini dans un schéma &quot;Hôtels&quot;).

Les relations de Schéma sont représentées par un schéma **** source dont le champ fait référence à un autre champ dans un schéma **de** destination. Dans les étapes qui suivent, &quot;Membres de la Fidélité&quot; sera le schéma source, tandis que &quot;Hôtels&quot; agira comme schéma de destination.

Pour définir une relation entre deux schémas, vous devez d’abord acquérir les `$id` valeurs des deux schémas. Si vous connaissez les noms d&#39;affichage (`title`) des schémas, vous pouvez trouver leurs `$id` valeurs en envoyant une requête GET au `/tenant/schemas` point de terminaison dans l&#39;API de registre des Schémas.

**Format d’API**

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

>[!NOTE]
>
>L’en-tête Accepter `application/vnd.adobe.xed-id+json` renvoie uniquement les titres, les ID et les versions des schémas résultants.

**Réponse**

Une réponse positive renvoie une liste de schémas définis par votre organisation, y compris leur `name`, `$id`, `meta:altId`et `version`.

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

Enregistrez les `$id` valeurs des deux schémas pour lesquels vous souhaitez définir une relation. Ces valeurs seront utilisées dans les étapes suivantes.

## Définition des champs de référence pour les deux schémas

Dans le registre des Schémas, les descripteurs de relation fonctionnent de la même manière que les clés étrangères dans les tables SQL : un champ de l’schéma source fait référence à un champ d’un schéma de destination. Lors de la définition d’une relation, chaque schéma doit disposer d’un champ dédié à utiliser comme référence à l’autre schéma.

>[!IMPORTANT]
>
>Si les schémas doivent être activés pour une utilisation dans le Profil [client en temps](../../profile/home.md)réel, le champ de référence du schéma de destination doit être son identité **** principale. Ce didacticiel vous explique plus en détail ce point.

Si l’un des schémas n’a pas de champ à cet effet, vous devrez peut-être créer un mixin avec le nouveau champ et l’ajouter au schéma. Ce nouveau champ doit avoir la `type` valeur &quot;string&quot;.

Pour les besoins de ce didacticiel, le schéma de destination &quot;Hôtels&quot; contient déjà un champ à cet effet : `hotelId`. Cependant, le schéma source &quot;Membres de la loyauté&quot; n&#39;a pas de tel champ et doit recevoir un nouveau mixin qui ajoute un nouveau champ, `favoriteHotel`, sous son `TENANT_ID` espace de nommage.

### Créer un nouveau mixin

Pour ajouter un nouveau champ à un schéma, il doit d’abord être défini dans un mixin. You can create a new mixin by making a POST request to the `/tenant/mixins` endpoint.

**Format d’API**

```http
POST /tenant/mixins
```

**Requête**

La requête suivante crée un nouveau mixin qui ajoute un `favoriteHotel` champ sous l’ `TENANT_ID` espace de nommage de tout schéma auquel il est ajouté.

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

Une réponse réussie renvoie les détails du mixin nouvellement créé.

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
| `$id` | Le système en lecture seule générait un identifiant unique du nouveau mixin. Prend la forme d’un URI. |

Enregistrez l’ `$id` URI du mixin, à utiliser à l’étape suivante de l’ajout du mixin au schéma source.

### Ajouter le mixin au schéma source

Une fois que vous avez créé un mixin, vous pouvez l’ajouter au schéma source en exécutant une requête PATCH sur le `/tenant/schemas/{SCHEMA_ID}` point de terminaison.

**Format d’API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | URI codé en URL `$id` ou `meta:altId` du schéma source. |

**Requête**

La demande suivante ajoute le mixin &quot;Hôtel favori&quot; au schéma &quot;Membres fidélité&quot;.

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
| `op` | Opération PATCH à effectuer. Cette demande utilise l’ `add` opération. |
| `path` | Chemin d&#39;accès au champ de schéma où la nouvelle ressource sera ajoutée. Lors de l’ajout de mixins aux schémas, la valeur doit être `/allOf/-`définie. |
| `value.$ref` | Le `$id` de mixin à ajouter. |

**Réponse**

Une réponse réussie renvoie les détails du schéma mis à jour, qui inclut désormais la `$ref` valeur du mixin ajouté sous sa `allOf` baie.

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

## Définition des champs d&#39;identité principaux pour les deux schémas

>[!NOTE]
>
>Cette étape n’est requise que pour les schémas qui seront activés pour une utilisation dans le Profil [client en temps](../../profile/home.md)réel. Si vous ne souhaitez pas que l&#39;un ou l&#39;autre schéma participe à une union, ou si vos schémas disposent déjà d&#39;identités primaires définies, vous pouvez passer à l&#39;étape suivante de [création d&#39;un descripteur](#create-descriptor) d&#39;identité de référence pour le schéma de destination.

Pour que les schémas puissent être activés dans le Profil client en temps réel, une identité principale doit être définie. En outre, le schéma de destination d&#39;une relation doit utiliser son identité principale comme champ de référence.

Aux fins de ce didacticiel, l&#39;schéma source a déjà une identité principale définie, mais pas l&#39;schéma de destination. Vous pouvez marquer un champ de schéma comme champ d’identité principal en créant un descripteur d’identité. Pour ce faire, vous devez envoyer une requête POST au point de `/tenant/descriptors` terminaison.

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante crée un nouveau descripteur d&#39;identité qui définit le `hotelId` champ du schéma de destination &quot;Hôtels&quot; comme champ d&#39;identité principal.

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
| `@type` | Type de descripteur à créer. La `@type` valeur des descripteurs d&#39;identité est `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | Valeur du schéma de destination, obtenue à l’étape `$id` [](#define-schemas)précédente. |
| `xdm:sourceVersion` | Numéro de version du schéma. |
| `sourceProperty` | Chemin d’accès au champ spécifique qui servira d’identité principale au schéma. Ce chemin doit commencer par un &quot;/&quot; et ne pas se terminer par un, tout en excluant les espaces de nommage de &quot;propriétés&quot;. Par exemple, la requête ci-dessus utilise `/_{TENANT_ID}/hotelId` à la place de `/properties/_{TENANT_ID}/properties/hotelId`. |
| `xdm:namespace` | espace de nommage d&#39;identité du champ d&#39;identité. `hotelId` est une valeur ECID dans cet exemple. Par conséquent, l’espace de nommage &quot;ECID&quot; est utilisé. Pour obtenir une liste des espaces de nommage disponibles, reportez-vous à la présentation [de l&#39;espace de nommage](../../identity-service/home.md) d&#39;identité. |
| `xdm:isPrimary` | Propriété booléenne déterminant si le champ d&#39;identité sera l&#39;identité principale du schéma. Dans la mesure où cette requête définit une identité principale, la valeur est définie sur true. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau descripteur d&#39;identité créé.

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

Un descripteur d’identité de référence doit être appliqué aux champs de Schéma s’ils sont utilisés comme référence par d’autres schémas dans une relation. Puisque le `favoriteHotel` champ &quot;Membres de la loyauté&quot; se réfère au `hotelId` champ &quot;Hôtels&quot;, `hotelId` doit être doté d&#39;un descripteur d&#39;identité de référence.

Créez un descripteur de référence pour le schéma de destination en envoyant une requête POST au point de `/tenant/descriptors` terminaison.

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante crée un descripteur de référence pour le `hotelId` champ du schéma de destination &quot;Hôtels&quot;.

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
| `xdm:sourceSchema` | URL `$id` du schéma de destination. |
| `xdm:sourceVersion` | Numéro de version du schéma de destination. |
| `sourceProperty` | Chemin d&#39;accès au champ d&#39;identité principal du schéma de destination. |
| `xdm:identityNamespace` | espace de nommage d&#39;identité du champ de référence. `hotelId` est une valeur ECID dans cet exemple. Par conséquent, l’espace de nommage &quot;ECID&quot; est utilisé. Pour obtenir une liste des espaces de nommage disponibles, reportez-vous à la présentation [de l&#39;espace de nommage](../../identity-service/home.md) d&#39;identité. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau descripteur de référence créé pour le schéma de destination.

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

## Créer un descripteur de relation {#create-descriptor}

Les descripteurs de relation établissent une relation individuelle entre un schéma source et un schéma de destination. You can create a new relationship descriptor by making a POST request to the `/tenant/descriptors` endpoint.

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante crée un nouveau descripteur de relation, avec &quot;Membres de la fidélité&quot; comme schéma source et &quot;Membres de la fidélité héritée&quot; comme schéma de destination.

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
| `xdm:sourceSchema` | URL `$id` du schéma source. |
| `xdm:sourceVersion` | Numéro de version du schéma source. |
| `sourceProperty` : | Chemin d’accès au champ de référence dans le schéma source. |
| `xdm:destinationSchema` | URL `$id` du schéma de destination. |
| `xdm:destinationVersion` | Numéro de version du schéma de destination. |
| `destinationProperty` : | Chemin d’accès au champ de référence dans le schéma de destination. |

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

En suivant ce didacticiel, vous avez réussi à créer une relation de type &quot;un à un&quot; entre deux schémas. Pour plus d&#39;informations sur l&#39;utilisation des descripteurs à l&#39;aide de l&#39;API Schéma Registry, consultez le guide [de développement](../api/getting-started.md)Schéma Registry. Pour savoir comment définir les relations de schéma dans l’interface utilisateur, consultez le didacticiel sur la [définition des relations de schéma à l’aide de l’éditeur](relationship-ui.md)de Schéma.