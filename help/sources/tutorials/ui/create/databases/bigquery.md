---
title: Création d’une connexion Google Big Query Source dans l’interface utilisateur
description: Découvrez comment créer une connexion source Google Big Query à l’aide de l’interface utilisateur de Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 55%

---

# Créer une connexion source [!DNL Google Big Query] dans l’interface utilisateur

>[!IMPORTANT]
>
>La source [!DNL Google BigQuery] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Les connecteurs Source dans Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur de manière planifiée. Ce tutoriel décrit les étapes à suivre pour créer une connexion source [!DNL Google Big Query] à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Google BigQuery] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Pour accéder à votre compte [!DNL Google BigQuery] sur Platform, vous devez fournir les valeurs d’authentification OAuth 2.0 suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `project` | ID de projet par défaut du projet [!DNL Google BigQuery] sur lequel effectuer la requête. |
| `clientID` | La valeur d’identifiant utilisée pour générer le jeton d’actualisation. |
| `clientSecret` | La valeur secrète utilisée pour générer le jeton d’actualisation. |
| `refreshToken` | Jeton d’actualisation obtenu à partir de [!DNL Google] utilisé pour autoriser l’accès à [!DNL Google BigQuery]. |

Pour plus d&#39;informations sur ces valeurs, consultez [ce [!DNL Google BigQuery] document](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Connexion à votre compte Google BigQuery

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également sélectionner la source de votre choix à l’aide de la barre de recherche.

Sous la catégorie [!UICONTROL Bases de données], sélectionnez **[!UICONTROL Google BigQuery]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

La page **[!UICONTROL Se connecter à Google Big Query]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Google BigQuery] auquel vous souhaitez vous connecter, puis cliquez sur **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/google-big-query/existing.png)

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Google BigQuery]. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![](../../../../images/tutorials/create/google-big-query/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Google BigQuery]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/databases.md).
