---
keywords: Experience Platform;accueil;rubriques populaires;Square;square
title: Création d’une connexion Square Source dans l’interface utilisateur
description: Découvrez comment créer une connexion source Square à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 44%

---

# Créer une connexion source [!DNL Square] dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer un connecteur source [!DNL Square] à l’aide de l’interface utilisateur d’Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

### Collecter les informations d’identification requises

Pour accéder à l’Experience Platform de votre compte [!DNL Square], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| --- | --- |
| Hôte | URL de l’instance de [!DNL Square]. |
| Identifiant client | Identifiant client associé à votre compte [!DNL Square]. |
| Secret client | Secret client associé à votre compte [!DNL Square]. |
| Jeton d’accès | Le jeton d’accès est utilisé pour authentifier votre compte [!DNL Square] avec l’authentification OAuth 2.0. Le jeton d’accès peut être obtenu à partir de [!DNL Square]. |
| Actualiser le jeton | Le jeton d’actualisation est utilisé pour générer de nouveaux jetons d’accès une fois que votre jeton d’accès actuel expire. Le jeton d’actualisation peut être obtenu à partir de [!DNL Square]. |

Pour plus d’informations sur ces informations d’identification et sur la manière de les obtenir, consultez la [[!DNL Square] documentation sur OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Square] à Experience Platform.

## Connecter votre compte [!DNL Square]

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie [!UICONTROL Paiements], sélectionnez **[!UICONTROL Carré]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/square/catalog.png)

La page **[!UICONTROL Se connecter à Square]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL Square] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/square/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et les valeurs appropriées pour vos informations d’identification [!DNL Square]. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]**, puis patientez quelques instants le temps que la nouvelle connexion sʼétablisse.

![nouveau](../../../../images/tutorials/create/square/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez authentifié et avez créé une connexion source entre votre compte [!DNL Square] et Experience Platform. Vous pouvez maintenant passer au tutoriel suivant et [créer un flux de données pour importer des données de paiement dans Experience Platform](../../dataflow/payments.md).
