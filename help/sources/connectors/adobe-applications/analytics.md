---
title: Connecteur Source Adobe Analytics pour les données de suite de rapports
description: Ce document présente Analytics et décrit des cas d’utilisation des données Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 816c41613844e0d2b53003bc865f1996a86297c6
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 6%

---

# Connecteur source Adobe Analytics pour les données de suite de rapports

Adobe Experience Platform vous permet d’ingérer des données Adobe Analytics par le biais du connecteur source Analytics. Le connecteur source [!DNL Analytics] diffuse en temps réel les données collectées par [!DNL Analytics] vers Experience Platform, en convertissant les données [!DNL Analytics] au format SCDS en champs [!DNL Experience Data Model] (XDM) utilisables par Experience Platform.

Ce document présente une vue d’ensemble des [!DNL Analytics] et décrit des cas d’utilisation des données [!DNL Analytics].

## Adobe Analytics et données Analytics

[!DNL Analytics] est un moteur puissant qui vous permet d’en savoir plus sur vos clients, sur la manière dont ils interagissent avec vos propriétés web, de déterminer l’efficacité de vos dépenses en marketing numérique et d’identifier les améliorations à apporter. [!DNL Analytics] gère des trillions de transactions web par an et le connecteur source [!DNL Analytics] vous permet d’exploiter facilement ces riches données comportementales et d’enrichir le [!DNL Real-Time Customer Profile] en quelques minutes.

![Graphique illustrant le parcours de données de différentes applications Adobe, y compris Adobe Analytics.](./images/analytics-data-experience-platform.png)

À un niveau élevé, [!DNL Analytics] collecte des données à partir de divers canaux numériques et de plusieurs centres de données dans le monde entier. Une fois les données collectées, les règles VISTA (Visitor Identification, Segmentation and Transformation Architecture) et les règles de traitement sont appliquées pour donner forme aux données entrantes. Une fois que les données brutes ont subi ce traitement léger, elles sont considérées comme prêtes à être utilisées par [!DNL Real-Time Customer Profile]. Parallèlement à ce qui précède, les mêmes données traitées sont microbatchées et ingérées dans des jeux de données Experience Platform pour être utilisées par [!DNL Query Service] et d’autres applications de découverte de données.

Pour plus d’informations sur les règles de traitement](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=fr) consultez la [ présentation des règles de traitement .

## Modèle de données d’expérience (XDM)

XDM est une spécification documentée publiquement qui fournit des structures et des définitions communes à une application pour communiquer avec des services sur Experience Platform.

Le respect des normes XDM permet d’intégrer uniformément les données, ce qui facilite la diffusion des données et la collecte des informations.

Pour en savoir plus sur XDM, consultez la [présentation du système XDM](../../../xdm/home.md).

## Comment les champs sont-ils mappés d’Adobe Analytics à XDM ?

>[!IMPORTANT]
>
>Les transformations de la préparation des données peuvent ajouter de la latence au flux de données global. La latence supplémentaire ajoutée varie en fonction de la complexité de la logique de transformation.

Lorsqu’une connexion source est établie pour importer des données [!DNL Analytics] dans Experience Platform à l’aide de l’interface utilisateur d’Experience Platform, les champs de données sont automatiquement mappés et ingérés dans [!DNL Real-Time Customer Profile] en quelques minutes. Pour plus d’informations sur la création d’une connexion source avec [!DNL Analytics] à l’aide de l’interface utilisateur d’Experience Platform, consultez le tutoriel [Connecteur source Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Pour plus d’informations sur le mappage des champs entre [!DNL Analytics] et Experience Platform, consultez le guide [Mappage des champs Adobe Analytics](./mapping/analytics.md) .

## Quelle est la latence attendue pour les données Analytics sur Experience Platform ?

La latence attendue pour les données Analytics sur Experience Platform est décrite dans le tableau ci-dessous. La latence varie en fonction de la configuration du client, des volumes de données et des applications clientes. Par exemple, si l’implémentation d’Analytics est configurée avec `A4T`, la latence du pipeline passera à 5-10 minutes.

| Données Analytics | Latence attendue |
| -------------- | ---------------- |
| Nouvelles données à [!DNL Real-Time Customer Profile] (A4T **non** activé) | &lt; 2 minutes |
| Nouvelles données à [!DNL Real-Time Customer Profile] (A4T **est** activé) | jusqu’à 30 minutes |
| Nouvelles données pour le lac de données | &lt; 2,25 heures |
| Nouvelles données dans Customer Journey Analytics sans [assemblage](https://experienceleague.adobe.com/docs/analytics-platform/using/stitching/overview.html?lang=en) | &lt; 3,75 heures |
| Nouvelles données dans Customer Journey Analytics avec l’assemblage | &lt; 7 heures |
| Renvoi de moins de 10 milliards d’événements | &lt; 4 semaines |

Pour plus d’informations sur les latences de Customer Journey Analytics, voir : [Mécanismes de sécurisation de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html?lang=en).

Le renvoi Analytics pour les sandbox de production est défini par défaut sur 13 mois. Pour les données Analytics dans les sandbox hors production, le renvoi est défini sur trois mois. La limite de 10 milliards d’événements mentionnée dans le tableau ci-dessus est strictement liée à la latence attendue.

Pour les sandbox de production, si vous disposez d’une licence pour le SKU supplémentaire qui vous autorise à importer plus de 13 mois de données de renvoi historiques, contactez Adobe pour demander le renvoi étendu.

Lorsque vous créez un flux de données source Analytics dans un sandbox de production, deux flux de données sont créés :

* Flux de données qui renvoie pendant 13 mois les données historiques de la suite de rapports dans le lac de données. Ce flux de données se termine lorsque le renvoi est terminé.
* Flux de données qui envoie des données actives au lac de données et à [!DNL Real-Time Customer Profile]. Ce flux de données s’exécute en continu.

>[!NOTE]
>
>Les données de renvoi Analytics ne sont pas ingérées dans [!DNL Profile] et ne sont donc pas prises en compte dans les profils de licence.

## Identifiants de Principal dans les données [!DNL Analytics]

Chaque accès du connecteur source [!DNL Analytics] contient un identifiant principal qui dépend de l’existence ou non d’un ECID ou d’un AAID. S’il existe un ECID, l’ECID est désigné comme identifiant principal. S’il existe un AAID, l’AAID est désigné comme principal.

Le tableau suivant fournit des informations supplémentaires sur les champs d’identité dans vos données [!DNL Analytics].

| Champ d’identité | Description |
| --- | --- |
| AAID | L’AAID est l’identifiant d’appareil principal dans Adobe Analytics. Il existe systématiquement dans chaque événement transmis par la source [!DNL Analytics]. L’AAID est parfois appelé l’*ID Analytics hérité* ou l’ID de cookie `s_vi`. Malgré cela, un AAID est créé même en l’absence du cookie `s_vi`. L’AAID est représenté par les colonnes `post_visid_high` et `post_visid_low` dans les [[!DNL Analytics] flux de données](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Sur un événement donné, le champ AAID contient une seule identité qui peut être l’un des différents types décrits dans l’[ordre des opérations pour les  [!DNL Analytics] IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Remarque** : au sein d’une suite de rapports complète, un AAID peut contenir plusieurs types d’événements. |
| ECID | L’ECID (Experience Cloud ID) est un champ d’identifiant d’appareil distinct, qui est renseigné dans Adobe Analytics lorsque [!DNL Analytics] est implémenté à l’aide du service d’identités d’Experience Cloud. L’ECID est parfois également appelé MCID (Marketing Cloud ID). Si un ECID existe sur un événement, l’AAID peut être basé sur l’ECID selon que le [délai de grâce](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) Analytics est configuré ou non. L’ECID est représenté par le `mcvisid` dans les flux de données Analytics. Pour plus d’informations sur l’ECID, consultez la [ présentation de l’ECID ](../../../identity-service/features/ecid.md). Pour plus d’informations sur le fonctionnement de l’ECID avec [!DNL Analytics], consultez le document sur les [demandes d’identification Analytics et Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html). |
| AACUSTOMID | L’AACUSTOMID est un champ d’identifiant distinct qui est renseigné dans Adobe Analytics en fonction de l’utilisation de la variable `s.VisitorID` dans l’implémentation [!DNL Analytics]. L’AACUSTOMID est représenté par la colonne `cust_visid` dans [[!DNL Analytics] flux de données](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Si l’AACUSTOMID est présent, l’AAID sera basé sur l’AACUSTOMID, car l’AACUSTOMID surpasse tous les autres identifiants comme défini par l’[ordre des opérations pour les  [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### Traitement des identités par la source de [!DNL Analytics]

La source [!DNL Analytics] transmet ces identités à Experience Platform sous forme XDM sous la forme suivante :

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Ces champs ne sont pas marqués comme identités. Au lieu de cela, les mêmes identités (si elles sont présentes dans l’événement) sont copiées dans le `identityMap` de XDM en tant que paires clé-valeur :

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

Lorsque l’identité ou les identités sont copiées dans `identityMap`, `endUserIDs._experience.mcid.namespace.code` est également défini sur le même événement :

* Si l’AAID est présent, `endUserIDs._experience.aaid.namespace.code` est défini sur « AAID ».
* Si l’ECID est présent, `endUserIDs._experience.mcid.namespace.code` est défini sur « ECID ».
* Si l’AACUSTOMID est présent, `endUserIDs._experience.aacustomid.namespace.code` est défini sur « AACUSTOMID ».

Dans le mappage d’identités, si l’ECID est présent, il est marqué comme l’identité principale de l’événement. Dans ce cas, l’AAID peut être basé sur l’ECID en raison de la [ période de grâce du service d’identités ](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). Dans le cas contraire, l’AAID est marqué comme l’identité principale de l’événement. L’AACUSTOMID n’est jamais marqué comme l’ID de Principal de l’événement. Cependant, en présence d’un AACUSTOMID, l’AAID est basé sur l’AACUSTOMID en raison de l’ordre des opérations d’Experience Cloud.

>[!NOTE]
>
>Vous pouvez utiliser la préparation de données pour filtrer les identités secondaires provenant d’Analytics, telles que l’AAID et l’AACUSTOMID. Si elles sont filtrées, ces identités ne seront pas ingérées dans le profil si elles sont disponibles dans les données Analytics entrantes. Les données non filtrées continueront à être chargées dans le lac de données.
