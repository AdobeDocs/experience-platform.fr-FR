---
title: Connexion de votre compte Salesforce à l’aide de l’interface utilisateur Experience Platform
description: Découvrez comment connecter votre compte Salesforce et importer vos données CRM dans Experience Platform à l’aide de l’interface utilisateur.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: a5ecd4ab1c543805870b846cfe0fccc5474333d4
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 23%

---

# Connectez-vous à [!DNL Salesforce] compte à Experience Platform à l’aide de l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour connecter votre [!DNL Salesforce] et importez vos données CRM dans Adobe Experience Platform à l’aide de l’interface utilisateur de l’Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une authentification [!DNL Salesforce] , vous pouvez ignorer le reste de ce document et passer au tutoriel sur [configuration d’un flux de données pour les données CRM](../../dataflow/crm.md).

### Collecter les informations d’identification requises {#gather-required-credentials}

Pour authentifier votre [!DNL Salesforce] par rapport à Experience Platform, vous devez fournir des valeurs qui correspondent aux [!DNL Salesforce] informations d’identification :

| Informations d’identification | Description |
| --- | --- |
| `environmentUrl` | L’URL de la variable [!DNL Salesforce] instance source. |
| `username` | Nom d’utilisateur de la variable [!DNL Salesforce] compte utilisateur. |
| `password` | Le mot de passe du [!DNL Salesforce] compte utilisateur. |
| `securityToken` | Jeton de sécurité pour la variable [!DNL Salesforce] compte utilisateur. |
| `apiVersion` | (Facultatif) La version de l’API REST de la variable [!DNL Salesforce] que vous utilisez. La valeur de la version d’API doit être formatée avec une valeur décimale. Par exemple, si vous utilisez la version d’API `52`, vous devez saisir la valeur sous la forme `52.0` Si ce champ n’est pas renseigné, Experience Platform utilisera automatiquement la dernière version disponible. |

Pour plus d’informations sur l’authentification, reportez-vous à la section [this [!DNL Salesforce] guide d&#39;authentification](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

Une fois que vous avez rassemblé vos informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour connecter votre [!DNL Salesforce] compte à Experience Platform.

## Connecter votre compte [!DNL Salesforce]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail des sources. La variable *[!UICONTROL Catalogue]* écran affiche diverses sources disponibles dans le catalogue des sources Experience Platform.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver une source spécifique à l’aide de l’option de recherche.

Sélectionner **[!UICONTROL CRM]** dans la liste des catégories de sources, puis sélectionnez **[!UICONTROL Ajouter des données]** de la [!DNL Salesforce] carte.

![Catalogue des sources sur l’interface utilisateur Experience Platform avec la carte source Salesforce sélectionnée.](../../../../images/tutorials/create/salesforce/catalog.png)

La variable **[!UICONTROL Connexion à Salesforce]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

>[!BEGINTABS]

>[!TAB Utiliser un compte Salesforce existant]

Pour utiliser un compte existant, sélectionnez **[!UICONTROL Compte existant]** puis sélectionnez le compte à utiliser dans la liste qui s’affiche. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Liste des comptes Salesforce authentifiés qui existent déjà dans votre organisation.](../../../../images/tutorials/create/salesforce/existing.png)

>[!TAB Créer un compte Salesforce]

Pour utiliser un nouveau compte, sélectionnez **[!UICONTROL Nouveau compte]** et indiquez un nom, une description et votre [!DNL Salesforce] informations d’identification d’authentification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]** et attendez quelques secondes pour que la nouvelle connexion soit établie.

![Interface dans laquelle vous pouvez créer un compte Salesforce en fournissant les informations d’authentification appropriées.](../../../../images/tutorials/create/salesforce/new.png)

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Salesforce]. Vous pouvez maintenant passer au tutoriel suivant et [configuration d’un flux de données pour importer des données [!DNL Platform]](../../dataflow/crm.md).
