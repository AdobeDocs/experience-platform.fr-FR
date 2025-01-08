---
title: Clés gérées par le client dans Adobe Experience Platform
description: Découvrez comment configurer vos propres clés de chiffrement pour les données stockées dans Adobe Experience Platform.
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: f2737355ca0652f434bd5f86acc65139f767e56f
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 26%

---

# Clés gérées par le client dans Adobe Experience Platform

Les données stockées sur Adobe Experience Platform sont chiffrées au repos à l’aide de clés au niveau du système. Si vous utilisez une application reposant sur Platform, vous pouvez choisir d’utiliser vos propres clés de chiffrement pour mieux contrôler la sécurité de vos données.

>[!AVAILABILITY]
>
>Si votre mise en œuvre d’Experience Platform s’exécute sur Amazon Web Services (AWS), vous avez la possibilité d’utiliser le service de gestion des clés (KMS) pour le chiffrement des données de Platform. Un Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la présentation multi-cloud de [Experience Platform ](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud). Pour en savoir plus sur la création et la gestion des clés de chiffrement dans AWS KMS, consultez le [guide sur le chiffrement des données AWS KMS](../key-management-service/overview.md).

>[!NOTE]
>
>Les données de profil client stockées dans l’[!DNL Azure Data Lake] de Platform et la banque de profils [!DNL Azure Cosmos DB] sont chiffrées exclusivement à l’aide de la fonction CMK, une fois activée. La révocation des clés dans vos entrepôts de données principaux peut prendre de **quelques minutes à 24 heures** et peut prendre plus de temps, **jusqu’à 7 jours** pour les entrepôts de données transitoires ou secondaires. Pour plus d’informations, consultez la section [implications de la révocation de l’accès à la clé](#revoke-access).

Ce document présente de manière générale le processus d’activation de la fonctionnalité de clés gérées par le client (CMK) dans Platform ainsi que les informations préalables requises pour réaliser ces étapes.

>[!NOTE]
>
>Pour les clients Customer Journey Analytics, suivez les instructions de la documentation du Customer Journey Analytics [](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=fr).

## Conditions préalables

Pour afficher et consulter la section [!UICONTROL Chiffrement] dans Adobe Experience Platform, vous devez avoir créé un rôle et attribué l’autorisation [!UICONTROL Gérer les clés gérées par le client] à ce rôle. Tout utilisateur disposant de l’autorisation [!UICONTROL Gérer les clés gérées par le client] peut activer la fonction CMK pour son organisation.

Pour plus d’informations sur l’attribution de rôles et d’autorisations dans Experience Platform, reportez-vous à la documentation sur la [configuration des autorisations](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Pour activer la fonction CMK, votre coffre de clés [!DNL Azure] doit être configuré avec les paramètres suivants :

* [Activer la protection contre le vidage](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Activer la suppression réversible](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configuration de l’accès à l’aide  [!DNL Azure]  contrôle d’accès en fonction du rôle](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

Veuillez lire la documentation associée pour mieux comprendre le processus.

## Résumé du processus {#process-summary}

La fonction CMK est incluse dans les offres Adobe Healthcare Shield et Privacy and Security Shield. Une fois que votre entreprise a acheté une licence pour l’une de ces offres, vous pouvez lancer un processus unique de configuration de la fonctionnalité.

>[!WARNING]
>
>Après avoir configuré la fonction CMK, vous ne pouvez pas revenir aux clés gérées par le système. Il vous incombe de gérer vos clés en toute sécurité et de fournir l’accès à votre coffre de clés, à votre clé et à votre application CMK dans [!DNL Azure] pour éviter de perdre l’accès à vos données.

Le processus se présente comme suit :

1. [Configurez un coffre  [!DNL Azure]  Key Vault](./azure-key-vault-config.md) en fonction des politiques de votre entreprise, puis [générez une clé de chiffrement](./azure-key-vault-config.md#generate-a-key) qui sera à la fin partagée avec Adobe.
1. Configurez l’application CMK avec votre client [!DNL Azure] par le biais des [appels d’API](./api-set-up.md#register-app) ou de l’[interface utilisateur](./ui-set-up.md#register-app).
1. Envoyez votre ID de clé de chiffrement à l’Adobe et lancez le processus d’activation de la fonctionnalité [dans l’interface utilisateur](./ui-set-up.md#send-to-adobe) ou avec un [appel API](./api-set-up.md#send-to-adobe).
1. Vérifiez le statut de la configuration pour vous assurer que la fonction CMK a été activée [dans l’interface utilisateur](./ui-set-up.md#check-status) ou avec un [appel API](./api-set-up.md#check-status).

Une fois le processus de configuration terminé, toutes les données intégrées à Platform dans l’ensemble des sandbox seront chiffrées à l’aide de votre configuration de clé [!DNL Azure]. Pour vous servir de la fonction CMK, vous utiliserez la fonctionnalité [!DNL Microsoft Azure] pouvant faire partie de leur [programme de préversion publique](https://azure.microsoft.com/fr-fr/support/legal/preview-supplemental-terms/).

## Implications de la révocation de l’accès aux clés {#revoke-access}

La révocation ou la désactivation de l’accès au coffre de clés, à la clé ou à l’application CMK peut entraîner des perturbations importantes, notamment des modifications avec rupture des opérations de votre plateforme. Une fois ces clés désactivées, les données de Platform peuvent devenir inaccessibles et toutes les opérations en aval qui reposent sur ces données cesseront de fonctionner. Il est essentiel de bien comprendre les impacts en aval avant d’apporter des modifications à vos configurations clés.

Si vous décidez de révoquer l’accès de Platform à vos données, vous pouvez le faire en supprimant le rôle d’utilisateur associé à l’application du coffre de clés dans [!DNL Azure].

### Chronologies de propagation {#propagation-timelines}

Une fois l’accès à la clé révoqué de votre coffre de clés [!DNL Azure], les modifications se propageront comme suit :

| **Type de magasin** | **Description** | **Planning** |
|---|---|---|
| Magasins de données de Principal | Ces magasins comprennent les magasins Azure Data Lake et Azure Cosmos DB Profile. Une fois l’accès à la clé révoqué, les données deviennent inaccessibles. | De **minutes à 24 heures**. |
| Magasins de données transitoires/mis en cache | Inclut les entrepôts de données utilisés pour les performances et les fonctionnalités des applications principales. L’impact de la révocation des clés est retardé. | **Jusqu’à 7 jours**. |

Par exemple, le tableau de bord du profil continuera à afficher les données de son cache pendant sept jours au maximum avant l’expiration des données et sera actualisé. De même, la réactivation de l’accès à l’application prend le même temps pour restaurer la disponibilité des données dans ces magasins.

>[!NOTE]
>
>Il existe deux exceptions spécifiques aux cas d’utilisation à l’expiration de sept jours du jeu de données sur les données non principales (mises en cache/transitoires). Pour plus d’informations sur ces fonctionnalités, consultez leurs documentations respectives.<ul><li>[Raccourcisseur d’URL Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=fr#message-preset-sms)</li><li>[Projections Edge](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Étapes suivantes

Pour lancer le processus, commencez par [configurer un [!DNL Azure] coffre Key Vault](./azure-key-vault-config.md) et [générer une clé de chiffrement](./azure-key-vault-config.md#generate-a-key) à partager avec Adobe.
