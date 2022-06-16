---
keywords: Experience Platform;accueil;rubriques populaires;
title: (Version bêta) Présentation du connecteur source Mixpanel
description: Découvrez comment connecter Mixpanel à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
hide: true
hidefromtoc: true
source-git-commit: e7a5e20721f5826ca1f4520b4a27d261eed1e4df
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 27%

---

# (version bêta) [!DNL Mixpanel]

>[!NOTE]
>
>Le [!DNL Mixpanel] La source est en version bêta. Voir [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

Experience Platform prend en charge l’ingestion de données à partir d’une application d’analyse tierce. La prise en charge des fournisseurs d’analyses inclut [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) est un outil d’analyse de produit qui vous permet de capturer des données sur la manière dont les utilisateurs interagissent avec un produit numérique. Mixpanel vous permet d’analyser ces données de produit à l’aide de rapports interactifs simples, qui vous permettent d’interroger et de visualiser les données en quelques clics seulement.

Les sources exploitent la variable [API d’exportation d’événements Mixpanel > Télécharger](https://developer.mixpanel.com/reference/raw-event-export) pour télécharger les données d’événement telles qu’elles sont reçues et stockées dans [!DNL Mixpanel], ainsi que toutes les propriétés d’événement (y compris `distinct_id`) et l’horodatage exact de l’envoi de l’événement à Experience Platform. Mixpanel utilise des jetons au porteur comme mécanisme d’authentification pour communiquer avec l’API d’exportation d’événements Mixpanel.

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Authentifiez votre [!DNL Mixpanel] account

Cette section décrit les étapes préalables à l’authentification de votre compte et à l’obtention de votre [!DNL Mixpanel] données vers Platform.

Pour créer une [!DNL Mixpanel] connexion source et flux de données, vous devez d’abord disposer d’un [!DNL Mixpanel] compte . Si vous n’avez pas de [!DNL Mixpanel] , voir [Enregistrement de panneau mixte](https://mixpanel.com/register/) pour créer votre compte.

Une fois que vous avez créé une [!DNL Mixpanel] , accédez à la [!DNL Project Details] dans le [!DNL Project Seettings] de la [!DNL Mixpanel] Interface utilisateur permettant de récupérer l’ID de votre projet et de configurer votre fuseau horaire.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

Ensuite, accédez au [!DNL Service Accounts] dans le [!DNL Project Settings] dans la [!DNL Mixpanel] Interface utilisateur pour récupérer les informations d’identification de votre compte de service.

>[!TIP]
>
>Pour les bonnes pratiques, sélectionnez un compte de service qui [n’expire pas](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Compte de service Mixpanel](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Enfin, créez une plateforme [schema](../../../xdm/schema/composition.md) requis pour [!DNL Mixpanel Event Export API]. Pour plus d’informations sur les mappages requis pour votre schéma, consultez le guide sur [création d’un [!DNL Mixpanel] connexion source dans l’interface utilisateur](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![Création d’un schéma](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Connexion [!DNL Mixpanel] vers Platform à l’aide d’API

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Mixpanel] à Platform à l’aide d’API ou de l’interface utilisateur :

* [Création d’une connexion source et d’un flux de données pour [!DNL Mixpanel] utilisation de l’API Flow Service](../../tutorials/api/create/analytics/mixpanel.md)

## Connexion [!DNL Mixpanel] vers Platform à l’aide de l’interface utilisateur

* [Créer une connexion source  [!DNL Mixpanel]  dans l’interface utilisateur](../../tutorials/ui/create/analytics/mixpanel.md)
* [Création d’un flux de données pour une connexion de source de succès client dans l’interface utilisateur](../../tutorials/ui/dataflow/analytics.md)

