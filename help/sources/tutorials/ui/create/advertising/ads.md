---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Google AdWords dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# Création d’un connecteur [!DNL Google AdWords] source dans l’interface utilisateur

>[!NOTE]
>Le [!DNL Google AdWords] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source dans l’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur [!DNL Google AdWords] source à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants de l&#39;Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une [!DNL Google AdWords] connexion, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données.](../../dataflow/payments.md)

### Collecte des informations d’identification requises

Pour accéder à votre [!DNL Google AdWords] compte [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `clientCustomerId` | ID client du compte AdWords. |
| `developerToken` | Jeton de développeur associé au compte de gestionnaire. |
| `refreshToken` | Jeton d’actualisation obtenu à partir [!DNL Google] de pour autoriser l’accès à AdWords. |
| `clientId` | ID client de l’ [!DNL Google] application utilisée pour acquérir le jeton d’actualisation. |
| `clientSecret` | Le secret client de l’ [!DNL Google] application utilisée pour acquérir le jeton d’actualisation. |

Pour plus d&#39;informations sur la prise en main, reportez-vous à ce document [AdWords de](https://developers.google.com/adwords/api/docs/guides/authentication)Google.

## Connecter votre [!DNL Google AdWords] compte

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer une nouvelle connexion de base entrante afin de lier votre [!DNL Google AdWords] compte à [!DNL Platform].

Connectez-vous à [l’Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]* . L’écran *[!UICONTROL Catalogue]* affiche diverses sources pour lesquelles vous pouvez créer des connexions de base entrantes et chaque source affiche le nombre de connexions de base existantes qui lui sont associées.

Sous la catégorie *[!UICONTROL Publicité]* , sélectionnez **[!UICONTROL Google AdWords]** pour afficher une barre d’informations sur le côté droit de l’écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou à la vue de sa documentation. Pour créer une connexion de base entrante, sélectionnez **[!UICONTROL Connexion source]**.

![catalogue](../../../../images/tutorials/create/ads/catalog.png)

La page *[!UICONTROL Se connecter à Google AdWords]* s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos [!DNL Google AdWords] informations d’identification pour la connexion de base. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un certain temps à la nouvelle connexion de base pour établir.

![connecter](../../../../images/tutorials/create/ads/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL Google AdWords] compte auquel vous voulez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/ads/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion de base à votre [!DNL Google AdWords] compte. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données publicitaires dans Platform](../../dataflow/advertising.md).