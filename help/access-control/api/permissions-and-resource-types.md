---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' des noms des autorisations et des types de ressources'
topic: developer guide
translation-type: tm+mt
source-git-commit: 7b354a96d70332cf7a7e9eff322cd3d6ee0fc96a

---


#  des noms des autorisations et des types de ressources

Vous pouvez  les noms de tous les types de ressources et d’autorisations en envoyant une requête GET au `/acl/reference` point de fin. Ces noms peuvent ensuite être utilisés dans les appels d’API pour [des stratégies](./effective-policies.md) efficaces pour l’utilisateur actuel.

Une **autorisation** est une stratégie gérée par l’intermédiaire d’Adobe Admin Console et mappée à zéro ou plusieurs stratégies de type ressource. Un type **de** ressource est une stratégie qui active des fonctionnalités de lecture, d’écriture et/ou de suppression pour un type spécifique de ressource de plateforme (tels que des jeux de données ou des  de).

**Format API**

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

Une réponse réussie renvoie un `permissions` objet et un `resource-types` objet, chacun contenant un complet de noms pour les autorisations d’accès ou les types de ressources, respectivement.

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
