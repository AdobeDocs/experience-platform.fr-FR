---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Présentation de la gouvernance, de la confidentialité et de la sécurité
description: Adobe Experience Platform fournit plusieurs services et outils qui vous permettent de contrôler en toute confiance vos données d’expérience collectées afin de respecter vos pratiques commerciales, vos obligations légales et votre processus de développement.
feature: Data Governance,Privacy
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 21%

---

# Gouvernance, confidentialité et sécurité dans Adobe Experience Platform

Adobe Experience Platform vous permet d’ingérer, d’analyser, d’optimiser et d’agir sur vos données afin d’améliorer considérablement les expériences client. Ces données sont vastes, complexes et incroyablement précieuses. En fonction de la nature de vos opérations de données, des juridictions sous lesquelles votre entreprise opère et de vos politiques organisationnelles concernant l’utilisation des données, vous devez contrôler et surveiller attentivement la collecte et l’utilisation des données d’expérience client afin de protéger vos intérêts commerciaux.

Experience Platform fournit plusieurs services et outils qui vous permettent de contrôler en toute confiance vos données d’expérience collectées afin de respecter vos pratiques commerciales, vos obligations juridiques et vos processus de développement. Les sections ci-dessous présentent chacun de ces services, ainsi que des liens vers la documentation pour plus d’informations.

Les services peuvent être classés en trois domaines :

* [Gouvernance des données](#governance)
* [Confidentialité   ](#privacy)
* [Sécurité](#security)

## Gouvernance des données {#governance}

La gouvernance des données est un concept essentiel qui est étroitement lié à chaque capacité en Experience Platform. La gouvernance des données représente votre capacité à contrôler et à comprendre vos données tout au long de leur parcours via Platform. Cela implique de maintenir la qualité des données, le lignage des données, le catalogage des données, etc.

### Gouvernance des données d’Adobe Experience Platform {#data-governance}

En tant que service Platform, la gouvernance des données de Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Il joue un rôle clé dans Experience Platform à différents niveaux, notamment l’étiquetage de l’utilisation des données, les stratégies d’utilisation des données, l’application des stratégies et la traçabilité des données.

Pour plus d’informations, consultez la [vue d’ensemble de la gouvernance des données](../../data-governance/home.md).

### Catalogue et jeux de données {#catalog}

Le service de catalogue est le système d’enregistrement de l’emplacement et de la traçabilité des données dans Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, le catalogue renferme les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

Le catalogue classe les données ingérées dans des jeux de données, chaque jeu de données contenant des métadonnées qui peuvent être utilisées pour étiqueter et catégoriser les données qu’il contient.

Pour plus d’informations sur le service, consultez la [présentation du service de catalogue](../../catalog/home.md) . Pour savoir comment gérer des jeux de données dans Experience Platform, consultez la [présentation des jeux de données](../../catalog/datasets/overview.md).

## Confidentialité    {#privacy}

La confidentialité est un problème critique pour votre entreprise, vos législateurs et vos clients. Comme les données personnelles collectées auprès de vos clients sont au coeur de presque tous les workflows Experience Platform, Platform fournit des services pour soutenir ces initiatives.

### Adobe Experience Platform Privacy Service  {#privacy-service}

Les réglementations légales relatives à la confidentialité, telles que le Règlement général sur la protection des données (RGPD) de l’Union européenne et la Loi sur la protection de la vie privée des consommateurs de Californie (CCPA), donnent aux citoyens de leur juridiction le droit d’accéder aux données personnelles que vous collectez et de les stocker et de les supprimer.

Adobe Experience Platform Privacy Service fournit une API RESTful et une interface utilisateur pour faciliter la gestion de ces requêtes. Avec Privacy Service, vous pouvez envoyer des demandes d’accès ou de suppression de données clients privées ou personnelles des applications Adobe Experience Cloud, ce qui facilite la conformité automatisée aux réglementations de confidentialité légales et organisationnelles.

Pour plus d’informations, consultez la [présentation du Privacy Service](../../privacy-service/home.md) .

### Traitement du consentement {#consent}

De nombreuses réglementations juridiques relatives à la confidentialité ont introduit des exigences de consentement actif et spécifique en ce qui concerne la collecte de données, la personnalisation et d’autres cas d’utilisation marketing. Pour répondre à ces exigences, Experience Platform vous permet de capturer les informations de consentement dans des profils client individuels et d’utiliser ces préférences comme facteur déterminant dans la manière dont les données de chaque client sont utilisées dans les workflows Platform en aval.

Pour savoir comment traiter les données de consentement et de préférence client à l’aide de la norme Adobe, consultez la présentation sur le [traitement du consentement dans Experience Platform](./consent/adobe/overview.md).

Pour plus d’informations sur le traitement des données de consentement des clients conformément au Transparency and Consent Framework (TCF) 2.0 de l’IAB, consultez la présentation de la [prise en charge du TCF 2.0 de l’IAB dans Platform](./consent/iab/overview.md).

## Sécurité {#security}

L’intégrité et la sécurité de vos données sont indispensables à votre entreprise et ce risque nécessite des capacités de sécurité de pointe. Pour relever ce défi, Platform fournit plusieurs outils pour vous aider à protéger vos opérations de données.

### Chiffrement des données

Toutes les données de Platform sont chiffrées en transit et au repos. Pour plus d’informations, consultez le document sur le [cryptage des données dans Platform](./encryption.md) .

### Contrôle d’accès {#access-control}

Experience Platform utilise Adobe Admin Console pour fournir un contrôle d’accès en fonction du rôle à diverses fonctionnalités de Platform. Cette fonctionnalité exploite les profils de produit dans l’Admin Console, liant les utilisateurs et utilisatrices à des autorisations et des sandbox.

Pour plus d’informations, consultez la [présentation du contrôle d’accès](../../access-control/home.md).

### Sandbox {#sandboxes}

Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

Pour répondre aux besoins de flexibilité en matière de développement, Experience Platform fournit des environnements de test qui divisent une instance de plateforme unique en environnements virtuels distincts pour vous aider à développer vos applications d’expérience numérique en fonction de votre propre cycle de vie de développement.

Pour plus d’informations, consultez la [Présentation des sandbox](../../sandboxes/home.md).

## Étapes suivantes

Ce document fournit un aperçu des différents services et outils de Platform impliqués dans la gouvernance, la confidentialité et la sécurité des données. Pour en savoir plus sur ces fonctionnalités, consultez la documentation associée à ce guide.
