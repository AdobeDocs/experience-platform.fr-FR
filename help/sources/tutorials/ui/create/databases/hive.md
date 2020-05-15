---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d'une Apache Hive sur le connecteur source Azure HDInsights dans l'interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Création d&#39;une Apache Hive sur le connecteur source Azure HDInsights dans l&#39;interface utilisateur

> [!NOTE]
> Le connecteur Apache Hive sur Azure HDInsights est en version bêta. Les fonctionnalités et la documentation peuvent être modifiées.

Les connecteurs source d’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer une Apache Hive sur un connecteur source Azure HDInsights à l&#39;aide de l&#39;interface utilisateur de la plate-forme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion Hive valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données.](../../dataflow/databases.md)

### Collecte des informations d’identification requises

Pour accéder à votre compte Hive sur la plate-forme, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Adresse IP ou nom d’hôte du serveur Hive. |
| `username` | Nom d’utilisateur utilisé pour accéder au serveur Hive. |
| `password` | Mot de passe correspondant à l’utilisateur. |

Pour plus d&#39;informations sur la prise en main, consultez [ce document](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted)Hive.

## Connecter votre compte Hive

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer un compte Hive afin de vous connecter à la plate-forme.

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’écran *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer un compte entrant et chaque source affiche le nombre de comptes et de flux de jeux de données existants qui lui sont associés.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie *Bases de données* , sélectionnez **Ruche** pour afficher une barre d&#39;informations sur le côté droit de l&#39;écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou à la vue de sa documentation. Pour créer une connexion entrante, sélectionnez **Connexion source**.

![catalogue](../../../../images/tutorials/create/hive/catalog.png)

La page *Se connecter à la ruche* s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **Nouveau compte**. Dans le formulaire d’entrée qui s’affiche, indiquez le nom de la connexion, une description facultative et vos informations d’identification Hive. Lorsque vous avez terminé, sélectionnez **Se connecter** , puis accordez un certain temps à l’établissement du nouveau compte.

![connecter](../../../../images/tutorials/create/hive/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte Hive avec lequel vous souhaitez vous connecter, puis sélectionnez **Suivant** pour continuer.

![existant](../../../../images/tutorials/create/hive/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte Hive. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans la plate-forme](../../dataflow/databases.md).