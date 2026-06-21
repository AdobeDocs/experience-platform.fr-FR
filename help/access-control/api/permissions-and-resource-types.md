---
keywords: Experience Platform;accueil;rubriques populaires;autorisations de contrôle d’accès;types de ressources de contrôle d’accès;api de contrôle d’accès
solution: Experience Platform
title: Point d’entrée de l’API de référence
description: Le point d’entrée de référence de l’API Access Control vous permet d’afficher les noms des autorisations et des types de ressources disponibles, qui peuvent ensuite être utilisés pour afficher des politiques de contrôle d’accès efficaces pour l’utilisateur actuel.
role: Developer
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
TQID: https://experienceleague.adobe.com/ak2eLdeLnJqU5hy6QxclFGAEnQ-BRnedmMAq-TFXxPU
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 189
ht-degree: 59%

---

# Point d’entrée de référence

>[!NOTE]
>
>Si un jeton d’utilisateur est transmis, l’utilisateur du jeton doit disposer d’un rôle « administrateur d’organisation » pour l’organisation demandée.

Vous pouvez répertorier les noms de tous les types d’autorisations et de ressources en envoyant une requête GET au point d’entrée `/acl/reference`. Ces noms peuvent ensuite être utilisés dans les appels API pour [afficher des politiques de contrôle d’accès efficaces](./effective-policies.md) pour l’utilisateur actuel.

Une autorisation est une politique gérée à l’aide d’Adobe Admin Console et mettant en correspondance zéro, une ou plusieurs politiques de type ressource. Un type de ressource est une politique activant des fonctionnalités de lecture, d’écriture et/ou de suppression pour un type spécifique de ressources de [!DNL Experience Platform] (comme des jeux de données ou des schémas).

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
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Réponse**

Une réponse réussie renvoie un objet `permissions` et un objet `resource-types` contenant chacun une liste complète de noms pour les autorisations d’accès ou les types de ressources, respectivement.

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
