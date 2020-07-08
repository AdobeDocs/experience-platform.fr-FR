---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Annexe du guide du développeur Catalog Service
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 1%

---


# Annexe du guide du développeur Catalog Service

Ce document contient des informations supplémentaires pour vous aider à utiliser l’API Catalogue.

## Vue d’objets liés {#view-interrelated-objects}

Certains objets de catalogue peuvent être interconnectés avec d’autres objets de catalogue. Les champs précédés de préfixes `@` dans les charges de réponse désignent les objets associés. Les valeurs de ces champs prennent la forme d’un URI, qui peut être utilisé dans une requête GET distincte pour récupérer les objets associés qu’ils représentent.

L&#39;exemple de jeu de données renvoyé dans le document lors de la [recherche d&#39;un jeu](look-up-object.md) de données spécifique contient un `files` champ avec la valeur URI suivante : `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. Le contenu du `files` champ peut être visualisé en utilisant cet URI comme chemin d’accès pour une nouvelle requête GET.

**Format d’API**

```http
GET {OBJECT_URI}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_URI}` | URI fourni par le champ d’objet interlié (à l’exclusion du `@` symbole). |

**Requête**

La requête suivante utilise l&#39;URI fournie avec la `files` propriété de l&#39;exemple de jeu de données pour récupérer une liste des fichiers associés au jeu de données.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d’objets associés. Dans cet exemple, une liste de fichiers de dataset est renvoyée.

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

## Effectuer plusieurs requêtes dans un seul appel

Le point de terminaison racine de l’API Catalog permet d’effectuer plusieurs requêtes au sein d’un seul appel. La charge utile de requête contient un tableau d’objets représentant ce qui serait normalement des requêtes individuelles, qui sont ensuite exécutées dans l’ordre.

Si ces requêtes sont des modifications ou des ajouts au catalogue et que l’une des modifications échoue, toutes les modifications sont annulées.

**Format d’API**

```http
POST /
```

**Requête**

La requête suivante crée un nouveau jeu de données, puis crée des vues connexes pour ce jeu de données. Cet exemple illustre l’utilisation du langage de modèle pour accéder aux valeurs renvoyées dans des appels précédents en vue de les utiliser dans des appels ultérieurs.

Par exemple, si vous souhaitez référencer une valeur renvoyée par une sous-requête précédente, vous pouvez créer une référence au format suivant : `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (où `{REQUEST_ID}` est l’identifiant fourni par l’utilisateur pour la sous-requête, comme illustré ci-dessous). Vous pouvez référencer n’importe quel attribut disponible dans le corps de l’objet de réponse d’une sous-requête précédente à l’aide de ces modèles.

>[!NOTE]
>
>Lorsqu’une sous-requête exécutée renvoie uniquement la référence à un objet (comme c’est le cas par défaut pour la plupart des requêtes POST et PUT dans l’API Catalog), cette référence est mise en alias par rapport à la valeur `id` et peut être utilisée comme `<<{OBJECT_ID}.id>>`valeur.

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
| `id` | ID fourni par l’utilisateur et attaché à l’objet de réponse afin que vous puissiez faire correspondre des requêtes à des réponses. Le catalogue ne stocke pas cette valeur et la renvoie simplement dans la réponse à des fins de référence. |
| `resource` | Chemin d’accès à la ressource relatif à la racine de l’API Catalogue. Le protocole et le domaine ne doivent pas faire partie de cette valeur et doivent être précédés de &quot;/&quot;. <br/><br/> Lorsque vous utilisez PATCH ou DELETE comme sous-requête `method`, incluez l’ID d’objet dans le chemin d’accès à la ressource. À ne pas confondre avec l’utilisateur `id`, le chemin de ressource utilise l’ID de l’objet Catalog lui-même (par exemple, `resource: "/dataSets/1234567890"`). |
| `method` | Nom de la méthode (GET, PUT, POST, PATCH ou DELETE) associé à l’action en cours dans la demande. |
| `body` | document JSON qui serait normalement transmis en tant que charge utile dans une demande POST, PUT ou PATCH. Cette propriété n’est pas requise pour les requêtes GET ou DELETE. |

**Réponse**

Une réponse réussie renvoie un tableau d’objets contenant les objets `id` que vous avez affectés à chaque requête, le code d’état HTTP de la requête individuelle et la réponse `body`. Comme les trois exemples de requêtes visaient tous à créer de nouveaux objets, le tableau `body` de chaque objet est un tableau contenant uniquement l’identifiant de l’objet nouvellement créé, comme c’est le cas avec les réponses POST les plus réussies dans le catalogue.

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

Soyez prudent lors de l’inspection de la réponse à une requête multiple, car vous devrez vérifier le code de chaque sous-requête individuelle et ne pas vous fier uniquement au code d’état HTTP de la requête POST parente.  Il est possible qu’une seule sous-requête renvoie une requête 404 (telle qu’une requête GET sur une ressource non valide) alors que la requête globale renvoie 200.

## En-têtes de demande supplémentaires

Le catalogue fournit plusieurs conventions d’en-tête pour vous aider à préserver l’intégrité de vos données lors des mises à jour.

### Si-Correspondance

Il est recommandé d’utiliser le contrôle de version d’objet pour éviter le type de corruption de données qui se produit lorsqu’un objet est enregistré par plusieurs utilisateurs presque simultanément.

Lors de la mise à jour d’un objet, il est recommandé d’effectuer d’abord un appel d’API à la vue (GET) pour l’objet à mettre à jour. Contenu dans la réponse (et tout appel où la réponse contient un seul objet) est un `E-Tag` en-tête contenant la version de l’objet. Si vous Ajoutez la version d’objet en tant qu’en-tête de requête nommé `If-Match` dans vos appels de mise à jour (PUT ou PATCH), la mise à jour ne réussira que si la version est toujours identique, ce qui évitera les collisions de données.

Si les versions ne correspondent pas (l&#39;objet a été modifié par un autre processus depuis que vous l&#39;avez récupéré), vous recevrez l&#39;état HTTP 412 (Échec de la précondition) indiquant que l&#39;accès à la ressource de cible a été refusé.

### Pragma

Il peut arriver que vous souhaitiez valider un objet sans enregistrer les informations. L’utilisation de l’ `Pragma` en-tête avec la valeur de `validate-only` permet d’envoyer des requêtes POST ou PUT à des fins de validation uniquement, ce qui empêche la persistance de toute modification des données.

## Compression des données

Compaction est un service Experience Platform qui fusionne les données de petits fichiers en fichiers plus volumineux sans modifier les données. Pour des raisons de performances, il est parfois bénéfique de combiner un ensemble de petits fichiers en fichiers plus volumineux afin de fournir un accès plus rapide aux données lors de l’interrogation.

Lorsque les fichiers d’un lot assimilé ont été compactés, l’objet Catalog associé est mis à jour à des fins de surveillance.