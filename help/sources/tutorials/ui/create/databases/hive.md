---
keywords: Experience Platform;accueil;rubriques les plus consultées;Apache Hive;Azure HDInsights;azure hdinsights
solution: Experience Platform
title: Création d’une Apache Hive sur la connexion source Azure HDInsights dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Apache Hive sur Azure HDInsights à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 3eb3cb02-9867-451a-b847-ab895310eedf
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 12%

---

# Créez une [!DNL Apache Hive] sur [!DNL Azure HDInsights] connexion source dans l’interface utilisateur.

>[!NOTE]
>
> Le connecteur [!DNL Apache Hive] sur [!DNL Azure HDInsights] est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez la [Présentation des sources](../../../../home.md#terms-and-conditions) .

Les connecteurs source de Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer un [!DNL Apache Hive] sur le connecteur source [!DNL Azure HDInsights] à l’aide de l’interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel](../../../../../xdm/tutorials/create-schema-ui.md) de l’éditeur de schémas : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Hive] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur [la configuration d’un flux de données](../../dataflow/databases.md)

### Collecte des informations d’identification requises

Pour accéder à votre compte [!DNL Hive] sur [!DNL Platform], vous devez fournir les valeurs suivantes :

| Credential | Description |
| ---------- | ----------- |
| `host` | Adresse IP ou nom d’hôte du serveur [!DNL Hive]. |
| `username` | Nom d’utilisateur que vous utilisez pour accéder au serveur [!DNL Hive]. |
| `password` | Mot de passe qui correspond à l’utilisateur. |

Pour plus d’informations sur la prise en main, voir [ce [!DNL Hive] document](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted).

## Connectez votre compte [!DNL Hive]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Hive] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie **[!UICONTROL Bases de données]**, sélectionnez **[!UICONTROL Hive]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un nouveau connecteur [!DNL Hive].

![catalogue](../../../../images/tutorials/create/hive/catalog.png)

La page **[!UICONTROL Se connecter à Hive]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Hive]. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Se connecter]**, puis laissez un certain temps pour établir la nouvelle connexion.

![connect](../../../../images/tutorials/create/hive/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Hive] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/hive/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Hive]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans  [!DNL Platform]](../../dataflow/databases.md).
