---
keywords: Experience Platform;service de requête;service de requête;requête
title: Exemple de cas d’utilisation pour Adobe Experience Platform Query Service
description: Exemple de bout en bout montrant la versatilité et les avantages de Adobe Experience Platform Query Service.
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: 79966442f5333363216da17342092a71335a14f0
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 3%

---

# Exemple de cas pratique pour Adobe Experience Platform [!DNL Query Service]

Ce document et la présentation vidéo qui l’accompagne fournissent un workflow de haut niveau de bout en bout qui montre comment Adobe Experience Platform [!DNL Query Service] tire parti des informations commerciales stratégiques de votre entreprise. En prenant l’exemple d’un cas pratique d’abandon de navigation, ce guide illustre les concepts clés suivants :

* L’importance essentielle du traitement des données pour maximiser le potentiel de Adobe Experience Platform.
* Méthodes pour créer la requête en fonction de votre architecture de données existante.
* Assurez-vous de la qualité des données en fonction de vos besoins et des méthodes permettant d’atténuer tout manque.
* Processus de planification de l’exécution d’une requête à une fréquence définie en vue de son utilisation en aval dans la segmentation et les destinations pour la personnalisation.
* Facilité pour les marketeurs d’inclure des attributs dérivés dans leurs audiences grâce à la puissance de [!DNL Query Service].

## Objectifs {#objectives}

Cette démonstration de workflow repose sur plusieurs services Adobe Experience Platform. Si vous souhaitez poursuivre, il est recommandé de bien comprendre les fonctionnalités et services suivants :

* Le [Principes de base de la composition des schémas du modèle de données d’expérience (XDM)](../../xdm/schema/composition.md)
* Comment [création de jeux de données et ingestion de données](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=fr)
* Comment [ingestion de données à l’aide du connecteur source Adobe Analytics](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=fr)
* [Segmentation](../../segmentation/home.md)
* [Destinations](../../destinations/home.md)

L’exemple d’abandon de navigation se concentre sur l’utilisation d’Adobe [!DNL Analytics] pour créer une audience exploitable particulière. L’audience est affinée afin d’inclure tous les clients qui ont consulté le site Web au cours des quatre derniers jours sans effectuer d’achat. Chaque profil de l’audience est ensuite ciblé avec le SKU le plus cher qui a résulté du modèle de comportement du client.

La requête elle-même est très prescriptive et inclut uniquement des données qui répondent aux critères du cas d’utilisation pour la définition de segment. Cela améliore les performances en réduisant au minimum la quantité de [!DNL Analytics] données en cours de traitement. Il commande également les données par prix du plus élevé au plus faible et choisit le SKU le plus cher que l’utilisateur parcourait.

La requête utilisée dans la présentation est présentée ci-dessous :

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
    customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(c._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset c
WHERE A._experience.analytics.customDimension.evars.evar1 = B.personKey.sourceID
AND productListItems[0].SKU = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

## [!DNL Query Service] exemple d’abandon de navigation à l’aide d’adobe analytics {#video-example}

La présentation vidéo présentée ci-dessous présente un cas pratique global et concret de vos données Experience Platform centrées sur [!DNL Query Service] et les intégrations Adobe analytics.

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Avantages de [!DNL Query Service] {#benefits}

Les fonctionnalités proposées par [!DNL Query Service] sert de nombreux objectifs. Vous pouvez l’utiliser pour tenir compte d’une logique complexe de segmentation, pour calculer divers attributs personnalisés à utiliser en aval ou pour simplifier considérablement la création de vos audiences.

[!DNL Query Service] vous permet d’inclure des contraintes dans vos requêtes afin de simplifier votre processus de création d’audiences. Cela améliore la qualité des données en assurant les bonnes conditions de qualification des données pour vos audiences. Le maintien de la qualité de votre requête permet d’obtenir une audience précise et facilite la fiabilité des données. Vous pouvez également sauvegarder votre audience en créant des schémas et des tableaux personnalisés basés sur des attributs dérivés de votre requête. Un tableau personnalisé peut être activé pour Profile et vous pouvez utiliser ces points de données pour la segmentation et la personnalisation. Cette fonctionnalité aide les marketeurs qui souhaitent créer une audience de personnes claire.

En outre, en incluant dans votre requête la logique qui satisfait toutes les conditions récurrentes ou statiques, [!DNL Query Service] extrait le fardeau de la segmentation élaborée.

Adobe Experience Platform fournit un référentiel de données et les outils nécessaires pour activer vos données de manière efficace et fiable. En conservant les données dans Platform, il vous permet d’obtenir des attributs lors de l’exécution d’autres processus et élimine la nécessité d’exporter des données vers des outils tiers pour la manipulation et le traitement. Ces frais généraux de traitement peuvent avoir une incidence considérable sur la chronologie d’un projet lorsqu’il s’agit de centaines d’attributs ou de campagnes. Les marketeurs disposent ainsi d’un emplacement unique pour accéder à leurs données et créer des campagnes, ainsi que d’un moyen très dynamique de segmenter et de personnaliser leurs messages.

## Étapes suivantes

En lisant ce document, vous devriez maintenant comprendre comment [!DNL Query Service] impacte non seulement la qualité de vos données et la facilité de la segmentation, mais également leur importance dans votre architecture de données pour l’ensemble du workflow de bout en bout. Pour des exemples SQL plus applicables qui utilisent Adobe Analytics avec [!DNL Query Service], reportez-vous à la section [Cas d’utilisation des variables de marchandisage Adobe Analytics](./merchandising-variables.md).

Autres documents présentant les avantages de [!DNL Query Service] Pour consulter les informations stratégiques de votre entreprise, reportez-vous à la section [cas d’utilisation du filtrage de robots](./bot-filtering.md) par exemple.

Vous pouvez également utiliser ces documents pour mieux comprendre [!DNL Query Service] fonctionnalités :

* [Conseils pour l’exécution des requêtes](../best-practices/writing-queries.md)
* [Conseils pour l’organisation des ressources de données](../best-practices/organize-data-assets.md).


