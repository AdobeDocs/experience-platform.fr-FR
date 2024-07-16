---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;contrôle d’accès basé sur les attributs;contrôle d’accès basé sur les attributs
solution: Experience Platform
title: Point de terminaison de l’API Access Control Policies
description: Le point de terminaison /policies de l’API de contrôle d’accès basé sur les attributs vous permet de gérer par programmation les stratégies dans Adobe Experience Platform.
role: Developer
exl-id: 07690f43-fdd9-4254-9324-84e6bd226743
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 10%

---

# Point de terminaison des stratégies de contrôle d’accès

>[!NOTE]
>
>Si un jeton utilisateur est transmis, l’utilisateur du jeton doit disposer d’un rôle &quot;d’administrateur org&quot; pour l’organisation demandée.

Les politiques de contrôle d&#39;accès sont des déclarations qui rassemblent les attributs pour établir les actions permises et non autorisées. Ces politiques peuvent être locales ou globales et peuvent remplacer d’autres politiques. Le point d’entrée `/policies` de l’API de contrôle d’accès basé sur les attributs vous permet de gérer par programmation les stratégies, y compris des informations sur les règles qui les régissent ainsi que leurs conditions d’objet respectives.

>[!IMPORTANT]
>
>Ce point de terminaison ne doit pas être confondu avec le point de terminaison `/policies` de l’ [API Policy Service](../../../data-governance/api/policies.md), qui est utilisé pour gérer les stratégies d’utilisation des données.

## Commencer

Le point de terminaison API utilisé dans ce guide fait partie de l’API de contrôle d’accès basé sur les attributs. Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Récupération dʼune liste de politiques {#list}

Envoyez une requête de GET au point de terminaison `/policies` pour répertorier toutes les stratégies existantes dans votre organisation.

**Format d’API**

```http
GET /policies
```

**Requête**

La requête suivante récupère une liste des stratégies existantes.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une réponse réussie renvoie une liste des stratégies existantes.

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
| `id` | Identifiant qui correspond à une stratégie. Cet identifiant est généré automatiquement et peut être utilisé pour rechercher, mettre à jour et supprimer une stratégie. |
| `imsOrgId` | L’organisation dans laquelle la stratégie interrogée est accessible. |
| `createdBy` | L’identifiant de l’utilisateur qui a créé la stratégie. |
| `createdAt` | Heure de création de la stratégie. La propriété `createdAt` s’affiche dans l’horodatage de l’époque unix. |
| `modifiedBy` | ID de l’utilisateur qui a mis à jour la stratégie pour la dernière fois. |
| `modifiedAt` | Heure de la dernière mise à jour de la stratégie. La propriété `modifiedAt` s’affiche dans l’horodatage de l’époque unix. |
| `name` | Nom de la stratégie. |
| `description` | (Facultatif) Une propriété qui peut être ajoutée pour fournir des informations supplémentaires sur une stratégie spécifique. |
| `status` | État actuel dʼune politique. Cette propriété définit si une stratégie est actuellement `active` ou `inactive`. |
| `subjectCondition` | Conditions appliquées à un sujet. Un sujet est un utilisateur avec certains attributs qui demande l’accès à une ressource pour effectuer une action. Dans ce cas, `subjectCondition` sont des conditions de type requête appliquées aux attributs d’objet. |
| `rules` | Ensemble de règles qui définissent une stratégie. Les règles définissent les combinaisons d’attributs autorisées pour que le sujet exécute correctement une action sur la ressource. |
| `rules.effect` | Effet résultant de la prise en compte des valeurs de `action`, `condition` et `resource`. Les valeurs possibles sont : `permit`, `deny` ou `indeterminate`. |
| `rules.resource` | Ressource ou objet auquel un sujet peut ou ne peut pas accéder.  Les ressources peuvent être des fichiers, des applications, des serveurs ou même des API. |
| `rules.condition` | Conditions appliquées à une ressource. Par exemple, si une ressource est un schéma, certains libellés peuvent lui être appliqués, ce qui contribue à déterminer si une action contre ce schéma est admissible ou non. |
| `rules.action` | Action autorisée d’un sujet par rapport à une ressource interrogée. Les valeurs possibles sont les suivantes : `read`, `create`, `edit` et `delete`. |

## Recherche des détails de la stratégie par identifiant {#lookup}

Effectuez une requête de GET au point de terminaison `/policies` tout en fournissant un identifiant de stratégie dans le chemin de requête pour récupérer des informations sur cette stratégie individuelle.

**Format d’API**

```http
GET /policies/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| {POLICY_ID} | L’identifiant de la stratégie que vous souhaitez récupérer. |

**Requête**

La requête suivante récupère des informations sur une stratégie individuelle.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/13138ef6-c007-495d-837f-0a248867e219 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une requête réussie renvoie des informations sur l’ID de stratégie interrogé.

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
| `id` | Identifiant qui correspond à une stratégie. Cet identifiant est généré automatiquement et peut être utilisé pour rechercher, mettre à jour et supprimer une stratégie. |
| `imsOrgId` | L’organisation dans laquelle la stratégie interrogée est accessible. |
| `createdBy` | L’identifiant de l’utilisateur qui a créé la stratégie. |
| `createdAt` | Heure de création de la stratégie. La propriété `createdAt` s’affiche dans l’horodatage de l’époque unix. |
| `modifiedBy` | ID de l’utilisateur qui a mis à jour la stratégie pour la dernière fois. |
| `modifiedAt` | Heure de la dernière mise à jour de la stratégie. La propriété `modifiedAt` s’affiche dans l’horodatage de l’époque unix. |
| `name` | Nom de la stratégie. |
| `description` | (Facultatif) Une propriété qui peut être ajoutée pour fournir des informations supplémentaires sur une stratégie spécifique. |
| `status` | État actuel dʼune politique. Cette propriété définit si une stratégie est actuellement `active` ou `inactive`. |
| `subjectCondition` | Conditions appliquées à un sujet. Un sujet est un utilisateur avec certains attributs qui demande l’accès à une ressource pour effectuer une action. Dans ce cas, `subjectCondition` sont des conditions de type requête appliquées aux attributs d’objet. |
| `rules` | Ensemble de règles qui définissent une stratégie. Les règles définissent les combinaisons d’attributs autorisées pour que le sujet exécute correctement une action sur la ressource. |
| `rules.effect` | Effet résultant de la prise en compte des valeurs de `action`, `condition` et `resource`. Les valeurs possibles sont : `permit`, `deny` ou `indeterminate`. |
| `rules.resource` | Ressource ou objet auquel un sujet peut ou ne peut pas accéder.  Les ressources peuvent être des fichiers, des applications, des serveurs ou même des API. |
| `rules.condition` | Conditions appliquées à une ressource. Par exemple, si une ressource est un schéma, certains libellés peuvent lui être appliqués, ce qui contribue à déterminer si une action contre ce schéma est admissible ou non. |
| `rules.action` | Action autorisée d’un sujet par rapport à une ressource interrogée. Les valeurs possibles sont les suivantes : `read`, `create`, `edit` et `delete`. |


## Création d’une politique {#create}

Pour créer une nouvelle stratégie, envoyez une requête de POST au point de terminaison `/policies`.

**Format d’API**

```http
POST /policies
```

**Requête**

La requête suivante crée une nouvelle stratégie nommée : `acme-integration-policy`.

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
| `name` | Nom de la stratégie. |
| `description` | (Facultatif) Une propriété qui peut être ajoutée pour fournir des informations supplémentaires sur une stratégie spécifique. |
| `imsOrgId` | L’organisation qui contient la stratégie. |
| `rules` | Ensemble de règles qui définissent une stratégie. Les règles définissent les combinaisons d’attributs autorisées pour que le sujet exécute correctement une action sur la ressource. |
| `rules.effect` | Effet résultant de la prise en compte des valeurs de `action`, `condition` et `resource`. Les valeurs possibles sont : `permit`, `deny` ou `indeterminate`. |
| `rules.resource` | Ressource ou objet auquel un sujet peut ou ne peut pas accéder.  Les ressources peuvent être des fichiers, des applications, des serveurs ou même des API. |
| `rules.condition` | Conditions appliquées à une ressource. Par exemple, si une ressource est un schéma, certains libellés peuvent lui être appliqués, ce qui contribue à déterminer si une action contre ce schéma est admissible ou non. |
| `rules.action` | Action autorisée d’un sujet par rapport à une ressource interrogée. Les valeurs possibles sont les suivantes : `read`, `create`, `edit` et `delete`. |

**Réponse**

Une requête réussie renvoie la nouvelle stratégie, y compris son identifiant de stratégie unique et les règles associées.

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
| `id` | Identifiant qui correspond à une stratégie. Cet identifiant est généré automatiquement et peut être utilisé pour rechercher, mettre à jour et supprimer une stratégie. |
| `name` | Nom d’une stratégie. |
| `rules` | Ensemble de règles qui définissent une stratégie. Les règles définissent les combinaisons d’attributs autorisées pour que le sujet exécute correctement une action sur la ressource. |
| `rules.effect` | Effet résultant de la prise en compte des valeurs de `action`, `condition` et `resource`. Les valeurs possibles sont : `permit`, `deny` ou `indeterminate`. |
| `rules.resource` | Ressource ou objet auquel un sujet peut ou ne peut pas accéder.  Les ressources peuvent être des fichiers, des applications, des serveurs ou même des API. |
| `rules.condition` | Conditions appliquées à une ressource. Par exemple, si une ressource est un schéma, certains libellés peuvent lui être appliqués, ce qui contribue à déterminer si une action contre ce schéma est admissible ou non. |
| `rules.action` | Action autorisée d’un sujet par rapport à une ressource interrogée. Les valeurs possibles sont les suivantes : `read`, `create`, `edit` et `delete`. |


## Mise à jour d’une stratégie par identifiant de stratégie {#put}

Pour mettre à jour les règles d’une stratégie individuelle, envoyez une requête de PUT au point de terminaison `/policies` tout en fournissant l’identifiant de la stratégie que vous souhaitez mettre à jour dans le chemin d’accès de la requête.

**Format d’API**

```http
PUT /policies/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| {POLICY_ID} | L’identifiant de la stratégie que vous souhaitez mettre à jour. |

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

Une réponse réussie renvoie la stratégie mise à jour.

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

## Mise à jour des propriétés de stratégie {#patch}

Pour mettre à jour les propriétés d’une stratégie individuelle, envoyez une requête de PATCH au point de terminaison `/policies` tout en fournissant l’identifiant de la stratégie que vous souhaitez mettre à jour dans le chemin d’accès de la requête.

**Format d’API**

```http
PATCH /policies/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| {POLICY_ID} | L’identifiant de la stratégie que vous souhaitez mettre à jour. |

**Requête**

La requête suivante remplace la valeur de `/description` dans l’ID de stratégie `c3863937-5d40-448d-a7be-416e538f955e`.

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

Une réponse réussie renvoie l’identifiant de stratégie interrogé avec une description mise à jour.

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

Pour supprimer une stratégie, envoyez une requête de DELETE au point de terminaison `/policies` tout en fournissant l’identifiant de la stratégie que vous souhaitez supprimer.

**Format d’API**

```http
DELETE /policies/{POLICY_ID}
```

| Paramètre | Description |
| --- | --- |
| {POLICY_ID} | Lʼidentifiant de la politique que vous souhaitez supprimer. |

**Requête**

La requête suivante supprime la stratégie avec l’ID `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.

Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) à la stratégie. Vous recevrez le statut HTTP 404 (Introuvable) car la stratégie a été supprimée de l’administration.
