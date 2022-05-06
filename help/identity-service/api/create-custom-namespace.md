---
keywords: Experience Platform;accueil;rubriques populaires;espace de noms;espaces de noms;espaces de noms;espace de noms;espace de noms d’identité;espace de noms d’identité;identité;identité
solution: Experience Platform
title: Création d’un espace de noms personnalisé dans l’API Identity Service
topic-legacy: API guide
description: À l’aide de l’API Identity Namespace, vous pouvez créer un espace de noms personnalisé qui sera disponible uniquement pour votre organisation.
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 57%

---

# Création d’un espace de noms personnalisé dans l’API Identity Service

En utilisant la variable [!DNL Identity Namespace] API, vous pouvez créer un espace de noms d’identité personnalisé qui sera disponible uniquement pour votre organisation.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
