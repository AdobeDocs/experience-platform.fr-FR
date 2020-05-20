---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un espace de nommage personnalisé
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 5%

---


# Création d’un espace de nommage personnalisé

A l&#39;aide de l&#39;API d&#39;Espace de nommage d&#39;identité, vous pouvez créer un espace de nommage d&#39;identité personnalisé qui ne sera disponible que pour votre organisation.

Pour obtenir des recommandations sur la création d’espaces de nommage personnalisés, consultez [la documentation](../troubleshooting-guide.md)FAQ sur Identity Service.

>[!NOTE] Les Espaces de nommage sont un qualificatif pour les identités. Ainsi, une fois un espace de nommage créé, il ne peut plus être supprimé.

**Format d’API**

```http
POST /idnamespace/identities
```

**Requête**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/idnamespace/identities \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
        "name": "Loyalty Member",
        "code": "Loyalty",
        "description": "Loyalty Program Member ID",
        "idType": "Cross_device"
      }'
```

**Réponse**

```json
{
    "updateTime": 1576286879075,
    "code": "Loyalty",
    "status": "ACTIVE",
    "description": "Loyalty Program Member ID",
    "id": 10093197,
    "createTime": 1576286879075,
    "idType": "Cross_device",
    "name": "Loyalty Member",
    "custom": true
}
```

## Étapes suivantes

Passez au didacticiel suivant pour [liste de l&#39;ID natif d&#39;une identité](./list-native-id.md)