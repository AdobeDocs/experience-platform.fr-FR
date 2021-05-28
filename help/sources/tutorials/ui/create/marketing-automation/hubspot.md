---
keywords: Experience Platform;accueil;rubriques les plus consultées;zone réactive;zone réactive
solution: Experience Platform
title: Création d’une connexion à la source HubSpot dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source HubSpot à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 452b7290-b9e8-4728-8b58-0e0c76bd9449
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 12%

---

# Création d’une connexion source [!DNL HubSpot] dans l’interface utilisateur

Les connecteurs source de Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer un connecteur source [!DNL HubSpot] à l’aide de l’interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel](../../../../../xdm/tutorials/create-schema-ui.md) de l’éditeur de schémas : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL HubSpot], vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/marketing-automation.md).

### Collecte des informations d’identification requises

Pour accéder à votre compte [!DNL HubSpot] sur [!DNL Platform], vous devez fournir les valeurs suivantes :

| Credential | Description |
| ---------- | ----------- |
| `clientId` | ID client associé à votre application [!DNL HubSpot]. |
| `clientSecret` | Le secret client associé à votre application [!DNL HubSpot]. |
| `accessToken` | Jeton d’accès obtenu lors de l’authentification initiale de votre intégration OAuth. |
| `refreshToken` | Jeton d’actualisation obtenu lors de l’authentification initiale de votre intégration OAuth. |

Pour plus d’informations sur la prise en main, consultez ce [[!DNL HubSpot] document](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

## Connectez votre compte [!DNL HubSpot]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL HubSpot] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie **[!UICONTROL Automatisation marketing]**, sélectionnez **[!UICONTROL HubSpot]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un nouveau connecteur [!DNL HubSpot].

![catalogue](../../../../images/tutorials/create/hubspot/catalog.png)

La page **[!UICONTROL Se connecter à HubSpot]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL HubSpot]. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Se connecter]**, puis laissez un certain temps pour établir la nouvelle connexion.

![connect](../../../../images/tutorials/create/hubspot/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL HubSpot] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/hubspot/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL HubSpot]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données du système d’automatisation du marketing dans  [!DNL Platform]](../../dataflow/marketing-automation.md).
