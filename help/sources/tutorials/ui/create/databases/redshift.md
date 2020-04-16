---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Amazon Redshift dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Création d’un connecteur source Amazon Redshift dans l’interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’assimiler des données externes sur une base planifiée. Ce didacticiel décrit la procédure à suivre pour créer un connecteur source Amazon Redshift (ci-après dénommé &quot;Redshift&quot;) à l’aide de l’interface utilisateur de la plateforme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   - [Principes de base de la composition](../../../../../xdm/schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)de l’éditeur de  : Découvrez comment créer des  personnalisées à l’aide de l’interface utilisateur de l’éditeur de  de.
- [](../../../../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion de base Redshift, vous pouvez ignorer le reste de ce et passer au didacticiel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecte des informations d’identification requises

Pour accéder à votre compte Redshift sur Platform, vous devez fournir les valeurs suivantes :

| **Informations d’identification** | **Description** |
| -------------- | --------------- |
| `server` | Serveur associé à votre compte Redshift. |
| `username` | Nom d’utilisateur associé à votre compte Redshift. |
| `password` | mot de passe associé à votre compte Redshift. |
| `database` | Base de données Redshift à laquelle vous accédez. |

Pour plus d&#39;informations sur la prise en main, reportez-vous à [ce](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)Redshift.

## Connectez votre compte Redshift

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer une nouvelle connexion de base entrante afin de lier votre compte Redshift à la plateforme.

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’écran *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer des connexions de base entrantes, et chaque source indique le nombre de connexions de base existantes qui lui sont associées.

Sous le  *Bases de données* , sélectionnez **Amazon Redshift** pour afficher une barre d’informations sur le côté droit de votre écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou au  sa documentation. Pour créer une connexion de base entrante, sélectionnez **Connexion source**.

![](../../../../images/tutorials/create/redshift/sources-catalog.png)

La page *Se connecter à Amazon Redshift* s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **Nouveau compte**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification Redshift pour la connexion de base. Lorsque vous avez terminé, sélectionnez **Se connecter** , puis accordez un peu de temps pour que la nouvelle connexion de base s’établisse.

![](../../../../images/tutorials/create/redshift/new-credentials.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte Redshift avec lequel vous souhaitez vous connecter, puis sélectionnez **Suivant** pour continuer.

![](../../../../images/tutorials/create/redshift/existing-credentials.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion de base à votre compte Redshift. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/databases.md).