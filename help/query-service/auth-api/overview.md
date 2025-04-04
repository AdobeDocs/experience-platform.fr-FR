---
title: Guide de l’API Data Distiller Authorization
description: Découvrez comment utiliser l’API d’autorisation de Distiller de données pour appliquer des restrictions IP réseau pour des connexions sécurisées via SQL. Utilisez cette API pour améliorer le contrôle d’accès aux données pour vos données Adobe Experience Platform.
role: Developer
exl-id: bcc5ea0e-cb6d-4c7b-bf9f-a0336f76c4c8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---

# Guide de l’API Data Distiller Authorization

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté le module complémentaire Distiller de données. Pour plus d’informations, contactez votre représentant ou représentante Adobe.

Utilisez l’API Data Distiller Authorization pour appliquer des restrictions basées sur des adresses IP. L’application de ces mesures permet de s’assurer que seuls les réseaux et les ordinateurs clients approuvés peuvent accéder aux données via SQL dans Adobe Experience Platform. Ces contrôles vous aident à respecter des normes de sécurité strictes tout en fournissant une surveillance et des alertes d&#39;accès en temps réel.

Avec cette API, vous pouvez configurer, appliquer et surveiller les restrictions IP pour l’accès aux données via l’interface SQL. Ce document présente de manière générale les principales fonctionnalités, les fonctions de point d’entrée et les futures fonctionnalités de l’API.

## Fonctionnalités clés

Les fonctionnalités suivantes vous permettent de définir des restrictions d’accès basées sur IP, de surveiller les tentatives d’accès et de personnaliser les paramètres de sécurité réseau pour Query Service :

- **Définir des contrôles d’accès aux données basés sur le réseau** : spécifiez les plages d’adresses IP autorisées pour l’accès à Query Service. Cette restriction s’applique spécifiquement aux connexions à la base de données SQL, y compris celles effectuées via les outils Business Intelligence (BI), les clients de base de données ou les interfaces de programmation telles que JDBC.
- **Activer la surveillance et les alertes complètes** : toutes les tentatives d’accès, y compris les connexions refusées, sont consignées et envoyées aux [journaux d’audit Adobe Experience Platform](../../landing/governance-privacy-security/audit-logs/overview.md) pour le suivi en temps réel. Utilisez cette fonctionnalité pour surveiller les modèles d’accès et détecter les violations de sécurité potentielles.
- **Configurer des restrictions IP flexibles** : spécifiez les adresses IP autorisées dans des formats de blocs CIDR et IP individuels. Ces paramètres s’appliquent par sandbox, ce qui vous permet d’adapter les restrictions réseau à vos besoins en matière de sécurité.

## Fonctionnalités d’audit et de surveillance

Pour prendre en charge les pratiques d’accès aux données sécurisé, Query Service consigne toutes les adresses IP client qui accèdent ou tentent d’accéder à Experience Platform. Les événements d’audit, y compris les connexions refusées, sont envoyés aux journaux d’audit Experience Platform. Cela permet d’effectuer les opérations suivantes :

- **Surveillance en temps réel** : suivez les modèles d’accès basés sur les adresses IP pour garantir la conformité.
- **Alerte en cas d’accès non autorisé** : identifier les tentatives d’accès provenant d’adresses IP non autorisées et y répondre.

Pour plus d’informations, consultez la [présentation des journaux d’audit](../../landing/governance-privacy-security/audit-logs/overview.md).

## Étapes suivantes

Commencez avec l’API d’autorisation de Distiller de données en consultant le [guide de prise en main](./getting-started.md) pour connaître les étapes de configuration essentielles, y compris les en-têtes requis et les conventions d’appel API. Consultez ensuite les guides spécifiques aux points d’entrée sur [l’accès IP](./ip-access.md) et [la validation IP](./validate.md) pour configurer et gérer l’accès aux données sécurisé.

Reportez-vous à la [documentation de référence OpenAPI d’autorisation de Distiller de données](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/) pour afficher un format normalisé et lisible par machine afin de faciliter l’intégration, les tests et l’exploration.

Pour plus d’informations sur les différents paramètres de réponse pour chaque jeu de données renvoyé, consultez la [documentation destinée aux développeurs et développeuses de l’API Datasets](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets).
