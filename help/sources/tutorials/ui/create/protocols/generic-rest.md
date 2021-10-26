---
keywords: Experience Platform;accueil;rubriques les plus consultées;API REST générique
title: Création d’une connexion à la source de l’API REST générique dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source de l’API REST générique à l’aide de l’interface utilisateur de Adobe Experience Platform.
source-git-commit: 94809a8e98c8de7a9a474fb5543b590fc51cb075
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 6%

---

# Créez un [!DNL Generic REST API] connexion source dans l’interface utilisateur

>[!NOTE]
>
> Le [!DNL Generic REST API] La source est en version bêta. Voir [Présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs bêta-étiquetés.

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Generic REST API] connecteur source à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension pratique des composants suivants de Platform :

* [Sources](../../../../home.md): Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### Collecte des informations d’identification requises

In order to access your [!DNL Generic REST API] account on Platform, you must provide valid credentials for the authentication type of your choice. Generic REST API supports both OAuth 2 refresh code and basic authentication. Consultez les tableaux suivants pour plus d’informations sur les informations d’identification des deux types d’authentification pris en charge.

#### OAuth 2 refresh code

| Credential | Description |
| --- | --- |
| Hôte | URL d’hôte de la source à laquelle vous effectuez votre demande. Cette valeur est requise et ne peut pas être ignorée à l’aide du remplacement du paramètre de requête. |
| URL du test d’autorisation | (Facultatif) L’URL du test d’autorisation est utilisée pour valider les informations d’identification lors de la création d’une connexion de base. Si elles ne sont pas fournies, les informations d’identification sont automatiquement vérifiées à l’étape de création de la connexion source. |
| Identifiant du client | (Facultatif) Identifiant client associé à votre compte utilisateur. |
| Client secret | (Facultatif) Le secret client associé à votre compte utilisateur. |
| Access token | Informations d’identification d’authentification Principales utilisées pour accéder à votre application. Le jeton d’accès représente l’autorisation de votre application, pour accéder à certains aspects des données d’un utilisateur. Cette valeur est requise et ne peut pas être ignorée à l’aide du remplacement du paramètre de requête. |
| Jeton d’actualisation | (Facultatif) Jeton utilisé pour générer un nouveau jeton d’accès, lorsque le jeton d’accès a expiré. |
| URL du jeton d’accès | (Facultatif) Le point de terminaison URL utilisé pour récupérer votre jeton d’accès. |
| Request parameter override | (Optional) A property that allows you to specify which credential parameters to override. |


#### Authentification de base

| Credential | Description |
| --- | --- |
| Hôte | URL d’hôte de la source à laquelle vous effectuez votre demande. |
| Nom d’utilisateur | Nom d’utilisateur correspondant à votre compte d’utilisateur. |
| Mot de passe | Mot de passe correspondant à votre compte utilisateur. |

## Connexion à votre compte API REST générique

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à la fonction [!UICONTROL Sources] workspace. Le [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Alternatively, you can find the specific source you wish to work with using the search bar.

Under the [!UICONTROL Protocols] category, select **[!UICONTROL Generic REST API]** and then select **[!UICONTROL Add data]**.

![catalogue](../../../../images/tutorials/create/generic-rest/catalog.png)

Le **[!UICONTROL Connexion à l’API REST générique]** s’affiche. On this page, you can either use new credentials or existing credentials.

### Compte existant

Pour connecter un compte existant, sélectionnez le compte API REST générique avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/generic-rest/existing.png)

### Nouveau compte

If you are creating a new account, select **[!UICONTROL New account]**, and then provide a name and an option description for your new [!DNL Generic REST API] account.

![new](../../../../images/tutorials/create/generic-rest/new.png)

#### Authentification à l’aide du code d’actualisation OAuth 2

[!DNL Generic REST API] prend en charge le code d’actualisation OAuth 2 et l’authentification de base. Pour vous authentifier à l’aide d’une authentification OAuth2, sélectionnez **[!UICONTROL OAuth2RefreshCode]**, saisissez vos informations d’identification OAuth 2, puis sélectionnez **[!UICONTROL Connexion à la source]**.

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### Authentification à l’aide de l’authentification de base

Pour utiliser l’authentification de base, sélectionnez **[!UICONTROL Authentification de base]**, indiquez votre hôte, votre nom d’utilisateur et votre mot de passe, puis sélectionnez **[!UICONTROL Connexion à la source]**.

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte API REST générique. Vous pouvez maintenant passer au tutoriel suivant et [configuration d’un flux de données pour importer des données dans Platform](../../dataflow/protocols.md).
