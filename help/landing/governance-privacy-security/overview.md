---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Présentation de la gouvernance, de la confidentialité et de la sécurité
description: Adobe Experience Platform fournit plusieurs services et outils qui vous permettent de contrôler en toute confiance vos données d’expérience collectées afin de respecter vos pratiques commerciales, vos obligations légales et votre processus de développement.
feature: Data Governance,Privacy
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 22%

---

# Gouvernance, confidentialité et sécurité dans Adobe Experience Platform

Adobe Experience Platform vous permet d’ingérer, d’analyser, d’optimiser et d’agir sur vos données pour améliorer considérablement les expériences client. Ces données sont vastes, complexes et d&#39;une valeur inestimable. Selon la nature de vos opérations de données, les juridictions légales sous lesquelles votre entreprise opère et vos politiques organisationnelles concernant l’utilisation des données, vous devez contrôler et surveiller attentivement la collecte et l’utilisation des données d’expérience client afin de protéger vos intérêts commerciaux.

Experience Platform fournit plusieurs services et outils qui vous permettent de contrôler en toute confiance vos données d’expérience collectées afin de respecter vos pratiques commerciales, vos obligations légales et vos processus de développement. Les sections ci-dessous présentent chacun de ces services, ainsi que des liens vers la documentation pour plus d’informations.

Les services peuvent être classés en trois domaines :

* [Gouvernance des données](#governance)
* [Confidentialité   &#x200B;](#privacy)
* [Sécurité](#security)

## Gouvernance des données {#governance}

La gouvernance des données est un concept essentiel qui est étroitement lié à toutes les fonctionnalités d’Experience Platform. La gouvernance des données représente votre capacité à contrôler et à comprendre vos données dans l’ensemble de son parcours via Experience Platform. Cela implique de maintenir la qualité des données, le lignage des données, le catalogage des données, etc.

### Gouvernance des données d’Adobe Experience Platform {#data-governance}

En tant que service Experience Platform, la gouvernance des données de Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Elle joue un rôle essentiel dans Experience Platform à différents niveaux, notamment dans l’étiquetage d’utilisation des données, les politiques d’utilisation des données, l’application des politiques et la traçabilité des données.

Pour plus d’informations, consultez la [vue d’ensemble de la gouvernance des données](../../data-governance/home.md).

### Catalogue et jeux de données {#catalog}

Le service de catalogue constitue le système d’enregistrement de l’emplacement et de la traçabilité des données dans Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, le catalogue renferme les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

Le catalogue organise les données ingérées en jeux de données, chaque jeu de données contenant des métadonnées qui peuvent être utilisées pour étiqueter et catégoriser les données qu’il contient.

Pour plus d’informations sur le service, consultez la présentation du service de catalogue [Catalog](../../catalog/home.md). Pour savoir comment gérer les jeux de données dans Experience Platform, consultez la [&#x200B; présentation des jeux de données &#x200B;](../../catalog/datasets/overview.md).

## Confidentialité    {#privacy}

La protection des renseignements personnels est un enjeu crucial pour votre entreprise, les législateurs et vos clients. Les données personnelles collectées auprès de vos clients étant au cœur de presque tous les workflows d’Experience Platform, Experience Platform fournit des services pour prendre en charge ces initiatives.

### Adobe Experience Platform Privacy Service  {#privacy-service}

Les réglementations légales relatives à la confidentialité, telles que le Règlement général sur la protection des données (RGPD) de l’Union européenne et le California Consumer Privacy Act (CCPA) accordent aux citoyens de leur juridiction le droit d’accéder aux données personnelles que vous collectez et stockez auprès d’eux, et de les supprimer.

Adobe Experience Platform Privacy Service fournit une API RESTful et une interface utilisateur pour faciliter la gestion de ces requêtes. Avec Privacy Service, vous pouvez envoyer des demandes d’accès ou de suppression de données clients privées ou personnelles depuis les applications Adobe Experience Cloud, ce qui facilite l’automatisation de la conformité aux réglementations légales et organisationnelles en matière de confidentialité.

Voir la présentation de [Privacy Service](../../privacy-service/home.md) pour plus d’informations.

### Traitement du consentement {#consent}

De nombreuses réglementations légales relatives à la confidentialité ont introduit des exigences de consentement actif et spécifique lorsqu’il s’agit de collecte de données, de personnalisation et d’autres cas d’utilisation marketing. Pour répondre à ces exigences, Experience Platform vous permet de capturer des informations de consentement dans des profils clients individuels et d’utiliser ces préférences comme facteur déterminant dans la manière dont les données de chaque client sont utilisées dans les workflows Experience Platform en aval.

Pour savoir comment traiter les données de consentement et de préférence des clients à l’aide de la norme Adobe, consultez la présentation sur le [traitement du consentement dans Experience Platform](./consent/adobe/overview.md).

Pour plus d’informations sur le traitement des données de consentement des clients conformément au Transparency and Consent Framework (TCF) 2.0 de l’IAB, consultez la présentation sur la prise en charge du [IAB TCF 2.0 dans Experience Platform](./consent/iab/overview.md).

## Sécurité {#security}

L&#39;intégrité et la sécurité de vos données sont indispensables à votre entreprise, et ce risque nécessite des fonctionnalités de sécurité de pointe. Pour relever ce défi, Experience Platform fournit plusieurs outils permettant de protéger vos opérations de données.

### Chiffrement des données

Toutes les données Experience Platform sont chiffrées en transit et au repos. Pour plus d’informations, consultez le document sur le [chiffrement des données dans Experience Platform](./encryption.md).

### Contrôle d’accès {#access-control}

Experience Platform utilise Adobe Admin Console pour fournir un contrôle d’accès en fonction du rôle à diverses fonctionnalités d’Experience Platform. Cette fonctionnalité exploite les profils de produit dans l’Admin Console, liant les utilisateurs et utilisatrices à des autorisations et des sandbox.

Pour plus d’informations, consultez la [présentation du contrôle d’accès](../../access-control/home.md).

### Sandbox {#sandboxes}

Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

Pour répondre aux besoins de flexibilité de développement, Experience Platform fournit des sandbox qui divisent une instance Experience Platform unique en environnements virtuels distincts pour vous aider à faire évoluer vos applications d’expérience digitale en fonction de votre propre cycle de vie de développement.

Pour plus d’informations, consultez la [Présentation des sandbox](../../sandboxes/home.md).

## Étapes suivantes

Ce document présente un aperçu des différents services et outils d’Experience Platform impliqués dans la gouvernance des données, la confidentialité et la sécurité. Pour en savoir plus sur ces fonctionnalités, reportez-vous à la documentation référencée tout au long de ce guide.
