---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source HubSpot dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---


# Création d’un connecteur [!DNL HubSpot] source dans l’interface utilisateur

> [!NOTE]
> Le [!DNL HubSpot] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source dans l’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur [!DNL HubSpot] source à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants de l&#39;Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion de [!DNL HubSpot] base, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux](../../dataflow/marketing-automation.md)de données d’automatisation marketing.

### Collecte des informations d’identification requises

Pour accéder à votre [!DNL HubSpot] compte [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `clientId` | ID client associé à votre [!DNL HubSpot] application. |
| `clientSecret` | Le secret client associé à votre [!DNL HubSpot] application. |
| `accessToken` | jeton d&#39;accès obtenu lors de l’authentification initiale de l’intégration OAuth. |
| `refreshToken` | Jeton d’actualisation obtenu lors de l’authentification initiale de votre intégration OAuth. |

Pour plus d&#39;informations sur la prise en main, reportez-vous à ce document [](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)HubSpot.

## Connecter votre [!DNL HubSpot] compte

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer une nouvelle connexion de base entrante afin de lier votre [!DNL HubSpot] compte à [!DNL Platform].

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">l’Adobe Experience Platform</a> , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]* . L’écran *[!UICONTROL Catalogue]* affiche diverses sources pour lesquelles vous pouvez créer des connexions de base entrantes et chaque source affiche le nombre de connexions de base existantes qui lui sont associées.

Sous la catégorie d’automatisation ** marketing, sélectionnez **[!UICONTROL HubSpot]** pour afficher une barre d’informations sur le côté droit de l’écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou à la vue de sa documentation. Pour créer une connexion de base entrante, sélectionnez **[!UICONTROL Connexion source]**.

![catalogue](../../../../images/tutorials/create/hubspot/catalog.png)

La page *[!UICONTROL Se connecter à HubSpot]* s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos [!DNL HubSpot] informations d’identification pour la connexion de base. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un certain temps à la nouvelle connexion de base pour établir.

![connecter](../../../../images/tutorials/create/hubspot/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL HubSpot] compte auquel vous voulez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/hubspot/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion de base à votre [!DNL HubSpot] compte. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer les données du système d’automatisation marketing dans Platform](../../dataflow/marketing-automation.md).