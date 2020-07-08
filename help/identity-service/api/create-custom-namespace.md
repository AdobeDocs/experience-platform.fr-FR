---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un espace de nommage personnalisé
topic: API guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 8%

---


# Création d’un espace de nommage personnalisé

A l&#39;aide de l&#39; [!DNL Identity Namespace] API, vous pouvez créer un espace de nommage d&#39;identité personnalisé qui sera disponible uniquement pour votre organisation.

Pour obtenir des recommandations sur la création d’espaces de nommage personnalisés, consultez [la documentation](../troubleshooting-guide.md)FAQ sur Identity Service.

>[!NOTE]
>
>Les Espaces de nommage sont un qualificatif pour les identités. Ainsi, une fois un espace de nommage créé, il ne peut plus être supprimé.

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