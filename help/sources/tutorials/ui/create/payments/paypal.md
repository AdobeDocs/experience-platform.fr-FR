---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source PayPal dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---


# Création d’un connecteur source PayPal dans l’interface utilisateur

> [!NOTE]
> Le connecteur PayPal est en version bêta. Les fonctionnalités et la documentation peuvent être modifiées.

Les connecteurs source d’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source PayPal à l&#39;aide de l&#39;interface utilisateur de la plate-forme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d&#39;une connexion de base PayPal, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d&#39;un flux de données](../../dataflow/payments.md)

### Collecte des informations d’identification requises

Pour accéder à votre plateforme de compte PayPal, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | URL de l&#39;instance PayPal. |
| `clientID` | ID client associé à votre application PayPal. |
| `clientSecret` | Le secret client associé à votre application PayPal. |

Pour plus d&#39;informations sur la prise en main, consultez ce document [PayPal](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Connectez votre compte PayPal

Une fois que vous avez rassemblé les informations d&#39;identification requises, vous pouvez suivre les étapes ci-dessous pour créer une nouvelle connexion de base entrante afin de lier votre compte PayPal à la plateforme.

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’écran *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer des connexions de base entrantes et chaque source affiche le nombre de connexions de base existantes qui lui sont associées.

Sous la catégorie *CRM* , sélectionnez **PayPal** pour afficher une barre d&#39;information sur le côté droit de l&#39;écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou à la vue de sa documentation. Pour créer une connexion de base entrante, sélectionnez **Connexion source**.

![catalogue](../../../../images/tutorials/create/paypal/catalog.png)

La page *Se connecter à PayPal* s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **Nouveau compte**. Sur le formulaire d&#39;entrée qui s&#39;affiche, fournissez la connexion de base avec un nom, une description facultative et vos informations d&#39;identification PayPal. Lorsque vous avez terminé, sélectionnez **Se connecter** , puis accordez un certain temps à la nouvelle connexion de base pour établir.

![connecter](../../../../images/tutorials/create/paypal/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte PayPal avec lequel vous souhaitez vous connecter, puis sélectionnez **Suivant** pour continuer.

![existant](../../../../images/tutorials/create/paypal/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion de base à votre compte PayPal. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données de gestion de la relation client dans la plate-forme](../../dataflow/payments.md).