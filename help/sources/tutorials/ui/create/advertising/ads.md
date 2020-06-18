---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Google AdWords dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: b9e9207741044f118d53ab8eb3d3d6cd7451132d
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---


# Création d’un connecteur source Google AdWords dans l’interface utilisateur

>[!NOTE]
>Le connecteur Google AdWords est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source dans l’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit la procédure à suivre pour créer un connecteur source Google AdWords à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants de l&#39;Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion Google AdWords, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données.](../../dataflow/payments.md)

### Collecte des informations d’identification requises

Pour accéder à votre compte Google AdWords Platform, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `clientCustomerId` | ID client du compte AdWords. |
| `developerToken` | Jeton de développeur associé au compte de gestionnaire. |
| `refreshToken` | Jeton d’actualisation obtenu auprès de Google pour autoriser l’accès à AdWords. |
| `clientId` | ID client de l’application Google utilisé pour acquérir le jeton d’actualisation. |
| `clientSecret` | Le secret client de l&#39;application google utilisé pour acquérir le jeton d&#39;actualisation. |

Pour plus d&#39;informations sur la prise en main, reportez-vous à ce document [AdWords de](https://developers.google.com/adwords/api/docs/guides/authentication)Google.

## Connectez votre compte Google AdWords

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer une nouvelle connexion de base entrante afin de lier votre compte Google AdWords à Platform.

Connectez-vous à [l’Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’écran *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer des connexions de base entrantes et chaque source affiche le nombre de connexions de base existantes qui lui sont associées.

Sous la catégorie *Publicité* , sélectionnez **Google AdWords** pour afficher une barre d’informations sur le côté droit de l’écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou à la vue de sa documentation. Pour créer une connexion de base entrante, sélectionnez **Connexion source**.

![catalogue](../../../../images/tutorials/create/ads/catalog.png)

La page *Se connecter à Google AdWords* s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **Nouveau compte**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification Google AdWords pour la connexion de base. Lorsque vous avez terminé, sélectionnez **Se connecter** , puis accordez un certain temps à la nouvelle connexion de base pour établir.

![connecter](../../../../images/tutorials/create/ads/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte Google AdWords avec lequel vous souhaitez vous connecter, puis sélectionnez **Suivant** pour continuer.

![existant](../../../../images/tutorials/create/ads/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion de base à votre compte Google AdWords. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données publicitaires dans Platform](../../dataflow/advertising.md).