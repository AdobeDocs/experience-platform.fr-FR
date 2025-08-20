---
title: Point d’entrée de l’API des événements d’audit
description: Découvrez comment récupérer les événements d’audit dans Experience Platform à l’aide de l’API Audit Query.
role: Developer
feature: Audits, API
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: dec895e3ea625fb86d1891bad713185d39c47c81
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 20%

---

# Point d’entrée des événements d’audit

Les journaux d’audit sont utilisés pour fournir des détails sur l’activité des utilisateurs pour divers services et fonctionnalités. Chaque action enregistrée dans un journal contient des métadonnées qui indiquent le type d’action, la date et l’heure, l’ID d’e-mail de l’utilisateur ou de l’utilisatrice qui a exécuté l’action et des attributs supplémentaires liés au type d’action. Le point d’entrée `/audit/events` de l’API [!DNL Audit Query] vous permet de récupérer par programmation les données d’événement pour l’activité de votre organisation dans [!DNL Experience Platform].

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de lʼ [[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

## Liste des événements d’audit

Vous pouvez récupérer les données d’événement en adressant une requête GET au point d’entrée `/audit/events`, en spécifiant les événements que vous souhaitez récupérer dans la payload.

**Format d’API**

```http
GET /audit/events
```

L’API [!DNL Audit Query] prend en charge l’utilisation de paramètres de requête pour paginer et filtrer les résultats lors de l’énumération d’événements.

| Paramètre | Description |
| --- | --- |
| `limit` | Nombre maximal d’enregistrements à renvoyer dans la réponse. La `limit` par défaut est de 50. |
| `start` | Pointeur vers le premier élément pour les résultats de recherche renvoyés. Pour accéder à la page de résultats suivante, ce paramètre doit être incrémenté de la même quantité que celle indiquée par « limit ». Exemple : pour accéder à la page de résultats suivante pour une requête avec une limite=50, utilisez le paramètre start=50, puis start=100 pour la page suivante, et ainsi de suite. |
| `queryId` | Lors de l’exécution d’une requête au point d’entrée /audit/events, la réponse inclut une propriété de chaîne queryId. Pour effectuer la même requête dans un appel distinct, vous pouvez inclure la valeur de l’identifiant en tant que paramètre de requête unique au lieu de configurer à nouveau manuellement les paramètres de recherche. |

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events?limit=10
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**Réponse**

Une réponse réussie renvoie les points de données obtenus pour les mesures et les filtres spécifiés dans la requête.

```json
{
  "_embedded": {
    "events": [
      {
        "id": "6ecc125d-da03-4882-a944-88c707ddc3f7",
        "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
        "permissionResource": "Dataset",
        "permissionType": "WRITE",
        "assetType": "Dataset",
        "action": "Create",
        "status": "Allow",
        "failureCode": "",
        "timestamp": "2025-06-24T16:50:28.318+0000",
        "version": "1.0",
        "imsOrgId": "{ORGANIZATION_ID}",
        "region": "VA7",
        "authId": "e6b46821-e2b4-4729-952f-2e4afd713b31",
        "assetId": "685ad754fb1abe2b263df4b3",
        "assetName": "my-dataset",
        "sandboxName": "prod",
        "sandboxId": "{SANDBOX_ID}",
        "userEmail": "{USER_EMAIL}",
        "userIpAddresses": [
          "130.*.*.*",
          "10.*.*.*"
        ],
        "enhancedEvents": [
          {
            "id": "0ee91e42-ac46-4f35-a01a-f74a1569c404",
            "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
            "permissionResource": "Dataset",
            "permissionType": "Write",
            "assetType": "Dataset",
            "action": "Create",
            "status": "Success",
            "failureCode": "",
            "timestamp": "2025-06-24T16:50:28.883+0000",
            "assetId": "685ad754fb1abe2b263df4b3",
            "assetName": "my-dataset"
          }
        ]
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?property=user%253D%253Ddraghici%2540adobe.com"
    },
    "page": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3&limit=50{&start}",
      "templated": true
    }
  },
  "page": {
    "size": 1,
    "totalElements": 1,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3"
}
```

| Propriété | Description |
| --- | --- |
| `events` | Tableau dont les objets représentent chacun des événements spécifiés dans la requête. Chaque objet contient des informations sur la configuration du filtre et les données d’événement renvoyées. |
| `userEmail` | Adresse électronique de l’utilisateur qui a exécuté l’événement. |
| `eventType` | Type d’événement. Les types d’événements incluent les `Core` et les `Enhanced`. |
| `imsOrgId` | L’identifiant de l’organisation sous laquelle l’événement a eu lieu. |
| `permissionResource` | Le produit ou la fonctionnalité qui a fourni l’autorisation effectue l’action. Une ressource peut être l’une des suivantes : <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | Type d’autorisation impliqué dans l’action. |
| `assetType` | Type de ressource Experience Platform sur laquelle l’action a été effectuée. |
| `assetId` | Identifiant unique de la ressource Experience Platform sur laquelle l’action a été effectuée. |
| `assetName` | Nom de la ressource Experience Platform sur laquelle l’action a été effectuée. |
| `action` | Type d’action qui a été enregistré pour l’événement. Une action peut être l’une des suivantes : <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | Statut de l’action. Un statut peut être l’un des suivants : </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style="table-layout:auto"}
