---
title: Connexion de votre compte Salesforce à l’aide de l’interface utilisateur Experience Platform
description: Découvrez comment connecter votre compte Salesforce et importer vos données CRM dans Experience Platform à l’aide de l’interface utilisateur.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: ae322ee421edd73cd5a3fb8499267cd417491318
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 19%

---

# Connectez votre compte [!DNL Salesforce] à un Experience Platform à l’aide de l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour connecter votre compte [!DNL Salesforce] et importer vos données CRM dans Adobe Experience Platform à l’aide de l’interface utilisateur Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’un compte [!DNL Salesforce] authentifié, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données pour les données CRM](../../dataflow/crm.md).

### Collecter les informations d’identification requises {#gather-required-credentials}

La source [!DNL Salesforce] prend en charge l’authentification de base et les informations d’identification du client OAuth2.

>[!BEGINTABS]

>[!TAB Authentification de base]

Vous devez fournir des valeurs pour les informations d’identification suivantes afin de connecter votre compte [!DNL Salesforce] à l’aide de l’authentification de base.

| Informations d’identification | Description |
| --- | --- |
| URL de l’environnement | URL de l’instance source [!DNL Salesforce]. Le format de l’URL d’environnement est `https://[domain].my.salesforce.com`. |
| Nom d’utilisateur | Nom d’utilisateur du compte utilisateur [!DNL Salesforce]. |
| Mot de passe | Mot de passe du compte utilisateur [!DNL Salesforce]. |
| Jeton de sécurité | Jeton de sécurité pour le compte utilisateur [!DNL Salesforce]. |
| Version de l’API | (Facultatif) La version de l’API REST de l’instance [!DNL Salesforce] que vous utilisez. La valeur de la version de l’API doit être formatée avec une valeur décimale. Par exemple, si vous utilisez la version d’API `52`, vous devez saisir la valeur `52.0`. Si ce champ n’est pas renseigné, Experience Platform utilisera automatiquement la dernière version disponible. |

Pour plus d&#39;informations sur l&#39;authentification, consultez [ce [!DNL Salesforce] guide d&#39;authentification](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB Informations d’identification du client OAuth2]

Vous devez fournir des valeurs pour les informations d’identification suivantes afin de connecter votre compte [!DNL Salesforce] à l’aide des informations d’identification du client OAuth2.

| Informations d’identification | Description |
| --- | --- |
| URL de l’environnement | URL de l’instance source [!DNL Salesforce]. Le format de l’URL d’environnement est `https://[domain].my.salesforce.com`. |
| Identifiant client | L’ID client est utilisé en tandem avec le secret client dans le cadre de l’authentification OAuth2. Ensemble, l’ID client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application sur [!DNL Salesforce]. |
| Secret client | Le secret client est utilisé en tandem avec l’ID client dans le cadre de l’authentification OAuth2. Ensemble, l’ID client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application sur [!DNL Salesforce]. |
| Version de l’API | Version de l’API REST de l’instance [!DNL Salesforce] que vous utilisez. La valeur de la version de l’API doit être formatée avec une valeur décimale. Par exemple, si vous utilisez la version d’API `52`, vous devez saisir la valeur `52.0`. Si ce champ n’est pas renseigné, Experience Platform utilisera automatiquement la dernière version disponible. |

Pour plus d’informations sur l’utilisation d’OAuth pour [!DNL Salesforce], consultez le [[!DNL Salesforce] guide sur les flux d’autorisation OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Une fois que vous avez rassemblé vos informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour connecter votre compte [!DNL Salesforce] à Experience Platform.

## Connecter votre compte [!DNL Salesforce]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sélectionnez **[!DNL Salesforce]** sous la catégorie *[!UICONTROL CRM]*, puis sélectionnez **[!UICONTROL Ajouter des données]**.

>[!TIP]
>
>Les sources dans le catalogue des sources affichent l’option **[!UICONTROL Configurer]** lorsqu’une source donnée n’a pas encore de compte authentifié. Une fois qu’il existe un compte authentifié, cette option devient **[!UICONTROL Ajouter des données]**.

![Catalogue des sources sur l’interface utilisateur Experience Platform avec la carte source Salesforce sélectionnée.](../../../../images/tutorials/create/salesforce/catalog.png)

La page **[!UICONTROL Se connecter à Salesforce]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Utiliser un compte existant

Pour utiliser un compte existant, sélectionnez **[!UICONTROL Compte existant]** , puis le compte à utiliser dans la liste qui s&#39;affiche. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Liste des comptes Salesforce authentifiés qui existent déjà dans votre organisation.](../../../../images/tutorials/create/salesforce/existing.png)

### Création d’un compte

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]** et fournissez un nom et une description pour votre nouveau compte [!DNL Salesforce].

![Interface dans laquelle vous pouvez créer un compte Salesforce en fournissant les informations d’authentification appropriées.](../../../../images/tutorials/create/salesforce/new.png)

Sélectionnez ensuite le type d&#39;authentification que vous souhaitez utiliser pour votre nouveau compte.

>[!BEGINTABS]

>[!TAB Authentification de base]

Pour une authentification de base, sélectionnez **[!UICONTROL Authentification de base]** , puis fournissez les valeurs des informations d’identification suivantes :

* URL de l’environnement
* Nom d’utilisateur
* Mot de passe
* Version de l’API (facultatif)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]**.

![Interface d’authentification de base pour la création de compte Salesforce.](../../../../images/tutorials/create/salesforce/basic.png)

>[!TAB Informations d’identification du client OAuth2]

Pour les informations d’identification du client OAuth 2, sélectionnez **[!UICONTROL OAuth2 Client Credential]**, puis fournissez des valeurs pour les informations d’identification suivantes :

* URL de l’environnement
* Identifiant client
* Secret client
* Version de l’API

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]**.

![Interface OAuth pour la création de compte Salesforce.](../../../../images/tutorials/create/salesforce/oauth2.png)

>[!ENDTABS]

### Ignorer l’aperçu des données d’exemple {#skip-preview-of-sample-data}

Au cours de l’étape de sélection des données, vous pouvez rencontrer un délai d’expiration lors de l’ingestion de tables volumineuses ou de fichiers de données. Vous pouvez ignorer l’aperçu des données pour contourner le délai d’expiration et tout en affichant votre schéma, bien que sans exemple de données. Pour ignorer l’aperçu des données, activez la bascule **[!UICONTROL Ignorer l’aperçu des données d’exemple]** .

Le reste du workflow restera le même. Le seul avertissement à retenir est que l’absence de prévisualisation des données peut empêcher la validation automatique des champs calculés et obligatoires lors de l’étape de mappage. Vous devrez ensuite valider manuellement ces champs lors du mappage.

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Salesforce]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans [!DNL Platform]](../../dataflow/crm.md).
