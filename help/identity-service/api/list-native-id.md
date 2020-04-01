---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Obtention de l’ID natif d’une identité
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Obtention du XID pour une identité

Les données d’identité sont généralement fournies sous la forme d’une valeur de chaîne d’ID et d’un d’identité  dans les données XDM assimilées et lors de la fourniture d’une identité en vue d’une utilisation dans un appel d’API. Lorsque des identités sont conservées dans Identity Service, un ID est généré et affecté à cette identité, appelé XID natif. Les API de plateformes nécessitant la prise en charge des données d’identité à l’aide de cette forme plus compacte pour l’ID agrégé et le  . XID est une chaîne codée en base 64.

>[!NOTE] Ce format est principalement destiné à un usage interne d’Adobe. Le XID natif en tant que valeur unique est plus efficace en termes d’espace et c’est ce qui est utilisé en interne dans les solutions de plateformes pour   et sérialisation. Cependant, il n&#39;est pas lisible par l&#39;homme, il est opaque et nécessite un appel séparé pour l&#39;obtenir à utiliser.

Acquérez le XID pour une valeur d’ID donnée et   à l’aide du service décrit dans cette section.

**Format API**

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
