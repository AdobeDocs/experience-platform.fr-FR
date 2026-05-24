---
keywords: Experience Platform;accueil;rubriques populaires;shopify;Shopify;
solution: Experience Platform
title: Présentation du connecteur Source Shopify
description: Découvrez comment connecter Shopify à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: 636b31a7-e5f9-434a-acd1-226096522495
TQID: https://experienceleague.adobe.com/jQm1yV7duOKceC-5mGXjVahXqF6UwZZ5MES-VUb1vvI
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 1d1baca838be7d394b5172efb333e59df76f85e2
workflow-type: tm+mt
source-wordcount: 392
ht-degree: 4%

---

# Connecteur source [!DNL Shopify]

Le connecteur source [!DNL Shopify] (par lots) vous permet d’importer de manière fiable vos données de storefront [!DNL Shopify] dans les applications Adobe selon un planning qui fonctionne pour vous. Au lieu de diffuser chaque événement en temps réel, vous pouvez le configurer pour collecter des données de votre boutique [!DNL Shopify] à intervalles réguliers (par lots), ce qui vous permet d’obtenir une ingestion prévisible et contrôlée.

Grâce à l’accès sécurisé à l’API de votre boutique [!DNL Shopify], vous pouvez configurer le connecteur pour extraire régulièrement les entités clés, telles que les clients, les commandes, les produits et les métadonnées associées, et les mapper à votre modèle de données. Cela vous permet d’effectuer les opérations suivantes :

- Créez une vue unifiée du comportement commercial de vos clients sur l’ensemble des canaux.
- Utilisez vos données [!DNL Shopify] pour orienter la segmentation, la personnalisation et le compte rendu des performances des audiences.
- Éliminez les exportations manuelles en vous appuyant sur des importations automatisées et reproductibles à grande échelle.

En centralisant vos données [!DNL Shopify] par le biais de tâches par lots planifiées, le connecteur source [!DNL Shopify] (par lots) vous permet de créer une base fiable pour les informations et l’orchestration de l’expérience, tout en réduisant l’effort opérationnel requis pour maintenir vos données à jour.

## Conditions préalables {#prerequisites}

### Collecter les informations d’identification requises

Pour connecter votre compte [!DNL Shopify] à Experience Platform, vous pouvez utiliser soit **authentification de base** soit un jeton d’accès **basé sur**. Assurez-vous que les informations d’identification suivantes sont prêtes :

>[!BEGINTABS]

>[!TAB  Authentification de base ]

| Informations d’identification | Description |
| --- | --- |
| `host` | Point d’entrée de votre serveur [!DNL Shopify]. |
| `accessToken` | Jeton d’accès de votre compte utilisateur [!DNL Shopify]. |
| `connectionSpec.id` | (**API uniquement**) La `connectionSpec.id` est requise lors de la création de connexions via l’API. Par [!DNL Shopify], utilisez : `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. Cette valeur spécifie le type de connecteur et ses méthodes d’authentification prises en charge. |

Pour plus d’informations sur la prise en main, consultez ce [[!DNL Shopify] document d’authentification](https://shopify.dev/concepts/about-apis/authentication).

>[!TAB Basé sur les jetons d’accès]

| Informations d’identification | Description |
| --- | --- |
| `host` | Point d’entrée de votre serveur [!DNL Shopify]. |
| `accessToken` | Jeton d’accès de votre compte utilisateur [!DNL Shopify]. |
| `connectionSpec.id` | (**API uniquement**) La `connectionSpec.id` est requise lors de la création de connexions via l’API. Par [!DNL Shopify], utilisez : `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. Cette valeur spécifie le type de connecteur et ses méthodes d’authentification prises en charge. |

>[!ENDTABS]

## Connexion de [!DNL Shopify] à Experience Platform à l’aide d’API

- [Créer une connexion de base Shopify à l’aide de l’API Flow Service](../../tutorials/api/create/ecommerce/shopify.md)
- [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
- [Créer un flux de données pour une source eCommerce à l’aide de l’API Flow Service](../../tutorials/api/collect/ecommerce.md)

## Connexion d’[!DNL Shopify] à Experience Platform à l’aide de l’interface utilisateur

- [Créer une connexion source Shopify dans l’interface utilisateur](../../tutorials/ui/create/ecommerce/shopify.md)
- [Créer un flux de données pour une connexion source eCommerce dans l’interface utilisateur](../../tutorials/ui/dataflow/ecommerce.md)

## Limites

L’aperçu n’est pas pris en charge pour les colonnes suivantes. Pour pallier ce problème, il est possible de créer des mappages pour ces champs à l’aide de l’API .

- `amountSpent`
- `totalPriceSet`
- `lineItems.quantity`
- `lineItems.name`
- `lineItems.sku`
- `transactions.formattedGateway`
- `variants.sku`
