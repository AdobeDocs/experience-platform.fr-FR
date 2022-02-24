---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;campagne;services gérés de campagne
title: Création d’une connexion source Adobe Campaign Managed Services à l’aide de l’interface utilisateur de Platform
description: Découvrez comment connecter Adobe Experience Platform à Adobe Campaign Managed Services à l’aide de l’interface utilisateur de Platform.
hide: true
hidefromtoc: true
source-git-commit: 24d7a549e83245fc363bd76f26ba58130e980c6c
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 1%

---


# Création d’une connexion source Adobe Campaign Managed Services à l’aide de l’interface utilisateur de Platform

Ce tutoriel décrit les étapes à suivre pour créer un connecteur source afin d’importer vos données Managed Services Adobe Campaign dans Adobe Experience Platform.

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Experience Platform :

* [Sources](../../../../home.md): Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Environnements de test](../../../../../sandboxes/home.md): Platform fournit des environnements de test virtuels qui divisent une instance de Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Connexion d’Adobe Campaign Managed Services à Platform

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à la fonction [!UICONTROL Sources] workspace. Le [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également utiliser la barre de recherche pour réduire les sources affichées.

Sous , **[!UICONTROL Adobe des applications]** catégorie, sélectionnez **[!UICONTROL Adobe Campaign Managed Services]** puis sélectionnez **[!UICONTROL Ajouter des données]**.

### Sélection des données

Le [!UICONTROL Sélectionner des données] s’affiche, vous permettant ainsi de configurer les valeurs de votre [!UICONTROL Instance Adobe Campaign], [!UICONTROL Mapping de ciblage], et [!UICONTROL Nom du schéma].

#### Sélectionner l’instance de campagne {#select-campaign-instance}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="Sélectionner l’instance de campagne"
>abstract="Nom de l’environnement Adobe Campaign Classic que vous souhaitez utiliser."
>text="Learn more in documentation"

#### Sélectionner le mapping de campagne {#select-campaign-mapping}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="Sélectionner le mapping de ciblage de campagne"
>abstract="Les mappings de ciblage sont des objets techniques utilisés par Campaign pour diffuser des messages. Ils contiennent tous les paramètres techniques nécessaires pour envoyer des diffusions (adresses, numéros de téléphone, indicateurs d&#39;opt-in, identifiants additionnels, etc.)."
>text="Learn more in documentation"

#### Sélectionner le schéma de campagne {#select-campaign-schema}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="Sélectionner le nom du schéma de campagne"
>abstract="Nom de l’entité définie dans la base de données Adobe Campaign."
>text="Learn more in documentation"
