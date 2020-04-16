---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source PayPal dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 8c67ba710b486501374020ab505b04931f327c0f

---


# Création d’un connecteur source PayPal dans l’interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’assimiler des données externes sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source PayPal à l’aide de l’interface utilisateur de la plateforme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)de l’éditeur de  : Découvrez comment créer des  personnalisées à l’aide de l’interface utilisateur de l’éditeur de  de.
* [](../../../../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d&#39;une connexion de base PayPal, vous pouvez ignorer le reste de ce et passer au didacticiel sur la [configuration d&#39;un flux de données](../../dataflow/payments.md)

### Collecte des informations d’identification requises

Pour accéder à votre plateforme de compte PayPal, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | URL de l’instance PayPal. |
| `clientID` | ID client associé à votre application PayPal. |
| `clientSecret` | Le secret client associé à votre application PayPal. |

Pour plus d&#39;informations sur la prise en main, reportez-vous à ce [PayPal](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Connectez votre compte PayPal

Une fois que vous avez rassemblé vos informations d&#39;identification requises, vous pouvez suivre les étapes ci-dessous pour créer une nouvelle connexion de base entrante afin de lier votre compte PayPal à la plateforme.

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’écran *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer des connexions de base entrantes, et chaque source indique le nombre de connexions de base existantes qui lui sont associées.

Sous le  *CRM***, sélectionnez** PayPalpour afficher une barre d&#39;information sur le côté droit de votre écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou au  sa documentation. Pour créer une connexion de base entrante, sélectionnez **Connexion source**.

![catalogue](../../../../images/tutorials/create/paypal/catalog.png)

La page *Se connecter à PayPal* s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **Nouveau compte**. Sur le formulaire d&#39;entrée qui s&#39;affiche, indiquez le nom de la connexion de base, une description facultative et vos informations d&#39;identification PayPal. Lorsque vous avez terminé, sélectionnez **Se connecter** , puis accordez un peu de temps pour que la nouvelle connexion de base s’établisse.

![connecter](../../../../images/tutorials/create/paypal/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte PayPal auquel vous souhaitez vous connecter, puis sélectionnez **Suivant** pour continuer.

![existant](../../../../images/tutorials/create/paypal/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion de base à votre compte PayPal. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données afin d’importer des données de gestion de la relation client dans Platform](../../dataflow/payments.md).