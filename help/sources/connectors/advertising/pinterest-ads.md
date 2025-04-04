---
keywords: Experience Platform;accueil;rubriques populaires;Pinterest Ads;
title: Présentation de Pinterest Ads Source
description: Découvrez comment connecter Pinterest Ads à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 6%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>La source [!DNL Pinterest Ads] est en version Beta. Lisez la [Présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs étiquetés Beta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’un système publicitaire tiers. La prise en charge des fournisseurs de publicité inclut [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) est un moteur de découverte visuelle permettant de trouver des recettes, un décor, une inspiration et d’autres idées sur le web. Elles sont présentées à petite échelle à l’aide d’images, de GIF animés et de vidéos au format carte. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) vous permet de faire croître votre entreprise et d&#39;atteindre 400 millions de personnes en utilisant [!DNL Pinterest].

Avec [!DNL Pinterest Ads], vous pouvez atteindre les utilisateurs par le biais de publicités ciblées pour découvrir et acheter vos produits. Les épingles de [!DNL Pinterest Ads] sont parrainées pour recevoir une exposition supplémentaire dans les résultats de recherche pertinents. Les utilisateurs abonnés à [!DNL Pinterest Business] peuvent choisir de promouvoir les épingles les plus performantes existantes, de créer une nouvelle image ou vidéo, ou même de promouvoir une image qui a été épinglée à partir d’un site web. [!DNL Pinterest Ads] propose plusieurs formats d’annonce publicitaire pour vous aider à atteindre vos objectifs de campagne spécifiques.

## API [!DNL Pinterest] {#pinterest-apis}

La source de [!DNL Pinterest Ads] utilise les API [!DNL Pinterest] pour récupérer vos données [!DNL Pinterest Ads], ainsi que toutes les performances et mesures. Les points d’entrée d’API pris en charge sont les suivants :

* [Analyse de Campaign](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Analyse des groupes publicitaires](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Analyses des publicités](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Utilisez la source de [!DNL Pinterest Ads] pour importer vos données de [!DNL Pinterest] dans Experience Platform, où vous pouvez ensuite exécuter des analyses de données. Les données sont renvoyées à partir de la date d’ingestion pendant une période antidatée de 90 jours. [!DNL Pinterest Ads] utilise des jetons porteur comme mécanisme d’authentification pour communiquer avec les API [!DNL Pinterest].

## Conditions préalables {#prerequisites}

La première étape de la création d’une connexion source [!DNL Pinterest Ads] consiste à vous assurer que vous disposez d’un compte de développeur Pinterest. Si vous n’en avez pas encore, visitez la page [s’inscrire](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) pour vous inscrire et créer votre compte.

### Configurer [!DNL Pinterest] application et générer un jeton d’accès {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Il est recommandé d’utiliser les API [!DNL Pinterest] pour générer votre jeton d’accès, car la génération de votre jeton d’accès dans l’interface utilisateur fournit un accès limité. Par le biais de l’interface utilisateur, vous ne pourrez accéder qu’aux portées suivantes : `pins:read`, `boards:read` et `user_accounts:read`. Cette limitation n’est pas adaptée à l’utilisation avec les points d’entrée Analytics de l’API [!DNL Pinterest].

Pour générer votre jeton d’accès, lisez les guides [!DNL Pinterest] sur [configuration de votre application](https://developers.pinterest.com/docs/getting-started/set-up-app/) et [authentification à l’aide d’OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Collecter les informations d’identification requises {#gather-required-credentials}

Pour connecter [!DNL Pinterest Ads] à Experience Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| --- | --- |
| Jeton d’accès | Jeton d’accès [!DNL Pinterest Ads] de votre compte d’utilisateur. Le compte utilisateur du jeton doit être soit le propriétaire du compte [!DNL Pinterest Ad] spécifié, soit avoir l&#39;un des rôles nécessaires qui lui sont accordés via Business Access : Admin, Analyst ou Campaign Manager. Pour plus d’informations sur le jeton d’accès, reportez-vous au guide [[!DNL Pinterest]  sur la génération de votre jeton d’accès](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| ID de compte publicitaire | Identifiant de compte publicitaire [!DNL Pinterest Ads] associé à votre unité opérationnelle. Pour plus d’informations sur la récupération de votre ID de compte publicitaire. Consultez le guide [[!DNL Pinterest]  sur la recherche d’identifiants dans Ads Manager](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Campagne, groupe publicitaire ou ID publicitaire | Identifiants `campaign`, `ad group` ou `ad` qui correspondent à l’identifiant de votre compte publicitaire. Pour obtenir les identifiants requis, accédez à la page [!DNL Pinterest] de **Pinterest Business Hub** > **Résumé du compte publicitaire** > **Campagnes** / **Groupes publicitaires** / **Publicités** et copiez les identifiants requis mentionnés juste en dessous de chacun de leurs noms. |

>[!NOTE]
>
>L’API [!DNL Pinterest] fournit des API individuelles pour récupérer les données associées à chaque identifiant. Par conséquent, vous ne devez transmettre que les identifiants correspondants pour le type d’identifiant qui vous intéresse.

## Mécanismes de sécurisation {#guardrails}

Les sections suivantes fournissent des informations sur les mécanismes de sécurisation des données pour [!DNL Pinterest].

### [!DNL Pinterest] de dates {#pinterest-date-range}

L’API [!DNL Pinterest] prend en charge un `start_date` et un paramètre `end_date` pour récupérer les données d’analyse entre une période donnée.

* La `start_date` ne peut pas être antérieure de plus de 90 jours à la date actuelle.
* La `end_date` ne peut pas être postérieure de plus de 90 jours à la `start_date`.

Lors de la planification de votre flux de données, vous devez configurer l’un des paramètres de fréquence et d’intervalle suivants :

| Fréquence | Intervalle |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Par exemple, si l’ingestion est définie le 15 mars 2023 avec un paramètre de fréquence et d’intervalle configuré sur `Day=1` ou `Hour=24`, l’API [!DNL Pinterest] ne récupère les données que depuis le 15 décembre 2022, car le calcul est antidaté pendant 90 jours.

### [!DNL Pinterest] de temps {#pinterest-time-range}

L’API [!DNL Pinterest] prend en charge différents types de granularité temporelle pour la manière dont les données peuvent être récupérées :

| Granularité temporelle | Description |
| --- | --- |
| **TOTAL** | Les mesures de données sont agrégées sur une période spécifiée. |
| **JOUR** | Les mesures de données sont réparties sur une base quotidienne. |
| **HEURE** | Les mesures de données sont réparties sur une base horaire. |
| **HEBDOMADAIRE** | Les mesures de données sont ventilées sur une base hebdomadaire. |
| **MENSUEL** | Les mesures de données sont ventilées sur une base mensuelle. |

Pour Experience Platform, la source de [!DNL Pinterest Ads] est configurée en interne sur `Day`, ce qui signifie que les données seront agrégées quotidiennement. Par exemple, si vous utilisez `impressions recorded` comme mesure, puisque la granularité est configurée en tant que `DAY`, vous obtiendrez des impressions `xx` sur les `day 1`, des impressions `yy` sur les `day 2`, etc.

>[!IMPORTANT]
>
>Pinterest impose une limite de taux de 1 000 appels API par jour à son API pour lire des informations provenant d’annonces, de groupes d’annonces ou de campagnes publicitaires. Pour plus d’informations sur les limites de taux applicables aux appels API sous-jacents, reportez-vous à la [[!DNL Pinterest]  documentation sur les limites de taux](https://developers.pinterest.com/docs/reference/ratelimits/).

## Connexion de [!DNL Pinterest Ads] à Experience Platform {#connect-to-platform}

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Pinterest Ads] à Experience Platform à l’aide d’API ou de l’interface utilisateur :

### Connexion de [!DNL Pinterest Ads] à Experience Platform à l’aide d’API {#connect-to-platform-using-api}

* [Créer une connexion de base Pinterest à l’aide de l’API Flow Service](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
* [Créer un flux de données pour une source publicitaire à l’aide de l’API Flow Service](../../tutorials/api/collect/advertising.md)

### Connexion d’[!DNL Pinterest Ads] à Experience Platform à l’aide de l’interface utilisateur {#connect-to-platform-using-ui}

* [Créer une connexion source Pinterest dans l’interface utilisateur](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Créer un flux de données pour une connexion source publicitaire dans l’interface utilisateur](../../tutorials/ui/dataflow/advertising.md)
