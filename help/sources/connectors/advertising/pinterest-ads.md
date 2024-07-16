---
keywords: Experience Platform;accueil;rubriques les plus consultées;publicités Pinterest
title: Présentation de Pinterest Ads Source
description: Découvrez comment connecter Pinterest Ads à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
badge: Version bêta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 14%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>La source [!DNL Pinterest Ads] est en version Beta. Pour plus d’informations sur l’utilisation de connecteurs étiquetés bêta, consultez la [Présentation des sources](../../home.md#terms-and-conditions) .

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’un système publicitaire tiers. [!DNL Pinterest Ads] est compatible avec les fournisseurs de publicité.

[[!DNL Pinterest]](https://www.pinterest.com) est un moteur de découverte visuelle qui permet de trouver des recettes, des décors à domicile, des modèles inspirés et d’autres idées sur le Web. Elles sont présentées à petite échelle à l’aide d’images, de GIFs animés et de vidéos en Presse-papiers. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) vous permet de développer votre entreprise et d’atteindre 400 millions de personnes en utilisant [!DNL Pinterest].

Avec [!DNL Pinterest Ads], vous pouvez atteindre les utilisateurs par le biais de publicités ciblées pour découvrir et acheter vos produits. Les pins de [!DNL Pinterest Ads] sont sponsorisés pour recevoir une exposition supplémentaire dans les résultats de recherche pertinents. Les utilisateurs abonnés à [!DNL Pinterest Business] peuvent choisir de promouvoir les pin&#39;s les plus performants existants, de créer une image ou une vidéo, ou même de promouvoir une image qui a été épinglée à partir d&#39;un site web. [!DNL Pinterest Ads] propose plusieurs formats publicitaires pour vous aider à atteindre vos objectifs de campagne spécifiques.

## [!DNL Pinterest] API {#pinterest-apis}

La source [!DNL Pinterest Ads] utilise les API [!DNL Pinterest] pour récupérer vos données [!DNL Pinterest Ads], ainsi que toutes les performances et mesures. Les points d’entrée d’API pris en charge sont les suivants :

* [Analyse de campagne](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Analyse du groupe publicitaire](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Analytics des publicités](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Utilisez la source [!DNL Pinterest Ads] pour importer vos données de [!DNL Pinterest] vers Experience Platform, où vous pouvez ensuite exécuter l’analyse des données. Les données sont renvoyées à partir de la date d’ingestion pour une période antidatée de 90 jours. [!DNL Pinterest Ads] utilise des jetons au porteur comme mécanisme d’authentification pour communiquer avec les API [!DNL Pinterest].

## Conditions préalables {#prerequisites}

La première étape de la création d’une connexion source [!DNL Pinterest Ads] consiste à vous assurer que vous disposez d’un compte de développeur Pinterest. Si vous n&#39;en avez pas déjà un, rendez-vous sur la page [inscrivez-vous](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) pour vous enregistrer et créer votre compte.

### Configurer l’application [!DNL Pinterest] et générer un jeton d’accès {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Il est recommandé d’utiliser les API [!DNL Pinterest] pour générer votre jeton d’accès, car la génération de votre jeton d’accès dans l’interface utilisateur fournit un accès limité. Grâce à l’interface utilisateur, vous ne pourrez accéder qu’aux portées suivantes : `pins:read`, `boards:read` et `user_accounts:read`. Cette limitation ne convient pas à l’utilisation avec les points d’entrée Analytics de l’API [!DNL Pinterest].

Pour générer votre jeton d’accès, lisez les [!DNL Pinterest] guides sur la [configuration de votre application](https://developers.pinterest.com/docs/getting-started/set-up-app/) et l’ [authentification à l’aide d’OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Collecter les informations d’identification requises {#gather-required-credentials}

Pour connecter [!DNL Pinterest Ads] à Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| --- | --- |
| Jeton d’accès | Jeton d’accès [!DNL Pinterest Ads] pour votre compte utilisateur. Le compte utilisateur du jeton doit être le propriétaire du compte [!DNL Pinterest Ad] spécifié ou disposer de l’un des rôles nécessaires qui lui sont attribués via Accès professionnel : Administrateur, Analyste ou Gestionnaire de campagnes. Pour plus d’informations sur le jeton d’accès, reportez-vous au [[!DNL Pinterest] guide de génération de votre jeton d’accès](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| Identifiant du compte publicitaire | L’ID de compte publicitaire [!DNL Pinterest Ads] associé pour votre unité opérationnelle. Pour plus d’informations sur la récupération de votre ID de compte publicitaire. Consultez le [[!DNL Pinterest] guide sur la recherche d’ID dans Ads Manager](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Identifiant de campagne, de groupe publicitaire ou de publicité | Les identifiants `campaign`, `ad group` ou `ad` qui correspondent à votre ID de compte publicitaire. Pour obtenir les ID requis, accédez à la page [!DNL Pinterest] de **Pinterest Business Hub** > **Résumé du compte publicitaire** > **Campagnes** / **Groupes publicitaires** / **Publicités** et copiez les ID requis mentionnés juste en dessous de chacun de leurs noms. |

>[!NOTE]
>
>L’API [!DNL Pinterest] fournit des API individuelles pour récupérer les données associées à chaque ID. Par conséquent, vous devez transmettre uniquement les identifiants correspondants pour le type d’identifiant qui vous intéresse.

## Mécanismes de sécurisation {#guardrails}

Les sections suivantes fournissent des informations sur les barrières de sécurité des données pour [!DNL Pinterest].

### [!DNL Pinterest] période {#pinterest-date-range}

L’API [!DNL Pinterest] prend en charge à la fois un paramètre `start_date` et un paramètre `end_date` pour récupérer les données d’analyse entre une période donnée.

* `start_date` ne peut pas être supérieur à 90 jours avant la date actuelle.
* `end_date` ne peut pas dépasser 90 jours après le `start_date`.

Lors de la planification de votre flux de données, vous devez configurer l’un des paramètres de fréquence et d’intervalle suivants :

| Fréquence | Intervalle |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Par exemple, si l’ingestion est définie le 15 mars 2023 avec un paramètre de fréquence et d’intervalle configuré sur `Day=1` ou `Hour=24`, alors l’API [!DNL Pinterest] récupérerait uniquement les données du 15 décembre 2022, car le calcul est antidaté de 90 jours.

### [!DNL Pinterest] sur une période {#pinterest-time-range}

L’API [!DNL Pinterest] prend en charge différents types de granularité temporelle pour la manière dont les données peuvent être récupérées :

| Granularité du temps | Description |
| --- | --- |
| **TOTAL** | Les mesures de données sont agrégées sur une période spécifiée. |
| **DAY** | Les mesures des données sont ventilées quotidiennement. |
| **HEURE** | Les mesures des données sont ventilées toutes les heures. |
| **HEEKLY** | Les mesures des données sont ventilées sur une base hebdomadaire. |
| **MENTHLY** | Les mesures des données sont ventilées sur une base mensuelle. |

Pour Platform, la source [!DNL Pinterest Ads] est configurée en interne sur `Day`, ce qui signifie que les données seront agrégées quotidiennement. Par exemple, en utilisant `impressions recorded` comme mesure, puisque la granularité est configurée comme `DAY`, vous obtenez `xx` impressions sur `day 1`, `yy` impressions sur `day 2`, etc.

>[!IMPORTANT]
>
>Pinterest impose une limite de taux de 1 000 appels d’API par jour à son API pour lire les informations des publicités, des groupes publicitaires ou des campagnes publicitaires. Pour plus d’informations sur les limites de taux applicables aux appels API sous-jacents, consultez la [[!DNL Pinterest] documentation sur les limites de taux](https://developers.pinterest.com/docs/reference/ratelimits/).

## Connecter [!DNL Pinterest Ads] à Platform {#connect-to-platform}

La documentation ci-dessous fournit des informations sur la connexion d’[!DNL Pinterest Ads] à Platform à l’aide d’API ou de l’interface utilisateur :

### Connecter [!DNL Pinterest Ads] à Platform à l’aide d’API {#connect-to-platform-using-api}

* [Création d’une connexion de base Pinterest à l’aide de l’API Flow Service](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
* [Création d’un flux de données pour une source publicitaire à l’aide de l’API Flow Service](../../tutorials/api/collect/advertising.md)

### Connecter [!DNL Pinterest Ads] à Platform à l’aide de l’interface utilisateur {#connect-to-platform-using-ui}

* [Création d’une connexion source Pinterest dans l’interface utilisateur](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Création d’un flux de données pour une connexion à une source publicitaire dans l’interface utilisateur](../../tutorials/ui/dataflow/advertising.md)
