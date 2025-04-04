---
keywords: Experience Platform;accueil;rubriques populaires;xid d’identité;XID
solution: Experience Platform
title: Obtention de l’ID natif pour une identité
description: Les données d’identité sont généralement fournies sous la forme d’une valeur de chaîne d’identifiant et d’un espace de noms d’identité dans les données XDM ingérées et dans l’identité fournie pour une utilisation dans un appel API. Lorsque des identités sont conservées dans le service d’identités, un identifiant est généré et affecté à cette identité. Il est appelé XID natif. Les API d’Experience Platform nécessitant des données d’identité prennent en charge l’utilisation de ce formulaire plus compact pour l’ID et l’espace de noms agrégés. XID est une chaîne codée en base 64.
role: Developer
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 58%

---

# Obtention de l’identifiant natif d’une identité

Les données d’identité sont généralement fournies sous la forme d’une valeur de chaîne d’identifiant et d’un espace de noms d’identité dans les données XDM ingérées et dans l’identité fournie pour une utilisation dans un appel API. Lorsque des identités sont conservées dans [!DNL Identity Service], un identifiant est généré et attribué à cette identité, appelé XID natif. Les API [!DNL Experience Platform] nécessitant des données d’identité prennent en charge l’utilisation de ce formulaire plus compact pour l’ID et l’espace de noms agrégés. XID est une chaîne codée en base 64.

>[!NOTE]
>
>Ce format est principalement destiné à une utilisation interne à Adobe. Le XID natif en tant que valeur unique est plus efficace en termes d’espace et est utilisé en interne dans les solutions [!DNL Experience Platform] pour le stockage et la sérialisation. Cependant, il est opaque, non lisible par l’utilisateur, et un appel séparé doit être effectué pour l’obtenir et l’utiliser.

Faites l’acquisition du XID pour une valeur d’identifiant et un espace de noms donnés à l’aide du service décrit dans cette section.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
