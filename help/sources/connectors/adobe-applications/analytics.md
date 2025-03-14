---
title: Connecteur Source Adobe Analytics pour les données d’une suite de rapports
description: Ce document fournit un aperçu d’Analytics et décrit les cas d’utilisation des données Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: d56a37c5b1c5768b3f6811be9d30d45628fdabca
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 7%

---

# Connecteur source Adobe Analytics pour les données de suite de rapports

Adobe Experience Platform vous permet d’ingérer des données Adobe Analytics par le biais du connecteur source Analytics. Le connecteur source [!DNL Analytics] diffuse en temps réel les données collectées par [!DNL Analytics] vers Platform, en convertissant des données [!DNL Analytics] au format SCDS en champs [!DNL Experience Data Model] (XDM) pour une utilisation par Platform.

Ce document fournit un aperçu de [!DNL Analytics] et décrit les cas d’utilisation des données [!DNL Analytics].

## Adobe Analytics et données Analytics

[!DNL Analytics] est un moteur puissant qui vous permet d’en savoir plus sur vos clients, sur la manière dont ils interagissent avec vos propriétés web, de déterminer l’efficacité de vos dépenses de marketing numérique et d’identifier les améliorations à apporter. [!DNL Analytics] gère des milliers de milliards de transactions web par an et le connecteur source [!DNL Analytics] vous permet d’exploiter facilement ces riches données comportementales et d’enrichir le [!DNL Real-Time Customer Profile] en quelques minutes.

![Graphique illustrant le parcours de données de différentes applications d’Adobe, y compris Adobe Analytics.](./images/analytics-data-experience-platform.png)

À un niveau élevé, [!DNL Analytics] collecte des données de divers canaux numériques et de plusieurs centres de données dans le monde entier. Une fois les données collectées, les règles VISTA (Visitor Identification, Segmentation and Transformation Architecture) et les règles de traitement sont appliquées pour façonner les données entrantes. Une fois que les données brutes ont subi ce traitement léger, elles sont alors considérées comme prêtes à être utilisées par [!DNL Real-Time Customer Profile]. Dans un processus parallèle, les mêmes données traitées sont microtraitées par lot et ingérées dans des jeux de données Platform pour être utilisées par [!DNL Query Service] et d’autres applications de découverte de données.

Pour plus d’informations sur les règles de traitement, consultez la [présentation des règles de traitement](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=fr) .

## Modèle de données d’expérience (XDM)

XDM est une spécification documentée publiquement qui fournit des structures et des définitions courantes pour qu’une application puisse communiquer avec des services sur Experience Platform.

Le respect des normes XDM permet d’intégrer uniformément les données, ce qui facilite la diffusion des données et la collecte des informations.

Pour en savoir plus sur XDM, consultez la [présentation du système XDM](../../../xdm/home.md).

## Comment les champs sont-ils mappés d’Adobe Analytics à XDM ?

>[!IMPORTANT]
>
>Les transformations de préparation des données peuvent ajouter une latence au flux de données global. La latence supplémentaire ajoutée varie en fonction de la complexité de la logique de transformation.

Lorsqu’une connexion source est établie pour importer des données [!DNL Analytics] dans Experience Platform à l’aide de l’interface utilisateur de Platform, les champs de données sont automatiquement mappés et ingérés dans [!DNL Real-Time Customer Profile] en quelques minutes. Pour obtenir des instructions sur la création d’une connexion source avec [!DNL Analytics] à l’aide de l’interface utilisateur de Platform, consultez le [tutoriel sur le connecteur source Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Pour plus d’informations sur le mappage des champs entre [!DNL Analytics] et l’Experience Platform, consultez le guide [Mapping des champs Adobe Analytics](./mapping/analytics.md) .

## Quelle est la latence attendue sur Platform pour les données Analytics ?

Le tableau ci-dessous décrit la latence attendue des données Analytics sur Platform. La latence varie en fonction de la configuration client, des volumes de données et des applications client. Par exemple, si l’implémentation d’Analytics est configurée avec `A4T`, la latence du pipeline passera à 5-10 minutes.

| Données Analytics | Latence attendue |
| -------------- | ---------------- |
| Nouvelles données pour [!DNL Real-Time Customer Profile] (A4T **not** enabled) | &lt; 2 minutes |
| Nouvelles données pour [!DNL Real-Time Customer Profile] (A4T **is** activé) | jusqu’à 30 minutes |
| Nouvelles données pour le lac de données | &lt; 2,25 heures |
| Nouvelles données pour Customer Journey Analytics sans [assemblage](https://experienceleague.adobe.com/docs/analytics-platform/using/stitching/overview.html?lang=en) | &lt; 3,75 heures |
| Nouvelles données à Customer Journey Analytics avec groupement | &lt; 7 heures |
| Renvoi de moins de 10 milliards d’événements | &lt; 4 semaines |

Pour plus d’informations sur les latences du Customer Journey Analytics, voir : [Barrières de sécurité du Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html?lang=en).

Le renvoi Analytics pour les environnements de test de production est défini par défaut sur 13 mois. Pour les données Analytics dans les environnements de test hors production, le renvoi est défini sur trois mois. La limite de 10 milliards d&#39;événements mentionnée dans le tableau ci-dessus est strictement en ce qui concerne la latence attendue.

Lorsque vous créez un flux de données source Analytics dans un environnement de test de production, deux flux de données sont créés :

* Flux de données qui effectue un renvoi de 13 mois des données de suite de rapports historiques dans le lac de données. Ce flux de données se termine une fois le renvoi terminé.
* Flux de données qui envoie des données actives au lac de données et à [!DNL Real-Time Customer Profile]. Ce flux de données s’exécute en continu.

>[!NOTE]
>
>Les données de renvoi Analytics ne sont pas ingérées dans [!DNL Profile] et ne sont donc pas prises en compte dans les profils de licence.

## Identifiants de Principal dans les données [!DNL Analytics]

Chaque accès du connecteur source [!DNL Analytics] contient un identifiant principal qui dépend de l’existence d’un ECID ou d’un AAID. S’il existe un ECID, l’ECID est désigné comme l’identifiant principal. S’il existe un AAID, celui-ci est désigné comme principal.

Le tableau suivant fournit plus d’informations sur les champs d’identité de vos données [!DNL Analytics].

| Champ d’identité | Description |
| --- | --- |
| AAID | L’AAID est l’identifiant d’appareil principal dans Adobe Analytics et il est garanti qu’il existe sur chaque événement transmis par le biais de la source [!DNL Analytics]. L’AAID est parfois appelé *identifiant Analytics hérité* ou ID de cookie `s_vi`. Malgré cela, un AAID est créé même si le cookie `s_vi` n’est pas présent. L’AAID est représenté par les colonnes `post_visid_high` et `post_visid_low` dans les [[!DNL Analytics] flux de données](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Sur tout événement donné, le champ AAID contient une identité unique qui peut être l’un des différents types décrits dans l’ [ordre des opérations pour [!DNL Analytics] IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Remarque** : dans une suite de rapports entière, un AAID peut contenir un mélange de types entre les événements. |
| ECID | L’ECID (identifiant Experience Cloud) est un champ d’identifiant d’appareil distinct, qui est renseigné dans Adobe Analytics lorsque [!DNL Analytics] est mis en oeuvre à l’aide du service d’identification Experience Cloud. L’ECID est parfois appelé MCID (ID de Marketing Cloud). Si un ECID existe sur un événement, l’AAID peut être basé sur l’ECID selon que la [période de grâce](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) d’Analytics est configurée ou non. L’ECID est représenté par le `mcvisid` dans les flux de données Analytics. Pour plus d’informations sur ECID, consultez la [présentation ECID](../../../identity-service/features/ecid.md). Pour plus d’informations sur le fonctionnement d’ECID avec [!DNL Analytics], consultez le document sur les [requêtes d’identifiant Analytics et d’Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html). |
| AACUSTOMID | AACUSTOMID est un champ d’identifiant distinct qui est renseigné dans Adobe Analytics en fonction de l’utilisation de la variable `s.VisitorID` dans l’implémentation de [!DNL Analytics]. L’AACUSTOMID est représenté par la colonne `cust_visid` dans les [[!DNL Analytics] flux de données](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Si l’AACUSTOMID est présent, l’AAID est basé sur l’AACUSTOMID, car l’AACUSTOMID l’emporte sur tous les autres identifiants, comme défini par l’[ordre des opérations pour les [!DNL Analytics] IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### Traitement des identités par la source [!DNL Analytics]

La source [!DNL Analytics] transmet ces identités à l’Experience Platform dans le formulaire XDM en tant que :

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Ces champs ne sont pas marqués comme identités. Au lieu de cela, les mêmes identités (si présentes dans l’événement) sont copiées dans les `identityMap` XDM en tant que paires clé-valeur :

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

Lorsque l’identité ou les identités sont copiées dans `identityMap`, `endUserIDs._experience.mcid.namespace.code` est également défini sur le même événement :

* Si AAID est présent, `endUserIDs._experience.aaid.namespace.code` est défini sur &quot;AAID&quot;.
* Si ECID est présent, `endUserIDs._experience.mcid.namespace.code` est défini sur &quot;ECID&quot;.
* Si AACUSTOMID est présent, `endUserIDs._experience.aacustomid.namespace.code` est défini sur &quot;AACUSTOMID&quot;.

Dans la carte d’identité, si ECID est présent, il est marqué comme identité principale de l’événement. Dans ce cas, AAID peut être basé sur ECID en raison de la [période de grâce Identity Service](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). Dans le cas contraire, AAID est marqué comme identité principale de l’événement. AACUSTOMID n’est jamais marqué comme identifiant de Principal pour l’événement. Cependant, si AACUSTOMID est présent, AAID est basé sur AACUSTOMID en raison de l’ordre des opérations Experience Cloud.

>[!NOTE]
>
>Vous pouvez utiliser la préparation de données pour filtrer les identités secondaires provenant d’Analytics, telles que AAID et AACUSTOMID. Si elles sont filtrées, ces identités ne seront pas ingérées dans Profile si elles sont disponibles dans les données Analytics entrantes. Les données non filtrées continueront à être chargées dans le lac de données.
