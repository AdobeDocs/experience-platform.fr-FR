---
title: Connecter Capillaire à Experience Platform à l’aide de l’interface utilisateur
description: Découvrez comment connecter Capillary à Experience Platform à l’aide de l’interface utilisateur
badge: Beta
exl-id: c90e6500-b92c-44ba-8de6-84e772bd9db1
source-git-commit: bd5611b23740f16e41048f3bc65f62312593a075
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 15%

---

# Connexion d’[!DNL Capillary Streaming Events] à Experience Platform à l’aide de l’interface utilisateur

>[!AVAILABILITY]
>
>La source [!DNL Capillary Streaming Events] est en version Beta. Lisez les [termes et conditions](../../../../home.md#terms-and-conditions) dans la présentation des sources pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Lisez ce guide pour savoir comment connecter votre base de données [!DNL Capillary] à Adobe Experience Platform à l’aide de l’espace de travail des sources dans l’interface utilisateur d’Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

## Parcourir le catalogue des sources

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]*. Sélectionnez la catégorie appropriée dans le panneau *[!UICONTROL Catégories]*. Vous pouvez également utiliser la barre de recherche pour accéder à la source spécifique que vous souhaitez utiliser.

Pour utiliser [!DNL Capillary], sélectionnez la carte source **[!UICONTROL Événements de streaming capillaires]** sous *[!UICONTROL Fidélité]*, puis sélectionnez **[!UICONTROL Ajouter des données]**.

>[!TIP]
>
>Les sources du catalogue affichent l’option **[!UICONTROL Configurer]** lorsqu’une source donnée ne dispose pas encore d’un compte authentifié. Une fois un compte authentifié créé, cette option devient **[!UICONTROL Ajouter des données]**.

![Le catalogue de sources dans l’interface utilisateur avec la carte Événements de diffusion en continu capillaires sélectionnée.](../../../../images/tutorials/create/capillary/catalog.png)

## Sélectionner les données

Utilisez ensuite l’interface *[!UICONTROL Sélectionner des données]* pour charger un exemple de fichier JSON afin de définir votre schéma source. Au cours de cette étape, vous pouvez utiliser l’interface de prévisualisation pour afficher la structure de fichiers de la payload. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![Étape de sélection des données du workflow des sources](../../../../images/tutorials/create/capillary/select-data.png)

## Détails du flux de données

Ensuite, vous devez fournir des informations concernant votre jeu de données et votre flux de données.

### Détails du jeu de données

Un jeu de données est une structure de stockage et de gestion pour une collection de données, généralement sous la forme d’une table, qui contient un schéma (des colonnes) et des champs (des lignes). Les données correctement ingérées par Experience Platform sont conservées sous forme de jeux de données dans le lac de données.

Au cours de cette étape, vous pouvez utiliser un jeu de données existant ou en créer un nouveau.

>[!NOTE]
>
>Que vous utilisiez un jeu de données existant ou en créiez un nouveau, vous devez vous assurer que votre jeu de données est **activé pour l’ingestion de profils**.

+++Sélectionnez pour connaître les étapes d’activation de l’ingestion de profil, des diagnostics d’erreur et de l’ingestion partielle.

Si votre jeu de données est activé pour le profil client en temps réel, au cours de cette étape, vous pouvez activer/désactiver le **[!UICONTROL jeu de données de profil]** pour activer vos données pour l’ingestion de profil. Vous pouvez également utiliser cette étape pour activer les **[!UICONTROL diagnostics d’erreur]** et **[!UICONTROL ingestion partielle]**.

* **[!UICONTROL Diagnostics d’erreur]** : sélectionnez **[!UICONTROL Diagnostics d’erreur]** pour demander à la source de générer des diagnostics d’erreur que vous pourrez référencer ultérieurement lors de la surveillance de l’activité du jeu de données et du statut du flux de données.
* **[!UICONTROL Ingestion partielle]** : l’ingestion par lots partielle est la possibilité d’ingérer des données contenant des erreurs, jusqu’à un certain seuil configurable. Cette fonctionnalité vous permet d’ingérer toutes vos données exactes dans Experience Platform, tandis que toutes vos données incorrectes sont traitées par lots séparément avec des informations sur les raisons de leur non-validité.

+++

### Détails du flux de données

Une fois votre jeu de données configuré, vous devez fournir des détails sur votre flux de données, y compris un nom, une description facultative et des configurations d’alerte.

![Interface des détails du flux de données](../../../../images/tutorials/create/capillary/dataflow-detail.png)

| Configurations du flux de données | Description |
| --- | --- |
| Nom du flux de données | Nom du flux de données.  Par défaut, le nom du fichier importé est utilisé. |
| Description | (Facultatif) Brève description de votre flux de données. |
| Alertes | Experience Platform peut générer des alertes basées sur des événements auxquelles les utilisateurs et utilisatrices peuvent s’abonner. Ces options permettent à un flux de données en cours d’exécution de les déclencher.  Pour plus d’informations, reportez-vous à la présentation des alertes [](../../alerts.md) <ul><li>**Début d’exécution du flux de données des sources** : sélectionnez cette alerte pour recevoir une notification lorsque l’exécution du flux de données commence.</li><li>**Succès de l’exécution du flux de données des sources** : sélectionnez cette alerte pour recevoir une notification si votre flux de données se termine sans erreur.</li><li>**Échec de l’exécution du flux de données des sources** : sélectionnez cette alerte pour recevoir une notification si l’exécution de votre flux de données se termine par des erreurs.</li></ul> |

{style="table-layout:auto"}

## Mappage

Utilisez l’interface de mappage pour mapper vos données source aux champs de schéma appropriés avant d’ingérer des données vers Experience Platform. Pour plus d’informations, consultez le guide de mappage [ dans l’interface utilisateur](../../../../../data-prep/ui/mapping.md).

>[!TIP]
>
>Vous pouvez télécharger le [Mappages d’événements et de profils](../../../../images/tutorials/create/capillary/mappings.zip) par [!DNL Capillary] et [importer les fichiers dans la préparation des données](../../../../../data-prep/ui/mapping.md#import-mapping) lorsque vous êtes prêt à mapper vos données.

![L’interface de mappage pour Capillary.](../../../../images/tutorials/create/capillary/mappings.png)

## Réviser

L’étape *[!UICONTROL Révision]* s’affiche et vous permet de consulter les détails de votre flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche le nom du compte, la plateforme source et le nom de la source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données cible et le schéma auquel le jeu de données se conforme.

Après avoir confirmé que les détails sont corrects, sélectionnez **[!UICONTROL Terminer]**.

![Étape de révision dans le workflow des sources.](../../../../images/tutorials/create/capillary/review.png)

## Récupérer l’URL du point d’entrée de diffusion en continu

Une fois la connexion créée, la page des détails des sources s’affiche. Cette page affiche les détails de la connexion que vous venez de créer, y compris les flux de données précédemment exécutés, l’identifiant et l’URL du point d’entrée de diffusion en continu.

![URL du point d’entrée de diffusion en continu.](../../../../images/tutorials/create/capillary/endpoint-url.png)
