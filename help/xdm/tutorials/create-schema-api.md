---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Création d’un  à l’aide de l’API de registre '
topic: tutorials
translation-type: tm+mt
source-git-commit: 5aad9fa71051a58fe1c4678553f47077d81d23fc

---


# Création d’un  à l’aide de l’API de registre 

Le Registre des  permet d’accéder à la bibliothèque  dans Adobe Experience Platform. La bibliothèque de  de contient les ressources mises à votre disposition par Adobe, les partenaires Experience Platform et les fournisseurs dont vous utilisez les applications. Le registre fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les ressources de bibliothèque disponibles sont accessibles.

Ce didacticiel utilise l&#39;API de registre de  pour vous guider dans les étapes de composition d&#39;un  de à l&#39;aide d&#39;une classe standard. Si vous préférez utiliser l’interface utilisateur dans la plateforme d’expérience, le didacticiel [de l’éditeur de ](create-schema-ui.md) fournit des instructions étape par étape pour exécuter des actions similaires dans l’éditeur de  de.

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
* [](../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
* [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Avant de commencer ce didacticiel, veuillez consulter le guide [du](../api/getting-started.md) développeur pour obtenir des informations importantes que vous devez connaître afin d&#39;effectuer des appels vers l&#39;API de Registre du . Cela inclut votre `{TENANT_ID}`, le concept de &quot;&quot; et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accept et à ses valeurs possibles).

Ce didacticiel décrit les étapes de la composition d’un de membres de fidélité qui décrit les données relatives aux membres d’un de fidélité au détail. Avant de commencer, vous souhaiterez peut-être  le [de fidélité](#complete-schema) complet des membres de la Loyauté dans l&#39;annexe.

## Composer un  avec une classe standard

Un  peut être considéré comme le modèle des données que vous souhaitez intégrer dans la plateforme d’expérience. Chaque  est composée d’une classe et de zéro ou plusieurs mixins. En d’autres termes, il n’est pas nécessaire d’ajouter un mixin pour définir un , mais dans la plupart des cas, au moins un mixin est utilisé.

### Affecter une classe

Le processus de composition  commence par la sélection d’une classe. La classe définit les principaux aspects comportementaux des données (enregistrements par rapport aux séries chronologiques), ainsi que les champs minimaux requis pour décrire les données qui seront assimilées.

Le que vous créez dans ce didacticiel utilise la classe XDM Individuelle . XDM Les  individuels sont une classe standard fournie par Adobe pour définir le comportement des enregistrements. Vous trouverez plus d&#39;informations sur le comportement dans les [bases de la composition](../schema/composition.md)des .

Pour affecter une classe, un appel d’API est effectué pour créer (POST) une nouvelle  de dans l’ de client. Cet appel inclut la classe que le va implémenter. Chaque  de ne peut implémenter qu&#39;une seule classe.

**Format API**

```http
POST /tenant/schemas
```

**Requête**

La requête doit inclure un `allOf` attribut qui fait référence `$id` à une classe. Cet attribut définit la &quot;classe de base&quot; que le va implémenter. Dans cet exemple, la classe de base est la classe XDM Individuel . La classe `$id` de XDM individuel est utilisée comme valeur du `$ref` champ dans le `allOf` tableau ci-dessous.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
  "type": "object",
  "title": "Loyalty Members",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile"
    }
  ]
}'
```

**Réponse**

Une requête réussie renvoie l’état de réponse HTTP 201 (Créé) avec un corps de réponse qui contient les détails du nouveau  de, y compris le `$id`, `meta:altIt`et `version`. Ces valeurs sont en lecture seule et sont attribuées par le Registre des  du.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551836845496,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### Cherchez un 

Pour  votre nouveau, exécutez une requête GET (lookup) à l’aide de l’ `meta:altId` ou de l’ `$id` URI codé en URL pour l’.

**Format API**

```http
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F533ca5da28087c44344810891b0f03d9\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

**Réponse **

Le format de réponse dépend de l’en-tête Accepter envoyé avec la requête. Tentez de tester différents en-têtes d’Accepter pour identifier celui qui répond le mieux à vos besoins.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551836845496,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### Ajouter un mixin {#add-a-mixin}

Maintenant que le Membres de la Fidélité a été créé et confirmé, des mixins peuvent être ajoutés.

Différents mixins standard sont disponibles, selon la classe de  sélectionnée. Chaque mixin contient un `intendedToExtend` champ qui définit la ou les classes avec lesquelles ce mixin est compatible.

Les mixins définissent des concepts, tels que &quot;nom&quot; ou &quot;adresse&quot;, qui peuvent être réutilisés dans n’importe quel qui doit capturer les mêmes informations.

**Format API**

```http
PATCH /tenant/schemas/{schema meta:altId or url encoded $id URI}
```

**Requête**

Cette demande met à jour (PATCH) le Membres Fidélité pour inclure les champs dans le mixin &quot;-personne-détails&quot;.

En ajoutant le mixin &quot;-personne-détails&quot;, le Membres de fidélité capture maintenant les informations sur les membres de la  de fidélité, comme leur prénom, leur nom et leur anniversaire.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-person-details"}}
      ]'
```

**Réponse**

La réponse affiche le nouveau mixin dans le `meta:extends` tableau et contient un `$ref` au mixin dans l’attribut `allOf` .

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551837227497,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### Ajouter un autre mixin

Vous pouvez désormais ajouter un autre mixin standard en répétant les étapes à l’aide d’un autre mixin.

>[!TIP] Il vaut la peine de consulter tous les mixins disponibles pour vous familiariser avec les champs inclus dans chacun. Vous pouvez (GET) tous les mixins disponibles pour une classe particulière en exécutant une requête sur chacun des &quot;global&quot; et &quot;locataire&quot;, en ne renvoyant que les mixins dont le champ &quot;meta:intentToExtend&quot; correspond à la classe que vous utilisez. Dans ce cas, il s’agit de la classe XDM Individuel , de sorte que le XDM Individuel  `$id` est utilisé :

```http
GET /global/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

**Format API**

```http
PATCH /tenant/schemas/{schema meta:altId or url encoded $id URI}
```

**Requête**

Cette demande met à jour (PATCH) le Membres fidélité  d’inclure les champs dans le mixin &quot;-détails--personnels&quot;, en ajoutant les champs &quot;adresse de domicile&quot;, &quot;adresse électronique&quot; et &quot;téléphone d’accueil&quot; à la .

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"}}
      ]'  
```

**Réponse**

La réponse affiche le nouveau mixin dans le `meta:extends` tableau et contient un `$ref` au mixin dans l’attribut `allOf` .

Le  Membres de fidélité doit désormais contenir trois `$ref` valeurs dans le `allOf` tableau : &quot;&quot;, &quot;détails de la personne-&quot; et &quot;détails de la personne--&quot;, comme illustré ci-dessous.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.2",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551837356241,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### Définir un nouveau mixage

Le des membres de fidélité doit capturer des informations propres au de fidélité. Ces informations ne sont incluses dans aucun des mixins standard.

Le Registre des  tient compte de cela en vous permettant de définir vos propres mixins dans le locataire . Ces mixins sont propres à votre organisation et ne sont ni visibles ni modifiables par quiconque en dehors de votre organisation IMS.

Pour créer (POST) un nouveau mixin, votre requête doit inclure un `meta:intendedToExtend` champ contenant les `$id` classes de base avec lesquelles le mixin est compatible, ainsi que les propriétés que le mixin va inclure.

Toutes les propriétés personnalisées doivent être imbriquées sous votre `TENANT_ID` afin d’éviter les collisions avec d’autres mixins ou champs.

**Format API**

```http
POST /tenant/mixins
```

**Requête**

Cette requête crée un nouveau mixin qui comporte un objet &quot;fidélité&quot; contenant quatre champs  spécifiques au de fidélité : &quot;loyaltyId&quot;, &quot;loyaltyLevel&quot;, &quot;loyaltyPoints&quot; et &quot;membersSince&quot;.

```SHELL
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Loyalty Member Details",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Loyalty Program Mixin.",
        "definitions": {
            "loyalty": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "loyalty": {
                      "type": "object",
                      "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier."
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total."
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program."
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
            "$ref": "#/definitions/loyalty"
            }
        ]
      }'
```

**Réponse**

Une requête réussie renvoie le statut de réponse HTTP 201 (Créé) avec un corps de réponse contenant les détails du nouveau mixin, y compris le `$id`, `meta:altIt`et `version`. Ces valeurs sont en lecture seule et sont attribuées par le Registre des  du.

```JSON
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Mixin.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyalty": {
                            "type": "object",
                            "properties": {
                                "loyaltyId": {
                                    "title": "Loyalty Identifier",
                                    "type": "string",
                                    "description": "Loyalty Identifier.",
                                    "meta:xdmType": "string"
                                },
                                "loyaltyLevel": {
                                    "title": "Loyalty Level",
                                    "type": "string",
                                    "meta:xdmType": "string"
                                },
                                "loyaltyPoints": {
                                    "title": "Loyalty Points",
                                    "type": "integer",
                                    "description": "Loyalty points total.",
                                    "meta:xdmType": "int"
                                },
                                "memberSince": {
                                    "title": "Member Since",
                                    "type": "string",
                                    "format": "date-time",
                                    "description": "Date the member joined the Loyalty Program.",
                                    "meta:xdmType": "date-time"
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
            "$ref": "#/definitions/loyalty"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.mixins.bb118e507bb848fd85df68fedea70c62",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62",
    "version": "1.1",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1551838135803,
        "repo:lastModifiedDate": 1552078296885,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### Ajouter le mixage personnalisé au 

Vous pouvez maintenant suivre les mêmes étapes pour [ajouter un mixin](#add-a-mixin) standard afin d’ajouter ce nouveau mixin à votre .

**Format API**

```http
PATCH /tenant/schemas/{schema meta:altId or url encoded $id URI}
```

**Requête**

Cette demande met à jour (PATCH) le Membres Fidélité afin d’inclure les champs dans le nouveau mélange &quot;Détails du membre Fidélité&quot;.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"}}
      ]'
```

**Réponse**

Vous pouvez constater que le mixin a bien été ajouté, car la réponse affiche maintenant le mixin nouvellement ajouté dans la `meta:extends` baie et contient un `$ref` au mixin dans l’ `allOf` attribut.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.3",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551838484129,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

###  le actuel 

Vous pouvez maintenant effectuer une requête GET pour  la  actuelle du et voir comment les mixins ajoutés ont contribué à la structure globale de la .

**Format API**

```http
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1'
```

**Réponse**

En utilisant l’en-tête `application/vnd.adobe.xed-full+json; version=1` Accepter, vous pouvez voir le  complet montrant toutes les propriétés. Ces propriétés sont les champs fournis par la classe et les mixins qui ont été utilisés pour composer le  du. Dans cet exemple de réponse, les attributs de propriété individuels ont été réduits pour l’espace. Vous pouvez le  complet du, y compris toutes les propriétés et leurs attributs, dans l’ [annexe](#appendix) à la fin de cette .

Sous `"properties"`cette page, vous pouvez voir le  de `_{TENANT_ID}` créé lors de l’ajout du mixin personnalisé. Au sein de ce   se trouve l’objet &quot;loyalty&quot; et les champs définis lors de la création du mixin.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {},
        "repositoryLastModifiedBy": {},
        "createdByBatchID": { },
        "modifiedByBatchID": {},
        "_repo": {},
        "identityMap": {},
        "_id": {},
        "timeSeriesEvents": {},
        "person": {},
        "homeAddress": {},
        "personalEmail": {},
        "homePhone": {},
        "mobilePhone": {},
        "faxPhone": {},
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### Création d’un type de données

Le mixage Fidélité que vous avez créé contient des propriétés de fidélité spécifiques qui peuvent être utiles dans d’autres  de. Par exemple, les données peuvent être assimilées dans le cadre d’un d’expériences ou utilisées par un  qui implémente une autre classe. Dans ce cas, il est logique d’enregistrer la hiérarchie d’objets en tant que type de données afin de faciliter la réutilisation de la définition ailleurs.

Les types de données vous permettent de définir une hiérarchie d’objets une seule fois et d’y faire référence dans un champ comme vous le feriez pour tout autre type scalaire.

En d’autres termes, les types de données permettent l’utilisation cohérente de structures à champs multiples, avec plus de souplesse que les mixins, car ils peuvent être inclus n’importe où dans un  en les ajoutant comme &quot;type&quot; d’un champ.

**Format API**

```http
POST /tenant/datatypes
```

**Requête**

La définition d’un type de données ne nécessite pas de champs `meta:extends` ou `meta:intendedToExtend` , pas plus que les champs ne doivent être imbriqués pour éviter les collisions.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Loyalty Details",
        "type": "object",
        "description": "Loyalty Member Details data type",
        "definitions": {
            "loyalty": {
                "type": "object",
                "properties": {
                    "loyaltyId": {
                    "title": "Loyalty Identifier",
                    "type": "string",
                    "description": "Loyalty Identifier."
                    },
                    "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "type": "string"
                    },
                    "loyaltyPoints": {
                    "title": "Loyalty Points",
                    "type": "integer",
                    "description": "Loyalty points total."
                    },
                    "memberSince": {
                    "title": "Member Since",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date the member joined the Loyalty Program."
                    }
                }
            }
        },
        "allOf": [
            {
            "$ref": "#/definitions/loyalty"
            }
        ]
      }'
```

**Réponse**

Une requête réussie renvoie le statut de réponse HTTP 201 (Créé) avec un corps de réponse contenant les détails du type de données nouvellement créé, y compris le `$id`, `meta:altIt`et `version`. Ces valeurs sont en lecture seule et sont attribuées par le Registre des  du.

```JSON
{
    "title": "Loyalty Details",
    "type": "object",
    "description": "Loyalty Member Details data type",
    "definitions": {
        "loyalty": {
            "properties": {
                "loyaltyId": {
                    "title": "Loyalty Identifier",
                    "type": "string",
                    "description": "Loyalty Identifier.",
                    "meta:xdmType": "string"
                },
                "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "loyaltyPoints": {
                    "title": "Loyalty Points",
                    "type": "integer",
                    "description": "Loyalty points total.",
                    "meta:xdmType": "int"
                },
                "memberSince": {
                    "title": "Member Since",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date the member joined the Loyalty Program.",
                    "meta:xdmType": "date-time"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/loyalty"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.49b594dabe6bec545c8a6d1a0991a4dd",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
    "version": "1.0",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1551840599469,
        "repo:lastModifiedDate": 1551840599469,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Vous pouvez effectuer une requête GET (recherche) à l’aide de l’ `$id` URI codée URL afin de directement le nouveau type de données. Veillez à inclure le paramètre `version` dans l’en-tête Accepter pour une demande de recherche.

### Utiliser le type de données dans le 

Maintenant que le type de données Détails de fidélité a été créé, vous pouvez mettre à jour (PATCH) le champ &quot;fidélité&quot; dans le mixin que vous avez créé pour référencer le type de données à la place des champs qui y étaient précédemment.

**Format API**

```http
PATCH /tenant/mixins/{mixin meta:altId or URL encoded $id URI}
```

**Requête**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.bb118e507bb848fd85df68fedea70c62 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      [
        {
            "op": "replace",
            "path": "/definitions/loyalty/properties/_{TENANT_ID}/properties",
            "value": {
                "loyalty": {
                    "title": "Loyalty",
                    "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "description": "Loyalty Info"
                }
            }
        }
      ]'
```

**Réponse**

La réponse inclut désormais une référence (`$ref`) au type de données dans l’objet &quot;loyalty&quot; au lieu des champs précédemment définis.

```JSON
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Mixin.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyalty": {
                            "title": "Loyalty",
                            "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                            "description": "Loyalty Info"
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
            "$ref": "#/definitions/loyalty"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.mixins.bb118e507bb848fd85df68fedea70c62",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62",
    "version": "1.2",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1551838135803,
        "repo:lastModifiedDate": 1552080570051,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

L’exécution d’une requête GET pour rechercher le présente désormais la référence au type de données sous &quot;properties/_{TENANT_ID}&quot;, comme indiqué ici :

```JSON
"_{TENANT_ID}": {
    "type": "object",
    "meta:xdmType": "object",
    "properties": {
        "loyalty": {
            "title": "Loyalty",
            "description": "Loyalty Info",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
            "properties": {
                "loyaltyId": {
                    "title": "Loyalty Identifier",
                    "type": "string",
                    "description": "Loyalty Identifier.",
                    "meta:xdmType": "string"
                },
                "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "loyaltyPoints": {
                    "title": "Loyalty Points",
                    "type": "integer",
                    "description": "Loyalty points total.",
                    "meta:xdmType": "int"
                },
                "memberSince": {
                    "title": "Member Since",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date the member joined the Loyalty Program.",
                    "meta:xdmType": "date-time"
                }
            }
        }
    }
}
```

### Définition d’un descripteur d’identité

Les  sont utilisées pour l’assimilation de données dans Experience Platform. Ces données sont en fin de compte utilisées dans plusieurs services pour créer un seul  unifié d’un individu. Pour faciliter ce processus, les champs clés peuvent être marqués comme &quot;Identité&quot; et, lors de l’assimilation des données, les données contenues dans ces champs sont insérées dans le &quot;Graphique d’identité&quot; de cette personne. Les données du graphique peuvent ensuite être accessibles par l’utilisateur en temps [réel](../../profile/home.md) et d’autres services Experience Platform pour fournir un assemblé de chaque client.

Les champs généralement identifiés comme &quot;Identité&quot; sont les suivants : adresse électronique, numéro de téléphone, ID [Experience Cloud (ECID)](https://marketing.adobe.com/resources/help/en_US/mcvid/), ID CRM ou autres champs d’ID uniques.

Tenez compte de tous les identifiants uniques propres à votre organisation, car il peut s’agir de bons champs d’identité.

Les descripteurs d’identité signalent que la &quot;sourceProperty&quot; de la &quot;sourceSchema&quot; est un identifiant unique qui doit être considéré comme une &quot;Identity&quot;.

Pour plus d&#39;informations sur l&#39;utilisation des descripteurs, consultez le [guide](../api/getting-started.md)du développeur du Registre des.

**Format API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante définit un descripteur d’identité sur le champ &quot;loyaltyId&quot;. Cela indique à la plateforme d’expérience d’utiliser l’identifiant unique du membre  fidélité (dans ce cas, l’adresse électronique du membre) pour rassembler les informations sur l’individu.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_{TENANT_ID}/loyalty/loyaltyId",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

>[!NOTE] Vous pouvez des valeurs &quot;xdm:&quot; ou en créer de nouvelles, à l’aide de l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)Identity Service. La valeur de &quot;xdm:property&quot; peut être &quot;xdm:code&quot; ou &quot;xdm:id&quot;, selon le &quot;xdm:&quot; utilisé.

**Réponse**

Une réponse réussie renvoie HTTP Status 201 (Créé) avec un corps de réponse contenant les détails du nouveau descripteur, y compris son `@id`corps. Il `@id` s’agit d’un champ en lecture seule attribué par le Registre des  du et utilisé pour référencer le descripteur dans l’API.

```JSON
{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/loyalty/loyaltyId",
    "xdm:namespace": "Email",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": false,
    "meta:containerId": "tenant",
    "@id": "e52fc732507e5aa9d63d00caa838d3c9fd97aa56"
}
```

## Activation des  pour une utilisation dans le client en temps réel 

En ajoutant la balise &quot; &quot; à l’ `meta:immutableTags` attribut, vous pouvez activer l’Membres de fidélité pour l’utilisation par le du client en temps réel.

Pour plus d&#39;informations sur l&#39;utilisation de  , reportez-vous à la section sur les [](../api/unions.md) dans le guide du développeur du registre des.

### Ajouter balise &quot;&quot;

Pour qu’un soit inclus dans le `meta:immutableTags` de l’ fusionné, la balise &quot;&quot; doit être ajoutée à l’attribut de l’. Pour ce faire, vous devez effectuer une demande PATCH pour mettre à jour le  de et ajouter le `meta:immutableTags` tableau avec la valeur &quot; &quot;.

**Format API**

```http
PATCH /tenant/schemas/{meta:altId or the url encoded $id URI}
```

**Requête**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**Réponse**

La réponse indique que l’opération a été effectuée correctement et que le  de contient désormais un attribut de niveau supérieur `meta:immutableTags`, qui est un tableau contenant la valeur &quot; &quot;.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

###    dans un 

Vous avez maintenant ajouté avec succès votre  à l’ de XDM Individuel  le. Pour voir un  de tous les  qui font partie du mêmede , vous pouvez exécuter une requête GET à l’aide des paramètres de l’pour filtrer la réponse.

En utilisant le paramètre `property` , vous pouvez spécifier que seuls les  contenant un `meta:immutableTags` champ `meta:class` égal à la `$id` classe de  XDM individuels sont renvoyés.

**Format API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

**Requête**

L’exemple de requête ci-dessous renvoie tous les qui font partie du XDM Individuel  le.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse est un filtré de  de, contenant uniquement ceux qui répondent aux deux exigences. N’oubliez pas que lors de l’utilisation de plusieurs paramètres de , une relation ET est supposée. Le format de la réponse du  dépend de l’en-tête Accepter envoyé dans la requête.

```JSON
{
    "results": [
        {
            "title": "Loyalty Members",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
            "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
            "version": "1.4"
        },
        {
            "title": "Schema 2",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e7297a6ddfc7812ab3a7b504a1ab98da",
            "meta:altId": "_{TENANT_ID}.schemas.e7297a6ddfc7812ab3a7b504a1ab98da",
            "version": "1.5"
        },
        {
            "title": "Schema 3",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/50f960bb810e99a21737254866a477bf",
            "meta:altId": "_{TENANT_ID}.schemas.50f960bb810e99a21737254866a477bf",
            "version": "1.2"
        },
        {
            "title": "Schema 4",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/dfebb19b93827b70bbad006137812537",
            "meta:altId": "_{TENANT_ID}.schemas.dfebb19b93827b70bbad006137812537",
            "version": "1.7"
        }
    ],
    "_links": {
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à composer un  à l’aide de mixins standard et d’un mixin que vous avez défini. Vous pouvez désormais utiliser ce pour créer un jeu de données et assimiler des données d’enregistrement dans Adobe Experience Platform.

Le  des membres fidèles complet, tel qu&#39;il a été créé tout au long de ce didacticiel, est disponible dans l&#39;annexe qui suit. En regardant le  du, vous pouvez voir comment les mixins contribuent à la structure globale et quels champs sont disponibles pour l’assimilation de données.

Une fois que vous avez créé plusieurs  de, vous pouvez définir des relations entre eux à l’aide de descripteurs de relation. Pour plus d’informations, consultez le didacticiel pour [définir une relation entre deux](relationship-api.md) . Pour obtenir des exemples détaillés sur la manière d’effectuer toutes les opérations (GET, POST, PUT, PATCH et DELETE) dans le registre, reportez-vous au guide [du développeur du registre](../api/getting-started.md) lorsque vous travaillez avec l’API.

## Annexe {#appendix}

Les informations suivantes complètent le didacticiel sur l’API.

## Membres de fidélité complets {#complete-schema}

Dans ce didacticiel, un  est composé pour décrire les membres d’un de fidélité au détail.

Le  implémente la classe XDM Individuel  et combine plusieurs mixins ; l’ajout d’informations sur les membres de fidélité à l’aide des mixins &quot;Détails de la personne&quot; et &quot;Détails personnels&quot; standard, ainsi que par le biais d’un mixin &quot;Détails de fidélité&quot; défini au cours du didacticiel.

L’exemple suivant montre le  des membres de fidélité terminé au format JSON :

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {
            "title": "Created by User Identifier",
            "type": "string",
            "description": "User id who has created the entity.",
            "meta:xdmField": "xdm:repositoryCreatedBy",
            "meta:xdmType": "string"
        },
        "repositoryLastModifiedBy": {
            "title": "Modified by User Identifier",
            "type": "string",
            "description": "User id who last modified the entity. At creation time, `modifiedByUser` is set as `createdByUser`.",
            "meta:xdmField": "xdm:repositoryLastModifiedBy",
            "meta:xdmType": "string"
        },
        "createdByBatchID": {
            "title": "Created by Batch Identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "The Data Set Files in Catalog Services which has been originating the creation of the entity.",
            "meta:xdmField": "xdm:createdByBatchID",
            "meta:xdmType": "string"
        },
        "modifiedByBatchID": {
            "title": "Modified by Batch Identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "The last Data Set Files in Catalog Services which has modified the entity. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
            "meta:xdmField": "xdm:modifiedByBatchID",
            "meta:xdmType": "string"
        },
        "_repo": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "createDate": {
                    "type": "string",
                    "format": "date-time",
                    "meta:immutable": true,
                    "meta:usereditable": false,
                    "examples": [
                        "2004-10-23T12:00:00-06:00"
                    ],
                    "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                    "meta:xdmField": "repo:createDate",
                    "meta:xdmType": "date-time"
                },
                "modifyDate": {
                    "type": "string",
                    "format": "date-time",
                    "meta:usereditable": false,
                    "examples": [
                        "2004-10-23T12:00:00-06:00"
                    ],
                    "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                    "meta:xdmField": "repo:modifyDate",
                    "meta:xdmType": "date-time"
                }
            }
        },
        "identityMap": {
            "type": "object",
            "meta:xdmType": "map",
            "meta:xdmField": "xdm:identityMap",
            "additionalProperties": {
                "type": "array",
                "meta:xdmType": "array",
                "items": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/identityitem",
                    "properties": {
                        "id": {
                            "title": "Identifier",
                            "type": "string",
                            "description": "Identity of the consumer in the related namespace.",
                            "meta:xdmField": "xdm:id",
                            "meta:xdmType": "string"
                        },
                        "authenticatedState": {
                            "description": "The state this identity is authenticated as for this observed ExperienceEvent.",
                            "type": "string",
                            "default": "ambiguous",
                            "enum": [
                                "ambiguous",
                                "authenticated",
                                "loggedOut"
                            ],
                            "meta:enum": {
                                "ambiguous": "Ambiguous",
                                "authenticated": "User identified by a login or simular action that was valid at the time of the event observation.",
                                "loggedOut": "User was identified by a login action at some point of time previously, but is not currently logged in."
                            },
                            "meta:xdmField": "xdm:authenticatedState",
                            "meta:xdmType": "string"
                        },
                        "primary": {
                            "title": "Primary",
                            "type": "boolean",
                            "default": false,
                            "description": "Indicates this identity is the preferred identity. Is used as a hint to help systems better organize how identities are queried.",
                            "meta:xdmField": "xdm:primary",
                            "meta:xdmType": "boolean"
                        }
                    }
                }
            }
        },
        "_id": {
            "title": "Identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "A unique identifier for the record.",
            "meta:xdmField": "@id",
            "meta:xdmType": "string"
        },
        "timeSeriesEvents": {
            "title": "Time-series Events",
            "description": "List of time-series based events that relate to schemas based on record.",
            "type": "array",
            "meta:xdmField": "xdm:timeSeriesEvents",
            "meta:xdmType": "array",
            "items": {
                "type": "object",
                "meta:xdmType": "object",
                "meta:referencedFrom": "https://ns.adobe.com/xdm/data/time-series",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "type": "string",
                        "format": "uri-reference",
                        "description": "A unique identifier for the time-series event.",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "timestamp": {
                        "title": "Timestamp",
                        "type": "string",
                        "format": "date-time",
                        "description": "The time when an event or observation occurred.",
                        "meta:xdmField": "xdm:timestamp",
                        "meta:xdmType": "date-time"
                    },
                    "eventType": {
                        "title": "Event Type",
                        "type": "string",
                        "description": "The primary event type for this timeseries record.",
                        "meta:enum": {
                            "advertising.completes": "Indicates if a timed media asset was watched to completion - this does not necessarily mean the viewer watched the whole video; viewer could have skipped ahead.",
                            "advertising.timePlayed": "Describes the amount of time spent by a user on a specific timed media asset.",
                            "advertising.federated": "Indicates if an experience event was created through data federation (data sharing between customers).",
                            "advertising.clicks": "Click(s) actions on an advertisement.",
                            "advertising.conversions": "A customer pre-defined action(s) which triggers an event for performance evaluation.",
                            "advertising.firstQuartiles": "A digital video ad has played through 25% of its duration at normal speed.",
                            "advertising.impressions": "Impression(s) of an advertisement to an end user with the potential of being viewed.",
                            "advertising.midpoints": "A digital video ad has played through 50% of its duration at normal speed.",
                            "advertising.starts": "A digital video ad has started playing.",
                            "advertising.thirdQuartiles": "A digital video ad has played through 75% of its duration at normal speed.",
                            "web.webpagedetails.pageViews": "View(s) of a webpage has occurred.",
                            "web.webinteraction.linkClicks": "Click of a web-link has occurred.",
                            "commerce.checkouts": "An action during a checkout process of a product list, there can be more than one checkout event if there are multiple steps in a checkout process. If there are multiple steps the event time information and referenced page or experience is used to identify the step individual events represent in order.",
                            "commerce.productListAdds": "Addition of a product to the product list. Example a product is added to a shopping cart.",
                            "commerce.productListOpens": "Initializations of a new product list. Example a shopping cart is created.",
                            "commerce.productListRemovals": "Removal(s) of a product entry from a product list. Example a product is removed from a shopping cart.",
                            "commerce.productListReopens": "A product list that was no longer accessible(abandoned) has been re-activated by the user. Example via a re-marketing activity.",
                            "commerce.productListViews": "View(s) of a product-list has occurred.",
                            "commerce.productViews": "View(s) of a product have occurred.",
                            "commerce.purchases": "An order has been accepted. Purchase is the only required action in a commerce conversion. Purchase must have a product list referenced.",
                            "commerce.saveForLaters": "Product list is saved for future use. Example a product wish list."
                        },
                        "meta:xdmField": "xdm:eventType",
                        "meta:xdmType": "string"
                    }
                }
            }
        },
        "person": {
            "title": "Person",
            "description": "An individual actor, contact, or owner.",
            "meta:xdmField": "xdm:person",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person",
            "properties": {
                "name": {
                    "title": "Full name",
                    "description": "The person's full name",
                    "meta:xdmField": "xdm:name",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
                    "properties": {
                        "firstName": {
                            "title": "First name",
                            "type": "string",
                            "description": "The first segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the preferred personal or given name.\n\nThe `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
                            "meta:xdmField": "xdm:firstName",
                            "meta:xdmType": "string"
                        },
                        "lastName": {
                            "title": "Last name",
                            "type": "string",
                            "description": "The last segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the inherited family name, surname, patronymic, or matronymic name.\n\nThe `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
                            "meta:xdmField": "xdm:lastName",
                            "meta:xdmType": "string"
                        },
                        "middleName": {
                            "title": "Middle name",
                            "type": "string",
                            "description": "Middle, alternative, or additional names supplied between the first name and last name.",
                            "meta:xdmField": "xdm:middleName",
                            "meta:xdmType": "string"
                        },
                        "courtesyTitle": {
                            "title": "Courtesy title",
                            "type": "string",
                            "description": "Normally an abbreviation of a persons *title*, *honorific*, or *salutation*.\nThe `courtesyTitle` is used in front of full or last name in opening texts.\ne.g Mr. Miss. or Dr J. Smith.\n",
                            "meta:xdmField": "xdm:courtesyTitle",
                            "meta:xdmType": "string"
                        },
                        "fullName": {
                            "title": "Full name",
                            "type": "string",
                            "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
                            "meta:xdmField": "xdm:fullName",
                            "meta:xdmType": "string"
                        }
                    }
                },
                "birthDate": {
                    "title": "Birth Date",
                    "type": "string",
                    "format": "date",
                    "description": "The full date a person was born.",
                    "meta:xdmField": "xdm:birthDate",
                    "meta:xdmType": "date"
                },
                "birthDayAndMonth": {
                    "title": "Birth Date",
                    "type": "string",
                    "pattern": "[0-1][0-9]-[0-9][0-9]",
                    "description": "The day and month a person was born, in the format MM-DD. This field should be used when the day and month of a person's birth is known, but not the year.",
                    "meta:xdmField": "xdm:birthDayAndMonth",
                    "meta:xdmType": "string"
                },
                "birthYear": {
                    "title": "Birth year",
                    "type": "integer",
                    "description": "The year a person was born including the century (yyyy, e.g 1983).  This field should be used when only the person's age is known, not the full birth date.",
                    "minimum": 1,
                    "maximum": 32767,
                    "meta:xdmField": "xdm:birthYear",
                    "meta:xdmType": "short"
                },
                "gender": {
                    "title": "Gender",
                    "type": "string",
                    "enum": [
                        "male",
                        "female",
                        "not_specified",
                        "non_specific"
                    ],
                    "meta:enum": {
                        "male": "Male",
                        "female": "Female",
                        "not_specified": "Not Specified",
                        "non_specific": "Nonspecific"
                    },
                    "description": "Gender identity of the person.\n",
                    "default": "not_specified",
                    "meta:xdmField": "xdm:gender",
                    "meta:xdmType": "string"
                },
                "repositoryCreatedBy": {
                    "title": "Created by User Identifier",
                    "type": "string",
                    "description": "User id who has created the entity.",
                    "meta:xdmField": "xdm:repositoryCreatedBy",
                    "meta:xdmType": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by User Identifier",
                    "type": "string",
                    "description": "User id who last modified the entity. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy",
                    "meta:xdmType": "string"
                },
                "createdByBatchID": {
                    "title": "Created by Batch Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The Data Set Files in Catalog Services which has been originating the creation of the entity.",
                    "meta:xdmField": "xdm:createdByBatchID",
                    "meta:xdmType": "string"
                },
                "modifiedByBatchID": {
                    "title": "Modified by Batch Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last Data Set Files in Catalog Services which has modified the entity. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmField": "xdm:modifiedByBatchID",
                    "meta:xdmType": "string"
                },
                "_repo": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmField": "repo:createDate",
                            "meta:xdmType": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmField": "repo:modifyDate",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        },
        "homeAddress": {
            "title": "Home Address",
            "description": "A home postal address.",
            "meta:xdmField": "xdm:homeAddress",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
            "properties": {
                "_id": {
                    "title": "Coordinates ID",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The unique identifier of the coordinates.",
                    "meta:xdmField": "@id",
                    "meta:xdmType": "string"
                },
                "_schema": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "description": {
                            "title": "Description",
                            "type": "string",
                            "description": "A description of what the coordinates identify.",
                            "meta:xdmField": "schema:description",
                            "meta:xdmType": "string"
                        },
                        "latitude": {
                            "title": "Latitude",
                            "type": "number",
                            "minimum": -90,
                            "maximum": 90,
                            "description": "The signed vertical coordinate of a geographic point.",
                            "meta:xdmField": "schema:latitude",
                            "meta:xdmType": "number"
                        },
                        "longitude": {
                            "title": "Longitude",
                            "type": "number",
                            "minimum": -180,
                            "maximum": 180,
                            "description": "The signed horizontal coordinate of a geographic point.",
                            "meta:xdmField": "schema:longitude",
                            "meta:xdmType": "number"
                        },
                        "elevation": {
                            "title": "Elevation",
                            "type": "number",
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
                            "meta:xdmField": "schema:elevation",
                            "meta:xdmType": "number"
                        }
                    }
                },
                "countryCode": {
                    "title": "Country code",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
                    "meta:xdmField": "xdm:countryCode",
                    "meta:xdmType": "string"
                },
                "stateProvince": {
                    "title": "State or province",
                    "type": "string",
                    "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
                    "examples": [
                        "US-CA",
                        "DE-BB",
                        "JP-13"
                    ],
                    "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
                    "meta:xdmField": "xdm:stateProvince",
                    "meta:xdmType": "string"
                },
                "city": {
                    "title": "City",
                    "type": "string",
                    "description": "The name of the city.",
                    "meta:xdmField": "xdm:city",
                    "meta:xdmType": "string"
                },
                "postalCode": {
                    "title": "Postal code",
                    "type": "string",
                    "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
                    "meta:xdmField": "xdm:postalCode",
                    "meta:xdmType": "string"
                },
                "dmaID": {
                    "title": "Designated Market Area",
                    "type": "integer",
                    "description": "The Nielsen Media Research designated market area.",
                    "meta:xdmField": "xdm:dmaID",
                    "meta:xdmType": "int"
                },
                "msaID": {
                    "title": "Metropolitan Statistical Area",
                    "type": "integer",
                    "description": "The Metropolitan Statistical Area in the USA where the observation occurred.",
                    "meta:xdmField": "xdm:msaID",
                    "meta:xdmType": "int"
                },
                "repositoryCreatedBy": {
                    "title": "Created by User Identifier",
                    "type": "string",
                    "description": "User id who has created the entity.",
                    "meta:xdmField": "xdm:repositoryCreatedBy",
                    "meta:xdmType": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by User Identifier",
                    "type": "string",
                    "description": "User id who last modified the entity. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy",
                    "meta:xdmType": "string"
                },
                "createdByBatchID": {
                    "title": "Created by Batch Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The Data Set Files in Catalog Services which has been originating the creation of the entity.",
                    "meta:xdmField": "xdm:createdByBatchID",
                    "meta:xdmType": "string"
                },
                "modifiedByBatchID": {
                    "title": "Modified by Batch Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last Data Set Files in Catalog Services which has modified the entity. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmField": "xdm:modifiedByBatchID",
                    "meta:xdmType": "string"
                },
                "_repo": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmField": "repo:createDate",
                            "meta:xdmType": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmField": "repo:modifyDate",
                            "meta:xdmType": "date-time"
                        }
                    }
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary address indicator. A Profile can have only one `primary` address at a given point of time.\n",
                    "meta:xdmField": "xdm:primary",
                    "meta:xdmType": "boolean"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Free form name of the address.",
                    "meta:xdmField": "xdm:label",
                    "meta:xdmType": "string"
                },
                "street1": {
                    "title": "Street 1",
                    "type": "string",
                    "description": "Primary Street level information, apartment number, street number and street name.",
                    "meta:xdmField": "xdm:street1",
                    "meta:xdmType": "string"
                },
                "street2": {
                    "title": "Street 2",
                    "type": "string",
                    "description": "Optional street information second line.",
                    "meta:xdmField": "xdm:street2",
                    "meta:xdmType": "string"
                },
                "street3": {
                    "title": "Street 3",
                    "type": "string",
                    "description": "Optional street information third line.",
                    "meta:xdmField": "xdm:street3",
                    "meta:xdmType": "string"
                },
                "street4": {
                    "title": "Street 4",
                    "type": "string",
                    "description": "Optional street information fourth line.",
                    "meta:xdmField": "xdm:street4",
                    "meta:xdmType": "string"
                },
                "region": {
                    "title": "Region",
                    "type": "string",
                    "description": "The region, county, or district portion of the address.",
                    "meta:xdmField": "xdm:region",
                    "meta:xdmType": "string"
                },
                "postOfficeBox": {
                    "title": "Post Office Box",
                    "type": "string",
                    "description": "Post office box of the address.",
                    "maxLength": 20,
                    "meta:xdmField": "xdm:postOfficeBox",
                    "meta:xdmType": "string"
                },
                "country": {
                    "title": "Country",
                    "type": "string",
                    "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
                    "meta:xdmField": "xdm:country",
                    "meta:xdmType": "string"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending Verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmField": "xdm:status",
                    "meta:xdmType": "string"
                },
                "statusReason": {
                    "title": "Status Reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmField": "xdm:statusReason",
                    "meta:xdmType": "string"
                },
                "lastVerifiedDate": {
                    "title": "Last Verified Date",
                    "type": "string",
                    "format": "date",
                    "description": "The date that the address was last verified as still belonging to the person.",
                    "meta:xdmField": "xdm:lastVerifiedDate",
                    "meta:xdmType": "date"
                }
            }
        },
        "personalEmail": {
            "title": "Personal Email",
            "description": "A personal email address.",
            "meta:xdmField": "xdm:personalEmail",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
            "properties": {
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary email indicator.\n\nA Profile can have only one `primary` email address at a given point of time.\n",
                    "meta:xdmField": "xdm:primary",
                    "meta:xdmType": "boolean"
                },
                "address": {
                    "title": "Address",
                    "type": "string",
                    "format": "email",
                    "description": "The technical address, e.g 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                    "meta:xdmField": "xdm:address",
                    "meta:xdmType": "string"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Additional display information that maybe available, e.g MS Outlook rich address controls display 'John Smith smithjr@company.uk', the 'John Smith' part is data that would be placed in the label.",
                    "meta:xdmField": "xdm:label",
                    "meta:xdmType": "string"
                },
                "type": {
                    "title": "Type",
                    "type": "string",
                    "description": "The way the account relates to the person. e.g 'work' or 'personal'",
                    "meta:enum": {
                        "unknown": "Unknown",
                        "personal": "Personal",
                        "work": "Work",
                        "education": "Education"
                    },
                    "meta:xdmField": "xdm:type",
                    "meta:xdmType": "string"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the email address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending Verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmField": "xdm:status",
                    "meta:xdmType": "string"
                },
                "statusReason": {
                    "title": "Status Reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmField": "xdm:statusReason",
                    "meta:xdmType": "string"
                }
            }
        },
        "homePhone": {
            "title": "Home Phone",
            "description": "Home phone number.",
            "meta:xdmField": "xdm:homePhone",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "properties": {
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator.\n\nUnlike for Address or EmailAddress, there can be multiple primary phone numbers; one per communication channel.\nThe communication channel is defined by the type:\n\n* `textMessaging`: type = `mobile`\n* `phone`: type = `home` | `work` | `unknown`\n* `fax`: type = `fax`\n",
                    "meta:xdmField": "xdm:primary",
                    "meta:xdmType": "boolean"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets (), hyphens - or characters to indicate sub dialing identifiers like extensions x. E.g 1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmField": "xdm:number",
                    "meta:xdmType": "string"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator or switchboard.",
                    "meta:xdmField": "xdm:extension",
                    "meta:xdmType": "string"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmField": "xdm:status",
                    "meta:xdmType": "string"
                },
                "statusReason": {
                    "title": "Status Reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmField": "xdm:statusReason",
                    "meta:xdmType": "string"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully Used"
                    },
                    "meta:xdmField": "xdm:validity",
                    "meta:xdmType": "string"
                }
            }
        },
        "mobilePhone": {
            "title": "Mobile Phone",
            "description": "Mobile phone number.",
            "meta:xdmField": "xdm:mobilePhone",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "properties": {
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator.\n\nUnlike for Address or EmailAddress, there can be multiple primary phone numbers; one per communication channel.\nThe communication channel is defined by the type:\n\n* `textMessaging`: type = `mobile`\n* `phone`: type = `home` | `work` | `unknown`\n* `fax`: type = `fax`\n",
                    "meta:xdmField": "xdm:primary",
                    "meta:xdmType": "boolean"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets (), hyphens - or characters to indicate sub dialing identifiers like extensions x. E.g 1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmField": "xdm:number",
                    "meta:xdmType": "string"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator or switchboard.",
                    "meta:xdmField": "xdm:extension",
                    "meta:xdmType": "string"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmField": "xdm:status",
                    "meta:xdmType": "string"
                },
                "statusReason": {
                    "title": "Status Reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmField": "xdm:statusReason",
                    "meta:xdmType": "string"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully Used"
                    },
                    "meta:xdmField": "xdm:validity",
                    "meta:xdmType": "string"
                }
            }
        },
        "faxPhone": {
            "title": "Fax Phone",
            "description": "Fax phone number.",
            "meta:xdmField": "xdm:faxPhone",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "properties": {
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator.\n\nUnlike for Address or EmailAddress, there can be multiple primary phone numbers; one per communication channel.\nThe communication channel is defined by the type:\n\n* `textMessaging`: type = `mobile`\n* `phone`: type = `home` | `work` | `unknown`\n* `fax`: type = `fax`\n",
                    "meta:xdmField": "xdm:primary",
                    "meta:xdmType": "boolean"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets (), hyphens - or characters to indicate sub dialing identifiers like extensions x. E.g 1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmField": "xdm:number",
                    "meta:xdmType": "string"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator or switchboard.",
                    "meta:xdmField": "xdm:extension",
                    "meta:xdmType": "string"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmField": "xdm:status",
                    "meta:xdmType": "string"
                },
                "statusReason": {
                    "title": "Status Reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmField": "xdm:statusReason",
                    "meta:xdmType": "string"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully Used"
                    },
                    "meta:xdmField": "xdm:validity",
                    "meta:xdmType": "string"
                }
            }
        },
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "title": "Loyalty",
                    "description": "Loyalty Info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
