---
keywords: Experience Platform ; accueil ; rubriques populaires ; trouver un sandbox ; rechercher un sandbox
solution: Experience Platform
title: Recherche d’un sandbox dans l’API
topic: guide du développeur
description: Vous pouvez rechercher un sandbox individuel en effectuant une requête de GET qui inclut la propriété name du sandbox dans le chemin de la requête.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 80%

---


# Recherche d’un sandbox dans l’API

Vous pouvez rechercher un environnement de test individuel en effectuant une requête GET comprenant la propriété `name` de l’environnement de test dans le chemin de requête.

**Format d’API**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | La propriété `name` de l’environnement de test que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère un environnement de test nommé « dev-2 ».

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de l’environnement de test, y compris son `name`, `title`, `state` et `type`.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| Propriété | Description |
| --- | --- |
| `name` | Le nom de l’environnement de test. Utilisé à des fins de recherche dans les appels API. |
| `title` | Le nom d’affichage de l’environnement de test. |
| `state` | L’état de traitement actuel de l’environnement de test. L’état d’un environnement de test peut correspondre à l’un des suivants : <ul><li>**création** : l’environnement de test a été créé, mais le système continue de le configurer.</li><li>**actif** : l’environnement de test est créé et actif.</li><li>**échec** : en raison d’une erreur, le système n’a pas pu configurer l’environnement de test et a été désactivé.</li><li>**supprimé** : l’environnement de test a été désactivé manuellement.</li></ul> |
| `type` | Le type d’environnement de test : « développement » ou « production ». |
| `isDefault` | Une propriété booléenne indiquant s’il s’agit de l’environnement de test par défaut de l’organisation. Il s’agit généralement de l’environnement de test de production. |
| `eTag` | L’identifiant d’une version spécifique de l’environnement de test. Utilisée pour le contrôle des versions et une mise en cache efficace, cette valeur est mise à jour chaque fois que l’environnement de test est modifié. |