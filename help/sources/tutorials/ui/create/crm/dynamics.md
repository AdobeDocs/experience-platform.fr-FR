---
keywords: Experience Platform;accueil;rubriques populaires;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamique
solution: Experience Platform
title: Création d’une connexion source Microsoft Dynamics dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Microsoft Dynamics à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 10%

---

# Création d’une connexion source [!DNL Microsoft Dynamics] dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion source [!DNL Microsoft Dynamics] (ci-après appelée &quot;[!DNL Dynamics]&quot;) à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel](../../../../../xdm/tutorials/create-schema-ui.md) de l’éditeur de schémas : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’un compte [!DNL Dynamics] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données pour une source CRM](../../dataflow/crm.md).

### Collecte des informations d’identification requises

| Credential | Description |
| ---------- | ----------- |
| `serviceUri` | URL du service de votre instance [!DNL Dynamics]. |
| `username` | Nom d’utilisateur de votre compte d’utilisateur [!DNL Dynamics]. |
| `password` | Mot de passe de votre compte [!DNL Dynamics]. |
| `servicePrincipalId` | Identifiant client de votre compte [!DNL Dynamics]. Cet identifiant est requis lors de l’utilisation de l’authentification principale et basée sur les clés du service. |
| `servicePrincipalKey` | Clé secrète principale du service. Ces informations d’identification sont requises lors de l’utilisation de l’authentification principale et basée sur les clés du service. |

Pour plus d’informations sur la prise en main, consultez [ce [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Connectez votre compte [!DNL Dynamics]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Dynamics] à Platform.

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie **[!UICONTROL CRM]** , sélectionnez **[!UICONTROL Microsoft Dynamics]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un nouveau connecteur [!DNL Dynamics].

![catalogue](../../../../images/tutorials/create/ms-dynamics/catalog.png)

La page **[!UICONTROL Se connecter à Dynamics]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom et une description facultative pour votre nouveau compte [!DNL Dynamics].

Le connecteur [!DNL Dynamics] fournit différents types d’authentification pour l’accès. Sous [!UICONTROL Authentification de compte], sélectionnez **[!UICONTROL Authentification de base]** pour utiliser des informations d’identification basées sur un mot de passe.

Une fois l’opération terminée, sélectionnez **[!UICONTROL Se connecter à la source]**, puis laissez un certain temps au nouveau compte pour établir.

![authentification de base](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

Vous pouvez également sélectionner **[!UICONTROL Service-principal et authentification par clé]** et connecter votre compte [!DNL Dynamics] en utilisant une combinaison de [!UICONTROL Service principal ID] et [!UICONTROL Clé principale de service].

>[!IMPORTANT]
>
> L’authentification de base dans [!DNL Dynamics] peut être bloquée par l’authentification à deux facteurs, qui n’est actuellement pas prise en charge par Platform. Dans ce cas, il est recommandé d’utiliser l’authentification par clé pour créer un connecteur source à l’aide de [!DNL Dynamics].

![authentification par clé](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Credential | Description |
| ---------- | ----------- |
| [!UICONTROL ID principal du service] | Identifiant client de votre compte [!DNL Dynamics]. Cet identifiant est requis lors de l’utilisation de l’authentification principale et basée sur les clés du service. |
| [!UICONTROL Clé principale du service] | Clé secrète principale du service. Ces informations d’identification sont requises lors de l’utilisation de l’authentification principale et basée sur les clés du service. |

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Dynamics] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour continuer.

![existant](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Dynamics]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/crm.md).
