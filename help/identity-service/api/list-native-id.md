---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Obtention de l’identifiant natif d’une identité
topic: API guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 73%

---


# Obtention du XID d’une identité

Les données d’identité sont généralement fournies sous la forme d’une valeur de chaîne d’identifiant et d’un espace de noms d’identité dans les données XDM ingérées et dans l’identité fournie pour une utilisation dans un appel API. When identities are persisted in [!DNL Identity Service], an ID is generated and assigned to that identity, called the native XID. [!DNL Platform]Les API nécessitant des données d’identité prennent en charge l’utilisation de cette forme plus compacte d’identifiant agrégé et d’espace de noms. XID est une chaîne codée en base 64.

>[!NOTE]
>
>Ce format est principalement destiné à un usage interne à Adobe. Native XID as a singular value is more space efficient and is what is used internally within [!DNL Platform] solutions for storage and serialization. Cependant, il est opaque, non lisible par l’utilisateur, et un appel séparé doit être effectué pour l’obtenir et l’utiliser.

Faites l’acquisition du XID pour une valeur d’identifiant donnée à l’aide du service décrit dans cette section.

**Format d’API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/identity?namespace={NAMESPACE}&id={ID_VALUE}
```

**Requête**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/identity?namespace=email&id=test@adobetest.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
