---
keywords: Experience Platform;accueil;rubriques populaires;Data Explorer Azure;explorateur de données Azure;explorateur de données;Data Explorer
solution: Experience Platform
title: Création d’une connexion source de Data Explorer Azure dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Azure Data Explorer à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 561bf948-fc92-4401-8631-e2a408667507
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 50%

---

# Créez un [!DNL Azure Data Explorer] connexion source dans l’interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’ingérer des données externes selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Azure Data Explorer] (ci-après dénommés &quot;[!DNL Data Explorer]&quot;) connecteur source à l’aide de [!DNL Platform] de l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Data Explorer] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Pour accéder au compte [!DNL Data Explorer] sur , vous devez fournir les valeurs suivantes :[!DNL Platform]

| Informations d’identification | Description |
| ---------- | ----------- |
| `endpoint` | Le point de terminaison de [!DNL Data Explorer] serveur. |
| `database` | Nom de la variable [!DNL Data Explorer] base de données. |
| `tenant` | L’identifiant de client unique utilisé pour se connecter à la variable [!DNL Data Explorer] base de données. |
| `servicePrincipalId` | L’identifiant principal de service unique utilisé pour se connecter à la variable [!DNL Data Explorer] base de données. |
| `servicePrincipalKey` | La clé principale de service unique utilisée pour se connecter à la variable [!DNL Data Explorer] base de données. |

Pour plus d’informations sur la prise en main, reportez-vous à la section [this [!DNL Data Explorer] document](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

## Connecter votre compte [!DNL Azure Data Explorer]

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Data Explorer] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder au **[!UICONTROL Sources]** workspace. Le **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , **[!UICONTROL Bases de données]** catégorie, sélectionnez **[!UICONTROL Data Explorer Azure]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un nouveau connecteur de Data Explorer.

![catalogue](../../../../images/tutorials/create/data-explorer/catalog.png)

Le **[!UICONTROL Connexion à Azure Data Explorer]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et [!DNL Data Explorer] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis accorder un certain temps pour établir la nouvelle connexion.

![connect](../../../../images/tutorials/create/data-explorer/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL Data Explorer] compte auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/data-explorer/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Data Explorer]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans [!DNL Platform]](../../dataflow/databases.md).
