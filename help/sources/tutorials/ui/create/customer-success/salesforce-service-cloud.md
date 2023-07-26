---
title: Connexion de votre compte Salesforce Service Cloud à l’aide de l’interface utilisateur de l’Experience Platform
description: Découvrez comment connecter votre compte Salesforce Service Cloud et importer vos données de succès client dans Experience Platform à l’aide de l’interface utilisateur.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: 57cdcbd5018e7f57261f09c6bddf5e2a8dcfd0d5
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 27%

---

# Connectez-vous à [!DNL Salesforce Service Cloud] compte à Experience Platform à l’aide de l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour connecter votre [!DNL Salesforce Service Cloud] et importez vos données de succès client dans Adobe Experience Platform à l’aide de l’interface utilisateur de l’Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’un [!DNL Salesforce Service Cloud] vous pouvez ignorer le reste de ce document et passer au tutoriel sur [configuration d’un flux de données pour une réussite client](../../dataflow/customer-success.md)

### Collecter les informations d’identification requises

Pour accéder à [!DNL Salesforce Service Cloud] sur Experience Platform, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| --- | --- |
| `environmentUrl` | L’URL de la variable [!DNL Salesforce Service Cloud] instance source. |
| `username` | Nom d’utilisateur de la variable [!DNL Salesforce Service Cloud] compte utilisateur. |
| `password` | Le mot de passe du [!DNL Salesforce Service Cloud] compte utilisateur. |
| `securityToken` | Jeton de sécurité pour la variable [!DNL Salesforce Service Cloud] compte utilisateur. |
| `apiVersion` | (Facultatif) La version de l’API REST de la variable [!DNL Salesforce Service Cloud] que vous utilisez. Si ce champ n’est pas renseigné, Experience Platform utilisera automatiquement la dernière version disponible. |

Pour plus d’informations sur l’authentification, reportez-vous à la section [this [!DNL Salesforce] guide d&#39;authentification](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

## Connecter votre compte [!DNL Salesforce Service Cloud]

Une fois que vous avez rassemblé vos informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre [!DNL Salesforce] compte à Experience Platform.

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail des sources. La variable *[!UICONTROL Catalogue]* écran affiche diverses sources disponibles dans le catalogue des sources Experience Platform.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver une source spécifique à l’aide de l’option de recherche.

Sélectionner **[!UICONTROL Succès des clients]** dans la liste des catégories de sources, puis sélectionnez **[!UICONTROL Ajouter des données]** de la [!DNL Salesforce Service Cloud] carte.

![Catalogue des sources sur l’interface utilisateur Experience Platform avec la carte source Salesforce Service Cloud sélectionnée.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

La variable **[!UICONTROL Connexion à Salesforce Service Cloud]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

>[!BEGINTABS]

>[!TAB Utiliser un compte Salesforce Service Cloud existant]

Pour utiliser un compte existant, sélectionnez **[!UICONTROL Compte existant]** puis sélectionnez le compte à utiliser dans la liste qui s’affiche. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Liste des comptes Salesforce authentifiés qui existent déjà dans votre organisation.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

>[!TAB Créer un compte Salesforce Service Cloud]

Pour utiliser un nouveau compte, sélectionnez **[!UICONTROL Nouveau compte]** et indiquez un nom, une description et votre [!DNL Salesforce Service Cloud] informations d’identification d’authentification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]** et attendez quelques secondes pour que la nouvelle connexion soit établie.

![Interface dans laquelle vous pouvez créer un compte Salesforce en fournissant les informations d’authentification appropriées.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Salesforce Service Cloud]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données de succès client dans Experience Platform ;](../../dataflow/customer-success.md).
