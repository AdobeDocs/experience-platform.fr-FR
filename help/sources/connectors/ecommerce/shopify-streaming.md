---
title: Shopify Streaming Source
description: Découvrez comment créer une connexion source et un flux de données pour ingérer des données en continu de votre instance Shopify vers Adobe Experience Platform
badge: « Version bêta »
hidefromtoc: y
hide: y
source-git-commit: 279d8e307c8ca5a799a47c6f903b9a082d9cf034
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 3%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>La source [!DNL Shopify Streaming] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform prend en charge l’ingestion de données à partir d’applications de diffusion en continu. La prise en charge des fournisseurs de diffusion en continu inclut [!DNL Shopify].

## Conditions préalables {#prerequisites}

La section suivante décrit les étapes préalables à suivre avant d’utiliser [!DNL Shopify Streaming] source.

Vous devez disposer d’un [!DNL Shopify] compte du partenaire afin de se connecter à la variable [!DNL Shopify] API. Si vous ne disposez pas déjà d’un compte de partenaire, inscrivez-vous à l’aide de la variable [[!DNL Shopify] tableau de bord des partenaires](https://www.shopify.com/partners).

### Créer votre application

Avec un [!DNL Shopify] compte partenaire, vous pouvez maintenant poursuivre et créer votre application à l’aide du tableau de bord des partenaires. Pour obtenir des instructions complètes sur la création de votre application dans [!DNL Shopify], lisez le [[!DNL Shopify] guide de prise en main](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

Une fois votre application créée, récupérez votre **ID client** et **secret client** de la **informations d’identification client** de l’onglet [!DNL Shopify] tableau de bord des partenaires. L’ID client et le secret client seront utilisés dans les étapes suivantes pour récupérer votre code d’autorisation et votre jeton d’accès.

### Récupération de votre code d’autorisation

Ensuite, récupérez votre code d’autorisation en saisissant le de `myshopify.com` URL dans votre navigateur, ainsi que les chaînes de requête qui définissent votre clé d’API, vos portées et l’URI de redirection.

Le format de cette URL est le suivant :

**Format d’API**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| Paramètre | Description |
| --- | --- |
| `shop` | Votre sous-domaine `myshopify.com` URL. |
| `api_key` | Votre [!DNL Shopify] ID client. Vous pouvez récupérer votre ID client à partir de la variable **informations d’identification client** de l’onglet [!DNL Shopify] tableau de bord des partenaires. |
| `scopes` | Type d’accès que vous souhaitez définir. Par exemple, vous pouvez définir des portées comme `scope=write_orders,read_customers` pour autoriser des autorisations de modification des commandes et de lecture des clients. |
| `redirect_uri` | URL du script qui générera le jeton d’accès. |

**Requête**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**Réponse**

Une réponse réussie renvoie votre URL de redirection, y compris le code d’autorisation requis pour générer votre jeton d’accès.

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### Récupération de votre jeton d’accès

Maintenant que vous disposez de votre ID client, de votre secret client et de votre code d’autorisation, vous pouvez récupérer votre jeton d’accès. Pour récupérer votre jeton d’accès, envoyez une demande de POST à la variable `myshopify.com` URL lors de l’ajout de cette URL avec [!DNL Shopify's] Point d’entrée de l’API : `/admin/oauth/access_token`.

**Format d’API**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**Requête**

La requête suivante génère un jeton d’accès pour votre [!DNL Shopify] instance.

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/oauth/access_token' \
  -H 'developer-token: {DEVELOPER_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'Cookie: _master_udr=xxx; request_method=POST'
  -d '{
    "client_id": "l6fiviermmzpram5i1spfub99shms3j9",
    "client_secret": "dajn3caxz9s7ti624ncyv_m4f60jnwi3ii3y3k",
    "code": "k6j2palgrbljja228ou8c20fmn7w41gz"
}'
```

**Réponse**

Une réponse réussie renvoie votre jeton d’accès et vos portées d’autorisation.

```json
{
  "access_token": "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",
  "scope": "write_orders,read_customers"
}
```

## Création d’un webhook pour la diffusion en continu [!DNL Shopify] data {#webhook}

Les webhooks permettent aux applications de rester synchronisées avec votre [!DNL Shopify] ou effectuer une action après qu’un événement particulier se produit dans un magasin. Pour la diffusion en continu [!DNL Shopify] données à Experience Platform, webhooks peut être utilisé pour définir le point de terminaison http et les rubriques d’abonnement.

**Requête**

La requête suivante crée un webhook pour votre [!DNL Shopify Streaming] data.

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/api/2022-07/webhooks.json' \
  -H 'X-Shopify-Access-Token: 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' \
  -H 'Content-Type: application/json' \; request_method=POST' \
  -d '{
  "webhook": {
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "format": "json"
  }
}'
```

| Paramètre | Description |
| --- | --- | 
| `webhook.address` | Point de terminaison http où les messages en continu sont envoyés. |
| `webhook.topic` | Rubrique de votre abonnement webhook. Pour plus d’informations, reportez-vous à la section [[!DNL Shopify] guide des rubriques des événements webhook](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | Le format de vos données. |

**Réponse**

Une réponse réussie renvoie des informations sur votre webhook, y compris les `id`, l’adresse et d’autres informations de métadonnées.

```json
{
  "webhook": {
    "id": 1091138715786,
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "created_at": "2022-07-20T07:15:23-04:00",
    "updated_at": "2022-07-20T07:15:23-04:00",
    "format": "json",
    "fields": [],
    "metafield_namespaces": [],
    "api_version": "2021-10",
    "private_metafield_namespaces": []
  }
}
```

### Limites {#limitations}

Vous trouverez ci-dessous une liste des limites connues que vous pouvez rencontrer lors de l’utilisation de webhooks avec la variable [!DNL Shopify Streaming] source.

* Il n’est pas garanti que vous puissiez organiser l’ordre de remise de différentes rubriques pour la même ressource. Par exemple, il est possible qu’une `products/update` webhook livré avant un événement `products/create` webhook.
* Vous pouvez définir votre webhook pour diffuser au moins une fois des événements webhook vers un point de terminaison . Cela signifie qu’un point de terminaison peut recevoir le même événement plusieurs fois. Vous pouvez rechercher des événements webhook en double en comparant les événements `X-Shopify-Webhook-Id` en-tête aux événements précédents.
* [!DNL Shopify] traite les réponses d’état HTTP 2xx comme des notifications réussies. Toutes les autres réponses de code d’état sont considérées comme des échecs. [!DNL Shopify] fournit un mécanisme de reprise pour les notifications webhook ayant échoué. Si la variable **aucune réponse après cinq secondes d’attente**, [!DNL Shopify] tente à nouveau la connexion **19 fois** au cours de la prochaine **48 heures**. S’il n’y a toujours pas de réponse avant la fin de la période de reprise, alors [!DNL Shopify] supprime le webhook.

## Étapes suivantes

Les tutoriels suivants décrivent les étapes à suivre pour connecter votre [!DNL Shopify Streaming] source à Experience Platform à l’aide de l’API et de l’interface utilisateur :

* [Création d’une connexion source Shopify et d’un flux de données à l’aide de l’API Flow Service](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [Création d’une connexion source Shopify et d’un flux de données dans l’interface utilisateur](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
