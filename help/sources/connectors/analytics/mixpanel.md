---
title: Présentation de Mixpanel Source Connector
description: Découvrez comment connecter Mixpanel à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: 6f8abca8f0db8a559fe62e6c143f2d0506d3b886
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 30%

---

# [!DNL Mixpanel]

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données à partir d’une application d’analyse tierce. [!DNL Mixpanel] est compatible avec les fournisseurs d’analyses.

[[!DNL Mixpanel]](https://www.mixpanel.com) est un outil d’analyse de produit qui vous permet de capturer des données sur la manière dont les utilisateurs interagissent avec un produit numérique. Mixpanel vous permet d’analyser ces données de produit à l’aide de rapports interactifs simples, qui vous permettent d’interroger et de visualiser les données en quelques clics seulement.

Les sources utilisent l’ [API d’exportation d’événements Mixpanel > Télécharger](https://developer.mixpanel.com/reference/raw-event-export) pour télécharger les données d’événement telles qu’elles sont reçues et stockées dans [!DNL Mixpanel], ainsi que toutes les propriétés d’événement (y compris `distinct_id`) et l’horodatage exact de l’événement a été envoyé à l’Experience Platform. Mixpanel utilise des jetons au porteur comme mécanisme d’authentification pour communiquer avec l’API d’exportation d’événements Mixpanel.

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Authentification de votre compte [!DNL Mixpanel]

Cette section décrit les étapes préalables à suivre pour authentifier votre compte et importer vos données [!DNL Mixpanel] dans Platform.

Pour créer une connexion source et un flux de données [!DNL Mixpanel], vous devez d’abord disposer d’un compte [!DNL Mixpanel] valide. Si vous ne disposez pas d’un compte [!DNL Mixpanel] valide, consultez la page [Mixpanel register](https://mixpanel.com/register/) pour créer votre compte.

Une fois que vous avez créé un compte [!DNL Mixpanel], accédez à l’onglet [!DNL Project Details] de la page [!DNL Project Seettings] de l’interface utilisateur [!DNL Mixpanel] pour récupérer l’ID de projet et configurer votre fuseau horaire.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

Ensuite, accédez à l’onglet [!DNL Service Accounts] de la page [!DNL Project Settings] de l’interface utilisateur [!DNL Mixpanel] pour récupérer les informations d’identification de votre compte de service.

>[!TIP]
>
>Pour les bonnes pratiques, sélectionnez un compte de service qui [ n&#39;expire pas](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Compte de service Mixpanel](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Enfin, créez une plateforme [schema](../../../xdm/schema/composition.md) requise pour [!DNL Mixpanel Event Export API]. Pour plus d’informations sur les mappages requis pour votre schéma, consultez le guide sur la [création d’une  [!DNL Mixpanel] connexion source dans l’interface utilisateur](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![Créer un schéma](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Connecter [!DNL Mixpanel] à Platform à l’aide d’API

La documentation ci-dessous fournit des informations sur la connexion d’[!DNL Mixpanel] à Platform à l’aide d’API ou de l’interface utilisateur :

* [Créez une connexion source et un flux de données pour  [!DNL Mixpanel]  à l’aide de l’API Flow Service](../../tutorials/api/create/analytics/mixpanel.md)

## Connecter [!DNL Mixpanel] à Platform à l’aide de l’interface utilisateur

* [Créer une connexion source  [!DNL Mixpanel]  dans l’interface utilisateur](../../tutorials/ui/create/analytics/mixpanel.md)
* [Création d’un flux de données pour une connexion de source de succès client dans l’interface utilisateur](../../tutorials/ui/dataflow/analytics.md)
