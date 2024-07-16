---
keywords: Experience Platform;accueil;rubriques populaires;répertorier les environnements de test disponibles;répertorier les environnements de test
solution: Experience Platform
title: Point de terminaison de l’API Sandbox disponible
description: Vous pouvez répertorier les environnements de test disponibles pour l’utilisateur actuel en envoyant une requête de GET au point de terminaison des environnements de test disponibles.
role: Developer
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 30%

---

# Point de terminaison des environnements de test disponibles

>[!NOTE]
>
>Contrairement aux autres points de terminaison fournis dans l’API Sandbox, ce point de terminaison est disponible pour tous les utilisateurs, y compris ceux qui ne disposent pas des autorisations d’accès à Sandbox Administration.

Vous pouvez répertorier les environnements de test disponibles pour l’utilisateur actuel en envoyant une requête de GET au point de terminaison des environnements de test disponibles.

**Format d’API**

```http
GET /{QUERY_PARAMS}
```

| Paramètre | Description |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs pour filtrer les résultats. Consultez le [document de l’annexe](./appendix.md#query) pour obtenir la liste des paramètres disponibles. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
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
| `name` | Le nom du sandbox. Utilisé à des fins de recherche dans les appels API. |
| `title` | Le nom d’affichage du sandbox. |
| `state` | L’état de traitement actuel du sandbox. Un sandbox peut avoir l’un des états suivants : <ul><li>`creating` : l’environnement de test a été créé, mais le système continue de le configurer.</li><li>`active` : l’environnement de test est créé et actif.</li><li>`failed` : en raison d’une erreur, le système n’a pas pu configurer l’environnement de test et est désactivé.</li><li>`deleted` : l’environnement de test a été désactivé manuellement.</li></ul> |
| `type` | Le type de sandbox : « développement » ou « production ». |
| `isDefault` | Une propriété booléenne indiquant si cet environnement de test est l’environnement de test de production par défaut pour l’organisation. |
| `eTag` | L’identifiant d’une version spécifique du sandbox. Utilisée pour le contrôle des versions et une mise en cache efficace, cette valeur est mise à jour chaque fois que le sandbox est modifié. |
