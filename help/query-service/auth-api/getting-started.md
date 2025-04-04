---
keywords: Experience Platform; Query Service; contrôle d’accès IP; autorisation; API; prise en main
title: Guide de l’API Data Distiller Authorization
description: Découvrez comment commencer à utiliser les restrictions d’autorisation et de plage d’adresses IP pour un accès sécurisé aux données dans Adobe Experience Platform Query Service.
role: Developer
exl-id: d93ce774-c8b2-4f15-a4d9-117d9aa5d9e7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 5%

---

# Prise en main de l’API d’autorisation de Data Distiller

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté le module complémentaire Distiller de données. Pour plus d’informations, contactez votre représentant ou représentante Adobe.

L’API Data Distiller Authorization offre aux entreprises un contrôle plus étroit sur l’accès aux données par l’intermédiaire de l’interface SQL de Adobe Experience Platform. Vous pouvez utiliser cette API pour définir des restrictions d’adresses IP, limiter l’accès aux données à des réseaux spécifiés et améliorer la surveillance de la sécurité.

Ce guide explique comment configurer les informations d’identification et les autorisations requises pour effectuer des appels à l’API d’autorisation de Distiller de données.

## Commencer {#getting-started}

Les sections suivantes fournissent des informations sur la préparation des valeurs d’autorisation requises et l’envoi de vos premières requêtes à l’API Data Distiller Authorization.

### Autorisations nécessaires {#required-permissions}

Pour activer les restrictions d’accès aux données sécurisées dans Query Service, vous devez disposer de l’autorisation **[!UICONTROL Gérer la Liste autorisée]**. Cette autorisation permet aux organisations de définir des plages d’adresses IP spécifiques (au format IPv4 ou IPv6) qui sont autorisées à accéder aux données dans Experience Platform via l’interface SQL. L’accès est géré au niveau du sandbox, où les utilisateurs peuvent configurer une liste d’adresses IP approuvées ou de blocs CIDR qui limitent l’accès aux réseaux autorisés uniquement.

>[!NOTE]
>
>Les administrateurs système peuvent configurer des autorisations d’utilisateur à partir de l’[Admin Console](https://adminconsole.adobe.com/) Adobe. Pour plus d’informations, consultez le [guide d’utilisation d’Admin Console](https://helpx.adobe.com/fr/enterprise/using/admin-console.html).

Les fonctionnalités suivantes sont disponibles avec l’autorisation **[!UICONTROL Gérer la Liste autorisée]** :

- **Définir des plages d’adresses IP autorisées** : seules les adresses IP ou les blocs CIDR provenant de ces plages définies peuvent accéder aux données dans Experience Platform à l’aide de SQL via Query Service.
- **Appliquer les vérifications de plage d’adresses IP** : les connexions provenant d’adresses IP en dehors des plages autorisées sont refusées.
- **Fonctionnalités d’audit et d’alerte** : toutes les tentatives d’accès, y compris les connexions refusées, sont consignées comme événements d’audit. Ces événements sont disponibles dans les [journaux d’audit Adobe Experience Platform](../../landing/governance-privacy-security/audit-logs/overview.md), ce qui permet de surveiller les violations de sécurité potentielles.

### Collecter des valeurs pour les en-têtes requis {#gather-values-for-required-headers}

Pour lancer des appels à l’API d’autorisation de Distiller de données, vous devez suivre le [tutoriel sur l’authentification de l’API Experience Platform](../../landing/api-authentication.md), qui fournit des valeurs pour les en-têtes requis dans les appels API. Insérez les en-têtes suivants dans chaque requête :

- **Autorisation** : `Bearer {ACCESS_TOKEN}`
- **x-api-key** : `{API_KEY}`
- **x-gw-ims-org-id** : `{ORG_ID}`
- **x-sandbox-name** : `{SANDBOX_NAME}`

>[!NOTE]
>
> Pour plus d’informations sur les sandbox, consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant une payload (POST, PUT, PATCH) nécessitent également cet en-tête :

- **Content-Type** : `application/json`

### Étapes suivantes

Une fois les autorisations requises et les valeurs d’en-tête collectées, vous êtes prêt à commencer à configurer les restrictions d’adresses IP pour Query Service. Consultez la documentation sur les points d’entrée pour obtenir des exemples détaillés d’opérations CRUD, notamment :

- Format d’API et exemples de paires requête/réponse.
- En-têtes, payloads et codes de réponse pour chaque opération.

Chaque exemple d’appel API montre comment formater des requêtes et interpréter des réponses, ce qui vous aide à appliquer un accès sécurisé à vos données dans Query Service.

Pour obtenir des instructions spécifiques sur la configuration et la validation des restrictions IP, reportez-vous à la documentation sur les points d’entrée [IP Access](./ip-access.md) et à la documentation sur les points d’entrée [IP Validation](./validate.md).

Reportez-vous à la [documentation de référence OpenAPI d’autorisation de Distiller de données](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/) pour afficher un format normalisé et lisible par machine afin de faciliter l’intégration, les tests et l’exploration.
