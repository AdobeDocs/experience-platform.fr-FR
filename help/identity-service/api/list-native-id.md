---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Obtenir l'ID natif d'une identité
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 1%

---


# Obtention du XID pour une identité

Les données d&#39;identité sont généralement fournies sous la forme d&#39;une valeur de chaîne d&#39;ID et d&#39;un espace de nommage d&#39;identité dans les données XDM ingérées et lors de la fourniture d&#39;une identité à utiliser dans un appel d&#39;API. Lorsque des identités sont conservées dans Identity Service, un identifiant est généré et affecté à cette identité, appelé XID natif. Les API de plateforme nécessitant la prise en charge des données d&#39;identité à l&#39;aide de ce formulaire plus compact pour l&#39;identifiant et l&#39;espace de nommage agrégés. XID est une chaîne codée en base 64.

>[!NOTE] Ce format est principalement destiné à un usage interne d’Adobe. Le XID natif en tant que valeur unique est plus efficace en termes d’espace et est ce qui est utilisé en interne dans les solutions de plateformes pour l’enregistrement et la sérialisation. Cependant, il n&#39;est pas lisible par l&#39;homme, il est opaque et nécessite un appel séparé pour l&#39;obtenir pour l&#39;utiliser.

Acquérez le XID pour une valeur d’ID et un espace de nommage donnés à l’aide du service décrit dans cette section.

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
