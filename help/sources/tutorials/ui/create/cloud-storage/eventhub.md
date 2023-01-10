---
keywords: Experience Platform;accueil;rubriques les plus consultées;centres d’événements Azure;centres d’événements;centres d’événements Azure
solution: Experience Platform
title: Création d’une connexion source Azure Event Hubs dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source Azure Event Hubs à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 39%

---


# Créez un [!DNL Azure Event Hubs] connexion source dans l’interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’ingérer des données externes selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour authentifier une [!DNL Azure Event Hubs] (ci-après dénommés &quot;[!DNL Event Hubs]&quot;) connecteur source à l’aide de [!DNL Platform] de l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Event Hubs] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/streaming/cloud-storage-streaming.md).

### Collecter les informations d’identification requises

Pour authentifier votre [!DNL Event Hubs] connecteur source, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `sasKeyName` | Nom de la règle d’autorisation, également appelé nom de clé SAS. |
| `sasKey` | La clé Principale de la variable [!DNL Event Hubs] espace de noms. Le `sasPolicy` que la variable `sasKey` correspond à `manage` les droits configurés pour [!DNL Event Hubs] liste à renseigner. |
| `namespace` | L’espace de noms de la variable [!DNL Event Hubs] vous y accédez. |

Pour plus d’informations sur ces valeurs, reportez-vous à la section [this [!DNL Event Hubs] document](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Connecter votre compte [!DNL Event Hubs]

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Event Hubs] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder au **[!UICONTROL Sources]** workspace. Le **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , **[!UICONTROL Stockage dans le cloud]** catégorie, sélectionnez **[!UICONTROL Centre d’événements Azure]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un connecteur Event Hubs.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Le **[!UICONTROL Connexion aux centres d’événements Azure]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et [!DNL Event Hubs] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis accorder un certain temps pour établir la nouvelle connexion.

![](../../../../images/tutorials/create/eventhub/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL Event Hubs] compte auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez connecté votre [!DNL Event Hubs] compte à [!DNL Platform]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données de votre espace de stockage dans le cloud dans [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
