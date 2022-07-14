---
keywords: Experience Platform;accueil;rubriques populaires;Connecteur source Analytics;analytics;Analytics;AAID;
title: Connecteur source Adobe Analytics pour les données d’une suite de rapports
description: Ce document présente Analytics et décrit les cas d’utilisation des données Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 352993365dfcd4f39e7aea337b014430f7bad41c
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 16%

---

# Connecteur source Adobe Analytics pour les données de suite de rapports

Adobe Experience Platform vous permet d’ingérer des données Adobe Analytics par le biais du connecteur source Analytics. Le [!DNL Analytics] source Connector diffuse les données collectées par [!DNL Analytics] vers Platform en temps réel, conversion au format SCDS [!DNL Analytics] données dans [!DNL Experience Data Model] Champs (XDM) à utiliser par Platform.

Ce document présente les [!DNL Analytics] et décrit les cas d’utilisation pour [!DNL Analytics] data.

## Adobe Analytics et données Analytics

[!DNL Analytics] est un moteur puissant qui vous aide à en savoir plus sur vos clients, sur la manière dont ils interagissent avec vos propriétés web, à déterminer l’efficacité de vos dépenses de marketing numérique et à identifier les améliorations à apporter. [!DNL Analytics] gère des trillions de transactions web par an et la variable [!DNL Analytics] le connecteur source vous permet d’exploiter facilement ces données comportementales enrichies et d’enrichir la [!DNL Real-time Customer Profile] en quelques minutes.

![](./images/analytics-data-experience-platform.png)

à un niveau élevé, [!DNL Analytics] collecte des données à partir de divers canaux numériques et de plusieurs centres de données dans le monde entier. Une fois les données collectées, les règles VISTA (Visitor Identification, Segmentation and Transformation Architecture) et les règles de traitement sont appliquées pour façonner les données entrantes. Une fois que les données brutes ont subi ce traitement léger, elles sont alors considérées comme prêtes à être utilisées par [!DNL Real-time Customer Profile]. Dans un processus parallèle mentionné ci-dessus, les mêmes données traitées sont microtraitées par lot et ingérées dans des jeux de données Platform pour être utilisées par [!DNL Data Science Workspace], [!DNL Query Service]et d’autres applications de découverte de données.

Voir [présentation des règles de traitement](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) pour plus d’informations sur les règles de traitement.

## Modèle de données d’expérience (XDM)

XDM est une spécification documentée publiquement qui fournit des structures et des définitions courantes pour qu’une application puisse communiquer avec des services sur  Experience Platform.

Le respect des normes XDM permet d’intégrer uniformément les données, ce qui facilite la diffusion des données et la collecte des informations.

Pour en savoir plus sur XDM, consultez la [présentation du système XDM](../../../xdm/home.md).

## Comment les champs sont-ils mappés d’Adobe Analytics à XDM ?

Lorsqu’une connexion source est établie pour apporter [!DNL Analytics] données dans Experience Platform à l’aide de l’interface utilisateur de Platform, les champs de données sont automatiquement mappés et ingérés dans [!DNL Real-time Customer Profile] en quelques minutes. Pour plus d’informations sur la création d’une connexion source avec [!DNL Analytics] à l’aide de l’interface utilisateur de Platform, reportez-vous à la section [Tutoriel sur le connecteur source Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Pour plus d’informations sur le mappage des champs entre [!DNL Analytics] et Experience Platform, reportez-vous à la section [Mappage des champs Adobe Analytics](./mapping/analytics.md) guide.

## Quelle est la latence attendue sur Platform pour les données Analytics ?

Le tableau ci-dessous décrit la latence attendue des données Analytics sur Platform. La latence varie selon la configuration client, les volumes de données et les applications clients. Par exemple, si l’implémentation d’Analytics est configurée avec `A4T`, la latence du pipeline passera à 5-10 minutes.

| Données Analytics | Latence attendue |
| -------------- | ---------------- |
| Nouvelles données pour [!DNL Real-time Customer Profile] (A4T) **not** enabled) | &lt; 2 minutes |
| Nouvelles données pour [!DNL Real-time Customer Profile] (A4T) **is** enabled) | &lt; 15 minutes |
| Nouvelles données pour le lac de données | &lt; 90 minutes |
| Renvoi des données (13 mois de données ou 10 milliards d’événements, selon la valeur la plus faible) | &lt; 4 semaines |

>[!NOTE]
>
>Les données de renvoi Analytics ne sont pas ingérées dans [!DNL Profile] et n’est donc pas pris en compte dans les profils de licence.

## Identifiants Principal dans [!DNL Analytics] data

Chaque accès à partir de [!DNL Analytics] Le connecteur source contient un identifiant Principal qui dépend de l’existence d’un ECID ou d’un AAID. S’il existe un ECID, celui-ci est désigné comme l’identifiant Principal. S’il existe un AAID, celui-ci est désigné comme la Principale.

Le tableau suivant fournit des informations supplémentaires sur les champs d’identité dans votre [!DNL Analytics] data.

| Champ d’identité | Description |
| --- | --- |
| AAID | L’AAID est l’identifiant d’appareil Principal dans Adobe Analytics et il est garanti qu’il existe sur chaque événement transmis par le biais de la variable [!DNL Analytics] source. AAID est parfois appelé *Identifiant Analytics hérité* ou comme `s_vi` ID de cookie. Malgré cela, un AAID est créé même si la variable `s_vi` n’est pas présent. L’AAID est représenté par la variable `post_visid_high` et `post_visid_low` colonnes dans [[!DNL Analytics] flux de données](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=fr). Sur un événement donné, le champ AAID contient une identité unique qui peut être l’un des différents types décrits dans la variable [ordre des opérations pour [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Remarque**: Dans une suite de rapports entière, un AAID peut contenir un mélange de types entre les événements. |
| ECID | L’ECID (identifiant Experience Cloud) est un champ d’identifiant d’appareil distinct, qui est renseigné dans Adobe Analytics lorsque [!DNL Analytics] est mis en oeuvre à l’aide du service Experience Cloud Identity. L’ECID est parfois appelé MCID (ID de Marketing Cloud). Si un ECID existe sur un événement, l’AAID peut être basé sur l’ECID selon que l’Analytics [période de grâce](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) est configuré. L’ECID est représenté par la variable `mcvisid` dans les flux de données Analytics. Pour plus d’informations sur ECID, voir [Présentation d’ECID](../../../identity-service/ecid.md). Pour plus d’informations sur le fonctionnement d’ECID avec [!DNL Analytics], voir le document sur [Requêtes d’Analytics et d’ID d’Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html?lang=en). |
| AACUSTOMID | AACUSTOMID est un champ d’identifiant distinct renseigné dans Adobe Analytics en fonction de l’utilisation de la variable `s.VisitorID` dans la variable [!DNL Analytics] implémentation. L’AACUSTOMID est représenté par le `cust_visid` colonne dans [[!DNL Analytics] flux de données](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Si l’AACUSTOMID est présent, l’AAID est basé sur l’AACUSTOMID, car l’AACUSTOMID l’emporte sur tous les autres identifiants, tels que définis par la variable [ordre des opérations pour [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### Comment [!DNL Analytics] source traite les identités

Le [!DNL Analytics] source transmet ces identités à Experience Platform dans un formulaire XDM en tant que :

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Ces champs ne sont pas marqués comme identités. Au lieu de cela, les mêmes identités sont copiées dans les `identityMap` en tant que paires clé-valeur :

* `{ “key”: “AAID”, “value”: [ { “id”: “<identity>”, “primary”: <true or false> } ] }`
* `{ “key”: “ECID”, “value”: [ { “id”: “<identity>”, “primary”: <true or false> } ] }`
* `{ “key”: “AACUSTOMID”, “value”: [ { “id”: “<identity>”, “primary”: false } ] }`

Dans la carte d’identité, si ECID est présent, il est marqué comme identité Principale de l’événement. Dans ce cas, AAID peut être basé sur ECID en raison de la variable [Période de grâce d’Identity Service](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). Dans le cas contraire, AAID est marqué comme identité Principale de l’événement. AACUSTOMID n’est jamais marqué comme ID Principal de l’événement. Cependant, si AACUSTOMID est présent, AAID est basé sur AACUSTOMID en raison de l’ordre des opérations Experience Cloud.

### Customer Journey Analytics et identifiant Principal

Pour Customer Journey Analytics, la définition de l’ID de Principal n’est importante que si vous décidez d’utiliser l’ID de Principal comme ID de personne. Cependant, ce n’est pas obligatoire. Vous pouvez choisir une autre colonne d’identité comme ID de personne.