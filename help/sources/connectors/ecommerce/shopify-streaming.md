---
title: Source de streaming Shopify
description: Découvrez comment créer une connexion source et un flux de données pour ingérer des données de flux de votre instance Shopify vers Adobe Experience Platform
badge: Beta
last-substantial-update: 2023-04-26T00:00:00Z
exl-id: ae991913-68b5-4bbb-b8a5-e566d67a4c1a
source-git-commit: 4c7b23592a1784a5f2daa5518b512fa458a2c3ad
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>La source [!DNL Shopify Streaming] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform prend en charge l’ingestion de données provenant d’applications de diffusion en continu. La prise en charge des fournisseurs de streaming inclut [!DNL Shopify].

## Conditions préalables {#prerequisites}

La section suivante décrit les étapes préalables à suivre avant d’utiliser la source de [!DNL Shopify Streaming].

Vous devez disposer d’un compte partenaire [!DNL Shopify] valide pour vous connecter aux API [!DNL Shopify]. Si vous ne disposez pas encore d’un compte partenaire, inscrivez-vous en utilisant le tableau de bord [[!DNL Shopify] partenaires](https://www.shopify.com/partners).

### Création de votre application

Avec un compte partenaire [!DNL Shopify] valide, vous pouvez maintenant continuer et créer votre application à l’aide du tableau de bord des partenaires. Pour obtenir des instructions complètes sur la création de votre application dans [!DNL Shopify], consultez le guide [[!DNL Shopify]  de prise en main ](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

Une fois votre application créée, récupérez vos **identifiant client** et **secret client** dans l’onglet **informations d’identification du client** du tableau de bord des partenaires [!DNL Shopify]. L’identifiant client et le secret client seront utilisés dans les étapes suivantes pour récupérer votre code d’autorisation et votre jeton d’accès.

### Récupérer le code d’autorisation

Ensuite, récupérez votre code d’autorisation en saisissant l’URL `myshopify.com` de votre domaine dans votre navigateur, ainsi que les chaînes de requête qui définissent votre clé API, les portées et l’URI de redirection.

Le format de cette URL est le suivant :

**Format d’API**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| Paramètre | Description |
| --- | --- |
| `shop` | Votre URL de `myshopify.com` de sous-domaine. |
| `api_key` | Votre identifiant client [!DNL Shopify]. Vous pouvez récupérer votre identifiant client à partir de l’onglet **informations d’identification du client** du tableau de bord des partenaires [!DNL Shopify]. |
| `scopes` | Type d’accès à définir. Par exemple, vous pouvez définir les portées comme `scope=write_orders,read_customers` pour autoriser les autorisations de modification des commandes et de lecture des clients. |
| `redirect_uri` | URL du script qui va générer le jeton d’accès. |

**Requête**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**Réponse**

Une réponse réussie renvoie votre URL de redirection, y compris le code d’autorisation requis pour générer votre jeton d’accès.

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### Récupérer votre jeton d’accès

Maintenant que vous disposez de votre identifiant client, secret client et code d’autorisation, vous pouvez récupérer votre jeton d’accès. Pour récupérer votre jeton d’accès, envoyez une requête POST à l’URL de `myshopify.com` de votre domaine tout en ajoutant cette URL avec [!DNL Shopify's] point d’entrée de l’API : `/admin/oauth/access_token`.

**Format d’API**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**Requête**

La requête suivante génère un jeton d’accès pour votre instance [!DNL Shopify].

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

Une réponse réussie renvoie votre jeton d’accès et les portées d’autorisation.

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## Créer un webhook pour la diffusion en continu de données [!DNL Shopify] {#webhook}

Les Webhooks permettent aux applications de rester synchronisées avec vos données [!DNL Shopify] ou d’effectuer une action après qu’un événement particulier se soit produit dans un magasin. Pour la diffusion en continu de données de [!DNL Shopify] vers Experience Platform, les webhooks peuvent être utilisés pour définir le point d’entrée http et les rubriques à abonner.

**Requête**

La requête suivante crée un webhook pour vos données [!DNL Shopify Streaming].

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/api/2022-07/webhooks.json' \
  -H 'X-Shopify-Access-Token: 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' \
  -H 'Content-Type: application/json' \; request_method=POST' \
  -d '{
  "webhook": {
    "address": "https://dcs.adobedc.net/collection/114ae3c01f3ac77c704465f83d7d79be150fc39a5a794a214cd4ab65a5901340?x-adobe-flow-id=d9eb4a58-6a6b-4f11-9dba-6d1e0ed43bad",
    "topic": "orders/create",
    "format": "json"
  }
}'
```

| Paramètre | Description |
| --- | --- | 
| `webhook.address` | Point d’entrée http où les messages en flux continu sont envoyés. Le modèle du webhook est le suivant : `https://dcs.adobedc.net/collection/%7BINLET_ID%7D?{x-adobe-flow-id}={FLOW_ID}.` |
| `webhook.topic` | Rubrique de votre abonnement webhook. Pour plus d’informations, consultez le [[!DNL Shopify] guide des rubriques des événements webhook](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | Format des données. |

**Réponse**

Une réponse réussie renvoie des informations sur votre webhook, y compris son `id`, son adresse et d’autres informations de métadonnées correspondantes.

```json
{
  "webhook": {
    "id": 1091138715786,
    "address": "https://dcs.adobedc.net/collection/114ae3c01f3ac77c704465f83d7d79be150fc39a5a794a214cd4ab65a5901340?x-adobe-flow-id=d9eb4a58-6a6b-4f11-9dba-6d1e0ed43bad",
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

Voici une liste des limites connues que vous pouvez rencontrer lors de l’utilisation de Webhooks avec la source [!DNL Shopify Streaming].

* Il n’est pas garanti que vous puissiez organiser l’ordre de diffusion de différents sujets pour la même ressource. Par exemple, il est possible qu’un webhook `products/update` soit diffusé avant un webhook `products/create`.
* Vous pouvez définir votre webhook pour diffuser des événements webhook à un point d’entrée au moins une fois. Cela signifie qu’un point d’entrée peut recevoir le même événement plusieurs fois. Vous pouvez rechercher des événements webhook en double en comparant l’en-tête `X-Shopify-Webhook-Id` aux événements précédents.
* [!DNL Shopify] traite les réponses de statut HTTP 2xx comme des notifications réussies. Toute autre réponse de code d’état est considérée comme un échec. [!DNL Shopify] fournit un mécanisme de reprise pour les notifications webhook ayant échoué. S’il n’y a **aucune réponse après avoir attendu cinq secondes**, [!DNL Shopify] réessayera la connexion **19 fois** au cours des **48 heures suivantes**. S’il n’y a toujours pas de réponse à la fin de la période de reprise, [!DNL Shopify] supprime le webhook.

## Étapes suivantes

Les tutoriels suivants décrivent les étapes à suivre pour connecter votre source [!DNL Shopify Streaming] à Experience Platform à l’aide de l’API et de l’interface utilisateur :

* [Créer une connexion source et un flux de données de streaming Shopify à l’aide de l’API Flow Service](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [Créer une connexion source et un flux de données de streaming Shopify dans l’interface utilisateur](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
