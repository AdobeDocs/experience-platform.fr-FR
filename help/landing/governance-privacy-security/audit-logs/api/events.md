---
title: Point de terminaison de l’API des événements d’audit
description: Découvrez comment récupérer des événements d’audit dans Experience Platform à l’aide de l’API de requête d’audit.
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: c7887391481def872c40dd6ed1193bf562b9d0cf
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 20%

---

# Point d’entrée des événements d’audit

Les journaux d’audit permettent de fournir des détails sur l’activité des utilisateurs pour divers services et fonctionnalités. Chaque action enregistrée dans un journal contient des métadonnées qui indiquent le type d’action, la date et l’heure, l’ID d’e-mail de l’utilisateur ou de l’utilisatrice qui a exécuté l’action et des attributs supplémentaires liés au type d’action. Le point d’entrée `/audit/events` de l’API [!DNL Audit Query] vous permet de récupérer par programmation les données d’événement pour l’activité de votre organisation dans [!DNL Platform].

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de lʼ [[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

## Liste des événements de contrôle

Vous pouvez récupérer les données d’événements en envoyant une requête de GET au point de terminaison `/audit/events`, en spécifiant les événements que vous souhaitez récupérer dans la payload.

**Format d’API**

```http
GET /audit/events
```

L’API [!DNL Audit Query] prend en charge l’utilisation de paramètres de requête pour la page et le filtrage des résultats lors de la liste d’événements.

| Paramètre | Description |
| --- | --- |
| `limit` | Nombre maximal d’enregistrements à renvoyer dans la réponse. La valeur par défaut `limit` est 50. |
| `start` | Pointeur vers le premier élément pour les résultats de recherche renvoyés. Pour accéder à la page de résultats suivante, ce paramètre doit être incrémenté de la même quantité que celle indiquée par la limite. Exemple : pour accéder à la page de résultats suivante pour une requête avec limit=50, utilisez le paramètre start=50, puis start=100 pour la page après cela, etc. |
| `queryId` | Lors de l’exécution d’une requête sur le point de terminaison /audit/events, la réponse inclut une propriété de chaîne queryId. Pour effectuer la même requête dans un appel distinct, vous pouvez inclure la valeur Id comme paramètre de requête unique au lieu de reconfigurer manuellement les paramètres de recherche. |

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

Une réponse réussie renvoie les points de données résultants pour les mesures et les filtres spécifiés dans la requête.

```json
{
   "_embedded": {
     "customerAuditLogList": [
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "32b72208-3035-4bc6-b434-39e34401a864",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "5NphpgUQdQnjTWOcS9DSMs2wD1EUMlYG",
         "authId": "96715f98-d100-4575-8491-ebbcea654eb9",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:58:09.745+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "a178736a-8fa1-47da-bac5-b0d9e741e414",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "7AlGIAhWvaEzYWHLzvuf26AAFAkqSyKg",
         "authId": "60fc1077-4aef-4e1f-a5ff-f64183e060f4",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:28:00.301+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "ccfe8c77-9b93-481d-a561-0b2edf3b77dc",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "hArqS4CAa8wfRPnKuxV4yaA82atxwzYu",
         "authId": "80b7d887-9338-4cd5-9d79-2483b03f0160",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T20:58:07.750+0000"
       }
     ]    
   },
   "_links": {
     "self": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?limit=10&start=0&property=type%253D%253Dcore"
     },
     "next": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&start=10&limit=10"
     },
     "page": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&limit=10{&start}",
       "templated": true
     }
  },
  "page": {
    "size": 10,
    "totalElements": 3,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2"
}
```

| Propriété | Description |
| --- | --- |
| `customerAuditLogList` | Tableau dont les objets représentent chacun des événements spécifiés dans la requête. Chaque objet contient des informations sur la configuration du filtre et les données d’événement renvoyées. |
| `userEmail` | Adresse électronique de l’utilisateur qui a exécuté l’événement. |
| `eventType` | Type d’événement. Les types d’événements incluent `Core` et `Enhanced`. |
| `imsOrgId` | ID de l’organisation sous laquelle l’événement a eu lieu. |
| `permissionResource` | Le produit ou la fonctionnalité qui a fourni l’autorisation effectue l’action. Une ressource peut être l’une des suivantes : <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | Type d’autorisation associé à l’action. |
| `assetType` | Type de ressource Platform sur laquelle l’action a été effectuée. |
| `assetId` | Identifiant unique de la ressource Platform sur laquelle l’action a été effectuée. |
| `assetName` | Nom de la ressource Platform sur laquelle l’action a été effectuée. |
| `action` | Type d’action enregistrée pour l’événement. Une action peut être l’une des suivantes : <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | État de l’action. Un état peut être l’un des suivants : </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style="table-layout:auto"}
