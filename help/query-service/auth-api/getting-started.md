---
keywords: Experience Platform ; Query Service ; contrôle d’accès IP ; autorisation ; API ; prise en main
title: Guide de l’API d’autorisation de Query Service
description: Découvrez comment commencer à utiliser les restrictions d’autorisation et de plage d’adresses IP pour un accès sécurisé aux données dans Adobe Experience Platform Query Service.
role: Developer
exl-id: d93ce774-c8b2-4f15-a4d9-117d9aa5d9e7
source-git-commit: bf696c8836407a2fea82e9078201cb1f5004bcf8
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 6%

---

# Guide de l’API Query Service Authorization

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté le module complémentaire Data Distiller. Pour en savoir plus, contactez votre représentant ou représentante Adobe.

L’API Query Service Authorization permet aux entreprises de mieux contrôler l’accès aux données via l’interface SQL de Adobe Experience Platform. Vous pouvez utiliser cette API pour définir des restrictions d’IP, limiter l’accès aux données à des réseaux spécifiés et améliorer la surveillance de la sécurité.

Ce guide explique comment configurer les informations d’identification d’autorisation et les autorisations requises pour effectuer des appels vers l’API Query Service Authorization.

## Commencer {#getting-started}

Les sections suivantes fournissent des informations sur la préparation des valeurs d’autorisation requises et l’envoi de vos premières requêtes à l’API Query Service Authorization.

### Autorisations nécessaires {#required-permissions}

Pour activer les restrictions d’accès aux données sécurisées dans Query Service, vous avez besoin de l’autorisation **[!UICONTROL Gérer la Liste autorisée]**. Cette autorisation permet aux entreprises de définir des plages d’adresses IP spécifiques (au format IPv4 ou IPv6) autorisées à accéder aux données de Platform via l’interface SQL. L’accès est géré au niveau de l’environnement de test, où les utilisateurs peuvent configurer une liste d’adresses IP approuvées ou de blocs CIDR qui limitent l’accès uniquement aux réseaux autorisés.

>[!NOTE]
>
>Les administrateurs système peuvent configurer des autorisations utilisateur à partir de l’Adobe [Admin Console](https://adminconsole.adobe.com/). Pour plus d’informations, consultez le [guide d’utilisation d’Admin Console](https://helpx.adobe.com/fr/enterprise/using/admin-console.html).

Les fonctionnalités suivantes sont disponibles avec l’autorisation **[!UICONTROL Gérer la Liste autorisée]** :

- **Définir des plages d’adresses IP autorisées** : seules les adresses IP ou les blocs CIDR de ces plages définies peuvent accéder aux données de Platform à l’aide de SQL via Query Service.
- **Exiger des vérifications de plage d’adresses IP** : les connexions à partir d’adresses IP en dehors des plages autorisées sont refusées.
- **Fonctionnalités d’audit et d’alerte** : toutes les tentatives d’accès, y compris les connexions refusées, sont consignées en tant qu’événements de contrôle. Ces événements sont disponibles dans les [journaux d’audit Adobe Experience Platform](../../landing/governance-privacy-security/audit-logs/overview.md), ce qui permet de surveiller les violations de sécurité potentielles.

### Collecter des valeurs pour les en-têtes requis {#gather-values-for-required-headers}

Pour lancer des appels à l’API Query Service Authorization, vous devez suivre le [tutoriel sur l’authentification de l’API Platform](../../landing/api-authentication.md), qui fournit des valeurs pour les en-têtes requis dans les appels d’API. Incluez les en-têtes suivants dans chaque requête :

- **Autorisation** : `Bearer {ACCESS_TOKEN}`
- **x-api-key** : `{API_KEY}`
- **x-gw-ims-org-id** : `{ORG_ID}`
- **x-sandbox-name** : `{SANDBOX_NAME}`

>[!NOTE]
>
> Pour plus d’informations sur les environnements de test, consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) nécessitent également cet en-tête :

- **Content-Type** : `application/json`

### Étapes suivantes

Lorsque les autorisations requises et les valeurs d’en-tête sont collectées, vous êtes prêt à commencer à configurer les restrictions IP pour Query Service. Passez à la documentation du point de terminaison pour obtenir des exemples détaillés des opérations CRUD, notamment :

- Format de l’API et exemples de paires requête/réponse.
- En-têtes, payloads et codes de réponse pour chaque opération.

Chaque exemple d’appel API montre comment formater des requêtes et interpréter des réponses, ce qui vous permet d’appliquer un accès sécurisé à vos données dans Query Service.

Pour obtenir des instructions spécifiques sur la configuration et la validation des restrictions IP, reportez-vous à la [documentation du point d’entrée d’accès IP](./ip-access.md) et à la [ documentation du point d’entrée de validation IP](./validate.md).
