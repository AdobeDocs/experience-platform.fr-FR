---
keywords: Experience Platform ; accueil ; rubriques populaires ; sandbox de liste
solution: Experience Platform
title: Sandbox de liste dans l’API
topic: guide du développeur
description: Pour liste de tous les sandbox appartenant à votre organisation IMS (principal ou non), envoyez une demande de GET au point de terminaison /sandbox.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 62%

---


# sandbox de liste dans l’API

Pour répertorier tous les environnements de test appartenant à votre organisation IMS (actifs ou non), effectuez une requête GET vers le point de terminaison `/sandboxes`.

**Format d’API**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Paramètre | Description |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs en fonction desquels filtrer les résultats. Pour plus d&#39;informations, consultez la section [Paramètres de requête](#query). |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d’environnements de test appartenant à votre organisation, y compris des détails tels que `name`, `title`, `state` et `type`.

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
        },
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
    ],
    "_page": {
        "limit": 4,
        "count": 4
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes/?limit={limit}&offset={offset}",
            "templated": true
        },
        "prev": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=0&limit=1",
            "templated": null
        },
        "page": {
            "href": "https://platform-int.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=1&limit=1",
            "templated": null
        }
    }
}
```

| Propriété | Description |
| --- | --- |
| `name` | Le nom de l’environnement de test. Utilisé à des fins de recherche dans les appels API. |
| `title` | Le nom d’affichage de l’environnement de test. |
| `state` | L’état de traitement actuel de l’environnement de test. Un environnement de test peut avoir l’un des états suivants : <br/><ul><li>**création** : l’environnement de test a été créé, mais le système continue de le configurer.</li><li>**actif** : l’environnement de test est créé et actif.</li><li>**échec** : en raison d’une erreur, le système n’a pas pu configurer l’environnement de test et a été désactivé.</li><li>**supprimé** : l’environnement de test a été désactivé manuellement.</li></ul> |
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