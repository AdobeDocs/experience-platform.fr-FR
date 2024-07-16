---
keywords: Experience Platform;accueil;rubriques les plus consultées;zone réactive;zone réactive
solution: Experience Platform
title: Création d’une connexion HubSpot Source dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source HubSpot à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 452b7290-b9e8-4728-8b58-0e0c76bd9449
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 45%

---

# Créer une connexion source [!DNL HubSpot] dans l’interface utilisateur

Les connecteurs Source dans Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur de manière planifiée. Ce tutoriel décrit les étapes à suivre pour créer un connecteur source [!DNL HubSpot] à l’aide de l’interface utilisateur de [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL HubSpot], vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/marketing-automation.md).

### Collecter les informations d’identification requises

Pour accéder à votre compte [!DNL HubSpot] sur [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `clientId` | L’ID client associé à votre application [!DNL HubSpot]. |
| `clientSecret` | Le secret client associé à votre application [!DNL HubSpot]. |
| `accessToken` | Jeton d’accès obtenu lors de l’authentification initiale de votre intégration OAuth. |
| `refreshToken` | Jeton d’actualisation obtenu lors de l’authentification initiale de votre intégration OAuth. |

Pour plus d&#39;informations sur la prise en main, consultez ce [[!DNL HubSpot] document](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

## Connecter votre compte [!DNL HubSpot]

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL HubSpot] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Automatisation marketing]**, sélectionnez **[!UICONTROL HubSpot]**. Si c&#39;est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un nouveau connecteur [!DNL HubSpot].

![catalogue](../../../../images/tutorials/create/hubspot/catalog.png)

La page **[!UICONTROL Se connecter à HubSpot]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL HubSpot]. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** et laissez un certain temps à la nouvelle connexion pour établir.

![connect](../../../../images/tutorials/create/hubspot/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL HubSpot] auquel vous souhaitez vous connecter, puis cliquez sur **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/hubspot/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL HubSpot]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données du système d’automatisation du marketing dans [!DNL Platform]](../../dataflow/marketing-automation.md).
