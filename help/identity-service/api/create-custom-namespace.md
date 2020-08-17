---
keywords: Experience Platform;home;popular topics;namespace;Namespace;namespaces;Namespaces;identity namespace;Identity namespace;identity;Identity
solution: Experience Platform
title: Création d’un espace de noms personnalisé
topic: API guide
description: À l’aide de l’API Identity Namespace, vous pouvez créer un espace de noms personnalisé qui sera disponible uniquement pour votre organisation.
translation-type: tm+mt
source-git-commit: 3376d6cace9ab196f457e2bf7b84cde06693103c
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 81%

---


# Création d’un espace de noms personnalisé

Using the [!DNL Identity Namespace] API, you can create a custom identity namespace that will be available only to your organization.

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