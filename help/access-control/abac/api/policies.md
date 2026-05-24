---
keywords: Experience Platform;accueil;rubriques populaires;api;Contrôle d’accès basé sur les attributs;contrôle d’accès basé sur les attributs
solution: Experience Platform
title: Point d’entrée de l’API des politiques de contrôle d’accès
description: Le point d’entrée /policies de l’API de contrôle d’accès basé sur les attributs vous permet de gérer les politiques par programmation dans Adobe Experience Platform.
role: Developer
exl-id: 07690f43-fdd9-4254-9324-84e6bd226743
TQID: https://experienceleague.adobe.com/nM8mWpFl4mf07cg2FwAoN6sdoNC--PSgN29TtRT0knA
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: adf04a6a-050f-44bc-a52c-db79ccb22ebfid: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2: id: a16ec9c0-4484-4842-b9a0-5504cde38e6aid: d175cb4c-5781-454e-a826-bf6dff786265
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 1439
ht-degree: 10%

---

# Point d’entrée des politiques de contrôle d’accès

>[!NOTE]
>
>Si un jeton d’utilisateur est transmis, l’utilisateur du jeton doit disposer d’un rôle « administrateur d’organisation » pour l’organisation demandée.

Les politiques de contrôle d’accès sont des instructions qui rassemblent des attributs pour établir des actions admissibles et non admissibles. Ces politiques peuvent être locales ou globales et peuvent remplacer d’autres politiques. Le point d’entrée `/policies` de l’API de contrôle d’accès basé sur les attributs vous permet de gérer par programmation les politiques, y compris les informations sur les règles qui les régissent ainsi que leurs conditions d’objet respectives.

>[!IMPORTANT]
>
>Ce point d’entrée ne doit pas être confondu avec le point d’entrée `/policies` de l’API [Policy Service](../../../data-governance/api/policies.md), qui est utilisé pour gérer les politiques d’utilisation des données.

## Prise en main

Le point d’entrée de l’API utilisé dans ce guide fait partie de l’API de contrôle d’accès basé sur les attributs. Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Récupération dʼune liste de politiques {#list}

Envoyez une requête GET au point d’entrée `/policies` pour répertorier toutes les politiques existantes de votre organisation.

**Format d’API**

```http
GET /policies
```

**Requête**

La requête suivante récupère une liste des politiques existantes.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une réponse réussie renvoie une liste de politiques existantes.

```json
{
  {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652892767559,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/xql/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.read",
                  "com.adobe.action.write",
                  "com.adobe.action.view"
              ]
          },
          {
              "effect": "Permit",
              "resource": "/orgs/{IMS_ORG}/sandboxes/*/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.delete"
              ]
          },
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
              "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
              "actions": [
                  "com.adobe.action.write"
              ]
          }
      ],
      "_etag": "\"0300593f-0000-0200-0000-62852ff80000\""
  },
  {
      "id": "13138ef6-c007-495d-837f-0a248867e219",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652859368555,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652890780206,
      "name": "Documentation-Copy",
      "description": "xyz",
      "status": "active",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Permit",
              "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          },
          {
              "effect": "Deny",
              "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          }
      ],
      "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
  },
}
```

| Propriété | Description |
| --- | --- |
| `id` | Identifiant qui correspond à une politique. Cet identifiant est généré automatiquement et peut être utilisé pour rechercher, mettre à jour et supprimer une politique. |
| `imsOrgId` | Organisation dans laquelle la politique interrogée est accessible. |
| `createdBy` | L’identifiant de l’utilisateur qui a créé la politique. |
| `createdAt` | Heure à laquelle la politique a été créée. La propriété `createdAt` est affichée à l’époque Unix. |
| `modifiedBy` | L’identifiant de la dernière personne à avoir mis à jour la politique. |
| `modifiedAt` | Heure à laquelle la politique a été mise à jour pour la dernière fois. La propriété `modifiedAt` est affichée à l’époque Unix. |
| `name` | Nom de la politique. |
| `description` | (Facultatif) Propriété pouvant être ajoutée pour fournir des informations supplémentaires sur une politique particulière. |
| `status` | État actuel dʼune politique. Cette propriété définit si une politique est actuellement `active` ou `inactive`. |
| `subjectCondition` | Conditions appliquées à un sujet. Un objet est un utilisateur disposant de certains attributs qui demande l’accès à une ressource pour effectuer une action. Dans ce cas, `subjectCondition` conditions de type requête sont appliquées aux attributs de l’objet. |
| `rules` | Ensemble de règles qui définissent une politique. Les règles définissent les combinaisons d’attributs autorisées pour que le sujet effectue une action vers la ressource. |
| `rules.effect` | Effet obtenu après prise en compte des valeurs pour `action`, `condition` et `resource`. Les valeurs possibles sont : `permit`, `deny` ou `indeterminate`. |
| `rules.resource` | Ressource ou objet auquel un sujet peut ou ne peut pas accéder.  Les ressources peuvent être des fichiers, des applications, des serveurs ou même des API. |
| `rules.condition` | Conditions appliquées à une ressource. Par exemple, si une ressource est un schéma, certains libellés peuvent lui être appliqués et déterminer si une action contre ce schéma est autorisée ou non. |
| `rules.action` | Action qu’un sujet est autorisé à effectuer sur une ressource interrogée. Les valeurs possibles sont les suivantes : `read`, `create`, `edit` et `delete`. |

## Rechercher les détails de la politique par ID {#lookup}

Envoyez une requête GET au point d’entrée `/policies` tout en fournissant un identifiant de politique dans le chemin d’accès de la requête pour récupérer des informations sur cette politique individuelle.

**Format d’API**

```http
GET /policies/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| {POLICY_ID} | L’identifiant de la politique que vous souhaitez récupérer. |

**Requête**

La requête suivante récupère des informations sur une politique individuelle.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/13138ef6-c007-495d-837f-0a248867e219 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une requête réussie renvoie des informations sur l’ID de politique interrogé.

```json
{
  "policies": [
    {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "5555467B5D8013E50A494220@AdobeOrg",
      "createdBy": "example@AdobeID",
      "createdAt": 1652892767559,
      "modifiedBy": "example@AdobeID",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
        {
          "effect": "Deny",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/xql/schemas/*/schema-fields/*",
          "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
          "actions": [
            "com.adobe.action.read",
            "com.adobe.action.write",
            "com.adobe.action.view"
          ]
        },
        {
          "effect": "Permit",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/*/schemas/*/schema-fields/*",
          "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
          "actions": [
            "com.adobe.action.delete"
          ]
        },
        {
          "effect": "Deny",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
          "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
          "actions": [
            "com.adobe.action.write"
          ]
        }
      ],
      "etag": "\"0300593f-0000-0200-0000-62852ff80000\""
    }
  ]
}
```

| Propriété | Description |
| --- | --- |
| `id` | Identifiant qui correspond à une politique. Cet identifiant est généré automatiquement et peut être utilisé pour rechercher, mettre à jour et supprimer une politique. |
| `imsOrgId` | Organisation dans laquelle la politique interrogée est accessible. |
| `createdBy` | L’identifiant de l’utilisateur qui a créé la politique. |
| `createdAt` | Heure à laquelle la politique a été créée. La propriété `createdAt` est affichée à l’époque Unix. |
| `modifiedBy` | L’identifiant de la dernière personne à avoir mis à jour la politique. |
| `modifiedAt` | Heure à laquelle la politique a été mise à jour pour la dernière fois. La propriété `modifiedAt` est affichée à l’époque Unix. |
| `name` | Nom de la politique. |
| `description` | (Facultatif) Propriété pouvant être ajoutée pour fournir des informations supplémentaires sur une politique particulière. |
| `status` | État actuel dʼune politique. Cette propriété définit si une politique est actuellement `active` ou `inactive`. |
| `subjectCondition` | Conditions appliquées à un sujet. Un objet est un utilisateur disposant de certains attributs qui demande l’accès à une ressource pour effectuer une action. Dans ce cas, `subjectCondition` conditions de type requête sont appliquées aux attributs de l’objet. |
| `rules` | Ensemble de règles qui définissent une politique. Les règles définissent les combinaisons d’attributs autorisées pour que le sujet effectue une action vers la ressource. |
| `rules.effect` | Effet obtenu après prise en compte des valeurs pour `action`, `condition` et `resource`. Les valeurs possibles sont : `permit`, `deny` ou `indeterminate`. |
| `rules.resource` | Ressource ou objet auquel un sujet peut ou ne peut pas accéder.  Les ressources peuvent être des fichiers, des applications, des serveurs ou même des API. |
| `rules.condition` | Conditions appliquées à une ressource. Par exemple, si une ressource est un schéma, certains libellés peuvent lui être appliqués et déterminer si une action contre ce schéma est autorisée ou non. |
| `rules.action` | Action qu’un sujet est autorisé à effectuer sur une ressource interrogée. Les valeurs possibles sont les suivantes : `read`, `create`, `edit` et `delete`. |


## Création d’une politique {#create}

Pour créer une politique, envoyez une requête POST au point d’entrée `/policies`.

**Format d’API**

```http
POST /policies
```

**Requête**

La requête suivante crée une politique nommée : `acme-integration-policy`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "name": "acme-integration-policy",
      "description": "Policy for ACME",
      "imsOrgId": "{IMS_ORG}",
      "rules": [
        {
          "effect": "Permit",
          "resource": "/orgs/{IMS_ORG}/sandboxes/*",
          "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
          "actions": [
            "com.adobe.action.read"
          ]
        }
      ]
    }'
```

| Paramètre | Description |
| --- | --- |
| `name` | Nom de la politique. |
| `description` | (Facultatif) Propriété pouvant être ajoutée pour fournir des informations supplémentaires sur une politique particulière. |
| `imsOrgId` | Organisation qui contient la politique. |
| `rules` | Ensemble de règles qui définissent une politique. Les règles définissent les combinaisons d’attributs autorisées pour que le sujet effectue une action vers la ressource. |
| `rules.effect` | Effet obtenu après prise en compte des valeurs pour `action`, `condition` et `resource`. Les valeurs possibles sont : `permit`, `deny` ou `indeterminate`. |
| `rules.resource` | Ressource ou objet auquel un sujet peut ou ne peut pas accéder.  Les ressources peuvent être des fichiers, des applications, des serveurs ou même des API. |
| `rules.condition` | Conditions appliquées à une ressource. Par exemple, si une ressource est un schéma, certains libellés peuvent lui être appliqués et déterminer si une action contre ce schéma est autorisée ou non. |
| `rules.action` | Action qu’un sujet est autorisé à effectuer sur une ressource interrogée. Les valeurs possibles sont les suivantes : `read`, `create`, `edit` et `delete`. |

**Réponse**

Une requête réussie renvoie la nouvelle politique créée, y compris son identifiant de politique unique et les règles associées.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988384458,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Policy for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

| Propriété | Description |
| --- | --- |
| `id` | Identifiant qui correspond à une politique. Cet identifiant est généré automatiquement et peut être utilisé pour rechercher, mettre à jour et supprimer une politique. |
| `name` | Nom d’une politique. |
| `rules` | Ensemble de règles qui définissent une politique. Les règles définissent les combinaisons d’attributs autorisées pour que le sujet effectue une action vers la ressource. |
| `rules.effect` | Effet obtenu après prise en compte des valeurs pour `action`, `condition` et `resource`. Les valeurs possibles sont : `permit`, `deny` ou `indeterminate`. |
| `rules.resource` | Ressource ou objet auquel un sujet peut ou ne peut pas accéder.  Les ressources peuvent être des fichiers, des applications, des serveurs ou même des API. |
| `rules.condition` | Conditions appliquées à une ressource. Par exemple, si une ressource est un schéma, certains libellés peuvent lui être appliqués et déterminer si une action contre ce schéma est autorisée ou non. |
| `rules.action` | Action qu’un sujet est autorisé à effectuer sur une ressource interrogée. Les valeurs possibles sont les suivantes : `read`, `create`, `edit` et `delete`. |


## Mise à jour d’une politique par ID de politique {#put}

Pour mettre à jour les règles d’une politique individuelle, envoyez une requête PUT au point d’entrée `/policies` et indiquez l’identifiant de la politique à mettre à jour dans le chemin de requête.

**Format d’API**

```http
PUT /policies/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| {POLICY_ID} | Identifiant de la politique à mettre à jour. |

**Requête**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/8cf487d7-3642-4243-a8ea-213d72f694b9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
      "imsOrgId": "{IMS_ORG}",
      "name": "test-2",
      "rules": [
      {
        "effect": "Deny",
        "resource": "/orgs/{IMS_ORG}/sandboxes/*",
        "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
        "actions": [
          "com.adobe.action.read"
        ]
      }
    ]
  }'
```

**Réponse**

Une réponse réussie renvoie la politique mise à jour.

```json
{
    "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988866647,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652989297287,
    "name": "test-2",
    "description": null,
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Deny",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

## Mettre à jour les propriétés de la politique {#patch}

Pour mettre à jour les propriétés d’une politique individuelle, envoyez une requête PATCH au point d’entrée `/policies` et indiquez l’identifiant de la politique à mettre à jour dans le chemin de requête.

**Format d’API**

```http
PATCH /policies/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| {POLICY_ID} | Identifiant de la politique à mettre à jour. |

**Requête**

La requête suivante remplace la valeur de `/description` dans l’ID de politique `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "replace",
        "path": "/description",
        "value": "Pre-set policy to be applied for ACME"
      }
    ]
  }'
```

| Opérations | Description |
| --- | --- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour le rôle. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Chemin d’accès du paramètre à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |

**Réponse**

Une réponse réussie renvoie l’ID de politique interrogé avec la description mise à jour.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "acp_accessControlService",
    "createdAt": 1652988384458,
    "modifiedBy": "acp_accessControlService",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Pre-set policy to be applied for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

## Supprimer une politique {#delete}

Pour supprimer une politique, envoyez une requête DELETE au point d’entrée `/policies` et indiquez l’identifiant de la politique à supprimer.

**Format d’API**

```http
DELETE /policies/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| {POLICY_ID} | Lʼidentifiant de la politique que vous souhaitez supprimer. |

**Requête**

La requête suivante supprime la politique portant l’ID `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une réponse réussie renvoie un statut HTTP 204 (Pas de contenu) et un corps vide.

Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) à la politique. Vous recevrez un statut HTTP 404 (Introuvable), car la politique a été supprimée de l’administration.
