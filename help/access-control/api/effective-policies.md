---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Vue de politiques efficaces
topic: developer guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 1%

---


# Vue de politiques efficaces

Pour vue des stratégies efficaces pour l’utilisateur actuel, envoyez une requête POST au point de `/acl/effective-policies` terminaison dans l’API de Contrôle d&#39;accès. Les autorisations et types de ressources que vous souhaitez récupérer doivent être fournis dans la charge utile de la demande sous la forme d&#39;un tableau. Ceci est démontré dans l’exemple d’appel d’API ci-dessous.

**Format d’API**

```http
POST /acl/effective-policies
```

**Requête**

Les requêtes suivantes récupèrent des informations sur l&#39;autorisation &quot;Gérer les jeux de données&quot; et l&#39;accès au type de ressource &quot;schémas&quot; pour l&#39;utilisateur actuel.

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

>[!NOTE] Pour obtenir une liste complète des autorisations et des types de ressources qui peuvent être fournis dans le tableau de charge utile, reportez-vous à la section de l&#39;annexe sur les autorisations [acceptées et les types](#accepted-permissions-and-resource-types)de ressources.

**Réponse**

Une réponse réussie renvoie des informations sur les autorisations et les types de ressources fournis dans la requête. La réponse inclut les autorisations actives dont dispose l&#39;utilisateur actuel pour les types de ressources spécifiés dans la requête. Si des autorisations incluses dans la charge utile de requête sont actives pour l’utilisateur actuel, l’API renvoie l’autorisation avec un astérisque (`*`) pour indiquer que l’autorisation est active. Toutes les autorisations fournies dans la requête qui ne sont pas actives pour l’utilisateur sont ignorées de la charge utile de réponse.

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

Ce document décrit comment appeler l&#39;API Contrôle d&#39;accès pour renvoyer des informations sur les autorisations actives et les stratégies associées pour les types de ressources. Pour plus d’informations sur le contrôle d&#39;accès pour la plateforme d’expérience, voir la présentation [du](../home.md)contrôle d&#39;accès.

## Annexe

Cette section fournit des informations supplémentaires sur l’utilisation de l’API de Contrôle d&#39;accès.

### Autorisations et types de ressources acceptés

Vous trouverez ci-dessous une liste d’autorisations et de types de ressources que vous pouvez inclure dans la charge utile d’une requête POST au point de `/acl/active-permissions` terminaison.

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
