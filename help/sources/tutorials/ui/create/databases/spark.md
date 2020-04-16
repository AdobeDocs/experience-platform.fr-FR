---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d'Apache Spark sur le connecteur source Azure HDInsights dans l'interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: ae059f93f09dbbae4f1ef46f68901071afba9729

---


# Création d&#39;Apache Spark sur le connecteur source Azure HDInsights dans l&#39;interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’assimiler des données externes sur une base planifiée. Ce didacticiel décrit la procédure à suivre pour créer un Apache Spark sur un connecteur source Azure HDInsights à l&#39;aide de l&#39;interface utilisateur de la plate-forme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)de l’éditeur de  : Découvrez comment créer des  personnalisées à l’aide de l’interface utilisateur de l’éditeur de  de.
* [](../../../../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion Spark valide, vous pouvez ignorer le reste de ce et passer au didacticiel sur la [configuration d’un flux de données.](../../dataflow/databases.md)

### Collecte des informations d’identification requises

Pour accéder à votre compte Spark sur la plateforme, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Adresse IP ou nom d’hôte du serveur Spark. |
| `username` | Nom d’utilisateur utilisé pour accéder au serveur Spark. |
| `password` | mot de passe correspondant à l’utilisateur. |

Pour plus d’informations sur la prise en main, reportez-vous à [cette](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview)Spark.

## Connectez votre compte Spark.

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer un compte Spark afin de vous connecter à la plateforme.

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’écran *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer un compte entrant et chaque source indique le nombre de comptes et de flux de jeux de données existants qui lui sont associés.

Vous pouvez sélectionner le  approprié dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous le  *Bases de données* , sélectionnez **Spark** pour afficher une barre d’informations sur le côté droit de l’écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou au  sa documentation. Pour créer une connexion entrante, sélectionnez **Connexion source**.

![catalogue](../../../../images/tutorials/create/spark/catalog.png)

La page *Se connecter à Spark* s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **Nouveau compte**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification Spark pour la connexion. Lorsque vous avez terminé, sélectionnez **Se connecter** , puis accordez du temps au nouveau compte pour l’établir.

![new](../../../../images/tutorials/create/spark/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte Spark avec lequel vous souhaitez vous connecter, puis sélectionnez **Suivant** pour continuer.

![existant](../../../../images/tutorials/create/spark/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte Spark. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/databases.md).