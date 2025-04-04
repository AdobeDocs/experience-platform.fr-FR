---
title: Clés gérées par le client dans Adobe Experience Platform
description: Découvrez comment configurer vos propres clés de chiffrement pour les données stockées dans Adobe Experience Platform.
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 6%

---

# Clés gérées par le client dans Adobe Experience Platform

Les données stockées sur Adobe Experience Platform sont chiffrées au repos à l’aide de clés au niveau du système. Si vous utilisez une application reposant sur Experience Platform, vous pouvez choisir d’utiliser vos propres clés de chiffrement pour mieux contrôler la sécurité de vos données.

>[!AVAILABILITY]
>
>Adobe Experience Platform prend en charge les clés gérées par le client (CMK) pour Microsoft Azure et Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Si votre mise en œuvre s’exécute sur AWS, vous avez la possibilité d’utiliser le service de gestion des clés (KMS) pour le chiffrement des données Experience Platform. Pour plus d’informations sur l’infrastructure prise en charge, consultez la [présentation d’Experience Platform multi-cloud](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).
>
>Pour en savoir plus sur la création et la gestion des clés de chiffrement dans AWS KMS, consultez le [guide sur le chiffrement des données AWS KMS](./aws/configure-kms.md). Pour les implémentations Azure, consultez le [Guide de configuration du coffre de clés Azure](./azure/azure-key-vault-config.md).

>[!NOTE]
>
>Pour [!DNL Azure] instances Experience Platform hébergées, les données de profil client stockées dans Experience Platform [!DNL Azure Data Lake] et le magasin de profils [!DNL Azure Cosmos DB] sont chiffrées exclusivement à l’aide de la fonction CMK une fois activée. La révocation des clés dans les entrepôts de données principaux peut prendre de **quelques minutes à 24 heures** et **jusqu’à 7 jours** pour les entrepôts de données transitoires ou secondaires. Pour plus d’informations, consultez la section [implications de la révocation de l’accès à la clé](#revoke-access).

Ce document présente de manière générale le processus d’activation de la fonctionnalité Clés gérées par le client (CMK) dans Experience Platform sur [!DNL Azure] et AWS, ainsi que les informations préalables requises pour réaliser ces étapes.

>[!NOTE]
>
>Pour les clients Customer Journey Analytics, suivez les instructions de la documentation de [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=fr).

## Conditions préalables

Pour activer la fonction CMK, l’environnement d’hébergement de votre plateforme ([!DNL Azure] ou AWS) doit répondre à des exigences de configuration spécifiques :

### Conditions préalables générales

Pour afficher la section [!UICONTROL Chiffrement] dans Adobe Experience Platform et y accéder, vous devez avoir créé un rôle et attribué l’autorisation [!UICONTROL Gérer les clés gérées par le client] à ce rôle.  Tout utilisateur disposant de l’autorisation [!UICONTROL Gérer les clés gérées par le client] peut activer la fonction CMK pour son organisation.

Pour plus d’informations sur l’attribution de rôles et d’autorisations dans Experience Platform, reportez-vous à la documentation sur la [configuration des autorisations](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

### Conditions préalables spécifiques à Azure

Pour les implémentations hébergées sur Azure, configurez votre coffre de clés [!DNL Azure] avec les paramètres suivants :

- [Activer la protection contre le vidage](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
- [Activer la suppression réversible](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
- [Configuration de l’accès à l’aide  [!DNL Azure]  contrôle d’accès en fonction du rôle](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

### Conditions préalables spécifiques à AWS

Pour les implémentations hébergées par AWS, configurez votre environnement AWS comme suit :

- Assurez-vous de disposer des autorisations nécessaires pour gérer les clés de chiffrement à l’aide de la gestion des identités et des accès (IAM) AWS. Pour plus d’informations, consultez la section [Politiques IAM pour AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html).
- Configurez AWS KMS avec la prise en charge de la fonction CMK. Reportez-vous au guide [Chiffrement des données AWS KMS](./aws/configure-kms.md).

## Résumé du processus {#process-summary}

Les clés gérées par le client (CMK) sont disponibles via les offres Adobe Healthcare Shield et Privacy and Security Shield. Sur Azure, la fonction CMK est prise en charge pour Healthcare Shield et Privacy and Security Shield. Sur AWS, la fonction CMK est prise en charge uniquement pour Privacy and Security Shield et n’est pas disponible pour Healthcare Shield. Une fois que votre entreprise a acheté une licence pour l’une de ces offres, vous pouvez lancer le processus de configuration unique pour activer le CMK.

>[!WARNING]
>
>Après avoir configuré la fonction CMK, vous ne pouvez pas revenir aux clés gérées par le système. Il vous incombe de gérer vos clés en toute sécurité afin d’éviter de perdre l’accès à vos données.

Le processus se présente comme suit :

### Pour Azure {#azure-process-summary}

1. [Configurez un [!DNL Azure] coffre Key Vault](./azure/azure-key-vault-config.md) en fonction des politiques de votre entreprise, puis [générez une clé de chiffrement](./azure/azure-key-vault-config.md#generate-a-key) à partager avec Adobe.
1. Configurez l’application CMK avec votre client [!DNL Azure] par le biais des [appels d’API](./azure/api-set-up.md#register-app) ou de l’[interface utilisateur](./azure/ui-set-up.md#register-app).
1. Envoyez votre identifiant de clé de chiffrement à Adobe et démarrez le processus d’activation de la fonctionnalité, soit [dans l’interface utilisateur](./azure/ui-set-up.md#send-to-adobe) soit avec un [appel API](./azure/api-set-up.md#send-to-adobe).
1. Vérifiez le statut de la configuration pour vous assurer que la fonction CMK a été activée, soit [dans l’interface utilisateur](./azure/ui-set-up.md#check-status) soit avec un [appel API](./azure/api-set-up.md#check-status).

Une fois le processus de configuration terminé pour les instances Experience Platform hébergées sur Azure, toutes les données intégrées à Experience Platform dans l’ensemble des sandbox seront chiffrées à l’aide de votre configuration de clé [!DNL Azure]. Pour vous servir de la fonction CMK, vous utiliserez la fonctionnalité [!DNL Microsoft Azure] pouvant faire partie de leur [programme de préversion publique](https://azure.microsoft.com/fr-fr/support/legal/preview-supplemental-terms/).

### Pour AWS {#aws-process-summary}

1. [Configurez AWS KMS](./aws/configure-kms.md) en configurant une clé de chiffrement à partager avec Adobe.
2. Suivez les instructions spécifiques à AWS dans le [guide de configuration de l’interface utilisateur](./aws/ui-set-up.md).
3. Validez la configuration pour confirmer que les données Experience Platform sont chiffrées à l’aide de la clé hébergée sur AWS.

<!--  Pending: or [API setup guide]() -->

Une fois le processus de configuration terminé pour les instances Experience Platform hébergées par AWS, toutes les données intégrées à Experience Platform dans l’ensemble des sandbox seront chiffrées à l’aide de votre configuration du service de gestion des clés (KMS) AWS. Pour utiliser la fonction CMK sur AWS, vous utiliserez le service de gestion des clés AWS afin de créer et de gérer vos clés de chiffrement conformément aux exigences de sécurité de votre entreprise.

## Implications de la révocation de l’accès aux clés {#revoke-access}

La révocation ou la désactivation de l’accès au coffre de clés, à la clé ou à l’application CMK dans Azure ou à la clé de chiffrement dans AWS peut entraîner des perturbations importantes, notamment des modifications avec rupture de vos opérations Experience Platform. Une fois les clés désactivées, les données d’Experience Platform peuvent devenir inaccessibles et toutes les opérations en aval qui reposent sur ces données cesseront de fonctionner. Il est essentiel de bien comprendre les impacts en aval avant d’apporter des modifications à vos configurations clés.

Pour révoquer l’accès d’Experience Platform à vos données dans [!DNL Azure], supprimez le rôle d’utilisateur associé à l’application du coffre de clés. Pour AWS, vous pouvez désactiver la clé ou mettre à jour l’instruction de politique. Pour obtenir des instructions détaillées sur le processus AWS, reportez-vous à la [section révocation des clés](./aws/ui-set-up.md#key-revocation).


### Chronologies de propagation {#propagation-timelines}

Une fois l’accès à la clé révoqué de votre coffre de clés [!DNL Azure], les modifications se propageront comme suit :

| **Type de magasin** | **Description** | **Planning** |
|---|---|---|
| Magasins de données de Principal | Inclut les magasins de profils de base de données Azure Cosmos (Azure Data Lake, AWS S3) et Azure. Une fois l’accès à la clé révoqué, les données deviennent inaccessibles. | De **minutes à 24 heures**. |
| Magasins de données transitoires/mis en cache | Inclut des entrepôts de données secondaires utilisés pour les performances et les fonctionnalités des applications principales. L’impact de la révocation des clés est retardé. | **Jusqu’à 7 jours**. |

Par exemple, le tableau de bord du profil continuera à afficher les données de son cache pendant sept jours au maximum avant l’expiration des données et sera actualisé. De même, la réactivation de l’accès à l’application prend le même temps pour restaurer la disponibilité des données dans ces magasins.

>[!NOTE]
>
>La réactivation de l’accès à l’application peut prendre le même temps que la révocation pour restaurer la disponibilité des données dans ces magasins.

>[!TIP]
>
>Il existe deux exceptions spécifiques aux cas d’utilisation à l’expiration de sept jours du jeu de données sur les données non principales (mises en cache/transitoires). Pour plus d’informations sur ces fonctionnalités, consultez leurs documentations respectives.<ul><li>[Raccourcisseur d’URL Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=fr#message-preset-sms)</li><li>[Projections Edge](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Étapes suivantes

Pour lancer le processus :

- Pour Azure : commencez par [configurer un coffre  [!DNL Azure]  Key Vault](./azure/azure-key-vault-config.md) et [générer une clé de chiffrement](./azure/azure-key-vault-config.md#generate-a-key) à partager avec Adobe.
- Pour AWS : [Configurez AWS KMS](./aws/configure-kms.md) et assurez-vous que les configurations IAM et KMS sont appropriées avant de passer aux guides de configuration de l’interface utilisateur ou de l’API.
