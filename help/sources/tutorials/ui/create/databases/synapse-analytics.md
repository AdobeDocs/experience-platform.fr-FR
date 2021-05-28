---
keywords: Experience Platform;accueil;rubriques les plus consultées;Azure synapse Analytics;Synapse;synapse;azure synapse analytics
solution: Experience Platform
title: Création d’une connexion source Analytics d’Azure synapse dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Analytics d’Azure synapse (ci-après appelée "Synapse") à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 1f1ce317-eaaf-4ad2-a5fb-236983220bd7
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 12%

---

# Création d’une connexion source [!DNL Azure Synapse Analytics] dans l’interface utilisateur

Les connecteurs source de Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes de création d’un connecteur source [!DNL Azure Synapse Analytics] (ci-après appelé &quot;[!DNL Synapse]&quot;) à l’aide de l’interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel](../../../../../xdm/tutorials/create-schema-ui.md) de l’éditeur de schémas : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Synapse] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecte des informations d’identification requises

Pour accéder à votre compte [!DNL Synapse] sur [!DNL Platform], vous devez fournir les valeurs suivantes :

| Credential | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion associée à votre authentification [!DNL Synapse]. Le modèle de chaîne de connexion [!DNL Synapse] est `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |

Pour plus d’informations sur cette valeur, voir [this [!DNL Synapse] document](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-sql-data-warehouse).

## Connectez votre compte [!DNL Synapse]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Synapse] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie **[!UICONTROL Bases de données]**, sélectionnez **[!UICONTROL Azure synapse Analytics]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un nouveau connecteur [!DNL Synapse].

![](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

La page **[!UICONTROL Se connecter à Azure synapse Analytics]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Synapse]. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Se connecter]**, puis laissez un certain temps pour établir la nouvelle connexion.

![](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Synapse] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Synapse]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans  [!DNL Platform]](../../dataflow/databases.md).
