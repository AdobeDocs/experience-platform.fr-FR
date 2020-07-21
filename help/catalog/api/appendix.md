---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Annexe du guide de développement du service de catalogue
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 78%

---


# [!DNL Catalog Service] annexe du guide du développeur

This document contains additional information to help you work with the [!DNL Catalog] API.

## Affichage d’objets interconnectés {#view-interrelated-objects}

Some [!DNL Catalog] objects can be interrelated with other [!DNL Catalog] objects. Tout champ précédé du préfixe `@` dans les payloads de réponse indique les objets associés. Les valeurs de ces champs prennent la forme d’un URI qui peut être utilisé dans une requête GET distincte pour récupérer les objets associés qu’ils représentent.

L’exemple de jeu de données renvoyé dans le document sur la [recherche d’un jeu de données spécifique](look-up-object.md) contient un champ `files` avec la valeur URI suivante : `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. Le contenu du champ `files` peut être visualisé en utilisant cet URI comme chemin d’accès à une nouvelle requête GET.

**Format d’API**

```http
GET {OBJECT_URI}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_URI}` | L’URI fourni par le champ d’objet interconnecté (hors symbole `@`). |

**Requête**

La requête suivante utilise l’URI fourni dans la propriété `files` de l’exemple de jeu de données pour récupérer une liste des fichiers associés au jeu de données.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d’objets associés. Dans cet exemple, une liste de fichiers de jeux de données est renvoyé.

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573256315368,
        "updated": 1573256315368
    },
    "148ac690-0280-11ea-8d23-8571a35dce49-1": {
        "id": "148ac690-0280-11ea-8d23-8571a35dce49-1",
        "batchId": "148ac690-0280-11ea-8d23-8571a35dce49",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573255982433,
        "updated": 1573255982433
    },
    "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1": {
        "id": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1",
        "batchId": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## Exécution de plusieurs requêtes dans un même appel

The root endpoint of the [!DNL Catalog] API allows for multiple requests to be made within a single call. Le payload de requête contient un tableau d’objets représentant ce qui serait normalement des requêtes individuelles, qui sont ensuite exécutées dans l’ordre.

If these requests are modifications or additions to [!DNL Catalog] and any one of the changes fails, all changes will revert.

**Format d’API**

```http
POST /
```

**Requête**

La requête suivante crée un jeu de données, puis crée des vues connexes pour ce jeu de données. Cet exemple montre comment utiliser le langage de modèle pour accéder aux valeurs renvoyées dans les précédents appels et les utiliser dans les appels suivants.

Par exemple, si vous souhaitez référencer une valeur renvoyée par une sous-requête précédente, vous pouvez créer une référence au format suivant : `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (`{REQUEST_ID}` correspondant à l’identifiant fourni par l’utilisateur pour la sous-requête, comme illustré ci-dessous). Vous pouvez référencer n’importe quel attribut disponible dans le corps d’objet de réponse d’une sous-requête précédente à l’aide de ces modèles.

>[!NOTE]
>
> Lorsqu’une sous-requête exécutée renvoie uniquement la référence à un objet (comme c’est le cas par défaut pour la plupart des requêtes POST et PUT dans l’API Catalog), cette référence reçoit la valeur `id` comme alias et peut être utilisée comme `<<{OBJECT_ID}.id>>`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "id": "firstObjectId",
      "resource": "/dataSets",
      "method": "post",
      "body": {
        "type": "raw",
        "name": "First Dataset"
      }
    }, 
    {
      "id": "secondObjectId",
      "resource": "/datasetViews",
      "method": "post",
      "body": {
        "status": "enabled",
        "dataSetId": "<<firstObjectId.id>>"
      }
    }
  ]'
```

| Propriété | Description |
| --- | --- |
| `id` | L’identifiant fourni par l’utilisateur et joint à l’objet de réponse afin d’améliorer la correspondance entre requêtes et réponses. [!DNL Catalog] ne stocke pas cette valeur et la renvoie simplement dans la réponse à des fins de référence. |
| `resource` | The resource path relative to the root of the [!DNL Catalog] API. Le protocole et le domaine ne doivent pas faire partie de cette valeur et doivent être précédés du symbole « / ». <br/><br/> En cas d’utilisation de PATCH ou DELETE comme `method` de sous-requête, incluez l’identifiant d’objet dans le chemin d’accès à la ressource. Not to be confused with the user-supplied `id`, the resource path uses the ID of the [!DNL Catalog] object itself (for example, `resource: "/dataSets/1234567890"`). |
| `method` | Le nom de la méthode (GET, PUT, POST, PATCH ou DELETE) associée à l’action de la requête. |
| `body` | Le document JSON normalement transmis comme payload d’une requête POST, PUT ou PATCH. Cette propriété n’est pas requise pour les requêtes GET ou DELETE. |

**Réponse**

Une réponse réussie renvoie un tableau d’objets contenant l’`id` affecté à chaque requête, le code d’état HTTP de la requête individuelle et la réponse `body`. Since the three sample requests were all to create new objects, the `body` of each object is an array containing only the ID of the newly created object, as is the standard with most successful POST responses in [!DNL Catalog].

```json
[
    {
        "id": "firstObjectId",
        "code": 200,
        "body": [
            "@/dataSets/5be230aef5b02914cd52dbfa"
        ]
    },
    {
        "id": "secondObjectId",
        "code": 200,
        "body": [
            "@/dataSetViews/5be230aef5b02914cd52dbfb"
        ]
    }
]
```

Soyez vigilant lors de l’inspection de la réponse à une requête multiple. En effet, vous devez vérifier le code de chaque sous-requête individuelle et ne pas vous fier uniquement au code d’état HTTP de la requête POST parente.  Il est possible qu’une sous-requête unique renvoie un code 404 (par exemple une requête GET sur une ressource non valide), alors que la requête globale renvoie un code 200.

## En-têtes de requête supplémentaires

[!DNL Catalog] fournit plusieurs conventions d’en-tête pour vous aider à maintenir l’intégrité de vos données lors des mises à jour.

### If-Match

Il est recommandé d’utiliser le contrôle de version d’objet pour éviter le type de corruption de données qui se produit lorsqu’un objet est enregistré presque simultanément par plusieurs utilisateurs.

Lors de la mise à jour d’un objet, il est recommandé d’effectuer d’abord un appel API pour afficher (GET) l’objet à mettre à jour. Un en-tête `E-Tag` contenant la version de l’objet est contenu dans la réponse (et dans tout appel de réponse contenant un objet unique). L’ajout de la version d’objet en tant qu’en-tête de requête nommé `If-Match` dans vos appels de mise à jour (PUT ou PATCH) entraîne la réussite de la mise à jour seulement si la version est toujours la même, ce qui permet d’éviter les collisions de données.

Si les versions ne correspondent pas (l’objet a été modifié par un autre processus depuis que vous l’avez récupéré), vous recevrez un état HTTP 412 (Precondition Failed) indiquant que l’accès à la ressource cible a été refusé.

### Pragma

Il peut arriver que vous souhaitiez valider un objet sans enregistrer les informations. L’utilisation de l’en-tête `Pragma` avec la valeur `validate-only` permet d’envoyer des requêtes POST ou PUT à des fins de validation uniquement, ce qui empêche la persistance de toute modification des données.

## Compactage des données

Compaction is an [!DNL Experience Platform] service that merges data from small files into larger files without changing any data. Pour des raisons de performances, il est parfois bénéfique de combiner un ensemble de petits fichiers en fichiers plus volumineux afin de fournir un accès plus rapide aux données lors de l’interrogation.

When the files in an ingested batch have been compacted, its associated [!DNL Catalog] object is updated for monitoring purposes.