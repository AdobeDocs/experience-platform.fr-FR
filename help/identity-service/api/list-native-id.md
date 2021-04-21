---
keywords: Experience Platform ; accueil ; rubriques populaires ; identité xid ; XID
solution: Experience Platform
title: Obtention de l’ID natif pour une identité
topic-legacy: API guide
description: Les données d’identité sont généralement fournies sous la forme d’une valeur de chaîne d’identifiant et d’un espace de noms d’identité dans les données XDM ingérées et dans l’identité fournie pour une utilisation dans un appel API. Lorsque des identités sont conservées dans Identity Service, un identifiant est généré et affecté à cette identité. Il est appelé XID natif. Les API Platform nécessitant des données d’identité prennent en charge l’utilisation de cette forme plus compacte d’identifiant agrégé et d’espace de noms. XID est une chaîne codée en base 64.
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 76%

---

# Obtention de l’identifiant natif d’une identité

Les données d’identité sont généralement fournies sous la forme d’une valeur de chaîne d’identifiant et d’un espace de noms d’identité dans les données XDM ingérées et dans l’identité fournie pour une utilisation dans un appel API. Lorsque des identités sont conservées dans [!DNL Identity Service], un identifiant est généré et affecté à cette identité, appelé XID natif. [!DNL Platform]Les API nécessitant des données d’identité prennent en charge l’utilisation de cette forme plus compacte d’identifiant agrégé et d’espace de noms. XID est une chaîne codée en base 64.

>[!NOTE]
>
>Ce format est principalement destiné à un usage interne à Adobe. Le XID natif en tant que valeur unique est plus efficace en termes d’espace et est utilisé en interne dans les solutions [!DNL Platform] pour l’enregistrement et la sérialisation. Cependant, il est opaque, non lisible par l’utilisateur, et un appel séparé doit être effectué pour l’obtenir et l’utiliser.

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
