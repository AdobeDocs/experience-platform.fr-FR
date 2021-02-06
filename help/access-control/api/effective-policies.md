---
keywords: Experience Platform ; accueil ; thèmes populaires ; stratégies efficaces ; api contrôle d'accès
solution: Experience Platform
title: Point de terminaison de l’API Stratégies efficaces
topic: developer guide
description: Le contrôle d’accès dans Adobe Experience Platform vous permet de gérer les rôles et les autorisations pour diverses fonctionnalités de Platform à l’aide d’Adobe Admin Console. Ce document sert de guide pour la vue de stratégies efficaces à l’aide de l’API contrôle d'accès pour Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 68%

---


# Point final des politiques efficaces

Pour afficher des stratégies efficaces pour l’utilisateur actuel, envoyez une requête POST au point de terminaison `/acl/effective-policies` dans l’API [!DNL Access Control] Les autorisations et les types de ressources que vous souhaitez récupérer doivent être fournis dans le payload de la requête sous la forme de tableau. Ceci est illustré dans l’exemple d’appel API ci-dessous.

**Format d’API**

```http
POST /acl/effective-policies
```

**Requête**

Les requêtes suivantes récupèrent des informations sur l&#39;autorisation &quot;[!UICONTROL Gérer les jeux de données]&quot; et l&#39;accès au type de ressource &quot;[!UICONTROL schémas]&quot; pour l&#39;utilisateur actuel.

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

>[!NOTE]
>
>Pour obtenir une liste complète des autorisations et des types de ressources pouvant être fournis dans le tableau de payload, reportez-vous à la section de l’annexe sur [les autorisations acceptées et les types de ressources](#accepted-permissions-and-resource-types).

**Réponse**

Une réponse réussie renvoie des informations sur les autorisations et les types de ressources fournis dans la requête. La réponse inclut les autorisations actives dont dispose l’utilisateur actuel pour les types de ressources spécifiés dans la requête. Si des autorisations incluses dans le payload de la requête sont actives pour l’utilisateur actuel, l’API renvoie l’autorisation avec un astérisque (`*`) pour indiquer que l’autorisation est active. Les autorisations fournies dans la requête qui ne sont pas actives pour l’utilisateur sont omises du payload de réponse.

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

Ce document décrit comment appeler l&#39;API [!DNL Access Control] pour renvoyer des informations sur les autorisations principales et les stratégies associées pour les types de ressources. Pour plus d&#39;informations sur le contrôle d&#39;accès pour [!DNL Experience Platform], consultez la [présentation du contrôle d&#39;accès](../home.md).

## Annexe

Cette section fournit des informations supplémentaires sur l&#39;utilisation de l&#39;API [!DNL Access Control].

### Autorisations et types de ressources acceptés

Vous trouverez ci-dessous une liste d’autorisations et de types de ressources que vous pouvez inclure dans le payload d’une requête POST envoyée au point de terminaison `/acl/active-permissions`.

**Autorisations**

```plaintext
permissions/activate-destinations
permissions/evaluate-segments
permissions/execute-decisioning-activities
permissions/export-audience-for-segment
permissions/manage-datasets
permissions/manage-decisioning-activities
permissions/manage-decisioning-options
permissions/manage-destinations
permissions/manage-dsw
permissions/manage-dule-labels
permissions/manage-dule-policies
permissions/manage-identity-namespaces
permissions/manage-privacy-workflows
permissions/manage-profile-configs
permissions/manage-profiles
permissions/manage-queries
permissions/manage-schemas
permissions/manage-segments
permissions/manage-sources
permissions/reset-sandboxes
permissions/view-datasets
permissions/view-destinations
permissions/view-dule-labels
permissions/view-dule-policies
permissions/view-identity-namespaces
permissions/view-monitoring-dashboard
permissions/view-privacy-workflows
permissions/view-profile-configs
permissions/view-profiles
permissions/view-sandboxes
permissions/view-schemas
permissions/view-segments
permissions/view-sources
```

**Types de ressource**

```plaintext
resource-types/activation-associations
resource-types/activations
resource-types/activities
resource-types/analytics-source
resource-types/audience-manager-source
resource-types/bizible-source
resource-types/connection
resource-types/customer-attributes-source
resource-types/data-science-workspace
resource-types/dataset-preview
resource-types/datasets
resource-types/dule-label
resource-types/dule-policy
resource-types/enterprise-source
resource-types/identity-descriptor
resource-types/identity-namespaces
resource-types/launch-source
resource-types/marketing-action
resource-types/marketo-source
resource-types/monitoring
resource-types/offers
resource-types/placements
resource-types/privacy-consent
resource-types/privacy-content-delivery
resource-types/privacy-job
resource-types/profile-configs
resource-types/profile-datasets
resource-types/profiles
resource-types/query
resource-types/relationship-descriptor
resource-types/sandboxes
resource-types/schemas
resource-types/segment-jobs
resource-types/segments
resource-types/streaming-source
```
