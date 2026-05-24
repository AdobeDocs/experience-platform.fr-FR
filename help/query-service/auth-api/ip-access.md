---
keywords: Experience Platform;sécurité;accès-ip;QS-Auth;guide de l’API;query service;plages d’adresses IP
title: Point d’entrée d’accès IP
description: Découvrez comment gérer les plages d’adresses IP pour l’accès aux sandbox dans Query Service à l’aide du point d’entrée de l’API IP Access.
role: Developer
exl-id: fc15ab50-c125-4f00-a311-81fd41697c7d
TQID: https://experienceleague.adobe.com/SC9I9FnsssdyZ6YsQmP0m2roJ4YEIBsOUtvTYoIpa-0
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 424
ht-degree: 5%

---

# Point d’entrée d’accès IP

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté le module complémentaire Distiller de données. Pour plus d’informations, contactez votre représentant ou représentante Adobe.

Pour sécuriser l’accès aux données dans un sandbox Query Service spécifié, utilisez le point d’entrée Accès IP pour gérer les plages d’adresses IP autorisées. Vous pouvez utiliser cette API pour récupérer, configurer ou supprimer des plages d’adresses IP associées à l’identifiant de votre organisation.

Vous pouvez effectuer les actions suivantes avec l’API d’accès IP :

- **Récupérer toutes les plages d’adresses IP**
- **Définir de nouvelles plages d’adresses IP**
- **Supprimer des plages d’adresses IP existantes**

Ce document couvre les requêtes et réponses que vous pouvez effectuer et recevoir à partir du point d’entrée `/security/ip-access`.

>[!NOTE]
>
>Vous devez disposer d’un jeton d’utilisateur pour appeler cette API. Consultez le [guide de prise en main](./getting-started.md) pour plus d’informations sur l’acquisition des valeurs requises pour chacun des en-têtes.

## Récupérer toutes les plages d’adresses IP {#fetch-all-ip-ranges}

Récupérez une liste de toutes les plages d’adresses IP configurées pour votre sandbox. Si aucune plage d’adresses IP n’est définie, toutes les adresses IP sont autorisées par défaut et la réponse renvoie une liste vide dans `allowedIpRanges`.

**Format d’API**

```http
GET /security/ip-access
```

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/queryauth/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec une liste des plages d’adresses IP autorisées du sandbox.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "101.10.1.1"}
  ]
}
```

Le tableau suivant fournit une description et un exemple des propriétés du schéma de réponse :

| Propriété | Description | Exemple |
|------------------|---------------------------------------------|-----------------------------------------------------------------------------------------------|
| `imsOrg` | ID d’organisation du sandbox. | `{ORG_ID}` |
| `sandboxName` | Nom du sandbox où les restrictions IP s’appliquent. | `prod` |
| `channel` | Mode d’accès pour les restrictions IP. Actuellement, la seule valeur acceptée est `data_distiller`. Cette valeur signifie que des restrictions d’adresses IP sont appliquées aux connexions PSQL ou JDBC. | `data_distiller` |
| `allowedIpRanges` | Liste des adresses IP autorisées au format CIDR ou IP fixe. Chaque entrée peut inclure une description facultative. | `[{"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"}]` |

>[!NOTE]
>
>Le champ `allowedIpRanges` peut inclure deux types de spécifications IP :<br><ul><li>**CIDR** : notation CIDR standard (par exemple, `"136.23.110.0/23"`) pour définir des plages d’adresses IP.</li><li>**IP fixe** : adresses IP uniques pour les autorisations d’accès individuelles (par exemple, `"101.10.1.1"`).</li></ul>

## Définir de nouvelles plages d’adresses IP

Remplacez les plages d’adresses IP existantes en définissant une nouvelle liste pour le sandbox. Cette opération nécessite une liste complète de plages d’adresses IP, y compris celles qui restent inchangées.

**Format d’API**

```http
PUT /security/ip-access
```

**Requête**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/queryauth/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "ipRanges": [
       {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
       {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
       {"ipRange": "101.10.1.1"},
       {"ipRange": "163.77.30.9", "description": "Test server IP"}
     ]
   }'
```

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec les détails des plages d’adresses IP nouvellement configurées.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```

## Suppression de plages d’adresses IP {#delete-ip-ranges}

Supprimez toutes les plages d’adresses IP configurées pour le sandbox. Cette action supprime les plages d’adresses IP et renvoie la liste des adresses IP supprimées.

>[!NOTE]
>
>L’opération de suppression s’applique à l’ID d’organisation (`imsOrg`) et affecte toutes les plages d’adresses IP configurées pour le sandbox.

**Format d’API**

```http
DELETE /security/ip-access
```

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails des plages d’adresses IP supprimées.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "deletedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```
