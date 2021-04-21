---
keywords: Experience Platform ; accueil ; rubriques populaires ; liste principal sandbox ; liste sandbox
solution: Experience Platform
title: Liste Principale de sandbox pour l’utilisateur actuel dans l’API
topic-legacy: developer guide
description: Vous pouvez liste les sandbox principaux pour l’utilisateur actuel en adressant une demande de GET au point de terminaison racine.
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 63%

---

# Liste de sandbox principaux pour l’utilisateur actuel dans l’API

>[!NOTE]
>
>Contrairement aux autres points de terminaison fournis dans l’API Sandbox, ce point de terminaison est disponible pour tous les utilisateurs, y compris ceux ne disposant pas des autorisations d’accès à Sandbox Administration.

Vous pouvez répertorier les environnements de test actifs de l’utilisateur actuel en effectuant une requête GET sur le point de terminaison racine (`/`).

**Format d’API**

```http
GET /{QUERY_PARAMS}
```

| Paramètre | Description |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs en fonction desquels filtrer les résultats. Pour plus d&#39;informations, consultez la section [Paramètres de requête](#query). |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste des environnements de test actifs de l’utilisateur actuel, y compris des détails tels que `name`, `title`, `state` et `type`.

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
| `state` | L’état de traitement actuel de l’environnement de test. L’état d’un environnement de test peut correspondre à l’un des suivants : <ul><li>**création** : l’environnement de test a été créé, mais le système continue de le configurer.</li><li>**actif** : l’environnement de test est créé et actif.</li><li>**échec** : en raison d’une erreur, le système n’a pas pu configurer l’environnement de test et a été désactivé.</li><li>**supprimé** : l’environnement de test a été désactivé manuellement.</li></ul> |
| `type` | Le type d’environnement de test : « développement » ou « production ». |
| `isDefault` | Une propriété booléenne indiquant s’il s’agit de l’environnement de test par défaut de l’organisation. Il s’agit généralement de l’environnement de test de production. |
| `eTag` | L’identifiant d’une version spécifique de l’environnement de test. Utilisée pour le contrôle des versions et une mise en cache efficace, cette valeur est mise à jour chaque fois que l’environnement de test est modifié. |

## Utilisation des paramètres de requête {#query}

L’API [[!DNL Sandbox]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) prend en charge l’utilisation de paramètres de requête sur la page et filtre les résultats lors de la mise en liste des sandbox.

>[!NOTE]
>
>Les paramètres de requête `limit` et `offset` doivent être spécifiés ensemble. Si vous n&#39;en spécifiez qu&#39;un seul, l&#39;API renvoie une erreur. Si vous n’en spécifiez aucune, la limite par défaut est de 50 et le décalage est de 0.

| Paramètre | Description |
| --------- | ----------- |
| `limit` | Nombre maximal d&#39;enregistrements à renvoyer dans la réponse. |
| `offset` | Nombre d&#39;entités entre le premier enregistrement et le début (décalé) de la liste de réponse. |
