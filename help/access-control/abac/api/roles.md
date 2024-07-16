---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;contrôle d’accès basé sur les attributs;contrôle d’accès basé sur les attributs
solution: Experience Platform
title: Point de terminaison de l’API Rôles
description: Le point de terminaison /rôles de l’API de contrôle d’accès basé sur les attributs vous permet de gérer les rôles par programmation dans Adobe Experience Platform.
role: Developer
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 27%

---

# Point de terminaison des rôles

>[!NOTE]
>
>Si un jeton utilisateur est transmis, l’utilisateur du jeton doit disposer d’un rôle &quot;d’administrateur org&quot; pour l’organisation demandée.

Les rôles définissent l’accès dont dispose un administrateur, un spécialiste ou un utilisateur final aux ressources de votre entreprise. Dans un environnement de contrôle d’accès basé sur les rôles, la configuration de l’accès des utilisateurs est regroupée suivant les responsabilités et les besoins communs. Un rôle possède un jeu d’autorisations déterminé et les membres de votre organisation peuvent être affectés à un ou plusieurs rôles, selon la portée de l’accès en lecture ou en écriture dont ils ont besoin.

Le point d’entrée `/roles` de l’API de contrôle d’accès basé sur les attributs vous permet de gérer par programmation les rôles dans votre organisation.

## Commencer

Le point de terminaison API utilisé dans ce guide fait partie de l’API de contrôle d’accès basé sur les attributs. Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Récupération d’une liste de rôles {#list}

Vous pouvez répertorier tous les rôles existants appartenant à votre organisation en envoyant une requête GET au point de terminaison `/roles`.

**Format d’API**

```http
GET /roles/
```

**Requête**

La requête suivante récupère une liste de rôles appartenant à votre organisation.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une réponse réussie renvoie une liste de rôles de votre organisation, y compris des informations sur leur type de rôle respectif, leurs jeux d’autorisations et leurs attributs d’objet.

```json
{
  "roles": [
    {
      "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "name": "Administrator Role",
      "description": "Role for administrator type of responsibilities and access",
      "roleType": "user-defined",
      "permissionSets": [
        "manage-datasets",
        "manage-schemas"
      ],
      "sandboxes": [
        "prod"
      ],
      "subjectAttributes": {
        "labels": [
          "core/S1"
        ]
      },
      "createdBy": "{CREATED_BY}",
      "createdAt": 1648153201825,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1648153201825,
      "etag": null
    }
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "next": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "subjects": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    }
  }
}
```

| Propriété | Description |
| --- | --- |
| `id` | Identifiant qui correspond au rôle. Cet identifiant est généré automatiquement. |
| `name` | Nom de votre rôle. |
| `description` | La propriété description fournit des informations supplémentaires sur votre rôle. |
| `roleType` | Type désigné du rôle. Les valeurs possibles pour le type de rôle sont : `user-defined` et `system-defined`. |
| `permissionSets` | Les jeux d’autorisations représentent un groupe d’autorisations qu’un administrateur peut appliquer à un rôle. Un administrateur peut attribuer des jeux d’autorisations à un rôle au lieu d’affecter des autorisations individuelles. Vous pouvez ainsi créer des rôles personnalisés à partir d’un rôle prédéfini contenant un groupe d’autorisations. |
| `sandboxes` | Cette propriété affiche les environnements de test de votre organisation configurés pour un rôle particulier. |
| `subjectAttributes` | Attributs qui indiquent la corrélation entre un objet et les ressources de Platform auxquelles ils ont accès. |
| `subjectAttributes.labels` | Affiche les libellés d’utilisation des données appliqués au rôle interrogé. |

## Recherche d’un rôle {#lookup}

Vous pouvez rechercher un rôle individuel en effectuant une requête de GET qui inclut le `roleId` correspondant dans le chemin de la requête.

**Format d’API**

```http
GET /roles/{ROLE_ID}
```

| Paramètre | Description |
| --- | --- |
| {ROLE_ID} | L’identifiant du rôle que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère des informations pour `{ROLE_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une réponse réussie renvoie les détails de l’ID de rôle interrogé, y compris des informations sur son type de rôle, ses jeux d’autorisations et ses attributs d’objet.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Propriété | Description |
| --- | --- |
| `id` | Identifiant qui correspond au rôle. Cet identifiant est généré automatiquement. |
| `name` | Nom de votre rôle. |
| `description` | La propriété description fournit des informations supplémentaires sur votre rôle. |
| `roleType` | Type désigné du rôle. Les valeurs possibles pour le type de rôle sont : `user-defined` et `system-defined`. |
| `permissionSets` | Les jeux d’autorisations représentent un groupe d’autorisations qu’un administrateur peut appliquer à un rôle. Un administrateur peut attribuer des jeux d’autorisations à un rôle au lieu d’affecter des autorisations individuelles. Vous pouvez ainsi créer des rôles personnalisés à partir d’un rôle prédéfini contenant un groupe d’autorisations. |
| `sandboxes` | Cette propriété affiche les environnements de test de votre organisation configurés pour un rôle particulier. |
| `subjectAttributes` | Attributs qui indiquent la corrélation entre un objet et les ressources de Platform auxquelles ils ont accès. |
| `subjectAttributes.labels` | Affiche les libellés d’utilisation des données appliqués au rôle interrogé. |

## Recherche de sujets par identifiant de rôle

Vous pouvez également récupérer des sujets en envoyant une requête GET au point de terminaison `/roles` tout en fournissant un {ROLE_ID}.

**Format d’API**

```http
GET /roles/{ROLE_ID}/subjects
```

| Paramètre | Description |
| --- | --- |
| {ROLE_ID} | L’identifiant du rôle associé aux sujets que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère les sujets associés à `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une réponse réussie renvoie les sujets associés à l’ID de rôle interrogé, y compris l’ID de sujet et le type d’objet correspondants.

```json
{
  "items": [
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "PIRJ7WE5T3QT9Z4TCLVH86DE@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "WHPWE00MC26SHZ7AKBFG403D@AdobeID"
      },
  ]
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
      "self": {
          "href": "/roles/{ROLE_ID}/subjects",
          "templated": false,
          "type": null,
          "method": null
      },
      "page": {
          "href": "/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
          "templated": true,
          "type": null,
          "method": null
      }
  }
}
```

| Propriété | Description |
| --- | --- |
| `roleId` | Identifiant du rôle associé à l’objet interrogé. |
| `subjectType` | Type de l’objet interrogé. |
| `subjectId` | Identifiant qui correspond à l’objet interrogé. |

## Création d’un rôle {#create}

Pour créer un nouveau rôle, envoyez une requête de POST au point de terminaison `/roles` tout en fournissant des valeurs pour le nom, la description et le type de rôle de votre rôle.

**Format d’API**

```http
POST /roles/
```

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator Role",
    "description": "Role for administrator type of responsibilities and access",
    "roleType": "user-defined"
  }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de votre rôle. Assurez-vous que le nom de votre rôle est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre rôle. |
| `description` | (Facultatif) Une valeur descriptive que vous pouvez inclure pour fournir plus d’informations sur votre rôle. |
| `roleType` | Type désigné du rôle. Les valeurs possibles pour le type de rôle sont : `user-defined` et `system-defined`. |

**Réponse**

Une réponse réussie renvoie votre nouveau rôle, avec son identifiant de rôle correspondant, ainsi que des informations sur son type de rôle, ses jeux d’autorisations et les attributs de sujet.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Propriété | Description |
| --- | --- |
| `id` | Identifiant qui correspond au rôle. Cet identifiant est généré automatiquement. |
| `name` | Nom de votre rôle. |
| `description` | La propriété description fournit des informations supplémentaires sur votre rôle. |
| `roleType` | Type désigné du rôle. Les valeurs possibles pour le type de rôle sont : `user-defined` et `system-defined`. |
| `permissionSets` | Les jeux d’autorisations représentent un groupe d’autorisations qu’un administrateur peut appliquer à un rôle. Un administrateur peut attribuer des jeux d’autorisations à un rôle au lieu d’affecter des autorisations individuelles. Vous pouvez ainsi créer des rôles personnalisés à partir d’un rôle prédéfini contenant un groupe d’autorisations. |
| `sandboxes` | Cette propriété affiche les environnements de test de votre organisation configurés pour un rôle particulier. |
| `subjectAttributes` | Attributs qui indiquent la corrélation entre un objet et les ressources de Platform auxquelles ils ont accès. |
| `subjectAttributes.labels` | Affiche les libellés d’utilisation des données appliqués au rôle interrogé. |

## Mettre à jour un rôle {#patch}

Vous pouvez mettre à jour les propriétés d’un rôle en envoyant une requête de PATCH au point de terminaison `/roles` tout en fournissant l’identifiant de rôle et les valeurs correspondants pour les opérations que vous souhaitez appliquer.

**Format d’API**

```http
PATCH /roles/{ROLE_ID}
```

| Paramètre | Description |
| --- | --- |
| {ROLE_ID} | L’identifiant du rôle que vous souhaitez mettre à jour. |

**Requête**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/description",
        "value": "Role with permission sets for admin type of access"
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

Une réponse réussie renvoie le rôle mis à jour, y compris les nouvelles valeurs des propriétés que vous avez choisi de mettre à jour.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Propriété | Description |
| --- | --- |
| `id` | Identifiant qui correspond au rôle. Cet identifiant est généré automatiquement. |
| `name` | Nom de votre rôle. |
| `description` | La propriété description fournit des informations supplémentaires sur votre rôle. |
| `roleType` | Type désigné du rôle. Les valeurs possibles pour le type de rôle sont : `user-defined` et `system-defined`. |
| `permissionSets` | Les jeux d’autorisations représentent un groupe d’autorisations qu’un administrateur peut appliquer à un rôle. Un administrateur peut attribuer des jeux d’autorisations à un rôle au lieu d’affecter des autorisations individuelles. Vous pouvez ainsi créer des rôles personnalisés à partir d’un rôle prédéfini contenant un groupe d’autorisations. |
| `sandboxes` | Cette propriété affiche les environnements de test de votre organisation configurés pour un rôle particulier. |
| `subjectAttributes` | Attributs qui indiquent la corrélation entre un objet et les ressources de Platform auxquelles ils ont accès. |
| `subjectAttributes.labels` | Affiche les libellés d’utilisation des données appliqués au rôle interrogé. |

## Mise à jour d’un rôle par identifiant de rôle {#put}

Vous pouvez mettre à jour un rôle en envoyant une requête de PUT au point de terminaison `/roles` et en spécifiant l’ID de rôle correspondant au rôle que vous souhaitez mettre à jour.

**Format d’API**

```http
PUT /roles/{ROLE_ID}
```

**Requête**

La requête suivante met à jour le nom, la description et le type de rôle pour l’ID de rôle : `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator role for ACME",
    "description": "New administrator role for ACME",
    "roleType": "user-defined"
  }'
```

| Paramètre | Description |
| --- | --- |
| `name` | Nom mis à jour d’un rôle. |
| `description` | Description mise à jour d’un rôle. |
| `roleType` | Type désigné du rôle. Les valeurs possibles pour le type de rôle sont : `user-defined` et `system-defined`. |

**Réponse**

Une réponse réussie renvoie votre rôle mis à jour, y compris les nouvelles valeurs pour son nom, sa description et son type de rôle.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator role for ACME",
  "description": "New administrator role for ACME",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Propriété | Description |
| --- | --- |
| `id` | Identifiant qui correspond au rôle. Cet identifiant est généré automatiquement. |
| `name` | Nom de votre rôle. |
| `description` | La propriété description fournit des informations supplémentaires sur votre rôle. |
| `roleType` | Type désigné du rôle. Les valeurs possibles pour le type de rôle sont : `user-defined` et `system-defined`. |
| `permissionSets` | Les jeux d’autorisations représentent un groupe d’autorisations qu’un administrateur peut appliquer à un rôle. Un administrateur peut attribuer des jeux d’autorisations à un rôle au lieu d’affecter des autorisations individuelles. Vous pouvez ainsi créer des rôles personnalisés à partir d’un rôle prédéfini contenant un groupe d’autorisations. |
| `sandboxes` | Cette propriété affiche les environnements de test de votre organisation configurés pour un rôle particulier. |
| `subjectAttributes` | Attributs qui indiquent la corrélation entre un objet et les ressources de Platform auxquelles ils ont accès. |
| `subjectAttributes.labels` | Affiche les libellés d’utilisation des données appliqués au rôle interrogé. |

## Mettre à jour le sujet par ID de rôle

Pour mettre à jour les sujets associés à un rôle, envoyez une requête de PATCH au point de terminaison `/roles` tout en fournissant l’ID de rôle des sujets que vous souhaitez mettre à jour.

**Format d’API**

```http
PATCH /roles/{ROLE_ID}/subjects
```

| Paramètre | Description |
| --- | --- |
| {ROLE_ID} | Identifiant du rôle associé aux sujets que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour les sujets associés à `{ROLE_ID}`.

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/user",
        "value": "{USER ID}"
    }
]' 
```

| Opérations | Description |
| --- | --- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour le rôle. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Chemin d’accès du paramètre à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |

**Réponse**

Une réponse réussie renvoie votre rôle mis à jour, y compris les nouvelles valeurs pour les sujets.

```json
{
  "subjects": [
    [
      {
        "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID",
        "subjectType": "user"
      }
    ]
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
      "templated": true
    }
  }
}
```

## Suppression d’un rôle {#delete}

Pour supprimer un rôle, envoyez une requête de DELETE au point de terminaison `/roles` tout en spécifiant l’identifiant du rôle que vous souhaitez supprimer.

**Format d’API**

```http
DELETE /roles/{ROLE_ID}
```

| Paramètre | Description |
| --- | --- |
| {ROLE_ID} | L’identifiant du rôle que vous souhaitez supprimer. |

**Requête**

La requête suivante supprime le rôle avec l’ID `{ROLE_ID}`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.

Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) au rôle . Vous recevrez un état HTTP 404 (Not Found), car le rôle a été supprimé de l’administration.

## Ajout d’informations d’identification d’API {#apicredential}

Pour ajouter des informations d’identification d’API, envoyez une requête de PATCH au point de terminaison `/roles` tout en fournissant l’ID de rôle des sujets.

**Format d’API**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/api-integration",
        "value": "{TECHNICAL ACCOUNT ID}"
    }
]'   
```

| Opérations | Description |
| --- | --- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour le rôle. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Le chemin du paramètre à ajouter. |
| `value` | La valeur avec laquelle vous souhaitez ajouter votre paramètre. |

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.
