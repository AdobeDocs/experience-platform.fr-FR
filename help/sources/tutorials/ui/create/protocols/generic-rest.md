---
keywords: Experience Platform;accueil;rubriques populaires;API REST générique
title: Créer une connexion Source API REST générique dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source d’API REST générique à l’aide de l’interface utilisateur de Adobe Experience Platform.
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 23%

---

# Créer une connexion source [!DNL Generic REST API] dans l’interface utilisateur

>[!NOTE]
>
> La source [!DNL Generic REST API] est en version Beta. Consultez la [&#x200B; Présentation des sources &#x200B;](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs étiquetés Beta.

Ce tutoriel décrit les étapes à suivre pour créer un connecteur source [!DNL Generic REST API] à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Collecter les informations d’identification requises

Pour accéder au compte [!DNL Generic REST API] sur Experience Platform, vous devez fournir des informations d’identification valides pour le type d’authentification de votre choix. L’API REST générique prend en charge le code d’actualisation OAuth 2 et l’authentification de base. Consultez les tableaux suivants pour plus d’informations sur les informations d’identification des deux types d’authentification pris en charge.

#### Code d’actualisation OAuth 2

| Informations d’identification | Description |
| --- | --- |
| Hôte | L’URL hôte de la source à laquelle vous effectuez votre demande. Cette valeur est requise et ne peut pas être contournée à l’aide du remplacement du paramètre de requête. |
| URL du test d’autorisation | (Facultatif) L’URL du test d’autorisation est utilisée pour valider les informations d’identification lors de la création d’une connexion de base. Si elles ne sont pas fournies, les informations d’identification sont automatiquement vérifiées à l’étape de création de la connexion source. |
| Identifiant client | (Facultatif) Identifiant client associé à votre compte utilisateur. |
| Secret client | (Facultatif) Secret client associé à votre compte utilisateur. |
| Jeton d’accès | Informations d’identification d’authentification principales utilisées pour accéder à votre application. Le jeton d’accès représente l’autorisation de votre application d’accéder à des aspects particuliers des données d’un utilisateur. Cette valeur est requise et ne peut pas être contournée à l’aide du remplacement du paramètre de requête. |
| Actualiser le jeton | (Facultatif) Jeton utilisé pour générer un nouveau jeton d’accès, lorsque le jeton d’accès a expiré. |
| URL du jeton d’accès | (Facultatif) Point d’entrée de l’URL utilisé pour récupérer votre jeton d’accès. |
| Remplacement du paramètre de requête | (Facultatif) Propriété qui vous permet de spécifier les paramètres d’informations d’identification à remplacer. |


#### Authentification de base

| Informations d’identification | Description |
| --- | --- |
| Hôte | L’URL hôte de la source à laquelle vous effectuez votre demande. |
| Nom d’utilisateur | Nom d’utilisateur correspondant à votre compte utilisateur. |
| Mot de passe | Mot de passe correspondant à votre compte utilisateur . |

## Connecter votre compte d’API REST générique

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également sélectionner la source de votre choix à l’aide de la barre de recherche.

Dans la catégorie [!UICONTROL Protocoles], sélectionnez **[!UICONTROL API REST générique]** puis **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/generic-rest/catalog.png)

La page **[!UICONTROL Se connecter à l’API REST générique]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour connecter un compte existant, sélectionnez le compte d’API REST générique auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/generic-rest/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description d’option pour votre nouveau compte [!DNL Generic REST API].

![nouveau](../../../../images/tutorials/create/generic-rest/new.png)

#### S’authentifier à l’aide du code d’actualisation OAuth 2

[!DNL Generic REST API] prend en charge le code d’actualisation OAuth 2 et l’authentification de base. Pour vous authentifier à l’aide d’une authentification OAuth2, sélectionnez **[!UICONTROL OAuth2RefreshCode]**, fournissez vos informations d’identification OAuth 2, puis sélectionnez **[!UICONTROL Se connecter à la source]**.

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### S’authentifier à l’aide de l’authentification de base

Pour utiliser l’authentification de base, sélectionnez **[!UICONTROL Authentification de base]**, indiquez votre hôte, votre nom d’utilisateur et votre mot de passe, puis sélectionnez **[!UICONTROL Se connecter à la source]**.

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte d’API REST générique. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Experience Platform](../../dataflow/protocols.md).
