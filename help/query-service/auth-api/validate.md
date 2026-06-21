---
keywords: Experience Platform;sécurité;accès-ip;validation;guide de l’API;query service;vérification IP
title: Point d’entrée de validation IP
description: Découvrez comment valider l’accès IP pour les sandbox dans Query Service à l’aide du point d’entrée de l’API de validation IP.
role: Developer
exl-id: 4ce9ab1c-e333-4ed5-a430-43ffec36a46d
TQID: https://experienceleague.adobe.com/V1aW88dpU3EQXl-Zw45tK9FF-uA712xIiyvZjioJ6zE
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 230
ht-degree: 4%

---

# Point d’entrée de validation IP

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté le module complémentaire Distiller de données. Pour plus d’informations, contactez votre représentant ou représentante Adobe.

Utilisez le point d’entrée de l’API de validation IP pour vérifier si une adresse IP spécifiée est autorisée à accéder à un sandbox désigné dans Query Service. Cette vérification confirme si des restrictions d’accès s’appliquent ou si une adresse IP est autorisée à accéder aux données d’un sandbox.

## Valider l’adresse IP pour l’accès au sandbox {#validate-ip-for-sandbox-access}

Utilisez le point d’entrée de validation IP pour vérifier si une adresse IP donnée est autorisée à accéder aux données du sandbox spécifié. Si aucune restriction d’adresse IP n’est configurée pour le sandbox, toutes les adresses IP sont autorisées par défaut. S’il existe des restrictions IP ou CIDR, cette API vérifie si l’adresse IP spécifiée correspond à des plages configurées.

>[!NOTE]
>
>Vous pouvez accéder à ce point d’entrée avec **jetons d’utilisateur** ou **jetons de service**. Aucune exigence de rôle spécifique n’est nécessaire.

**Format d’API**

```http
POST /security/validate/ip-access
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/security/validate/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
       "ipAddress": "197.2.0.2"
     }'
```

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec une valeur booléenne indiquant si l’adresse IP est autorisée.

>[!NOTE]
>
>Le champ `isAllowed` de la réponse renvoie `true` si l’adresse IP fournie est autorisée à accéder au sandbox et `false` dans le cas contraire. Cette API prend en charge la validation dynamique de l’accès et la conformité de sécurité pour les environnements sandbox.

```json
{
"isAllowed": true
}
```
