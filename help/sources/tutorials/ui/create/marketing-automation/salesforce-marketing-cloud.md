---
keywords: Experience Platform;accueil;rubriques les plus consultées;Salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: Création d’une connexion source de Marketing Cloud Salesforce dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source de Marketing Cloud Salesforce à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 12%

---

# Création d’une connexion source [!DNL Salesforce Marketing Cloud] dans l’interface utilisateur

>[!NOTE]
>
> La source [!DNL Salesforce Marketing Cloud] est en version bêta. Voir la [présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources marquées bêta.

Les connecteurs source de Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes de création d’un connecteur source [!DNL Salesforce Marketing Cloud] à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel](../../../../../xdm/tutorials/create-schema-ui.md) de l’éditeur de schémas : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Salesforce Marketing Cloud], vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/marketing-automation.md).

### Collecte des informations d’identification requises

Pour accéder à votre compte [!DNL Salesforce Marketing Cloud] sur Platform, vous devez fournir les valeurs suivantes :

| Credential | Description |
| ---------- | ----------- |
| `host` | Serveur hôte de votre application. Il s’agit souvent de votre sous-domaine. |
| `clientId` | ID client associé à votre application [!DNL Salesforce Marketing Cloud]. |
| `clientSecret` | Le secret client associé à votre application [!DNL Salesforce Marketing Cloud]. |

Pour plus d’informations sur la prise en main, consultez ce [[!DNL Salesforce Marketing Cloud] document](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Connectez votre compte [!DNL Salesforce Marketing Cloud]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Salesforce Marketing Cloud] à Platform.

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également utiliser la barre de recherche pour affiner les connecteurs affichés.

Dans la catégorie [!UICONTROL Automatisation marketing], sélectionnez **[!UICONTROL Marketing Cloud Salesforce]**, puis **[!UICONTROL Configurer]**.

![catalogue](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

La page **[!UICONTROL Se connecter au Marketing Cloud Salesforce]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Salesforce Marketing Cloud]. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Se connecter]**, puis laissez un certain temps pour établir la nouvelle connexion.

![new](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Salesforce Marketing Cloud] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Salesforce Marketing Cloud]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données du système d’automatisation du marketing dans Platform](../../dataflow/marketing-automation.md).
