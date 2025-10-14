---
title: Présentation de Google Ads Source
description: Découvrez comment connecter Google Ads à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: 1f6257e0-213c-4723-a240-511c11c5833c
source-git-commit: ac90eea69f493bf944a8f9920426a48d62faaa6c
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 22%

---

# Source [!DNL Google Ads]

>[!NOTE]
>
>La source [!DNL Google Ads] est en version Beta. Consultez la [&#x200B; Présentation des sources &#x200B;](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs étiquetés Beta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’un système publicitaire tiers. La prise en charge des fournisseurs de publicité inclut [!DNL Google Ads].

## Conditions préalables {#prerequisites}

### Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

### Configuration des autorisations sur Experience Platform

Pour connecter votre compte [!DNL Google Ads] à Experience Platform **les autorisations** Afficher les sources et **[!UICONTROL Gérer les sources]** doivent être activées. Contactez votre administrateur de produit pour obtenir les autorisations nécessaires. Pour plus d’informations, consultez le [guide de l’interface utilisateur du contrôle d’accès](../../../access-control/ui/overview.md).

### Collecter les informations d’identification requises

Vous devez fournir les valeurs appropriées aux informations d’identification suivantes pour connecter votre compte [!DNL Google Ads] à Experience Platform.

| Informations d’identification | Description |
| --- | --- |
| `clientCustomerId` | L’identifiant client est le numéro de compte qui correspond au compte client [!DNL Google Ads] que vous souhaitez gérer avec l’API [!DNL Google Ads]. Cet identifiant suit le modèle de `123-456-7890`. |
| `loginCustomerId` | L’ID de client de connexion est le numéro de compte qui correspond à votre compte [!DNL Google Ads] Manager et qui est utilisé pour récupérer les données de rapport d’un client opérationnel spécifique. Pour plus d’informations sur l’ID de client de connexion, consultez la documentation de l’API [[!DNL Google Ads] &#x200B;](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| `developerToken` | Le jeton de développement vous permet d’accéder à l’API [!DNL Google Ads]. Vous pouvez utiliser le même jeton de développement pour effectuer des requêtes sur tous vos comptes [!DNL Google Ads]. Récupérez votre jeton de développeur en [vous connectant à votre compte Manager](https://ads.google.com/home/tools/manager-accounts/) puis en accédant à la page [!DNL API Center]. |
| `refreshToken` | Le jeton d’actualisation fait partie de l’authentification [!DNL OAuth2]. Ce jeton vous permet de régénérer vos jetons d’accès après leur expiration. |
| `clientId` | L’identifiant client est utilisé conjointement avec le secret client dans le cadre de l’authentification [!DNL OAuth2]. Ensemble, l’identifiant client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application à [!DNL Google]. |
| `clientSecret` | Le secret client est utilisé conjointement avec l’identifiant client dans le cadre de l’authentification [!DNL OAuth2]. Ensemble, l’identifiant client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application à [!DNL Google]. |
| `googleAdsApiVersion` | Version actuelle de l’API prise en charge par [!DNL Google Ads]. Bien que la dernière version soit `v18`, la dernière version prise en charge sur Experience Platform est `v17`. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Google Ads] est : `d771e9c1-4f26-40dc-8617-ce58c4b53702`. Cette valeur est requise si vous connectez votre compte [!DNL Google Ads] à l’aide de l’API [!DNL Flow Service]. |

## Connexion de [!DNL Google Ads] à Experience Platform

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Google Ads] à Experience Platform à l’aide d’API ou de l’interface utilisateur :

### Utiliser les API

* [Créer une connexion de base Google Ads à l’aide de l’API Flow Service](../../tutorials/api/create/advertising/ads.md)
* [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
* [Créer un flux de données pour une source publicitaire à l’aide de l’API Flow Service](../../tutorials/api/collect/advertising.md)

### Utilisation de l’interface utilisateur

* [Créer une connexion source Google Ads dans l’interface utilisateur](../../tutorials/ui/create/advertising/ads.md)
* [Créer un flux de données pour une connexion source publicitaire dans l’interface utilisateur](../../tutorials/ui/dataflow/advertising.md)
