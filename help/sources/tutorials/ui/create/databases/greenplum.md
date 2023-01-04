---
keywords: Experience Platform;accueil;rubriques les plus consultées;Greenplum;greenplum
solution: Experience Platform
title: Création d’une connexion à la source GreenPlum dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source GreenPlum à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: e6c6a495-25ce-4497-b20e-91374c7bb548
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 56%

---

# Créer une connexion source [!DNL GreenPlum] dans l’interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’ingérer des données externes selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer une [!DNL GreenPlum] connecteur source à l’aide de [!DNL Platform] de l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL GreenPlum] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter. [!DNL GreenPlum] en utilisant la variable [!DNL Flow Service] API.

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion utilisée pour se connecter à votre [!DNL GreenPlum] instance. Le modèle de chaîne de connexion pour [!DNL GreenPlum] is `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Pour plus d’informations sur la prise en main, reportez-vous à la section [ce document GreenPlum ;](https://docs.greenplum.org/6-7/security-guide/topics/Authenticate.html).

## Connecter votre compte [!DNL GreenPlum]

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL GreenPlum] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder au **[!UICONTROL Sources]** workspace. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , **[!UICONTROL Bases de données]** catégorie, sélectionnez **[!UICONTROL GreenPlum]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer [!DNL GreenPlum] connecteur.

![catalogue](../../../../images/tutorials/create/greenplum/catalog.png)

Le **[!UICONTROL Connexion à GreenPlum]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et [!DNL GreenPlum] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis accorder un certain temps pour établir la nouvelle connexion.

![connect](../../../../images/tutorials/create/greenplum/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL GreenPlum] compte auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour continuer.

![existant](../../../../images/tutorials/create/greenplum/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL GreenPlum]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans [!DNL Platform]](../../dataflow/databases.md).
