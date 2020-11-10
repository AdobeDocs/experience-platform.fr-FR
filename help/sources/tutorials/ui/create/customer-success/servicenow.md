---
keywords: Experience Platform;home;popular topics;ServiceNow;servicenow
solution: Experience Platform
title: Création d’un connecteur source ServiceNow dans l’interface utilisateur
topic: overview
type: Tutorial
description: Ce didacticiel décrit les étapes à suivre pour créer un connecteur source ServiceNow à l’aide de l’interface utilisateur de la plate-forme.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 14%

---


# Create a [!DNL ServiceNow] source connector in the UI

>[!NOTE]
>
>Le [!DNL ServiceNow] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur [!DNL ServiceNow] source à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’une [!DNL ServiceNow] connexion valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données.](../../dataflow/customer-success.md)

### Collecte des informations d’identification requises

Pour accéder à votre [!DNL ServiceNow] compte [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `endpoint` | The endpoint of the [!DNL ServiceNow] server. |
| `username` | Nom d’utilisateur utilisé pour la connexion au [!DNL ServiceNow] serveur pour l’authentification. |
| `password` | Mot de passe de connexion au [!DNL ServiceNow] serveur pour l’authentification. |

Pour plus d&#39;informations sur la prise en main, reportez-vous à [ [!DNL ServiceNow] ce document](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET).

## Connecter votre [!DNL ServiceNow] compte

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre [!DNL ServiceNow] compte à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]** . L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie de réussite **** du client, sélectionnez **[!UICONTROL ServiceNow]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Connecter la source]** pour créer un nouveau [!DNL ServiceNow] connecteur.

![](../../../../images/tutorials/create/servicenow/catalog.png)

La page **[!UICONTROL Se connecter à ServiceNow]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos [!DNL ServiceNow] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un peu de temps à la nouvelle connexion pour établir.

![](../../../../images/tutorials/create/servicenow/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL ServiceNow] compte auquel vous voulez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/servicenow/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre [!DNL ServiceNow] compte. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour y importer [!DNL Platform]](../../dataflow/customer-success.md)des données.
