---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
solution: Experience Platform
title: Création d’une connexion source de campagnes MailChimp à l’aide de l’interface utilisateur de Platform
topic-legacy: tutorial
description: Découvrez comment connecter Adobe Experience Platform à des campagnes MailChimp à l’aide de l’interface utilisateur de Platform.
exl-id: e8e1ed32-4277-44c9-aafc-6bb9e0a1fe0d
source-git-commit: ed185d0957c3cd84c33a6ff60c5ded2b17fbfe74
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 4%

---

# Créez un [!DNL Mailchimp Campaigns] Connexion source à l’aide de l’interface utilisateur de Platform

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Mailchimp] connecteur source à ingérer [!DNL Mailchimp Campaigns] données vers Adobe Experience Platform à l’aide de l’interface utilisateur.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md): Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md): Platform fournit des environnements de test virtuels qui divisent une instance de Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Collecte des informations d’identification requises

Pour apporter votre [!DNL Mailchimp Campaigns] données à Platform, vous devez d’abord fournir les informations d’authentification appropriées qui correspondent à vos [!DNL Mailchimp] compte .

Le [!DNL Mailchimp Campaigns] source prend en charge OAuth 2 Refresh Code et l’authentification de base. Pour plus d’informations sur ces types d’authentification, reportez-vous aux tableaux ci-dessous.

### Actualisation du code OAuth 2

| Informations d’identification | Description |
| --- | --- |
| Hôte | URL racine utilisée pour la connexion à l’API MailChimp. Le format de l’URL racine est le suivant : `https://{DC}.api.mailchimp.com`où `{DC}` représente le centre de données qui correspond à votre compte. |
| URL du test d’autorisation | L’URL du test d’autorisation est utilisée pour valider les informations d’identification lors de la connexion. [!DNL Mailchimp] vers Platform. Si ce n’est pas le cas, les informations d’identification sont automatiquement vérifiées à l’étape de création de la connexion source. |
| Jeton d’accès | Jeton d’accès correspondant utilisé pour authentifier votre source. Ceci est requis pour l’authentification basée sur OAuth. |

Pour plus d’informations sur l’utilisation d’OAuth 2 pour authentifier votre [!DNL Mailchimp] compte à Platform, voir [[!DNL Mailchimp] document sur l’utilisation d’OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/).

### Authentification de base

| Informations d’identification | Description |
| --- | --- |
| Hôte | URL racine utilisée pour la connexion à l’API MailChimp. Le format de l’URL racine est le suivant : `https://{DC}.api.mailchimp.com`où `{DC}` représente le centre de données qui correspond à votre compte. |
| Nom d’utilisateur | Nom d’utilisateur correspondant à votre compte MailChimp. Ceci est requis pour l’authentification de base. |
| Mot de passe | Mot de passe correspondant à votre compte MailChimp. Ceci est requis pour l’authentification de base. |

## Connectez-vous à [!DNL Mailchimp Campaigns] compte à Platform

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder au [!UICONTROL Sources] workspace. Le [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , [!UICONTROL Automatisation du marketing] catégorie, sélectionnez **[!UICONTROL Campagne Mailchimp]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/mailchimp-campaigns/catalog.png)

Le **[!UICONTROL Connecter le compte de campagnes Mailchimp]** s’affiche. Sur cette page, vous pouvez indiquer si vous accédez à un compte existant ou si vous choisissez de créer un compte.

### Compte existant

Pour utiliser un compte existant, sélectionnez la variable [!DNL Mailchimp Campaigns] compte avec lequel vous souhaitez créer un nouveau flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/mailchimp-campaigns/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description pour votre [!DNL Mailchimp Campaigns] Informations de connexion à la source.

![new](../../../../images/tutorials/create/mailchimp-campaigns/new.png)

#### Authentification à l’aide d’OAuth 2

Pour utiliser OAuth 2, sélectionnez [!UICONTROL Actualisation du code OAuth 2], indiquez les valeurs de votre hôte, de l’URL du test d’autorisation et du jeton d’accès, puis sélectionnez **[!UICONTROL Connexion à la source]**. Autorisez la validation de vos informations d’identification pendant quelques instants, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![oauth](../../../../images/tutorials/create/mailchimp-campaigns/oauth.png)

#### Authentification à l’aide de l’authentification de base

Pour utiliser l’authentification de base, sélectionnez [!UICONTROL Authentification de base], indiquez les valeurs de votre hôte, de votre nom d’utilisateur et de votre mot de passe, puis sélectionnez **[!UICONTROL Connexion à la source]**. Autorisez la validation de vos informations d’identification pendant quelques instants, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![basic](../../../../images/tutorials/create/mailchimp-campaigns/basic.png)

### Sélectionner [!DNL Mailchimp Campaigns] data

Une fois votre source authentifiée, vous devez fournir la variable `campaignId` qui correspond à votre [!DNL Mailchimp Campaigns] compte .

Sur le [!UICONTROL Sélectionner des données] , saisissez votre `campaignId` puis sélectionnez **[!UICONTROL Exploration]**.

![explorer](../../../../images/tutorials/create/mailchimp-campaigns/explore.png)

La page se met à jour dans une arborescence de schéma interactif qui vous permet d’explorer et d’inspecter la hiérarchie de vos données. Sélectionner **[!UICONTROL Suivant]** pour continuer.

![select-data](../../../../images/tutorials/create/mailchimp-campaigns/select-data.png)

## Étapes suivantes

Avec votre [!DNL Mailchimp] votre compte authentifié et votre [!DNL Mailchimp Campaigns] données sélectionnées, vous pouvez maintenant commencer à créer un flux de données pour importer vos données dans Platform. Pour obtenir des instructions détaillées sur la création d’un flux de données, consultez la documentation sur [création d’un flux de données pour importer des données d’automatisation du marketing dans Platform](../../dataflow/marketing-automation.md).
