---
keywords: Experience Platform;accueil;rubriques les plus consultées;Carré;carré
title: Création d’une connexion Source carrée dans l’interface utilisateur
description: Découvrez comment créer une connexion source au carré à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 56%

---

# Créer une connexion source [!DNL Square] dans l’interface utilisateur

Ce tutoriel décrit les étapes de création d’un connecteur source [!DNL Square] à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

### Collecter les informations d’identification requises

Pour accéder à votre plateforme de compte [!DNL Square], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| --- | --- |
| Hôte | URL de l’instance [!DNL Square]. |
| Identifiant client | L’ID client associé à votre compte [!DNL Square]. |
| Secret client | Le secret client associé à votre compte [!DNL Square]. |
| Jeton d’accès | Le jeton d’accès est utilisé pour authentifier votre compte [!DNL Square] avec l’authentification OAuth 2.0. Le jeton d’accès peut être obtenu à partir de [!DNL Square]. |
| Actualiser le jeton | Le jeton d’actualisation est utilisé pour générer de nouveaux jetons d’accès une fois que votre jeton d’accès actuel expire. Le jeton d’actualisation peut être obtenu à partir de [!DNL Square]. |

Pour plus d’informations sur ces informations d’identification et sur la manière de les obtenir, consultez la [[!DNL Square] documentation sur OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre la procédure ci-dessous et lier votre compte [!DNL Square] à Platform.

## Connecter votre compte [!DNL Square]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie [!UICONTROL payment], sélectionnez **[!UICONTROL Square]**, puis **[!UICONTROL Add data]**.

![catalogue](../../../../images/tutorials/create/square/catalog.png)

La page **[!UICONTROL Se connecter à Square]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL Square] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/square/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et les valeurs appropriées pour vos informations d’identification [!DNL Square]. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]**, puis patientez quelques instants le temps que la nouvelle connexion sʼétablisse.

![nouveau](../../../../images/tutorials/create/square/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez authentifié et avez créé une connexion source entre votre compte [!DNL Square] et Platform. Vous pouvez maintenant passer au tutoriel suivant et [créer un flux de données pour importer des données de paiements dans Platform](../../dataflow/payments.md).
