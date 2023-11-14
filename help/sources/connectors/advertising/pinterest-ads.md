---
keywords: Experience Platform;accueil;rubriques les plus consultées;publicités Pinterest
title: Présentation de la source pinterest Ads
description: Découvrez comment connecter Pinterest Ads à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
badge: Version Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 13%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>La source [!DNL Pinterest Ads] est en version Beta. Lisez la section [Présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs libellés en version bêta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’un système publicitaire tiers. La prise en charge des fournisseurs publicitaires inclut [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) est un moteur de découverte visuelle qui permet de trouver des recettes, des décors maison, des modèles inspirés et d’autres idées sur le Web. Elles sont présentées à petite échelle à l’aide d’images, de GIFs animés et de vidéos en Presse-papiers. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) vous permet de développer votre entreprise et d’atteindre 400 millions de personnes en utilisant [!DNL Pinterest].

Avec [!DNL Pinterest Ads], vous pouvez atteindre les utilisateurs par le biais de publicités ciblées pour découvrir et acheter vos produits. Pins à partir de [!DNL Pinterest Ads] sont sponsorisés pour recevoir une exposition supplémentaire dans les résultats de recherche pertinents. Utilisateurs abonnés à [!DNL Pinterest Business] Vous pouvez choisir de promouvoir les pin&#39;s les plus performants existants, de créer une image ou une vidéo, ou même de promouvoir une image qui a été épinglée à partir d’un site web. [!DNL Pinterest Ads] propose plusieurs formats d’annonces pour vous aider à atteindre vos objectifs de campagne spécifiques.

## [!DNL Pinterest] API {#pinterest-apis}

La variable [!DNL Pinterest Ads] tire parti de la source [!DNL Pinterest] API pour récupérer vos [!DNL Pinterest Ads] données, ainsi que toutes les performances et mesures. Les points d’entrée d’API pris en charge sont les suivants :

* [Analyse de campagne](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Analyse des groupes publicitaires](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Analyses des publicités](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Utilisez la variable [!DNL Pinterest Ads] source pour importer vos données [!DNL Pinterest] à Experience Platform, où vous pouvez ensuite exécuter data analytics. Les données sont renvoyées à partir de la date d’ingestion pour une période antidatée de 90 jours. [!DNL Pinterest Ads] utilise des jetons au porteur comme mécanisme d’authentification pour communiquer avec le [!DNL Pinterest] API.

## Conditions préalables {#prerequisites}

Première étape de la création d’un [!DNL Pinterest Ads] la connexion source permet de vous assurer que vous disposez d’un compte de développeur Pinterest. Si vous n’en avez pas déjà un, consultez la page [inscription](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) pour enregistrer et créer votre compte.

### Configuration [!DNL Pinterest] et générer un jeton d’accès {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Il est recommandé d’utiliser la variable [!DNL Pinterest] Les API pour générer votre jeton d’accès, car la génération de votre jeton d’accès dans l’interface utilisateur fournit un accès limité. Grâce à l’interface utilisateur, vous ne pourrez accéder qu’aux portées suivantes : `pins:read`, `boards:read` et `user_accounts:read`. Cette limitation ne convient pas à l’utilisation avec les points de terminaison analytics de la variable [!DNL Pinterest] API.

Pour générer votre jeton d’accès, lisez la section [!DNL Pinterest] guides sur [configuration de votre application](https://developers.pinterest.com/docs/getting-started/set-up-app/) et [authentification à l’aide d’OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Collecter les informations d’identification requises {#gather-required-credentials}

Pour connecter [!DNL Pinterest Ads] à Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| --- | --- |
| Jeton d’accès | La variable [!DNL Pinterest Ads] jeton d’accès pour votre compte d’utilisateur. Le compte utilisateur du jeton doit être le propriétaire de l’objet spécifié [!DNL Pinterest Ad] ou avoir l’un des rôles nécessaires qui leur sont attribués via Accès Entreprise : administrateur, Analyste ou Gestionnaire de campagnes. Pour plus d’informations sur le jeton d’accès, reportez-vous au [[!DNL Pinterest] guide de génération de votre jeton d’accès](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| Identifiant du compte publicitaire | Le rapport [!DNL Pinterest Ads] ID de compte publicitaire de votre unité opérationnelle. Pour plus d’informations sur la récupération de votre ID de compte publicitaire. Visitez le [[!DNL Pinterest] guide sur la recherche d’ID dans Ads Manager](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Identifiant de campagne, de groupe publicitaire ou de publicité | La variable `campaign`, `ad group`, ou `ad` ID correspondant à votre ID de compte publicitaire. Pour obtenir les ID requis, accédez à la [!DNL Pinterest] page pour **Pinterest Business Hub** > **Résumé du compte publicitaire** > **Campagnes** / **Groupes publicitaires** / **Publicités** et copiez les identifiants requis mentionnés juste en dessous de chacun de leurs noms. |

>[!NOTE]
>
>La variable [!DNL Pinterest] L’API fournit des API individuelles pour récupérer les données associées à chaque ID. Par conséquent, vous devez transmettre uniquement les identifiants correspondants pour le type d’identifiant qui vous intéresse.

## Mécanismes de sécurisation {#guardrails}

Les sections suivantes fournissent des informations sur les barrières de sécurité des données pour [!DNL Pinterest].

### [!DNL Pinterest] période {#pinterest-date-range}

La variable [!DNL Pinterest] API prend en charge `start_date` et un `end_date` pour récupérer les données d’analyse entre une période donnée.

* La variable `start_date` ne peut pas dépasser 90 jours avant la date actuelle.
* La variable `end_date` ne peut pas dépasser 90 jours après la `start_date`.

Lors de la planification de votre flux de données, vous devez configurer l’un des paramètres de fréquence et d’intervalle suivants :

| Fréquence | Intervalle |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Par exemple, si l’ingestion est définie le 15 mars 2023 avec une fréquence et un intervalle configurés sur `Day=1` ou `Hour=24`, puis la variable [!DNL Pinterest] L’API récupérerait uniquement les données du 15 décembre 2022, car le calcul est antidaté de 90 jours.

### [!DNL Pinterest] période {#pinterest-time-range}

La variable [!DNL Pinterest] L’API prend en charge différents types de granularité temporelle pour la manière dont les données peuvent être récupérées :

| Granularité du temps | Description |
| --- | --- |
| **TOTAL** | Les mesures de données sont agrégées sur une période spécifiée. |
| **JOUR** | Les mesures des données sont ventilées quotidiennement. |
| **HEURE** | Les mesures des données sont ventilées toutes les heures. |
| **HEBDOMADAIRE** | Les mesures des données sont ventilées sur une base hebdomadaire. |
| **MENSUEL** | Les mesures des données sont ventilées sur une base mensuelle. |

Pour Platform, la variable [!DNL Pinterest Ads] La source est configurée en interne sur `Day`, ce qui signifie que les données seront agrégées quotidiennement. Par exemple, en utilisant `impressions recorded` comme mesure, puisque la granularité est configurée comme `DAY`, vous obtiendriez `xx` impressions sur `day 1`, `yy` impressions sur `day 2` etc.

>[!IMPORTANT]
>
>Pinterest impose une limite de taux de 1 000 appels d’API par jour à son API pour lire les informations des publicités, des groupes publicitaires ou des campagnes publicitaires. Pour plus d’informations sur les limites de taux applicables aux appels API sous-jacents, reportez-vous à la section [[!DNL Pinterest] documentation sur les limites de taux](https://developers.pinterest.com/docs/reference/ratelimits/).

## Connecter [!DNL Pinterest Ads] à Platform {#connect-to-platform}

La documentation ci-dessous fournit des informations sur la connexion d’[!DNL Pinterest Ads] à Platform à l’aide d’API ou de l’interface utilisateur :

### Connecter [!DNL Pinterest Ads] à Platform à l’aide d’API {#connect-to-platform-using-api}

* [Création d’une connexion de base Pinterest à l’aide de l’API Flow Service](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
* [Création d’un flux de données pour une source publicitaire à l’aide de l’API Flow Service](../../tutorials/api/collect/advertising.md)

### Connecter [!DNL Pinterest Ads] à Platform à l’aide de l’interface utilisateur {#connect-to-platform-using-ui}

* [Création d’une connexion source Pinterest dans l’interface utilisateur](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Création d’un flux de données pour une connexion à une source publicitaire dans l’interface utilisateur](../../tutorials/ui/dataflow/advertising.md)
