---
title: Clés gérées par le client dans Adobe Experience Platform
description: Découvrez comment configurer vos propres clés de chiffrement pour les données stockées dans Adobe Experience Platform.
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 29%

---

# Clés gérées par le client dans Adobe Experience Platform

Les données stockées sur Adobe Experience Platform sont chiffrées au repos à l’aide de clés au niveau du système. Si vous utilisez une application reposant sur Platform, vous pouvez choisir d’utiliser vos propres clés de chiffrement pour mieux contrôler la sécurité de vos données.

>[!NOTE]
>
>Les données de profil client stockées dans la banque de profils [!DNL Azure Data Lake] et [!DNL Azure Cosmos DB] de Platform sont chiffrées exclusivement à l’aide du CMK, une fois activées. La révocation des clés dans vos entrepôts de données principaux peut prendre entre **quelques minutes et 24 heures** et peut prendre plus de temps, **jusqu’à 7 jours** pour les entrepôts de données transitoires ou secondaires. Pour plus d’informations, reportez-vous aux [ implications de la révocation de l’accès à la clé ](#revoke-access).

Ce document fournit un aperçu général du processus d’activation de la fonctionnalité de clés gérées par le client (CMK) dans Platform, ainsi que les informations préalables requises pour effectuer ces étapes.

>[!NOTE]
>
>Pour les clients Customer Journey Analytics, suivez les instructions de la [documentation du Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=fr).

## Conditions préalables

Pour afficher et consulter la section [!UICONTROL Chiffrement] dans Adobe Experience Platform, vous devez avoir créé un rôle et lui avoir attribué l’autorisation [!UICONTROL Gérer la clé gérée par le client]. Tout utilisateur disposant de l’autorisation [!UICONTROL Gérer la clé gérée par le client] peut activer le CMK pour son organisation.

Pour plus d&#39;informations sur l&#39;attribution des rôles et des autorisations en Experience Platform, consultez la [documentation sur la configuration des autorisations](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Pour activer le CMK, votre Key Vault [!DNL Azure] doit être configuré avec les paramètres suivants :

* [Activer la protection contre le vidage](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Activer soft-delete](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configurer l’accès à l’aide du  [!DNL Azure] contrôle d’accès basé sur les rôles](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

Veuillez lire la documentation liée pour mieux comprendre le processus.

## Résumé du processus {#process-summary}

La fonction CMK est incluse dans les offres Adobe Healthcare Shield et Privacy and Security Shield. Une fois que votre entreprise a acheté une licence pour l’une de ces offres, vous pouvez lancer un processus unique de configuration de la fonctionnalité.

>[!WARNING]
>
>Après avoir configuré la fonction CMK, vous ne pouvez pas revenir aux clés gérées par le système. Il vous incombe de gérer vos clés en toute sécurité et de fournir l’accès à votre coffre de clés, à votre clé et à votre application CMK dans [!DNL Azure] pour éviter de perdre l’accès à vos données.

Le processus se présente comme suit :

1. [Configurez un coffre  [!DNL Azure]  Key Vault](./azure-key-vault-config.md) en fonction des politiques de votre entreprise, puis [générez une clé de chiffrement](./azure-key-vault-config.md#generate-a-key) qui sera à la fin partagée avec Adobe.
1. Configurez l’application CMK avec votre client [!DNL Azure] par l’intermédiaire des [appels d’API](./api-set-up.md#register-app) ou de l’ [interface utilisateur](./ui-set-up.md#register-app).
1. Envoyez votre ID de clé de chiffrement pour l’Adobe et démarrez le processus d’activation de la fonctionnalité [ dans l’interface utilisateur](./ui-set-up.md#send-to-adobe) ou avec un [appel API](./api-set-up.md#send-to-adobe).
1. Vérifiez l’état de la configuration pour vérifier si le CMK a été activé [ dans l’interface utilisateur](./ui-set-up.md#check-status) ou avec un [appel API](./api-set-up.md#check-status).

Une fois le processus de configuration terminé, toutes les données intégrées à Platform dans l’ensemble des sandbox seront chiffrées à l’aide de votre configuration de clé [!DNL Azure]. Pour vous servir de la fonction CMK, vous utiliserez la fonctionnalité [!DNL Microsoft Azure] pouvant faire partie de leur [programme de préversion publique](https://azure.microsoft.com/fr-fr/support/legal/preview-supplemental-terms/).

## Conséquences de la révocation de l’accès à la clé {#revoke-access}

Le fait de révoquer ou de désactiver l’accès à l’application Key Vault, key ou CMK peut entraîner des perturbations importantes, notamment la rupture des modifications apportées aux opérations de votre plateforme. Une fois ces clés désactivées, les données de Platform peuvent devenir inaccessibles et toutes les opérations en aval qui dépendent de ces données cesseront de fonctionner. Il est essentiel de bien comprendre les impacts en aval avant d’apporter des modifications à vos configurations clés.

Si vous décidez de révoquer l’accès de Platform à vos données, vous pouvez le faire en supprimant le rôle d’utilisateur associé à l’application du Key Vault dans [!DNL Azure].

### Chronologies de propagation {#propagation-timelines}

Une fois l’accès à la clé révoqué de votre KeyVault [!DNL Azure], les modifications se propagent comme suit :

| **Type de magasin** | **Description** | **Planning** |
|---|---|---|
| Stockages de données de Principal | Ces magasins incluent les magasins Azure Data Lake et Azure Cosmos DB Profile. Une fois l’accès à la clé révoqué, les données deviennent inaccessibles. | Un **à 24 heures**. |
| Stockages de données mis en cache/transitoires | Inclut des entrepôts de données utilisés pour les fonctionnalités de performances et d’application de base. L’impact de la révocation de la clé est retardé. | **Jusqu’à 7 jours**. |

Par exemple, le tableau de bord du profil continuera à afficher les données de son cache pendant sept jours au maximum avant l’expiration et l’actualisation des données. De même, la réactivation de l’accès à l’application prend le même temps pour restaurer la disponibilité des données dans ces magasins.

>[!NOTE]
>
>Il existe deux exceptions spécifiques au cas d’utilisation à l’expiration du jeu de données de sept jours sur les données non primaires (mises en cache/transitoires). Pour plus d’informations sur ces fonctionnalités, consultez leur documentation respective.<ul><li>[Réducteur d’URL Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=fr#message-preset-sms)</li><li>[Projections Edge](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Étapes suivantes

Pour lancer le processus, commencez par [configurer un [!DNL Azure] Key Vault](./azure-key-vault-config.md) et [générer une clé de chiffrement](./azure-key-vault-config.md#generate-a-key) à partager avec Adobe.
