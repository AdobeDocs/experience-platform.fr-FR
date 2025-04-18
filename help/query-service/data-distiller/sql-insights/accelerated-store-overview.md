---
title: Présentation accélérée de la boutique
description: Découvrez comment utiliser la boutique accélérée dans Adobe Experience Platform pour obtenir des informations rapides et basées sur SQL à l’aide de données agrégées. Cette page décrit son utilisation prévue, les restrictions relatives aux données d’identité et de BI, ainsi que les bonnes pratiques pour assurer la conformité aux politiques de gouvernance des données d’Adobe.
source-git-commit: 5e8dccf91e8c83b4734b363539cfb911b5c2ae29
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# Présentation accélérée de la boutique

La boutique accélérée dans Adobe Experience Platform est une couche de stockage optimisée pour les performances, disponible via le SKU Data Distiller. Il est conçu pour contenir des jeux de données préagrégés, permettant des informations rapides et basées sur SQL ainsi qu’un rendu de tableau de bord.

Ce document explique comment utiliser correctement la boutique accélérée, pourquoi les jeux de données agrégés sont exemptés des processus d’hygiène des données standard et souligne que les données d’identité ne doivent pas être stockées. Pour rester en conformité avec les directives d’Adobe, vous devez respecter les politiques de gouvernance des données et les restrictions d’utilisation décrites dans ce document.

## Fonctionnalités principales {#key-capabilities}

La boutique accélérée est conçue spécifiquement pour offrir performances et efficacité. Il permet des workflows de requête et de création de rapports rationalisés en se concentrant sur les données agrégées. La liste ci-dessous met en évidence ses principales fonctionnalités :

- Fournir des tableaux de bord et des widgets haute performance à l’aide de requêtes SQL
- Stocker des jeux de données préagrégés conçus pour les informations récurrentes
- Prise en charge de la création de modèles de données personnalisés pour les cas d’utilisation de rapports

## Utilisation prévue {#intended-use}

La boutique accélérée est conçue **uniquement** pour stocker des données agrégées qui permettent une visualisation et un tableau de bord rationalisés. Son architecture n’est pas conçue pour prendre en charge des charges de travail complexes, telles que le traitement de la veille économique ou l’entreposage de données.

>[!IMPORTANT]
>
>La boutique accélérée ne remplace pas le lac de données ni une solution de stockage polyvalente.

## Restrictions d’utilisation {#usage-restrictions}

Pour assurer la conformité au modèle de gouvernance des données et aux conditions de licence d’Adobe, les restrictions suivantes s’appliquent :

- **Ne stockez pas de données d’événement brutes**
- **Ne pas stocker les données d’identité**
- **Ne stockez pas d’informations d’identification personnelle (PII)** telles que des adresses e-mail, des données de santé ou des identifiants de client
- **N’utilisez pas la boutique accélérée pour répliquer l’ensemble de votre lac de données**

Seules les données agrégées non identifiables peuvent être stockées dans la boutique accélérée. Les jeux de données agrégés ne peuvent pas faire l’objet d’une ingénierie à rebours pour révéler les données sources originales, ce qui les exempte des processus centralisés d’hygiène des données d’Experience Platform.

## Gouvernance et conformité {#governance-and-compliance}

L’utilisation de la boutique accélérée en dehors de son objectif prévu peut exposer votre entreprise au risque de violer le contrat de licence et les limites de gouvernance des données d’Adobe. Si des incidents de gouvernance des données se produisent en raison de modèles d’utilisation non pris en charge, votre entreprise en assume l’entière responsabilité.

Adobe n’est pas responsable des conséquences découlant d’une utilisation abusive de cette fonctionnalité.

Pour en savoir plus sur la gestion responsable des données dans Experience Platform, voir [Gouvernance, confidentialité et sécurité dans Experience Platform](../../../landing/governance-privacy-security/overview.md). Cette page décrit les services et outils qui vous aident à contrôler vos données d’expérience conformément aux politiques commerciales, aux exigences légales et aux normes de développement. Pour obtenir des liens vers des conseils plus détaillés sur l’étiquetage d’utilisation et l’application des politiques, consultez la [présentation de la gouvernance des données](../../../data-governance/home.md).

## Bonnes pratiques {#best-practices}

Pour garantir une utilisation efficace et conforme de la boutique accélérée, suivez les bonnes pratiques recommandées suivantes :

- Utilisez des jeux de données dérivés pour créer des tableaux préagrégés spécifiquement adaptés aux besoins de votre tableau de bord
- Évitez d’utiliser la boutique accélérée comme emplacement d’évaluation ou de sauvegarde pour les jeux de données bruts
- Examinez régulièrement votre utilisation pour vous assurer que celle-ci est conforme aux mécanismes de sécurisation recommandés par Adobe

## Étapes suivantes

En lisant ce document, vous avez appris ce qu’est la boutique accélérée, son utilisation prévue pour les données agrégées dans les scénarios de création de rapports et les règles de gouvernance à suivre pour garantir une utilisation conforme. Pour mieux comprendre et appliquer efficacement ces directives, explorez les ressources suivantes :

- [Présentation de SQL Insights](./overview.md) : découvrez comment SQL Insights permet la création de rapports optimisée pour les performances à l’aide de jeux de données agrégés.
- [Envoyer des requêtes accélérées](./send-accelerated-queries.md) : découvrez comment exécuter des requêtes sur la boutique accélérée pour alimenter les tableaux de bord et les widgets.
- [Gouvernance et hygiène des données](../../data-governance/overview.md) : passez en revue les politiques d’hygiène des données et les directives de gouvernance d’Adobe pour assurer leur utilisation conforme.
