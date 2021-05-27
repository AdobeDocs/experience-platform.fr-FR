---
keywords: Experience Platform;accueil;rubriques populaires;répertorier les environnements de test disponibles;répertorier les environnements de test
solution: Experience Platform
title: Point de terminaison de l’API Sandbox disponible
topic-legacy: developer guide
description: Vous pouvez répertorier les environnements de test disponibles pour l’utilisateur actuel en envoyant une requête de GET au point de terminaison des environnements de test disponibles.
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
source-git-commit: f00e6161d82f1fd7ba442be9f06283f3c866573f
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 41%

---

# Point de terminaison des environnements de test disponibles

>[!NOTE]
>
>Contrairement aux autres points de terminaison fournis dans l’API Sandbox, ce point de terminaison est disponible pour tous les utilisateurs, y compris ceux ne disposant pas des autorisations d’accès à Sandbox Administration.

Vous pouvez répertorier les environnements de test disponibles pour l’utilisateur actuel en envoyant une requête de GET au point de terminaison des environnements de test disponibles.

**Format d’API**

```http
GET /{QUERY_PARAMS}
```

| Paramètre | Description |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs en fonction desquels filtrer les résultats. Consultez le [document de l’annexe](./appendix.md#query) pour obtenir la liste des paramètres disponibles. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Réponse**

Une réponse réussie renvoie une liste d’environnements de test disponibles pour l’utilisateur actuel, y compris des détails tels que `name`, `title`, `state` et `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 3,
        "count": 1
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/?limit={limit}&offset={offset}",
            "templated": true
        }
    }
}
```

| Propriété | Description |
| --- | --- |
| `name` | Le nom de l’environnement de test. Utilisé à des fins de recherche dans les appels API. |
| `title` | Le nom d’affichage de l’environnement de test. |
| `state` | L’état de traitement actuel de l’environnement de test. L’état d’un environnement de test peut correspondre à l’un des suivants : <ul><li>`creating`: L’environnement de test a été créé, mais le système continue de le configurer.</li><li>`active`: L’environnement de test est créé et principal.</li><li>`failed`: En raison d’une erreur, le système n’a pas pu configurer l’environnement de test et est désactivé.</li><li>`deleted`: L’environnement de test a été désactivé manuellement.</li></ul> |
| `type` | Le type d’environnement de test : « développement » ou « production ». |
| `isDefault` | Une propriété booléenne indiquant si cet environnement de test est l’environnement de test de production par défaut pour l’organisation. |
| `eTag` | L’identifiant d’une version spécifique de l’environnement de test. Utilisée pour le contrôle des versions et une mise en cache efficace, cette valeur est mise à jour chaque fois que l’environnement de test est modifié. |
