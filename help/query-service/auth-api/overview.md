---
title: Guide de l’API d’autorisation de Data Distiller
description: Découvrez comment utiliser l’API Data Distiller Authorization pour appliquer des restrictions IP basées sur le réseau pour des connexions sécurisées via SQL. Utilisez cette API pour améliorer le contrôle d’accès aux données pour vos données Adobe Experience Platform.
role: Developer
exl-id: bcc5ea0e-cb6d-4c7b-bf9f-a0336f76c4c8
source-git-commit: ac29d10d3774a736d1e54255508ba244ff72f278
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---

# Guide de l’API d’autorisation de Data Distiller

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté le module complémentaire Data Distiller. Pour en savoir plus, contactez votre représentant ou représentante Adobe.

Utilisez l’API Data Distiller Authorization pour appliquer des restrictions basées sur les adresses IP. L’application de ces mesures garantit que seuls les réseaux et les machines clientes approuvés peuvent accéder aux données via SQL dans Adobe Experience Platform. Ces contrôles vous aident à respecter des normes de sécurité strictes tout en fournissant une surveillance et des alertes d’accès en temps réel.

Avec cette API, vous pouvez configurer, appliquer et surveiller les restrictions d’IP pour accéder aux données via l’interface SQL. Ce document présente de manière générale les principales fonctionnalités de l’API, les fonctions de point de terminaison et les futures fonctionnalités.

## Fonctionnalités clés

Les fonctionnalités suivantes vous permettent de définir des restrictions d’accès basées sur des adresses IP, de surveiller les tentatives d’accès et de personnaliser les paramètres de sécurité réseau de Query Service :

- **Définir des contrôles d’accès aux données basés sur le réseau** : spécifiez les plages d’adresses IP autorisées pour l’accès à Query Service. Cette restriction s’applique spécifiquement aux connexions de base de données SQL, y compris celles effectuées par le biais d’outils Business Intelligence (BI), de clients de base de données ou d’interfaces de programmation telles que JDBC.
- **Activer la surveillance et les alertes complètes** : toutes les tentatives d’accès, y compris les connexions refusées, sont consignées et envoyées aux [ journaux d’audit Adobe Experience Platform](../../landing/governance-privacy-security/audit-logs/overview.md) pour le suivi en temps réel. Utilisez cette fonctionnalité pour surveiller les schémas d’accès et détecter les failles de sécurité potentielles.
- **Configurer des restrictions d’IP flexibles** : spécifiez les adresses IP autorisées dans les formats de bloc d’IP et CIDR individuels. Ces paramètres s’appliquent par environnement de test, ce qui vous permet d’adapter les restrictions réseau à vos besoins de sécurité spécifiques.

## Fonctionnalités d’audit et de surveillance

Pour prendre en charge les pratiques d’accès aux données sécurisées, Query Service consigne toutes les adresses IP clientes qui accèdent à AEP ou tentent d’y accéder. Les événements d’audit, y compris les connexions refusées, sont envoyés aux journaux d’audit de Platform. Cela permet :

- **Surveillance en temps réel** : effectuez le suivi des modèles d’accès basés sur l’adresse IP pour garantir la conformité.
- **Alerte sur accès non autorisé** : identifiez les tentatives d’accès à partir d’adresses IP non autorisées et répondez-y.

Pour plus d’informations sur la journalisation de l’audit, consultez la [documentation du service d’audit](https://experienceleague.adobe.com/docs/experience-platform/audit/audit-overview.html).

## Étapes suivantes

Commencez avec l’API Data Distiller Authorization en consultant le [guide de prise en main](./getting-started.md) pour connaître les étapes de configuration essentielles, y compris les en-têtes requis et les conventions d’appel API. Ensuite, explorez les guides spécifiques aux points de terminaison sur [Accès IP](./ip-access.md) et [Validation IP](./validate.md) pour configurer et gérer l’accès aux données sécurisé.
