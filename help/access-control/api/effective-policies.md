---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' des stratégies efficaces'
topic: developer guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


#  des stratégies efficaces

Pour  des stratégies efficaces pour l’utilisateur actuel, faites une requête POST au point de `/acl/effective-policies` fin dans l’API . Les autorisations et les types de ressources que vous souhaitez récupérer doivent être fournis dans la charge utile de requête sous la forme d’un tableau. Ceci est illustré dans l’exemple d’appel d’API ci-dessous.

**Format API**

```http
POST /acl/effective-policies
```

**Requête**

Les requêtes suivantes récupèrent des informations sur l’autorisation &quot;Gérer les jeux de données&quot; et l’accès au type de ressource &quot;&quot; pour l’utilisateur actuel.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE] Pour obtenir un complet des autorisations et des types de ressources pouvant être fournis dans le tableau de charge utile, reportez-vous à la section de l’annexe sur les autorisations [acceptées et les types](#accepted-permissions-and-resource-types)de ressources.

**Réponse**

Une réponse réussie renvoie des informations sur les autorisations et les types de ressources fournis dans la requête. La réponse inclut les autorisations actives dont dispose l’utilisateur actuel pour les types de ressource spécifiés dans la requête. Si des autorisations incluses dans la charge utile de requête sont actives pour l’utilisateur actuel, l’API renvoie l’autorisation avec un astérisque (`*`) pour indiquer que l’autorisation est active. Les autorisations fournies dans la requête qui ne sont pas actives pour l’utilisateur sont ignorées de la charge utile de réponse.

```json
{
    "policies": {
        "/resource-types/schemas": [
            "read",
            "write",
            "delete"
        ],
        "/permissions/manage-datasets": [
            "*"
        ]
    }
}
```

## Étapes suivantes

Ce  décrit comment effectuer des appels à l’API  pour renvoyer des informations sur les autorisations actives et les stratégies associées pour les types de ressources. Pour plus d’informations sur les  de la plateforme d’expérience, reportez-vous à la présentation [du  de](../home.md).

## Annexe

Cette section fournit des informations supplémentaires sur l’utilisation de l’API .

### Autorisations et types de ressources acceptés

Vous trouverez ci-dessous un  d’autorisations et de types de ressources que vous pouvez inclure dans la charge utile d’une requête POST au point de `/acl/active-permissions` fin.

**Autorisations**

```plaintext
"permissions/activate-destinations"
"permissions/export-audience-for-segments"
"permissions/manage-datasets"
"permissions/manage-destinations"
"permissions/manage-identity-namespaces"
"permissions/manage-profiles"
"permissions/manage-sandboxes"
"permissions/manage-schemas"
"permissions/reset-sandboxes"
"permissions/view-datasets"
"permissions/view-destinations"
"permissions/view-identity-namespaces"
"permissions/view-monitoring-dashboard"
"permissions/view-profiles"
"permissions/view-sandboxes"
"permissions/view-schemas"
```

**Types de ressource**

```plaintext
"resource-types/classes"
"resource-types/connections"
"resource-types/data-types"
"resource-types/dataset-data"
"resource-types/datasets"
"resource-types/destinations"
"resource-types/dule-labels"
"resource-types/identity-descriptors"
"resource-types/identity-namespaces"
"resource-types/mixins"
"resource-types/monitoring"
"resource-types/profile-configs
"resource-types/profile-datasets"
"resource-types/profiles"
"resource-types/relationship-descriptors"
"resource-types/reset-sandboxes"
"resource-types/sandboxes"
"resource-types/schemas"
"resource-types/segment-jobs"
"resource-types/segments"
```
