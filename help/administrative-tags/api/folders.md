---
title: Point d’entrée des dossiers
description: Découvrez comment créer, mettre à jour, gérer et supprimer des dossiers à l’aide des API Adobe Experience Platform.
role: Developer
exl-id: ee43d699-725d-4ffd-a71b-049eeb3b4d7c
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 5%

---

# Point d’entrée des dossiers

>[!IMPORTANT]
>
>L’URL du point d’entrée pour ce jeu de points d’entrée est `https://experience.adobe.io`.

Les dossiers sont une fonctionnalité qui vous permet de mieux organiser vos objets commerciaux pour une navigation et une catégorisation plus simples.

Ce guide fournit des informations pour vous aider à mieux comprendre les dossiers et comprend des exemples d’appels API pour effectuer des actions de base à l’aide de l’API.

## Prise en main

Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, y compris les en-têtes requis et la manière de lire des exemples d’appels API.

## Récupération d’une liste de dossiers {#list}

Vous pouvez récupérer une liste de dossiers appartenant à votre organisation en envoyant une requête GET au point d’entrée `/folder` et en spécifiant le type de dossier et l’identifiant du dossier parent.

**Format d’API**

```http
GET /folders/{FOLDER_TYPE}/{PARENT_FOLDER_ID}/subfolders
```

| Paramètre | Description |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Type d’objets contenus dans le dossier. Les valeurs prises en charge comprennent `segment` et `dataset`. |
| `{PARENT_FOLDER_ID}` | L’identifiant du dossier parent à partir duquel vous récupérez la liste des dossiers. Pour afficher la liste de tous les dossiers parents, utilisez l’`root` d’ID de dossier. |

**Requête**

+++Exemple de requête pour répertorier tous les dossiers de jeux de données de niveau supérieur

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/root/subfolders
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec une liste de tous les dossiers de niveau supérieur pour le jeu de données de votre organisation.

+++Exemple de réponse contenant une liste de tous les dossiers de niveau supérieur pour le jeu de données de votre organisation.

```json
{
    "id": "c626b4f7-223b-4486-8900-00c266e31dd1",
    "name": "ParentFolder",
    "noun": "Dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": null,
    "createdAt": "2023-01-12T03:31:00.118+00:00",
    "modifiedBy": null,
    "modifiedAt": "2023-01-13T05:47:06.718+00:00",
    "_links": null,
    "children": [
        {
            "id": "09d86b23-4819-471b-8a2a-05774ed268de",
            "name": "ChildFolder.1",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-12T12:51:39.284+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-12T12:51:39.284+00:00",
            "_links": null,
            "children": []
        },
        {
            "id": "fd2f6a68-ef65-470d-ab31-b02b7b2241ca",
            "name": "ChildFolder.2",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-13T03:38:40.006+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-13T03:38:40.006+00:00",
            "_links": null,
            "children": []
        }
    ]
}
```

+++

## Créer un dossier {#create}

Vous pouvez créer un dossier en adressant une requête POST au point d’entrée `/folder` et en spécifiant le type de dossier.

**Format d’API**

```http
POST /folders/{FOLDER_TYPE}
```

| Paramètre | Description |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Type d’objets contenus dans le dossier. Les valeurs prises en charge comprennent `segment` et `dataset`. |

**Requête**

+++Exemple de requête pour créer un dossier.

```shell
curl -X POST https://experience.adobe.io/unifiedfolders/folders/dataset
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "name": "SampleFolder",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5"
 }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom du dossier à créer. |
| `parentId` | L’identifiant du dossier parent. |

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails du dossier que vous venez de créer.

+++Exemple de réponse contenant des détails sur le dossier que vous venez de créer.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": null
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | L’identifiant du dossier nouvellement créé. |
| `createdBy` | Identifiant de l’utilisateur qui a créé le dossier. |
| `createdAt` | Date et heure de la création du dossier. |
| `modifiedBy` | L’identifiant de la dernière personne ayant modifié le dossier. |
| `modifiedAt` | Date et heure de la dernière mise à jour du dossier. |

+++

## Récupération d’un dossier spécifique {#get}

Vous pouvez récupérer un dossier spécifique qui appartient à votre organisation en adressant une requête GET au point d’entrée `/folder` et en spécifiant le type de dossier et l’identifiant du dossier.

**Format d’API**

```http
GET /folders/{FOLDER_TYPE}/{FOLDER_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Type d’objets contenus dans le dossier. Les valeurs prises en charge comprennent `segment` et `dataset`. |
| `{FOLDER_ID}` | L’identifiant du dossier que vous récupérez. |

**Requête**

+++Exemple de requête pour récupérer un dossier spécifique

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails du dossier demandé.

+++Exemple de réponse contenant des détails sur le dossier demandé.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | L’identifiant du dossier demandé. |
| `name` | Nom du dossier demandé. |
| `parentId` | L’identifiant du dossier parent. |
| `createdBy` | Identifiant de l’utilisateur qui a créé le dossier. |
| `createdAt` | Date et heure de la création du dossier. |
| `modifiedBy` | ID du dernier utilisateur à avoir mis à jour le dossier. |
| `modifiedAt` | Date et heure de la dernière mise à jour du dossier. |
| `status` | Statut du dossier demandé. Les valeurs prises en charge comprennent `IN_USE` et `ARCHIVED`. |

+++

## Validation d’un dossier spécifié {#validate}

Vous pouvez vérifier si un dossier est éligible pour contenir des objets en envoyant une requête GET au point d’entrée `/folder/{FOLDER_TYPE}/{FOLDER_ID}/validate` et en fournissant le type de dossier et l’identifiant.

**Format d’API**

```http
GET /folders/{FOLDER_TYPE}/{FOLDER_ID}/validate
```

| Paramètre | Description |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Type d’objets contenus dans le dossier. Les valeurs prises en charge comprennent `segment` et `dataset`. |
| `{FOLDER_ID}` | L’identifiant du dossier que vous validez. |

**Requête**

+++Exemple de requête pour valider un dossier spécifique

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Un statut réussi renvoie un statut HTTP 200 avec les détails du dossier que vous validez.

+++Un exemple de réponse contient les détails du dossier validé

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

+++

## Mettre à jour un dossier spécifique {#update}

Vous pouvez mettre à jour les détails d’un dossier spécifique qui appartient à votre organisation en envoyant une requête PATCH au point d’entrée `/folder` et en spécifiant le type de dossier et l’identifiant du dossier.

**Format d’API**

```http
PATCH /folders/{FOLDER_TYPE}/{FOLDER_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Type d’objets contenus dans le dossier. Les valeurs prises en charge comprennent `segment` et `dataset`. |
| `{FOLDER_ID}` | L’identifiant du dossier que vous mettez à jour. |

**Requête**

+++Exemple de requête pour mettre à jour un dossier spécifique

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '[{
    "op": "replace",
    "path": "/name",
    "value": "RenamedSampleFolder"
 }]'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations sur votre dossier nouvellement mis à jour.

```json
{
    "id": "eafab5bf-3457-4b7f-b366-3c5399bd98f1",
    "name": "RenamedSampleFolder",
    "noun": "dataset",
    "parentFolderId": null,
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "183807A65A0F5D180A494004@AdobeID",
    "createdAt": "2024-03-05T01:42:36.910+00:00",
    "modifiedBy": "183807A65A0F5D180A494004@AdobeID",
    "modifiedAt": "2024-03-05T01:45:54.740+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/eafab5bf-3457-4b7f-b366-3c5399bd98f1"
        }
    },
    "namespace": null
}
```

## Suppression d’un dossier spécifique {#delete}

Vous pouvez supprimer un dossier spécifique qui appartient à votre organisation en adressant une requête DELETE au `/folder` et en spécifiant le type de dossier et l’identifiant du dossier.

***Format API**

```http
DELETE /folders/{FOLDER_TYPE}/{FOLDER_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{FOLDER_TYPE}` | Type d’objets contenus dans le dossier. Les valeurs prises en charge comprennent `segment` et `dataset`. |
| `{FOLDER_ID}` | L’identifiant du dossier que vous supprimez. |

**Requête**

+++Exemple de requête pour supprimer un dossier spécifique

```shell
curl -X DELETE https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec un corps de message vous informant de la suppression du dossier.

```json
{
    "message": "delete request accepted successfully"
}
```

## Étapes suivantes

Vous êtes arrivé au bout de ce guide. À présent, vous comprenez mieux comment créer, gérer et supprimer des dossiers à l’aide de l’API Adobe Experience Platform.
