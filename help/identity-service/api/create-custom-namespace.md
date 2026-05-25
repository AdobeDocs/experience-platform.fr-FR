---
keywords: Experience Platform;accueil;rubriques populaires;espace de noms;espace de noms;espaces de noms;Espaces de noms;espace de noms d’identité;Espace de noms d’identité;identité;Identité
solution: Experience Platform
title: Créer un espace de noms personnalisé dans l’API Identity Service
description: À l’aide de l’API Identity Namespace, vous pouvez créer un espace de noms personnalisé qui sera disponible uniquement pour votre organisation.
role: Developer
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
TQID: https://experienceleague.adobe.com/RXRNB0iqPLf0tKeAxh5JM7uJWmKWultFqHhztx76g-A
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 52%

---

# Créer un espace de noms personnalisé dans l’API Identity Service

À l’aide de l’API [!DNL Identity Namespace], vous pouvez créer un espace de noms d’identité personnalisé qui ne sera disponible que pour votre organisation.

Pour obtenir des recommandations sur la création d’espaces de noms personnalisés, reportez-vous aux [questions fréquentes sur le service dʼidentités](../troubleshooting-guide.md).

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
