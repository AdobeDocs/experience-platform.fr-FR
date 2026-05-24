---
keywords: Experience Platform;query service;Query service;requête
title: Exemple de cas d’utilisation de Adobe Experience Platform Query Service
description: Exemple complet pour démontrer la polyvalence et les avantages de Adobe Experience Platform Query Service.
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
TQID: https://experienceleague.adobe.com/rwleF1-pMq0uCxuX1d3ut3uKDk0esgek9FOpOpXCOdM
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
  - id: ed0d8d0e-04b9-4326-be72-a0fbca265377
subfeature_v2:
  - id: b784da9a-7978-4766-bf1f-5ab2b23d894a
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b4dd41a7-ccf8-4e9d-918e-acaab534a307
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 731
ht-degree: 2%

---

# Exemple de cas d’utilisation de Adobe Experience Platform [!DNL Query Service]

Ce document et la présentation vidéo qui l’accompagne fournissent un workflow de bout en bout détaillé démontrant comment Adobe Experience Platform [!DNL Query Service] bénéficie aux informations commerciales stratégiques de votre entreprise. À l’aide d’un cas d’utilisation d’abandon de navigation, ce guide illustre les concepts clés suivants :

* Importance du traitement des données pour optimiser le potentiel de Adobe Experience Platform.
* Méthodes de création de la requête en fonction de votre architecture de données existante.
* Garantissez une qualité de données répondant à vos besoins, ainsi que des méthodes permettant de pallier les insuffisances.
* Processus permettant de planifier l’exécution d’une requête à une fréquence définie pour une utilisation en aval dans la segmentation et les destinations pour la personnalisation.
* La facilité pour les professionnels du marketing d’inclure des jeux de données dérivés dans leurs audiences grâce à la puissance de [!DNL Query Service].

## Objectifs {#objectives}

Cette démonstration de workflow repose sur plusieurs services Adobe Experience Platform. Si vous souhaitez suivre cette procédure, il est recommandé de bien comprendre les fonctionnalités et services suivants :

* Les [principes de base de la composition de schémas du modèle de données d’expérience (XDM)](../../xdm/schema/composition.md)
* Comment [&#x200B; créer des jeux de données et ingérer des données &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
* Comment [ingérer des données à l’aide du connecteur source Adobe Analytics](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=fr)
* [Segmentation](../../segmentation/home.md)
* [Destinations](../../destinations/home.md)

L’exemple d’abandon de la navigation est centré sur l’utilisation des données Adobe [!DNL Analytics] pour créer une audience exploitable particulière. L’audience est affinée afin d’inclure chaque client ou cliente qui a parcouru le site web au cours des quatre derniers jours, mais n’a pas effectué d’achat. Chaque profil de l’audience est ensuite ciblé avec le SKU le plus coûteux résultant du modèle de comportement du client ou de la cliente.

La requête elle-même est très normative et inclut uniquement des données qui répondent aux critères du cas d’utilisation pour la définition de segment. Cela améliore les performances en réduisant au minimum la quantité de données [!DNL Analytics] en cours de traitement. Il classe également les données par prix, du plus élevé au plus bas, et choisit le SKU le plus cher que l’utilisateur était en train de parcourir.

La requête utilisée dans la présentation est visible ci-dessous :

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

## [!DNL Query Service] exemple d’abandon de la navigation avec adobe analytics {#video-example}

La présentation vidéo présentée ci-dessous fournit un cas d’utilisation holistique et réel de vos données Experience Platform, axé sur les intégrations [!DNL Query Service] et Adobe Analytics.

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Avantages de la [!DNL Query Service] {#benefits}

Les fonctionnalités fournies par [!DNL Query Service] servent à de nombreux objectifs. Vous pouvez l’utiliser pour répondre à une logique complexe de segmentation, pour calculer divers attributs personnalisés à utiliser en aval ou pour simplifier considérablement la création de vos audiences.

[!DNL Query Service] permet d’inclure des contraintes dans vos requêtes afin de simplifier le processus de création de votre audience. Cela améliore la qualité des données en s’assurant que les bonnes données sont qualifiées pour vos audiences. Le maintien de la qualité des résultats de votre requête dans une audience précise et contribue à la fiabilité des données. Vous pouvez également enregistrer votre audience en créant des schémas et des tables personnalisées en fonction des attributs dérivés de votre requête. Un tableau personnalisé peut être activé pour Profil et vous pouvez utiliser ces points de données pour la segmentation et la personnalisation. Cette fonctionnalité est utile pour les marketeurs qui souhaitent créer une audience claire de personnes.

En outre, en incluant dans votre requête une logique qui satisfait à toutes les conditions récurrentes ou statiques, [!DNL Query Service] extrait la charge d’une segmentation élaborée.

Adobe Experience Platform fournit un référentiel de données et les outils nécessaires pour activer vos données de manière efficace et fiable. En conservant les données au sein d’Experience Platform, vous pouvez obtenir des attributs lors de l’exécution d’autres processus et n’avez plus besoin d’exporter des données vers des outils tiers pour les manipuler et les traiter. Ces surcharges de traitement peuvent avoir un impact important sur la chronologie d’un projet lorsque vous traitez des centaines d’attributs ou de campagnes. Les marketeurs disposent ainsi d’un emplacement unique pour accéder à leurs données et créer des campagnes, ainsi que d’un moyen très dynamique de segmenter et de personnaliser leurs messages.

## Étapes suivantes

En lisant ce document, vous devriez maintenant comprendre comment [!DNL Query Service] affecte non seulement la qualité de vos données et la facilité de segmentation, mais aussi son importance dans votre architecture de données pour l’ensemble du workflow de bout en bout. Pour obtenir des exemples SQL plus applicables qui utilisent Adobe Analytics avec [!DNL Query Service], consultez le cas d’utilisation des variables de marchandisage d’Adobe Analytics [&#128279;](./merchandising-variables.md).

Le [cas d’utilisation du filtrage des robots](./bot-filtering.md) est un autre document qui illustre les avantages de l’[!DNL Query Service] aux informations commerciales stratégiques de votre organisation.

Vous pouvez également utiliser ces documents pour mieux comprendre [!DNL Query Service] fonctionnalités :

* [Conseils pour l’exécution des requêtes](../best-practices/writing-queries.md)
* [Conseils pour l’organisation des ressources de données](../best-practices/organize-data-assets.md).


