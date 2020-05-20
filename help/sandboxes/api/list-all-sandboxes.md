---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Liste de tous les sandbox
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 2%

---


# Liste de tous les sandbox

Pour liste de tous les sandbox appartenant à votre organisation IMS (actifs ou non), envoyez une requête GET au point de `/sandboxes` terminaison.

**Format d’API**

```http
GET /sandboxes
```

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste de sandbox appartenant à votre organisation, y compris des détails tels que `name`, `title`, `state`et `type`.

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
    ]
}
```

| Propriété | Description |
| --- | --- |
| `name` | Nom du sandbox. Utilisé à des fins de recherche dans les appels d’API. |
| `title` | Nom d’affichage du sandbox. |
| `state` | Etat de traitement actuel du sandbox. L’état d’un sandbox peut être l’un des suivants : <br/><ul><li>**création**: Le sandbox a été créé, mais est toujours en cours d&#39;approvisionnement par le système.</li><li>**actif**: Le sandbox est créé et actif.</li><li>**échec**: En raison d&#39;une erreur, le sandbox n&#39;a pas pu être configuré par le système et est désactivé.</li><li>**supprimé**: Le sandbox a été désactivé manuellement.</li></ul> |
| `type` | Type de sandbox, &quot;développement&quot; ou &quot;production&quot;. |
| `isDefault` | Propriété booléenne indiquant si ce sandbox est le sandbox par défaut pour l’organisation. Il s’agit généralement du sandbox de production. |
| `eTag` | Identificateur d’une version spécifique du sandbox. Utilisée pour le contrôle des versions et l’efficacité de la mise en cache, cette valeur est mise à jour chaque fois qu’une modification est apportée au sandbox. |
