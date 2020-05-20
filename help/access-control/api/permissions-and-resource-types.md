---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Noms de Liste des autorisations et des types de ressources
topic: developer guide
translation-type: tm+mt
source-git-commit: 7b354a96d70332cf7a7e9eff322cd3d6ee0fc96a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---


# Noms de Liste des autorisations et des types de ressources

Vous pouvez liste les noms de tous les types d’autorisations et de ressources en envoyant une requête GET au point de `/acl/reference` terminaison. Ces noms peuvent ensuite être utilisés dans les appels d’API pour [vue des stratégies](./effective-policies.md) efficaces pour l’utilisateur actuel.

Une **autorisation** est une stratégie gérée par l’intermédiaire d’Adobe Admin Console et qui correspond à zéro ou plusieurs stratégies de type ressource. Un type **de** ressource est une stratégie qui active des fonctionnalités de lecture, d&#39;écriture et/ou de suppression pour un type spécifique de ressource de plateforme (par exemple, des jeux de données ou des schémas).

**Format d’API**

```http
GET /acl/reference
```

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/acl/reference \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Réponse**

Une réponse réussie renvoie un `permissions` objet et un `resource-types` objet, chacun contenant une liste complète de noms pour les autorisations d&#39;accès ou les types de ressources, respectivement.

```json
{
  "permissions": {
    "export-audience-for-segment": {
      "segments": [
        "read"
      ]
    },
    "manage-datasets": {
      "connection": [
        "read",
        "write",
        "delete"
      ],
      "datasets": [
        "read",
        "write",
        "delete"
      ]
    }
    {"..."}
  },
  "resource-types": {
    "classes": [
      "read",
      "write",
      "delete"
    ],
    "connection": [
      "read",
      "write",
      "delete"
    ],
    "data-types": [
      "read",
      "write",
      "delete"
    ],
    "...": [
      "..."
    ]
  }
}
```
