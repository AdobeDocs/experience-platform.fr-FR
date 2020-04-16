---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source de publicités Google dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 3b5821d641d35e1190ea9fecfd4def5beced6ecc

---


# Création d’un connecteur source de publicités Google dans l’interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’assimiler des données externes sur une base planifiée. Ce didacticiel décrit la procédure à suivre pour créer un connecteur source de publicités Google à l’aide de l’interface utilisateur de la plate-forme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)de l’éditeur de  : Découvrez comment créer des  personnalisées à l’aide de l’interface utilisateur de l’éditeur de  de.
* [](../../../../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion de base de publicités Google, vous pouvez ignorer le reste de ce et passer au didacticiel sur la [configuration d’un flux de données.](../../dataflow/payments.md)

### Collecte des informations d’identification requises

Pour accéder à votre plateforme de compte Google Ads, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `clientCustomerId` | ID client du compte Publicités. |
| `developerToken` | Jeton de développeur associé au compte du gestionnaire. |
| `refreshToken` | Jeton d’actualisation obtenu auprès de Google pour autoriser l’accès aux publicités. |
| `clientId` | ID client de l’application Google utilisé pour acquérir le jeton d’actualisation. |
| `clientSecret` | Le secret client de l’application google utilisé pour acquérir le jeton d’actualisation. |

Pour plus d&#39;informations sur la prise en main, reportez-vous à ce [Google Publicités](https://developers.google.com/adwords/api/docs/guides/authentication).

## Connectez votre compte Publicités Google.

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer une nouvelle connexion de base entrante afin de lier votre compte Google Ads à la plateforme.

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’écran *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer des connexions de base entrantes, et chaque source indique le nombre de connexions de base existantes qui lui sont associées.

Sous le  *Publicité* , sélectionnez Publicités **** Google pour afficher une barre d’informations sur le côté droit de votre écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou au  sa documentation. Pour créer une connexion de base entrante, sélectionnez **Connexion source**.

![catalogue](../../../../images/tutorials/create/ads/catalog.png)

La page *Se connecter à Google Publicités* s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **Nouveau compte**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification Google Ads pour la connexion de base. Lorsque vous avez terminé, sélectionnez **Se connecter** , puis accordez un peu de temps pour que la nouvelle connexion de base s’établisse.

![connecter](../../../../images/tutorials/create/ads/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte Google Publicités avec lequel vous souhaitez vous connecter, puis sélectionnez **Suivant** pour continuer.

![existant](../../../../images/tutorials/create/ads/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion de base à votre compte Google Publicités. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données publicitaires dans Platform](../../dataflow/advertising.md).