---
keywords: Experience Platform ; sécurité ; accès ip ; validation ; guide API ; service de requête ; vérification IP
title: Point de terminaison de validation IP
description: Découvrez comment valider l’accès IP pour les environnements de test dans Query Service à l’aide du point de terminaison de l’API de validation d’IP.
role: Developer
exl-id: 4ce9ab1c-e333-4ed5-a430-43ffec36a46d
source-git-commit: bf696c8836407a2fea82e9078201cb1f5004bcf8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 4%

---

# Point de terminaison de validation IP

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté le module complémentaire Data Distiller. Pour en savoir plus, contactez votre représentant ou représentante Adobe.

Utilisez le point de terminaison de l’API de validation d’IP pour vérifier si une adresse IP spécifiée est autorisée à accéder à un environnement de test désigné dans Query Service. Cette vérification confirme si des restrictions d’accès s’appliquent ou si une adresse IP est autorisée à accéder aux données dans un environnement de test.

## Validation de l’adresse IP pour l’accès aux environnements de test {#validate-ip-for-sandbox-access}

Utilisez le point de terminaison Validation IP pour vérifier si une adresse IP donnée est autorisée à accéder aux données de l’environnement de test spécifié. Si aucune restriction d’IP n’est configurée pour l’environnement de test, toutes les adresses IP sont autorisées par défaut. S’il existe des restrictions d’adresse IP ou CIDR, cette API vérifie si l’adresse IP spécifiée correspond à des plages configurées.

>[!NOTE]
>
>Vous pouvez accéder à ce point de terminaison avec les **jetons utilisateur** ou les **jetons de service**. Aucune exigence de rôle spécifique n’est nécessaire.

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

Une réponse réussie renvoie un état HTTP 200 avec une valeur booléenne indiquant si l’adresse IP est autorisée.

>[!NOTE]
>
>Le champ `isAllowed` de la réponse renvoie `true` si l’adresse IP fournie est autorisée à accéder à l’environnement de test et `false` dans le cas contraire. Cette API prend en charge la validation dynamique de l’accès et la conformité en matière de sécurité pour les environnements de test.

```json
{
"isAllowed": true
}
```
