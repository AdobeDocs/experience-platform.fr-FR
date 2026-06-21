---
keywords: Experience Platform;accueil;rubriques populaires;lister les sandbox disponibles;lister les sandbox
solution: Experience Platform
title: Point d’entrée de l’API Sandbox disponible
description: Vous pouvez répertorier les sandbox disponibles pour l’utilisateur actuel en adressant une requête GET au point d’entrée des sandbox disponibles.
role: Developer
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
TQID: https://experienceleague.adobe.com/ijchlEdB6CyniZi9O9OC0elSbKK1IeyYlS5EjljU2fc
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: adf04a6a-050f-44bc-a52c-db79ccb22ebf
subfeature_v2:
  - id: a9eb38d5-9d89-492f-af4e-b968a07f2d91
  - id: d21bd11d-08df-4cd6-ad8f-cb59a09de5c0
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 256
ht-degree: 33%

---

# Point d’entrée des sandbox disponibles

>[!NOTE]
>
>Contrairement aux autres points d’entrée fournis dans l’API Sandbox, ce point d’entrée est disponible pour tous les utilisateurs, y compris ceux ne disposant pas d’autorisations d’accès d’administration Sandbox.

Vous pouvez répertorier les sandbox disponibles pour l’utilisateur actuel en adressant une requête GET au point d’entrée des sandbox disponibles.

**Format d’API**

```http
GET /{QUERY_PARAMS}
```

| Paramètre | Description |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs en fonction desquels filtrer les résultats. Voir le [document annexe](./appendix.md#query) pour obtenir une liste des paramètres disponibles. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Réponse**

Une réponse réussie renvoie une liste de sandbox disponibles pour l’utilisateur actuel, y compris des détails tels que `name`, `title`, `state` et `type`.

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
| `state` | L’état de traitement actuel du sandbox. Un sandbox peut avoir l’un des états suivants : <ul><li>`creating` : le sandbox a été créé, mais est toujours en cours d’approvisionnement par le système.</li><li>`active` : le sandbox est créé et actif.</li><li>`failed` : en raison d’une erreur, le sandbox n’a pas pu être configuré par le système et est désactivé.</li><li>`deleted` : le sandbox a été désactivé manuellement.</li></ul> |
| `type` | Le type de sandbox : « développement » ou « production ». |
| `isDefault` | Propriété booléenne indiquant si ce sandbox est le sandbox de production par défaut de l’organisation. |
| `eTag` | L’identifiant d’une version spécifique du sandbox. Utilisée pour le contrôle des versions et une mise en cache efficace, cette valeur est mise à jour chaque fois que le sandbox est modifié. |
