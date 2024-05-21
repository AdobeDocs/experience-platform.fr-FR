---
title: Création d’une connexion PubSub-Source Google dans l’interface utilisateur
description: Découvrez comment créer un connecteur source Google PubSub à l’aide de l’interface utilisateur de Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: fcac805e151d6142886eb8e05da0eb1babad2f69
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 36%

---

# Créer une connexion source [!DNL Google PubSub] dans l’interface utilisateur

>[!IMPORTANT]
>
>La variable [!DNL Google PubSub] source est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-time Customer Data Platform Ultimate.

Ce tutoriel décrit les étapes à suivre pour créer une connexion de source [!DNL Google PubSub] (ci-après dénommée « [!DNL PubSub] ») à l’aide de l’interface utilisateur de Platform.

## Commencer

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Si vous disposez déjà d’une connexion [!DNL PubSub] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecter les informations d’identification requises

Pour connecter votre [!DNL PubSub] compte à Experience Platform. Pour plus d’informations sur l’authentification et la configuration des prérequis, consultez la section [[!DNL PubSub source] aperçu](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).


>[!BEGINTABS]

>[!TAB Authentification basée sur un projet]

| Informations d’identification | Description |
| --- | --- |
| Identifiant de projet | Identifiant de projet requis pour authentifier [!DNL PubSub]. |
| Informations d’identification | Informations d’identification requises pour l’authentification [!DNL PubSub]. Vous devez vous assurer de placer l’intégralité du fichier JSON après avoir supprimé les espaces blancs de vos informations d’identification. |

>[!TAB Authentification par thème et par abonnement]

| Informations d’identification | Description |
| --- | --- |
| Informations d’identification | Informations d’identification requises pour l’authentification [!DNL PubSub]. Vous devez vous assurer de placer l’intégralité du fichier JSON après avoir supprimé les espaces blancs de vos informations d’identification. |
| Nom de la rubrique | Le nom de votre [!DNL PubSub] abonnement. Dans [!DNL PubSub], les abonnements permettent de recevoir des messages, en s’abonnant à la rubrique sur laquelle les messages ont été publiés. **Remarque**: une seule [!DNL PubSub] abonnement ne peut être utilisé que pour un seul flux de données. Pour créer plusieurs flux de données, vous devez disposer de plusieurs abonnements. |
| Nom de l’abonnement | Le nom de votre [!DNL PubSub] abonnement. Dans [!DNL PubSub], les abonnements permettent de recevoir des messages, en s’abonnant à la rubrique sur laquelle les messages ont été publiés. |

>[!ENDTABS]

Pour plus d’informations sur ces valeurs, consultez le document suivant : [Authentification PubSub](https://cloud.google.com/pubsub/docs/authentication). Si vous utilisez l’authentification par compte de service, consultez le [guide de PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) et suivez les instructions pour générer vos informations d’identification.

>[!TIP]
>
>Si vous utilisez l’authentification par compte de service, assurez-vous que vous avez accordé un accès utilisateur suffisant à votre compte de service et qu’il n’y a pas d’espaces blancs supplémentaires dans le fichier JSON lors de la copie et du collage de vos informations d’identification.

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre la procédure ci-dessous et lier votre compte [!DNL PubSub] à Platform.

## Connecter votre compte [!DNL PubSub]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. La variable [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie [!UICONTROL Espace de stockage], sélectionnez **[!UICONTROL Google PubSub]**, puis cliquez sur **[!UICONTROL Ajouter des données]**.

![Catalogue des sources sur l’interface utilisateur Experience Platform.](../../../../images/tutorials/create/google-pubsub/catalog.png)

La page **[!UICONTROL Connexion à Google PubSub]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL PubSub] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![La sélection de compte existante dans le workflow des sources.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nouveau compte

>[!TIP]
>
>* Lors de la création d’un compte avec accès restreint, vous devez indiquer au moins un nom de rubrique ou d’abonnement. L’authentification échoue si les deux valeurs sont manquantes.
>* Une fois créée, vous ne pouvez pas modifier le type d&#39;authentification d&#39;un [!DNL Google PubSub] connexion de base. Pour modifier le type d&#39;authentification, vous devez créer une nouvelle connexion de base.

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description facultative de votre nouvelle [!DNL PubSub] compte .

![Nouvelle interface de compte pour Google PubSub dans le processus des sources](../../../../images/tutorials/create/google-pubsub/new.png)

La variable [!DNL PubSub] source vous permet de spécifier le type d’accès que vous souhaitez autoriser lors de l’authentification. Vous pouvez configurer votre compte pour qu’il dispose d’une authentification basée sur le projet ou d’une authentification par rubrique et par abonnement. L’authentification basée sur un projet vous permet d’accorder l’accès au projet racine dans votre compte, tandis que l’authentification par rubrique et par abonnement vous permet de restreindre l’accès à un [!DNL PubSub] rubrique et abonnement.

>[!BEGINTABS]

>[!TAB Authentification basée sur un projet]

Pour créer un compte ayant accès à la racine [!DNL PubSub] dossier du projet. Sélectionner **[!UICONTROL Identifiants d’authentification Google PubSub]** comme type d’authentification et fournissez votre ID de projet et vos informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Nouvelle interface de compte pour le PubSub Google avec accès racine sélectionné.](../../../../images/tutorials/create/google-pubsub/root.png)

>[!TAB Authentification par thème et par abonnement]

Pour créer un compte avec accès limité uniquement à un [!DNL PubSub] rubrique et abonnement, sélectionnez **[!UICONTROL Informations d’identification d’authentification de Google PubSub]** et indiquez ensuite vos informations d’identification, nom de rubrique et/ou nom d’abonnement. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Nouvelle interface de compte pour la sous-source de publication Google avec accès limité sélectionné.](../../../../images/tutorials/create/google-pubsub/scoped.png)

>[!ENDTABS]

>[!NOTE]
>
>Entité de sécurité (rôles) affectée à une [!DNL PubSub] les projets sont hérités dans toutes les rubriques et tous les abonnements créés dans une [!DNL PubSub] projet. Si vous souhaitez qu’une entité (rôle) ait accès à une rubrique spécifique, cette entité (rôle) doit également être ajoutée à l’abonnement correspondant à la rubrique. Pour plus d’informations, consultez la section [[!DNL PubSub] documentation sur le contrôle d’accès](<https://cloud.google.com/pubsub/docs/access-control>).

## Sélectionner les données

Une authentification réussie vous permet d’accéder au [!UICONTROL Sélectionner des données] , où vous pouvez naviguer dans votre [!DNL PubSub] hiérarchie des données et sélectionnez les données à importer dans Experience Platform.

>[!BEGINTABS]

>[!TAB Authentification basée sur un projet]

Si vous vous êtes authentifié avec un accès basé sur un projet, la variable [!UICONTROL Sélectionner des données] L’interface affiche tous les abonnements au sein de votre projet auxquels est associée une rubrique.

![L’étape de sélection des données du workflow des sources avec authentification basée sur le projet.](../../../../images/tutorials/create/google-pubsub/root-folders.png)

>[!TAB Authentification par thème et par abonnement]

Si vous vous êtes authentifié avec une rubrique et un accès par abonnement, la variable [!UICONTROL Sélectionner des données] l’affichage de l’interface peut varier en fonction des informations que vous avez fournies.

* Si vous indiquez uniquement le nom de la rubrique, l’interface affiche toutes les paires rubrique-abonnement qui correspondent à la rubrique fournie.
* Si vous fournissez uniquement le nom de l’abonnement, l’interface affiche toutes les paires rubrique-abonnement qui correspondent au nom d’abonnement fourni.
* Si des noms de rubrique et d’abonnement sont fournis, l’interface affiche la paire rubrique-abonnement qui correspond aux deux valeurs fournies.

![L’étape de sélection des données du workflow des sources avec l’authentification par rubrique et par abonnement.](../../../../images/tutorials/create/google-pubsub/scoped-folders.png)

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une connexion entre votre [!DNL PubSub] compte et plateforme. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données de diffusion en continu depuis votre espace de stockage dans Platform](../../dataflow/streaming/cloud-storage-streaming.md).
