---
keywords: Experience Platform;accueil;rubriques populaires;Google PubSub;google pubsub
solution: Experience Platform
title: Créer une connexion de source Google PubSub dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer un connecteur source Google PubSub à l’aide de l’interface utilisateur de Platform.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: da7b6fe8f9d274b8e5f27138a1baf8caf63a0c01
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 100%

---

# Créer une connexion source [!DNL Google PubSub] dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion de source [!DNL Google PubSub] (ci-après dénommée « [!DNL PubSub] ») à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandboxes](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuelles qui divisent une instance de Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Si vous disposez déjà d’une connexion [!DNL PubSub] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecter les informations d’identification requises

Pour connecter [!DNL PubSub] à Platform, vous devez fournir une valeur valide pour les informations d’identification suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `projectId` | Identifiant de projet requis pour l’authentification [!DNL PubSub]. |
| `credentials` | Informations d’identification ou identifiant de clé privée requis pour l’authentification [!DNL PubSub]. |

Pour plus d’informations sur ces valeurs, consultez le document suivant : [Authentification PubSub](https://cloud.google.com/pubsub/docs/authentication). Si vous utilisez l’authentification par compte de service, consultez le [guide de PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) et suivez les instructions pour générer vos informations d’identification.

>[!TIP]
>
>Si vous utilisez l’authentification par compte de service, assurez-vous que vous avez accordé un accès utilisateur suffisant à votre compte de service et qu’il n’y a pas d’espaces blancs supplémentaires dans le fichier JSON lors de la copie et du collage de vos informations d’identification.

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre la procédure ci-dessous et lier votre compte [!DNL PubSub] à Platform.

## Connecter votre compte [!DNL PubSub]

Dans l’[interface utilisateur de Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à lʼespace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche plusieurs sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également sélectionner la source de votre choix à l’aide de la barre de recherche.

Dans la catégorie [!UICONTROL Espace de stockage], sélectionnez **[!UICONTROL Google PubSub]**, puis cliquez sur **[!UICONTROL Ajouter des données]**.

![catalog](../../../../images/tutorials/create/google-pubsub/catalog.png)

La page **[!UICONTROL Connexion à Google PubSub]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL PubSub] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis entrez un nom, une description (facultative) et vos informations d’authentification [!DNL PubSub] dans le formulaire de saisie. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]** puis patientez quelques instants le temps d’établir la nouvelle connexion.

![nouveau](../../../../images/tutorials/create/google-pubsub/new.png)

## Étapes suivantes

Vous êtes arrivé au bout de ce tutoriel, félicitations ! Grâce à celui-ci, vous avez créé une connexion entre votre compte [!DNL PubSub] et Platform. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données de diffusion en continu depuis votre espace de stockage dans Platform](../../dataflow/streaming/cloud-storage-streaming.md).
