---
keywords: Experience Platform;accueil;rubriques les plus consultées;ServiceNow;servicenow
solution: Experience Platform
title: Création d’une connexion source ServiceNow dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source ServiceNow à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 66c12f4d-8b0c-4bb2-910d-9e09fa364c94
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 12%

---

# Création d’une connexion source [!DNL ServiceNow] dans l’interface utilisateur

Les connecteurs source de Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer un connecteur source [!DNL ServiceNow] à l’aide de l’interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel](../../../../../xdm/tutorials/create-schema-ui.md) de l’éditeur de schémas : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL ServiceNow] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur [la configuration d’un flux de données](../../dataflow/customer-success.md)

### Collecte des informations d’identification requises

Pour accéder à votre compte [!DNL ServiceNow] sur [!DNL Platform], vous devez fournir les valeurs suivantes :

| Credential | Description |
| ---------- | ----------- |
| `endpoint` | Point d’entrée du serveur [!DNL ServiceNow]. |
| `username` | Nom d’utilisateur utilisé pour se connecter au serveur [!DNL ServiceNow] à des fins d’authentification. |
| `password` | Mot de passe de connexion au serveur [!DNL ServiceNow] pour l’authentification. |

Pour plus d’informations sur la prise en main, voir [ce [!DNL ServiceNow] document](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET).

## Connectez votre compte [!DNL ServiceNow]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL ServiceNow] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie **[!UICONTROL Succès client]**, sélectionnez **[!UICONTROL ServiceNow]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Connecter la source]** pour créer un nouveau connecteur [!DNL ServiceNow].

![](../../../../images/tutorials/create/servicenow/catalog.png)

La page **[!UICONTROL Se connecter à ServiceNow]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL ServiceNow]. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Se connecter]**, puis laissez un certain temps pour établir la nouvelle connexion.

![](../../../../images/tutorials/create/servicenow/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL ServiceNow] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/servicenow/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL ServiceNow]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans  [!DNL Platform]](../../dataflow/customer-success.md).
