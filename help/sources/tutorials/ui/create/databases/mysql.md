---
keywords: Experience Platform;accueil;rubriques les plus consultées;mysql;MySQL
solution: Experience Platform
title: Création d’une connexion source MySQL dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source MySQL à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 45%

---

# Créer une connexion source [!DNL MySQL] dans l’interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’ingérer des données externes selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer une [!DNL MySQL] connexion source à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une [!DNL MySQL] vous pouvez ignorer le reste de ce document et passer au tutoriel sur [configuration d’un flux de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Pour accéder à [!DNL MySQL] compte sur [!DNL Platform], vous devez fournir la valeur suivante :

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Le [!DNL MySQL] Chaîne de connexion associée à votre compte. Le [!DNL MySQL] Le modèle de chaîne de connexion est le suivant : `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. Vous pouvez en savoir plus sur les chaînes de connexion et comment les obtenir en lisant le [[!DNL MySQL] document](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html). |

## Connecter votre compte [!DNL MySQL]

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL MySQL] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder au **[!UICONTROL Sources]** workspace. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Sous , **[!UICONTROL Bases de données]** catégorie, sélectionnez **[!UICONTROL MySQL]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer [!DNL MySQL] connecteur.

![](../../../../images/tutorials/create/my-sql/catalog.png)

Le **[!UICONTROL Connexion à MySQL]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et [!DNL MySQL] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis accorder un certain temps pour établir la nouvelle connexion.

![](../../../../images/tutorials/create/my-sql/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL MySQL] compte auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/my-sql/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte MySQL. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans [!DNL Platform]](../../dataflow/databases.md).
