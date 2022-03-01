---
keywords: Experience Platform;accueil;rubriques les plus consultées;Google PubSub;google pubsub
solution: Experience Platform
title: Création d’une connexion PubSub-Source Google dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer un connecteur Google PubSub-source à l’aide de l’interface utilisateur de Platform.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: da7b6fe8f9d274b8e5f27138a1baf8caf63a0c01
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 9%

---

# Créez un [!DNL Google PubSub] connexion source dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Google PubSub] (ci-après dénommés &quot;[!DNL PubSub]&quot;) à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Si vous disposez déjà d’un [!DNL PubSub] vous pouvez ignorer le reste de ce document et passer au tutoriel sur [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecte des informations d’identification requises

Pour vous connecter [!DNL PubSub] Pour Platform, vous devez fournir une valeur valide pour les informations d’identification suivantes :

| Credential | Description |
| ---------- | ----------- |
| `projectId` | ID de projet requis pour l’authentification [!DNL PubSub]. |
| `credentials` | Identifiant d’identification ou identifiant de clé privée requis pour l’authentification [!DNL PubSub]. |

Pour plus d’informations sur ces valeurs, voir [Authentification PubSub](https://cloud.google.com/pubsub/docs/authentication) document. Si vous utilisez l’authentification par compte de service, reportez-vous à la section [PubSub, guide](https://cloud.google.com/docs/authentication/production#create_service_account) pour savoir comment générer vos informations d’identification.

>[!TIP]
>
>Si vous utilisez l’authentification par compte de service, assurez-vous que vous avez accordé un accès utilisateur suffisant à votre compte de service et qu’il n’y a pas d’espaces blancs supplémentaires dans le fichier JSON lors de la copie et du collage de vos informations d’identification.

Une fois que vous avez rassemblé vos informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre [!DNL PubSub] compte à Platform.

## Connectez-vous à [!DNL PubSub] account

Dans le [Interface utilisateur de Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder au [!UICONTROL Sources] workspace. Le [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de la barre de recherche.

Sous , [!UICONTROL Stockage dans le cloud] catégorie, sélectionnez **[!UICONTROL Google PubSub]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/google-pubsub/catalog.png)

Le **[!UICONTROL Connexion à Google PubSub]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez la variable [!DNL PubSub] compte avec lequel vous souhaitez créer un nouveau flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et votre [!DNL PubSub] informations d’identification d’authentification sur le formulaire de saisie. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]** puis accorder un certain temps pour établir la nouvelle connexion.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion entre votre [!DNL PubSub] compte et plateforme. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer dans Platform des données de diffusion en continu provenant de votre espace de stockage dans le cloud](../../dataflow/streaming/cloud-storage-streaming.md).
