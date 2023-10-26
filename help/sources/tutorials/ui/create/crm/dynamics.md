---
keywords: Experience Platform;accueil;rubriques les plus consultées;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamique
solution: Experience Platform
title: Création d’une connexion source Microsoft Dynamics dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source Microsoft Dynamics à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 31%

---

# Créer une connexion source [!DNL Microsoft Dynamics] dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Microsoft Dynamics] (ci-après dénommés &quot;[!DNL Dynamics]&quot;) connexion source à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’un [!DNL Dynamics] , vous pouvez ignorer le reste de ce document et passer au tutoriel sur [configuration d’un flux de données pour une source CRM](../../dataflow/crm.md).

### Collecter les informations d’identification requises

Pour authentifier votre [!DNL Dynamics] source, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

>[!BEGINTABS]

>[!TAB Authentification de base]

| Informations d’identification | Description |
| --- | --- |
| `serviceUri` | L’URL du service de votre [!DNL Dynamics] instance. |
| `username` | Le nom d’utilisateur de votre [!DNL Dynamics] compte utilisateur. |
| `password` | Le mot de passe de votre [!DNL Dynamics] compte . |

>[!TAB Authentification principale et clé de service]

| Informations d’identification | Description |
| --- | --- |
| `servicePrincipalId` | L’ID client de votre [!DNL Dynamics] compte . Cet identifiant est requis lors de l’utilisation de l’authentification principale et basée sur les clés du service. |
| `servicePrincipalKey` | Clé secrète principale du service. Ces informations d’identification sont requises lors de l’utilisation de l’authentification principale et basée sur les clés du service. |

>[!ENDTABS]

Pour plus d’informations sur la prise en main, reportez-vous à la section [this [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Connecter votre compte [!DNL Dynamics]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. La variable [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , [!UICONTROL CRM] catégorie, sélectionnez **[!UICONTROL Microsoft Dynamics]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Le catalogue de sources avec Microsoft Dynamics sélectionné.](../../../../images/tutorials/create/ms-dynamics/catalog.png)

La variable **[!UICONTROL Connexion au compte Microsoft Dynamics]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez la variable [!DNL Dynamics] compte que vous souhaitez utiliser, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour continuer.

![Interface du compte existant.](../../../../images/tutorials/create/ms-dynamics/existing.png) 

### Nouveau compte

>[!TIP]
>
>Une fois créé, vous ne pouvez pas modifier le type d&#39;authentification d&#39;un [!DNL Dynamics] connexion de base. Pour modifier le type d&#39;authentification, vous devez créer une nouvelle connexion de base.

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description facultative de votre nouvelle [!DNL Dynamics] compte .

![Nouvelle interface de création de compte.](../../../../images/tutorials/create/ms-dynamics/new.png)

Vous pouvez utiliser l’authentification de base ou l’authentification principale de service et l’authentification de clé lors de la création d’un [!DNL Dynamics] compte .

>[!BEGINTABS]

>[!TAB Authentification de base]

Pour créer une [!DNL Dynamics] compte avec authentification de base, sélectionnez [!UICONTROL Authentification de base] puis indiquez des valeurs pour votre [!UICONTROL Service URI], [!UICONTROL Nom d’utilisateur], et [!UICONTROL Password]. **Remarque**: authentification de base dans [!DNL Dynamics] peut être bloqué par l’authentification à deux facteurs, qui n’est actuellement pas prise en charge par Platform. Dans ce cas, il est recommandé d’utiliser l’authentification par clé pour créer un connecteur source en utilisant [!DNL Dynamics].

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]** puis accorder un certain temps pour établir le nouveau compte.

![Interface d’authentification de base.](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB Authentification principale et clé de service]

Pour créer une [!DNL Dynamics] compte avec authentification principal de service et clé, sélectionnez **[!UICONTROL Authentification principale et clé de service]** puis indiquez des valeurs pour votre [!UICONTROL ID principal du service] et [!UICONTROL Clé principale du service].

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]** puis accorder un certain temps pour établir le nouveau compte.

![Interface d’authentification des clés principales de service.](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Dynamics]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/crm.md).
