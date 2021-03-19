---
keywords: Experience Platform ; accueil ; rubriques populaires ; Google PubSub ; google pubsub
solution: Experience Platform
title: Création d’une connexion Google PubSub Source dans l’interface utilisateur
topic: aperçu
type: Tutoriel
description: Découvrez comment créer un connecteur de source Google PubSub à l’aide de l’interface utilisateur de la plate-forme.
translation-type: tm+mt
source-git-commit: b5358ce206888c413035b46fe751520fd9aefb14
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 9%

---


# Créer une connexion source [!DNL Google PubSub] dans l’interface utilisateur

>[!NOTE]
>
> Le connecteur [!DNL Google PubSub] est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../../../home.md#terms-and-conditions).

Ce didacticiel décrit les étapes à suivre pour créer un [!DNL Google PubSub] (ci-après dénommé &quot;[!DNL PubSub]&quot;) à l’aide de l’interface utilisateur de la plate-forme.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de plate-forme.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Si vous disposez déjà d&#39;une connexion [!DNL PubSub] valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur [la configuration d&#39;un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecte des informations d’identification requises

Pour connecter [!DNL PubSub] à la plate-forme, vous devez fournir une valeur valide pour les informations d&#39;identification suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `projectId` | ID de projet requis pour authentifier [!DNL PubSub]. |
| `credentials` | Identifiant d’identification ou de clé privée requis pour authentifier [!DNL PubSub]. |

Pour plus d’informations sur ces valeurs, voir le document [Authentification PubSub](https://cloud.google.com/pubsub/docs/authentication) suivant. Si vous utilisez l’authentification basée sur un compte de service, consultez le [Guide PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) suivant pour savoir comment générer vos informations d’identification.

>[!TIP]
>
>Si vous utilisez l’authentification basée sur un compte de service, assurez-vous que vous avez accordé un accès utilisateur suffisant à votre compte de service et qu’aucun espace blanc supplémentaire ne figure dans le fichier JSON lors de la copie et du collage de vos informations d’identification.

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL PubSub] à la plateforme.

## Connectez votre compte [!DNL PubSub]

Dans l&#39;[interface utilisateur de la plate-forme](https://platform.adobe.com), sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l&#39;aide de la barre de recherche.

Sous la catégorie [!UICONTROL enregistrement du cloud], sélectionnez **[!UICONTROL Google PubSub]**, puis **[!UICONTROL Ajouter les données]**.

![catalogue](../../../../images/tutorials/create/google-pubsub/catalog.png)

La page **[!UICONTROL Se connecter à Google PubSub]** apparaît. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL PubSub] avec lequel vous souhaitez créer un nouveau flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nouveau compte

Si vous créez un nouveau compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis indiquez un nom, une description facultative et vos informations d&#39;authentification [!DNL PubSub] dans le formulaire d&#39;entrée. Une fois terminé, sélectionnez **[!UICONTROL Se connecter à la source]**, puis attendez un certain temps pour que la nouvelle connexion s&#39;établisse.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion entre votre compte [!DNL PubSub] et votre plateforme. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données en flux continu de votre enregistrement cloud dans Platform](../../dataflow/streaming/cloud-storage-streaming.md).
