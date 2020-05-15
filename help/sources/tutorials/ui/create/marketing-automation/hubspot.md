---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source HubSpot dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# Création d’un connecteur source HubSpot dans l’interface utilisateur

> [!NOTE]
> Le connecteur HubSpot est en version bêta. Les fonctionnalités et la documentation peuvent être modifiées.

Les connecteurs source d’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source HubSpot à l’aide de l’interface utilisateur de la plate-forme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion de base HubSpot, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux](../../dataflow/marketing-automation.md)de données d’automatisation marketing.

### Collecte des informations d’identification requises

Pour accéder à votre compte HubSpot sur la plate-forme, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `clientId` | ID client associé à votre application HubSpot. |
| `clientSecret` | Le secret client associé à votre application HubSpot. |
| `accessToken` | jeton d&#39;accès obtenu lors de l’authentification initiale de l’intégration OAuth. |
| `refreshToken` | Jeton d’actualisation obtenu lors de l’authentification initiale de votre intégration OAuth. |

Pour plus d&#39;informations sur la prise en main, reportez-vous à ce document [](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)HubSpot.

## Connectez votre compte HubSpot.

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer une nouvelle connexion de base entrante afin de lier votre compte HubSpot à la plate-forme.

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’écran *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer des connexions de base entrantes et chaque source affiche le nombre de connexions de base existantes qui lui sont associées.

Sous la catégorie d’automatisation ** marketing, sélectionnez **HubSpot** pour afficher une barre d’informations sur le côté droit de l’écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou à la vue de sa documentation. Pour créer une connexion de base entrante, sélectionnez **Connexion source**.

![catalogue](../../../../images/tutorials/create/hubspot/catalog.png)

La page *Se connecter à HubSpot* s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **Nouveau compte**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification HubSpot pour la connexion de base. Lorsque vous avez terminé, sélectionnez **Se connecter** , puis accordez un certain temps à la nouvelle connexion de base pour établir.

![connecter](../../../../images/tutorials/create/hubspot/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte HubSpot avec lequel vous souhaitez vous connecter, puis sélectionnez **Suivant** pour continuer.

![existant](../../../../images/tutorials/create/hubspot/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion de base à votre compte HubSpot. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données afin d’importer les données du système d’automatisation du marketing dans la plate-forme](../../dataflow/marketing-automation.md).