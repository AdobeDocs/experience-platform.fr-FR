---
keywords: Experience Platform;accueil;rubriques populaires;Data Explorer Azure;explorateur de données Azure;explorateur de données;Data Explorer
solution: Experience Platform
title: Création d’une connexion Source Azure Data Explorer dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source Azure Data Explorer à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 561bf948-fc92-4401-8631-e2a408667507
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 41%

---

# Créer une connexion source [!DNL Azure Data Explorer] dans l’interface utilisateur

Les connecteurs Source dans Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur de manière planifiée. Ce tutoriel décrit les étapes de création d’un connecteur source [!DNL Azure Data Explorer] (ci-après appelé &quot;[!DNL Data Explorer]&quot;) à l’aide de l’interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Data Explorer] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Pour accéder à votre compte [!DNL Data Explorer] sur [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `endpoint` | Point d’entrée du serveur [!DNL Data Explorer]. |
| `database` | Nom de la base de données [!DNL Data Explorer]. |
| `tenant` | L’identifiant de tenant unique utilisé pour se connecter à la base de données [!DNL Data Explorer]. |
| `servicePrincipalId` | L’identifiant principal de service unique utilisé pour se connecter à la base de données [!DNL Data Explorer]. |
| `servicePrincipalKey` | Clé principale de service unique utilisée pour la connexion à la base de données [!DNL Data Explorer]. |

Pour plus d&#39;informations sur la prise en main, consultez [ce [!DNL Data Explorer] document](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

## Connecter votre compte [!DNL Azure Data Explorer]

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Data Explorer] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Bases de données]**, sélectionnez **[!UICONTROL Data Explorer Azure]**. Si c&#39;est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un nouveau connecteur de Data Explorer.

![catalogue](../../../../images/tutorials/create/data-explorer/catalog.png)

La page **[!UICONTROL Se connecter à Azure Data Explorer]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Data Explorer]. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** et laissez un certain temps à la nouvelle connexion pour établir.

![connect](../../../../images/tutorials/create/data-explorer/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Data Explorer] auquel vous souhaitez vous connecter, puis cliquez sur **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/data-explorer/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Data Explorer]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans [!DNL Platform]](../../dataflow/databases.md).
