---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Création d’un connecteur source Microsoft Dynamics dans l’interface utilisateur
topic: overview
type: Tutorial
description: Ce didacticiel décrit les étapes à suivre pour créer un connecteur source Microsoft Dynamics (ci-après appelé "Dynamics") à l'aide de l'interface utilisateur de la plate-forme.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 10%

---


# Create a [!DNL Microsoft Dynamics] source connector in the UI

Les connecteurs source de Adobe Experience Platform permettent d’importer des données de gestion de la relation client provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source [!DNL Microsoft Dynamics] (ci-après dénommé &quot;[!DNL Dynamics]&quot;) à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model] (XDM) Système](../../../../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [[ !Profil client en temps réel DNL]](../../../../../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’un [!DNL Dynamics] compte valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données](../../dataflow/crm.md).

### Collecte des informations d’identification requises

| Informations d’identification | Description |
| ---------- | ----------- |
| `serviceUri` | URL de service de votre [!DNL Dynamics] instance. |
| `username` | Nom d’utilisateur de votre compte [!DNL Dynamics] d’utilisateur. |
| `password` | Mot de passe de votre [!DNL Dynamics] compte. |

Pour plus d&#39;informations sur la prise en main, reportez-vous à [ [!DNL Dynamics] ce document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Connecter votre [!DNL Dynamics] compte

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre [!DNL Dynamics] compte à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]** . L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Bases de données]** , sélectionnez **[!UICONTROL Dynamics]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un nouveau [!DNL Dynamics] connecteur.

![catalogue](../../../../images/tutorials/create/ms-dynamics/catalog.png)

La page **[!UICONTROL Se connecter à Dynamics]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos [!DNL Dynamics] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un peu de temps à la nouvelle connexion pour établir.

![connecter](../../../../images/tutorials/create/ms-dynamics/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL Dynamics] compte auquel vous voulez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour continuer.

![existant](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre [!DNL Dynamics] compte. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour y importer [!DNL Platform]](../../dataflow/crm.md)des données.