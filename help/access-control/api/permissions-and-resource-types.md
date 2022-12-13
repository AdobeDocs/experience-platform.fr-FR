---
keywords: Experience Platform;accueil;rubriques populaires;autorisations de contrôle d’accès;types de ressources de contrôle d’accès;api de contrôle d’accès
solution: Experience Platform
title: Point d’entrée de l’API de référence
topic-legacy: developer guide
description: Le point de terminaison de référence de l’API Access Control vous permet d’afficher les noms des autorisations disponibles et des types de ressources, qui peuvent ensuite être utilisés pour afficher des stratégies de contrôle d’accès efficaces pour l’utilisateur actuel.
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 67%

---

# Point d’entrée de référence

Vous pouvez répertorier les noms de tous les types d’autorisations et de ressources en envoyant une requête GET au point de terminaison `/acl/reference`. Ces noms peuvent ensuite être utilisés dans les appels API à [Affichage des stratégies de contrôle d’accès efficaces](./effective-policies.md) pour l’utilisateur actuel.

Une autorisation est une stratégie gérée à l’aide d’Adobe Admin Console et mettant en correspondance zéro, une ou plusieurs stratégies de type ressource. Un type de ressource est une stratégie activant des fonctionnalités de lecture, d’écriture et/ou de suppression pour un type spécifique de ressources de [!DNL Platform] (comme des jeux de données ou des schémas).

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
