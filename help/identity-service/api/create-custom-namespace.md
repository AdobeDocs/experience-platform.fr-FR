---
keywords: Experience Platform ; accueil ; sujets populaires ; espace de nommage ; Espace de nommage ; espaces de nommage ; Espaces de nommage ; espace de nommage d'identité ; espace de nommage d'identité ; identité ; identité
solution: Experience Platform
title: Création d’un Espace de nommage personnalisé dans l’API Identity Service
topic-legacy: API guide
description: À l’aide de l’API Identity Namespace, vous pouvez créer un espace de noms personnalisé qui sera disponible uniquement pour votre organisation.
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 57%

---

# Création d’un espace de nommage personnalisé dans l’API Identity Service

L&#39;API [!DNL Identity Namespace] vous permet de créer un espace de nommage d&#39;identité personnalisé qui ne sera disponible que pour votre organisation.

Pour obtenir des recommandations sur la création d’espaces de noms personnalisés, reportez-vous à aux [questions fréquentes sur Identity Service](../troubleshooting-guide.md).

>[!NOTE]
>
>Les espaces de noms sont des qualificateurs d’identités. Par conséquent, une fois qu’un espace de noms a été créé, il ne peut pas être supprimé.

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

Passez au tutoriel suivant pour [répertorier l’identifiant natif d’une identité](./list-native-id.md).
