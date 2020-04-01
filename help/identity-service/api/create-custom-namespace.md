---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Création d’un  personnalisé '
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Création d&#39;un  personnalisé 

A l’aide de l’API  d’identité  vous pouvez créer un d’identité  personnalisé qui sera disponible uniquement pour votre organisation.

Pour obtenir des recommandations sur la création d’ de  personnalisées, reportez-vous à [la documentation](../troubleshooting-guide.md)FAQ sur Identity Service.

>[!NOTE]   sont un qualificatif pour les identités. Ainsi, une fois qu’un   a été créé, il ne peut plus être supprimé.

**Format API**

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

Passez au didacticiel suivant pour [l’ID natif d’une identité.](./list-native-id.md)