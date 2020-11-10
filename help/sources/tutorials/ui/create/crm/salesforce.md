---
keywords: Experience Platform;home;popular topics;Salesforce;salesforce
solution: Experience Platform
title: Création d’un connecteur source Salesforce dans l’interface utilisateur
topic: overview
type: Tutorial
description: Ce didacticiel décrit les étapes à suivre pour créer un connecteur source Salesforce à l’aide de l’interface utilisateur de la plate-forme.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 13%

---


# Create a [!DNL Salesforce] source connector in the UI

Les connecteurs source de Adobe Experience Platform permettent d’importer des données de gestion de la relation client provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur [!DNL Salesforce] source à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’un [!DNL Salesforce] compte valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données](../../dataflow/crm.md).

### Collecte des informations d’identification requises

| Informations d’identification | Description |
| ---------- | ----------- |
| `environmentUrl` | The URL of the [!DNL Salesforce] source instance. |
| `username` | Nom d’utilisateur du compte [!DNL Salesforce] d’utilisateur. |
| `password` | Mot de passe du compte [!DNL Salesforce] utilisateur. |
| `securityToken` | Jeton de sécurité pour le compte [!DNL Salesforce] utilisateur. |

Pour plus d&#39;informations sur la prise en main, consultez [ce document](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)Salesforce.

## Connecter votre [!DNL Salesforce] compte

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre [!DNL Salesforce] compte à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]** . L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Bases de données]** , sélectionnez **[!UICONTROL Salesforce]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un connecteur Salesforce.

![catalogue](../../../../images/tutorials/create/salesforce/catalog.png)

La page **[!UICONTROL Se connecter à Salesforce]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos [!DNL Salesforce] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un peu de temps à la nouvelle connexion pour établir.

![connecter](../../../../images/tutorials/create/salesforce/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL Salesforce] compte auquel vous voulez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour continuer.

![existant](../../../../images/tutorials/create/salesforce/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre [!DNL Salesforce] compte. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour y importer [!DNL Platform]](../../dataflow/crm.md)des données.