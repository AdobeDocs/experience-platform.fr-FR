---
keywords: Experience Platform;accueil;rubriques populaires;politiques effectives;api contrôle dʼaccès
solution: Experience Platform
title: Point d’entrée de lʼAPI Effective Policies
description: Découvrez comment afficher des stratégies d’accès efficaces à l’aide de l’API Access Control for Adobe Experience Platform.
role: Developer
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 74%

---

# Point d’entrée des politiques effectives

>[!NOTE]
>
>Si un jeton utilisateur est transmis, l’utilisateur du jeton doit disposer d’un rôle &quot;d’administrateur org&quot; pour l’organisation demandée.

Pour afficher des stratégies de contrôle d’accès efficaces pour l’utilisateur actuel, envoyez une requête de POST au point de terminaison `/acl/effective-policies` dans l’API [!DNL Access Control]. Les autorisations et les types de ressources que vous souhaitez récupérer doivent être fournis dans le payload de la requête sous la forme de tableau. Ceci est illustré dans l’exemple d’appel API ci-dessous.

**Format d’API**

```http
POST /acl/effective-policies
```

**Requête**

Les requêtes suivantes récupèrent des informations sur lʼautorisation « [!UICONTROL Gérer des jeux de données] » et lʼaccès au type de ressource « [!UICONTROL schémas] » pour lʼutilisateur actuel.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Ce document explique comment effectuer des appels à l’API [!DNL Access Control] pour renvoyer des informations sur les autorisations actives et les stratégies d’accès associées pour les types de ressources. Pour plus dʼinformations sur le contrôle dʼaccès dʼ[!DNL Experience Platform], consultez la [présentation du contrôle dʼaccès](../home.md).

## Annexe

Cette section fournit des informations supplémentaires sur lʼutilisation de lʼAPI [!DNL Access Control].

### Autorisations et types de ressources acceptés

Vous trouverez ci-dessous une liste d’autorisations et de types de ressources que vous pouvez inclure dans le payload d’une requête POST envoyée au point d’entrée `/acl/active-permissions`.

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
