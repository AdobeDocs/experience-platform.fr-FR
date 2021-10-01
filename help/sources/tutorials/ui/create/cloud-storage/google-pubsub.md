---
keywords: Experience Platform;accueil;rubriques les plus consultées;Google PubSub;google pubsub
solution: Experience Platform
title: Création d’une connexion Google PubSub Source dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer un connecteur Google PubSub-source à l’aide de l’interface utilisateur de Platform.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 9%

---

# Création d’une connexion source [!DNL Google PubSub] dans l’interface utilisateur

>[!NOTE]
>
> Le connecteur [!DNL Google PubSub] est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez la [Présentation des sources](../../../../home.md#terms-and-conditions) .

Ce tutoriel décrit les étapes de création d’un [!DNL Google PubSub] (ci-après appelé &quot;[!DNL PubSub]&quot;) à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Si vous disposez déjà d’une connexion [!DNL PubSub] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecte des informations d’identification requises

Pour connecter [!DNL PubSub] à Platform, vous devez fournir une valeur valide pour les informations d’identification suivantes :

| Credential | Description |
| ---------- | ----------- |
| `projectId` | ID de projet requis pour l’authentification [!DNL PubSub]. |
| `credentials` | Identifiant d’identification ou identifiant de clé privée requis pour l’authentification [!DNL PubSub]. |

Pour plus d’informations sur ces valeurs, consultez le document [Authentification PubSub](https://cloud.google.com/pubsub/docs/authentication) suivant. Si vous utilisez l’authentification par compte de service, reportez-vous au [Guide PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) suivant pour savoir comment générer vos informations d’identification.

>[!TIP]
>
>Si vous utilisez l’authentification par compte de service, assurez-vous que vous avez accordé un accès utilisateur suffisant à votre compte de service et qu’il n’y a pas d’espaces blancs supplémentaires dans le fichier JSON lors de la copie et du collage de vos informations d’identification.

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL PubSub] à Platform.

## Connectez votre compte [!DNL PubSub]

Dans l’ [interface utilisateur de la plateforme](https://platform.adobe.com), sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources] . L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de la barre de recherche.

Dans la catégorie [!UICONTROL Stockage dans le cloud] , sélectionnez **[!UICONTROL Google PubSub]**, puis **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/google-pubsub/catalog.png)

La page **[!UICONTROL Se connecter à Google PubSub]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL PubSub] avec lequel vous souhaitez créer un nouveau flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis indiquez un nom, une description facultative et vos informations d’authentification [!DNL PubSub] dans le formulaire de saisie. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]**, puis laissez un certain temps pour établir la nouvelle connexion.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion entre votre compte [!DNL PubSub] et Platform. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données en flux continu de votre espace de stockage dans le cloud dans Platform](../../dataflow/streaming/cloud-storage-streaming.md).
