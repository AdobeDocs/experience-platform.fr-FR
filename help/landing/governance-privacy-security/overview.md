---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Présentation de la gouvernance, de la confidentialité et de la sécurité
topic-legacy: overview
description: Adobe Experience Platform fournit plusieurs services et outils qui vous permettent de contrôler en toute confiance les données d’expérience collectées afin de respecter vos pratiques commerciales, vos obligations légales et votre processus de développement.
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 17%

---

# Gouvernance, confidentialité et sécurité à Adobe Experience Platform

Adobe Experience Platform vous permet d’assimiler, d’analyser, d’optimiser et d’agir sur vos données afin d’améliorer considérablement les expériences client. Ces données sont vastes, complexes et incroyablement précieuses. En fonction de la nature de vos opérations de données, des juridictions sous lesquelles votre entreprise exerce ses activités et de vos stratégies organisationnelles en matière d’utilisation des données, vous devez contrôler et surveiller attentivement la collecte et l’utilisation des données d’expérience client afin de protéger vos intérêts commerciaux.

Experience Platform fournit plusieurs services et outils qui vous permettent de contrôler en toute confiance les données d’expérience collectées afin de respecter vos pratiques commerciales, vos obligations légales et vos processus de développement. Les sections ci-dessous présentent chacun de ces services, ainsi que des liens vers la documentation pour de plus amples informations.

Les services peuvent être classés en trois domaines :

* [Gouvernance des données](#governance)
* [Confidentialité](#privacy)
* [Sécurité](#security)

## Gouvernance des données {#governance}

La gouvernance des données est un concept essentiel qui est étroitement lié à toutes les capacités des Experience Platform. La gouvernance des données représente votre capacité à contrôler et à comprendre vos données tout au long de leur parcours via la plate-forme. Cela implique de maintenir la qualité des données, le lignage des données, le catalogage des données, etc.

### Gouvernance des données d’Adobe Experience Platform {#data-governance}

En tant que service de plateforme, Adobe Experience Platform Data Governance vous permet de gérer les données client et de vous assurer de la conformité aux réglementations, restrictions et règles applicables à l’utilisation des données. Il joue un rôle clé au sein de l’Experience Platform à divers niveaux, notamment en ce qui concerne l’étiquetage de l’utilisation des données, les stratégies d’utilisation des données, l’application des règles et la lignée des données.

Pour plus d&#39;informations, consultez la [Présentation de la gouvernance des données](../../data-governance/home.md).

### Catalogue et jeux de données {#catalog}

Le service de catalogue constitue le système d’enregistrement de l’emplacement et de la liaison des données dans Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, le catalogue renferme les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

Le catalogue classe les données imbriquées dans des jeux de données, chaque jeu de données contenant des métadonnées pouvant être utilisées pour classer et classer les données qu’il contient.

Pour plus d’informations sur le service, voir [Présentation du service de catalogue](../../catalog/home.md). Pour savoir comment gérer des jeux de données dans l&#39;Experience Platform, consultez l&#39;[aperçu des jeux de données](../../catalog/datasets/overview.md).

## Confidentialité {#privacy}

La confidentialité est un problème crucial pour votre entreprise, vos législateurs et vos clients. Comme les données personnelles collectées auprès de vos clients sont au coeur de presque tous les workflows Experience Platform, Platform fournit des services pour soutenir ces initiatives.

### Adobe Experience Platform Privacy Service {#privacy-service}

Les réglementations légales en matière de confidentialité, telles que le Règlement général sur la protection des données de l&#39;Union européenne (RGPD) et la Loi sur la protection des renseignements personnels des consommateurs (LPCPC) de Californie, accordent aux citoyens de leur territoire le droit d&#39;accéder aux données personnelles que vous collectez et stockez auprès d&#39;eux et de les supprimer.

Adobe Experience Platform Privacy Service fournit une API RESTful et une interface utilisateur pour aider à gérer ces requêtes. Avec Privacy Service, vous pouvez envoyer des demandes d&#39;accès ou de suppression de données client privées ou personnelles des applications Adobe Experience Cloud, ce qui vous permet de respecter automatiquement les réglementations légales et de confidentialité de l&#39;entreprise.

Pour plus d’informations, consultez la [Présentation de Privacy Service.](../../privacy-service/home.md)

### Traitement du consentement {#consent}

De nombreuses réglementations légales en matière de confidentialité ont introduit des exigences de consentement principal et spécifique en matière de collecte de données, de personnalisation et d&#39;autres cas d&#39;utilisation marketing. Afin de répondre à ces exigences, l&#39;Experience Platform vous permet de capturer les informations de consentement dans des profils de client individuels et d&#39;utiliser ces préférences comme facteur déterminant dans la manière dont les données de chaque client sont utilisées dans les workflows de plateforme en aval.

Pour savoir comment traiter les données de consentement et de préférence des clients à l&#39;aide de la norme Adobe, consultez la présentation du traitement du consentement [dans Experience Platform](./consent/adobe/overview.md).

Pour savoir comment traiter les données de consentement des clients conformément au Cadre de transparence et de consentement (TCF) 2.0 de l’IAB, voir l’aperçu sur [la prise en charge de l’IAB TCF 2.0 dans Platform](./consent/iab/overview.md).

## Sécurité {#security}

L&#39;intégrité et la sécurité de vos données sont indispensables à votre entreprise et ce risque nécessite des capacités de sécurité de pointe. Pour relever ce défi, Platform fournit plusieurs outils pour vous aider à protéger vos opérations de données.

### Contrôle d’accès {#access-control}

Experience Platform utilise le Adobe Admin Console pour fournir un contrôle d&#39;accès basé sur les rôles à diverses fonctionnalités de la plate-forme. Cette fonctionnalité exploite les profils de produit dans Admin Console, liant les utilisateurs à des autorisations et des environnements de test.

Pour plus d’informations, consultez la [présentation du contrôle d’accès](../../access-control/home.md).

### Environnements de test {#sandboxes}

Experience Platform est conçu pour enrichir les applications d’expérience numérique à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience numérique en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

Afin de répondre au besoin de flexibilité de développement, Experience Platform fournit des sandbox qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour vous aider à développer vos applications d&#39;expérience numérique en fonction de votre propre cycle de vie de développement.

Pour plus d’informations, consultez la [présentation des environnements de test](../../sandboxes/home.md).

## Étapes suivantes

Ce document présente un aperçu des divers services et outils de la plate-forme impliqués dans la gouvernance des données, la confidentialité et la sécurité. Pour en savoir plus sur ces fonctionnalités, consultez la documentation à laquelle ce guide est associé.
