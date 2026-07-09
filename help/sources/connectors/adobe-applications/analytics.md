---
title: Connecteur source Adobe Analytics pour les données de suite de rapports
description: Ce document présente un aperçu du connecteur source Adobe Analytics pour Adobe Experience Platform.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
TQID: https://experienceleague.adobe.com/tn8xFuLHCbCI09BI92znF-tHumF9luCTeY8OCVDZcgQ
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
subfeature_v2:
  - id: b572b7ff-a413-4173-b2b4-d7d3874f1b9b
  - id: b784da9a-7978-4766-bf1f-5ab2b23d894a
  - id: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
source-git-commit: 2f54212d8592c5ebc45b847c5f8269ddddfeb622
workflow-type: tm+mt
source-wordcount: 1735
ht-degree: 1%

---

# Connecteur source Adobe Analytics pour les données de suite de rapports

Adobe Experience Platform vous permet d’ingérer des données Adobe Analytics par le biais du connecteur source Analytics. Le connecteur diffuse les données de la suite de rapports dans un jeu de données Platform en temps réel, en les convertissant au format XDM.

## Fonctionnement du connecteur source Analytics

Vous continuez à utiliser votre implémentation Adobe Analytics existante, telle qu’AppMeasurement ou l’extension de balise Adobe Analytics, pour collecter des données dans vos suites de rapports. Le connecteur source ne modifie pas la manière dont vous collectez ou générez des rapports sur ces données. Une fois que vos données ont atteint les serveurs de collecte de données Analytics, le connecteur en capture une copie.

![Graphique illustrant le parcours de données de différentes applications Adobe, y compris Adobe Analytics.](./images/analytics-data-experience-platform.png)

Cette copie est une forme partiellement traitée de chaque accès, connue sous le nom de *valeurs moyennes*. Analytics produit des valeurs moyennes après le prétraitement (comme les règles de traitement), mais avant le traitement au niveau des visites et des visiteurs. Par conséquent, ils n’incluent pas le contexte de post-traitement, tel que le numéro de visite. L’accès d’origine continue à travers le pipeline pour être écrit dans votre suite de rapports comme d’habitude.

Le connecteur diffuse ces valeurs moyennes en temps réel dans un jeu de données dans Experience Platform. Depuis le lac de données, les données sont disponibles pour Query Service et d’autres applications de découverte de données, et elles peuvent également enrichir le profil client en temps réel.

Pour plus d’informations sur la manière dont Analytics collecte et traite les données, y compris l’étape de valeur moyenne, voir [&#x200B; Ordre de traitement des données dans Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/technotes/processing-order).

## Mappage des champs Adobe Analytics à XDM

Lorsque vous créez une connexion source dans l’interface utilisateur d’Experience Platform, les champs Analytics sont automatiquement mappés à [XDM](/help/xdm/home.md) et ingérés dans un jeu de données Platform. Pour plus d’informations, consultez le tutoriel [Connecteur source Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Pour plus d’informations sur le mappage des champs entre Analytics et Experience Platform, consultez le guide [Mappage des champs Adobe Analytics](./mapping/analytics.md) .

>[!IMPORTANT]
>
>Les transformations de la préparation des données peuvent ajouter de la latence au flux de données global. La quantité de latence supplémentaire varie en fonction de la complexité de la logique de transformation.

## Identifiants de Principal dans les données Analytics

Chaque accès du connecteur source Analytics contient un identifiant principal qui dépend de l’existence ou non d’un ECID ou d’un AAID. S’il existe un ECID, l’ECID est désigné comme identifiant principal. S’il existe un AAID, l’AAID est désigné comme principal.

Le tableau suivant fournit des informations supplémentaires sur les champs d’identité de vos données Analytics.

| Champ d’identité | Description |
| --- | --- |
| AAID | L’AAID est l’identifiant d’appareil principal dans Adobe Analytics. Il existe systématiquement dans chaque événement transmis par la source Analytics. L’AAID est parfois appelé l’*ID Analytics hérité* ou l’ID de cookie `s_vi`. Malgré cela, un AAID est créé même en l’absence du cookie `s_vi`. L’AAID est représenté par les colonnes `post_visid_high` et `post_visid_low` dans les [flux de données Analytics](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Sur un événement donné, le champ AAID contient une identité unique qui peut être l’un des différents types décrits dans l’[ordre des opérations pour les ID Analytics](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Remarque** : au sein d’une suite de rapports complète, un AAID peut contenir plusieurs types d’événements. |
| ECID | L’ECID (ID Experience Cloud) est un champ d’identifiant d’appareil distinct, qui est renseigné dans Adobe Analytics lorsqu’Analytics est implémenté à l’aide du service d’identification des visiteurs. L’ECID est parfois également appelé MCID (Marketing Cloud ID). Si un ECID existe sur un événement, l’AAID peut être basé sur l’ECID selon que le [délai de grâce](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) Analytics est configuré ou non. L’ECID est représenté par le `mcvisid` dans les flux de données Analytics. Pour plus d’informations sur l’ECID, consultez la [&#x200B; présentation de l’ECID &#x200B;](/help/identity-service/features/ecid.md). Pour plus d’informations sur le fonctionnement d’ECID avec Analytics, consultez le document sur les [requêtes d’Analytics et d’Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html). |
| AACUSTOMID | L’AACUSTOMID est un champ d’identifiant distinct qui est renseigné dans Adobe Analytics en fonction de l’utilisation de la variable [`visitorID`](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/config-vars/visitorid) dans l’implémentation d’Analytics. Si l’AACUSTOMID est présent, l’AAID est basé sur l’AACUSTOMID, car l’AACUSTOMID surpasse tous les autres identifiants comme défini par l’[ordre des opérations pour les Analytics ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### Traitement des identités par la source Analytics

La source Analytics transmet ces identités à Experience Platform sous forme XDM sous la forme suivante :

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

Dans le mappage d’identités, si l’ECID est présent, il est marqué comme l’identité principale de l’événement. Dans ce cas, l’AAID peut être basé sur l’ECID en raison de la [&#x200B; période de grâce du service d’identification des visiteurs &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). Dans le cas contraire, l’AAID est marqué comme l’identité principale de l’événement. L’AACUSTOMID n’est jamais marqué comme l’ID de Principal de l’événement. Cependant, en présence d’un AACUSTOMID, l’AAID est basé sur l’AACUSTOMID en raison de l’ordre des opérations dans Experience Cloud.

## Précision de l’horodatage des accès et ordre des événements

Le connecteur reçoit les données Analytics sous forme de valeurs moyennes, qui comportent des dates et heures d’accès de deuxième niveau. Comme Analytics enregistre le temps avec une précision de deuxième niveau uniquement et ne suit pas la durée inférieure à la seconde, l’ordre des accès collectés au cours de la même seconde n’est pas déterministe. Par conséquent, l’ordre des événements de même seconde ingérés par le connecteur peut différer de celui affiché dans les rapports Analytics.

Customer Journey Analytics résout les horodatages sur la [milliseconde](https://experienceleague.adobe.com/en/docs/analytics-platform/using/connections/combined-dataset), mais les données provenant d’Analytics ne renseignent que les secondes entières. L’horodatage seul ne peut donc pas établir l’ordre relatif des événements qui partagent la même seconde. Cela est plus visible lorsque plusieurs accès sont collectés au cours de la même seconde (par exemple, une page vue et un accès Adobe Target (A4T)).

Pour plus d’informations sur la précision de l’horodatage Analytics, consultez les documentations Adobe Analytics [horodatage](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/timestamp) variable et [Profondeur d’accès](https://experienceleague.adobe.com/en/docs/analytics/components/dimensions/hit-depth). Pour les champs d’horodatage que le connecteur mappe à XDM (`hit_time_gmt` et `post_cust_hit_time_gmt`), consultez le guide [Mappage de champs Adobe Analytics](./mapping/analytics.md) .

Les options disponibles pour la précision de l’horodatage sont les suivantes :

* **Acceptez les différences mineures de commande de même seconde.** Pour la plupart des rapports, l’effet est limité aux événements qui partagent la même seconde et n’affecte pas les mesures agrégées. Il s’agit de l’approche recommandée, y compris pour les scénarios mixtes de pages vues et d’Adobe Target (A4T).
* **Pour les cas d’utilisation sensibles à la commande, préférez le SDK Web.** L’envoi de données via le [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/collection/home) directement vers Experience Platform et Customer Journey Analytics préserve la précision de l’horodatage de moins de la seconde (milliseconde) et évite le retraitement par Analytics. Cette approche est recommandée lorsque l’ordre des événements est important.

## Latence des données et renvoi

La latence attendue des données Analytics sur Experience Platform est décrite dans le tableau ci-dessous. La latence varie en fonction de la configuration du client, des volumes de données et des applications clientes. Par exemple, si l’implémentation d’Analytics est configurée avec A4T, la latence du pipeline augmente de 5 à 10 minutes.

| Données Analytics | Latence attendue |
| --- | --- |
| Nouvelles données du profil client en temps réel (A4T **non** activé) | &lt; 2 minutes |
| Nouvelles données du profil client en temps réel (A4T **est** activé) | jusqu’à 30 minutes |
| Nouvelles données dans le lac de données | &lt; 2,25 heures |
| Nouvelles données dans Customer Journey Analytics sans [assemblage](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/stitching/overview) | &lt; 3,75 heures |
| Nouvelles données dans Customer Journey Analytics avec l’assemblage | &lt; 7 heures |
| Renvoi de moins de 10 milliards d’événements | &lt; 4 semaines |

Pour plus d’informations sur les latences de Customer Journey Analytics, voir : [Mécanismes de sécurisation de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html?lang=en).

Le renvoi Analytics pour les sandbox de production est défini par défaut sur 13 mois. Pour les données Analytics dans les sandbox hors production, le renvoi est défini sur trois mois. La limite de 10 milliards d’événements mentionnée dans le tableau ci-dessus est strictement liée à la latence attendue.

Lorsque vous créez un flux de données source Analytics dans un sandbox de production, deux flux de données sont créés :

* Flux de données qui renvoie pendant 13 mois les données historiques de la suite de rapports dans le lac de données. Ce flux de données se termine lorsque le renvoi est terminé.
* Flux de données qui envoie des données actives au lac de données et au profil client en temps réel. Ce flux de données s’exécute en continu.

## Bonnes pratiques

Suivez ces bonnes pratiques pour éviter de dépasser vos droits de licence et de surcharger vos mesures de stockage total et de richesse des données :

* Configurez la durée de vie (TTL) de rétention des jeux de données d’événements d’expérience dès le début pour optimiser la gestion du cycle de vie des données et l’efficacité du stockage. Pour plus d’informations, consultez le guide sur la [gestion de la conservation des jeux de données d’événements d’expérience dans le lac de données à l’aide de TTL](/help/catalog/datasets/experience-event-dataset-retention-ttl-guide.md).
* Lorsque vous créez un flux de données source Analytics, commencez par configurer le connecteur afin d’ingérer les données uniquement dans le lac de données. Après avoir confirmé que le flux de données fonctionne, vous pouvez activer l’ingestion de profil pour le jeu de données. Cette approche fonctionne mieux lorsque les filtres de ligne et de colonne réduisent efficacement le volume de données. Pour en savoir plus, consultez la documentation [connexion d’Adobe Analytics à Experience Platform](../../tutorials/ui/create/adobe-applications/analytics.md).

## Questions fréquentes

+++Les données de renvoi Analytics sont-elles comptabilisées dans le nombre de profils sous licence ?

Non. Les données de renvoi Analytics ne sont pas ingérées dans le profil et ne sont donc pas prises en compte dans vos droits de licence.

+++

+++Puis-je importer plus de 13 mois de données historiques ?

Le renvoi Analytics pour les sandbox de production est défini par défaut sur 13 mois et les sandbox hors production sont limités à trois mois. Pour les sandbox de production, si vous disposez d’une licence pour le SKU supplémentaire qui vous autorise à importer plus de 13 mois de données de renvoi historiques, contactez Adobe pour demander le renvoi étendu.

+++

+++Comment empêcher l’ingestion d’identités secondaires (AAID et AACUSTOMID) dans le profil client en temps réel ?

Vous pouvez utiliser la préparation de données pour filtrer les identités secondaires provenant d’Analytics, telles que l’AAID et l’AACUSTOMID. Si elles sont filtrées, ces identités ne sont pas ingérées dans le profil même si elles sont disponibles dans les données Analytics entrantes.

+++
