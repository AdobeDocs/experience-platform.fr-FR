---
title: Créer une connexion Source Google PubSub dans l’interface utilisateur
description: Découvrez comment créer un connecteur source Google PubSub à l’aide de l’interface utilisateur d’Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 24%

---

# Créer une connexion source [!DNL Google PubSub] dans l’interface utilisateur

>[!IMPORTANT]
>
>La source [!DNL Google PubSub] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Ce tutoriel décrit les étapes à suivre pour créer un [!DNL Google PubSub] (ci-après dénommé « [!DNL PubSub] ») à l’aide de l’interface utilisateur d’Experience Platform.

## Commencer

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Si vous disposez déjà d’une connexion [!DNL PubSub] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecter les informations d’identification requises

Vous devez fournir des valeurs pour les propriétés de connexion décrites ci-dessous afin de connecter votre compte [!DNL PubSub] à Experience Platform. Pour plus d’informations sur l’authentification et la configuration requise, consultez la [[!DNL PubSub source] présentation](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).


>[!BEGINTABS]

>[!TAB Authentification basée sur le projet]

| Informations d’identification | Description |
| --- | --- |
| ID de projet | Identifiant de projet requis pour authentifier [!DNL PubSub]. |
| Informations d’identification | Informations d’identification requises pour authentifier [!DNL PubSub]. Vous devez vous assurer de placer le fichier JSON complet après avoir supprimé les espaces blancs de vos informations d’identification. |

>[!TAB Authentification par rubrique et par abonnement]

| Informations d’identification | Description |
| --- | --- |
| Informations d’identification | Informations d’identification requises pour authentifier [!DNL PubSub]. Vous devez vous assurer de placer le fichier JSON complet après avoir supprimé les espaces blancs de vos informations d’identification. |
| Nom de la rubrique | Nom de votre abonnement [!DNL PubSub]. Dans [!DNL PubSub], les abonnements vous permettent de recevoir des messages, en vous abonnant à la rubrique dans laquelle les messages ont été publiés. **Remarque** : un seul abonnement [!DNL PubSub] ne peut être utilisé que pour un seul flux de données. Pour créer plusieurs flux de données, vous devez disposer de plusieurs abonnements. |
| Nom d&#39;abonnement | Nom de votre abonnement [!DNL PubSub]. Dans [!DNL PubSub], les abonnements vous permettent de recevoir des messages, en vous abonnant à la rubrique dans laquelle les messages ont été publiés. |

>[!ENDTABS]

Pour plus d’informations sur ces valeurs, consultez le document suivant : [Authentification PubSub](https://cloud.google.com/pubsub/docs/authentication). Si vous utilisez l’authentification par compte de service, consultez le [guide de PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) et suivez les instructions pour générer vos informations d’identification.

>[!TIP]
>
>Si vous utilisez l’authentification par compte de service, assurez-vous que vous avez accordé un accès utilisateur suffisant à votre compte de service et qu’il n’y a pas d’espaces blancs supplémentaires dans le fichier JSON lors de la copie et du collage de vos informations d’identification.

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL PubSub] à Experience Platform.

## Connecter votre compte [!DNL PubSub]

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie [!UICONTROL Espace de stockage], sélectionnez **[!UICONTROL Google PubSub]**, puis cliquez sur **[!UICONTROL Ajouter des données]**.

![Le catalogue de sources sur l’interface utilisateur d’Experience Platform.](../../../../images/tutorials/create/google-pubsub/catalog.png)

La page **[!UICONTROL Connexion à Google PubSub]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL PubSub] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Sélection du compte existant dans le workflow des sources.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nouveau compte

>[!TIP]
>
>* Lors de la création d’un compte avec un accès restreint, vous devez fournir au moins un de vos nom de rubrique ou nom d’abonnement. L’authentification échoue si les deux valeurs sont manquantes.
>* Une fois créé, vous ne pouvez pas modifier le type d’authentification d’une connexion de base [!DNL Google PubSub]. Pour modifier le type d’authentification, vous devez créer une connexion de base.

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description facultative pour votre nouveau compte [!DNL PubSub].

![Nouvelle interface de compte pour la source Google PubSub dans le workflow des sources](../../../../images/tutorials/create/google-pubsub/new.png)

La source [!DNL PubSub] vous permet de spécifier le type d’accès que vous souhaitez autoriser lors de l’authentification. Vous pouvez configurer votre compte pour qu’il dispose d’une authentification par projet ou d’une authentification par rubrique et par abonnement. L’authentification par projet vous permet d’accorder l’accès au projet au niveau racine dans votre compte, tandis que l’authentification par rubrique et par abonnement vous permet de restreindre l’accès à une rubrique et à un abonnement [!DNL PubSub] spécifiques.

>[!BEGINTABS]

>[!TAB Authentification basée sur le projet]

Pour créer un compte ayant accès au dossier racine du projet [!DNL PubSub], procédez comme suit : Sélectionnez **[!UICONTROL Informations d’identification d’authentification Google PubSub]** comme type d’authentification et indiquez votre ID de projet et vos informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Nouvelle interface de compte pour la source Google PubSub avec un accès racine sélectionné.](../../../../images/tutorials/create/google-pubsub/root.png)

>[!TAB Authentification par rubrique et par abonnement]

Pour créer un compte avec un accès limité uniquement à une rubrique et à un abonnement [!DNL PubSub] spécifiques, sélectionnez **[!UICONTROL Informations d’authentification Google PubSub Scoped]** puis fournissez vos informations d’identification, le nom de la rubrique et/ou le nom de l’abonnement. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Nouvelle interface de compte pour la source Google PubSub avec un accès étendu sélectionné.](../../../../images/tutorials/create/google-pubsub/scoped.png)

>[!ENDTABS]

>[!NOTE]
>
>Les principaux (rôles) affectés à un projet [!DNL PubSub] sont hérités dans toutes les rubriques et tous les abonnements créés dans un projet [!DNL PubSub]. Si vous souhaitez qu’un principal (rôle) ait accès à une rubrique spécifique, ce principal (rôle) doit également être ajouté à l’abonnement correspondant à la rubrique. Pour plus d’informations, consultez la [[!DNL PubSub] documentation sur le contrôle d’accès](<https://cloud.google.com/pubsub/docs/access-control>).

## Sélectionner les données

Une authentification réussie vous amène à l’étape [!UICONTROL Sélectionner les données], où vous pouvez parcourir votre hiérarchie de données [!DNL PubSub] et sélectionner les données à importer dans Experience Platform.

>[!BEGINTABS]

>[!TAB Authentification basée sur le projet]

Si vous vous êtes authentifié avec un accès basé sur un projet, l’interface [!UICONTROL Sélectionner les données] affiche tous les abonnements de votre projet auxquels une rubrique est associée.

![Étape de sélection des données du workflow des sources avec authentification par projet.](../../../../images/tutorials/create/google-pubsub/root-folders.png)

>[!TAB Authentification par rubrique et par abonnement]

Si vous vous êtes authentifié avec une rubrique et un accès par abonnement, l’affichage de l’interface [!UICONTROL Sélectionner les données] peut varier en fonction des informations que vous avez fournies.

* Si vous indiquez uniquement le nom de la rubrique, l’interface affiche toutes les paires rubrique-abonnement qui correspondent à la rubrique fournie.
* Si vous indiquez uniquement le nom de l’abonnement, l’interface affiche toutes les paires rubrique-abonnement qui correspondent au nom d’abonnement fourni.
* Si des noms de rubrique et d’abonnement sont fournis, l’interface affiche la paire rubrique-abonnement qui correspond aux deux valeurs fournies.

![Étape de sélection des données du workflow des sources avec authentification par rubrique et par abonnement.](../../../../images/tutorials/create/google-pubsub/scoped-folders.png)

>[!ENDTABS]

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion entre votre compte [!DNL PubSub] et Experience Platform. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données de flux depuis votre espace de stockage dans Experience Platform](../../dataflow/streaming/cloud-storage-streaming.md).
