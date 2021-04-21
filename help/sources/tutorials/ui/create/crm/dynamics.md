---
keywords: Experience Platform;accueil;rubriques populaires;Microsoft Dynamics;microsoft dynamic;Dynamics;Dynamics;dynamic
solution: Experience Platform
title: Création d'une connexion Microsoft Dynamics Source dans l'interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Microsoft Dynamics à l'aide de l'interface utilisateur Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 10%

---

# Créer une connexion source [!DNL Microsoft Dynamics] dans l’interface utilisateur

Ce didacticiel décrit les étapes à suivre pour créer une connexion source [!DNL Microsoft Dynamics] (ci-après appelée &quot;[!DNL Dynamics]&quot;) à l’aide de l’interface utilisateur Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d&#39;un compte [!DNL Dynamics] valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur [la configuration d&#39;un flux de données pour une source de gestion de la relation client](../../dataflow/crm.md).

### Collecte des informations d’identification requises

| Informations d’identification | Description |
| ---------- | ----------- |
| `serviceUri` | URL de service de votre instance [!DNL Dynamics]. |
| `username` | Nom d’utilisateur de votre compte d’utilisateur [!DNL Dynamics]. |
| `password` | Mot de passe de votre compte [!DNL Dynamics]. |
| `servicePrincipalId` | ID client de votre compte [!DNL Dynamics]. Cet identifiant est requis lors de l’utilisation de l’authentification principale et de l’authentification par clé. |
| `servicePrincipalKey` | Clé secrète principale du service. Ces informations d’identification sont requises lors de l’utilisation de l’authentification principale de service et de l’authentification par clé. |

Pour plus d&#39;informations sur la prise en main, consultez [ce [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Connectez votre compte [!DNL Dynamics]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Dynamics] à la plateforme.

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail [!UICONTROL Sources]. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL CRM]**, sélectionnez **[!UICONTROL Microsoft Dynamics]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter les données]** pour créer un connecteur [!DNL Dynamics].

![catalogue](../../../../images/tutorials/create/ms-dynamics/catalog.png)

La page **[!UICONTROL Se connecter à Dynamics]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d&#39;entrée qui s&#39;affiche, indiquez un nom et une description facultative pour votre nouveau compte [!DNL Dynamics].

Le connecteur [!DNL Dynamics] fournit différents types d&#39;authentification pour l&#39;accès. Sous [!UICONTROL Authentification du compte], sélectionnez **[!UICONTROL Authentification de base]** pour utiliser des informations d’identification basées sur un mot de passe.

Une fois terminé, sélectionnez **[!UICONTROL Se connecter à la source]**, puis attendez un peu de temps pour que le nouveau compte s&#39;établisse.

![authentification de base](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

Vous pouvez également sélectionner **[!UICONTROL Authentification du principal de service et de la clé]** et connecter votre compte [!DNL Dynamics] en utilisant une combinaison de [!UICONTROL ID principal de service] et [!UICONTROL clé principale de service].

>[!IMPORTANT]
>
> L&#39;authentification de base dans [!DNL Dynamics] peut être bloquée par l&#39;authentification à deux facteurs, qui n&#39;est actuellement pas prise en charge par Platform. Dans ce cas, il est recommandé d&#39;utiliser l&#39;authentification par clé pour créer un connecteur source à l&#39;aide de [!DNL Dynamics].

![authentification par clé](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Informations d’identification | Description |
| ---------- | ----------- |
| [!UICONTROL ID principal du service] | ID client de votre compte [!DNL Dynamics]. Cet identifiant est requis lors de l’utilisation de l’authentification principale et de l’authentification par clé. |
| [!UICONTROL Clé principale de service] | Clé secrète principale du service. Ces informations d’identification sont requises lors de l’utilisation de l’authentification principale de service et de l’authentification par clé. |

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Dynamics] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour continuer.

![existant](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte [!DNL Dynamics]. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/crm.md).
