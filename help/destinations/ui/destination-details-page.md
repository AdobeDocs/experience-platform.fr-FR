---
keywords: destinations;destination;page des détails des destinations;page des détails des destinations
title: Afficher les détails de la destination
description: La page de détails d’une destination individuelle fournit un aperçu des détails de destination. Les détails de la destination incluent le nom de destination, l’identifiant, les audiences mappées à la destination et les contrôles permettant de modifier l’activation et d’activer et désactiver le flux de données.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 12%

---

# Afficher les détails de la destination

## Vue d’ensemble {#overview}

Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez afficher et surveiller les attributs et les activités de vos destinations. Ces détails incluent le nom et l’identifiant de la destination, des commandes pour activer ou désactiver les destinations, etc. Les détails incluent également des mesures pour les enregistrements de profil activés, les identités activées, en échec et exclues, ainsi qu’un historique des exécutions de flux de données.

>[!NOTE]
>
>La page des détails des destinations fait partie de la [!UICONTROL Destinations] de l’espace de travail [!DNL Platform] [!DNL UI]. Voir [[!UICONTROL Destinations] présentation de workspace](./destinations-workspace.md) pour plus d’informations.

## Afficher les détails de la destination {#view-details}

Suivez les étapes ci-dessous pour afficher plus de détails sur une destination existante.

1. Connectez-vous à l’[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Sélectionner **[!UICONTROL Parcourir]** dans l’en-tête supérieur pour afficher vos destinations existantes.

   ![Parcourir les destinations](../assets/ui/details-page/browse-destinations.png)

1. Sélectionnez l’icône filtre ![Icône Filtre](../assets/ui/details-page/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrage des destinations](../assets/ui/details-page/filter-destinations.png)

1. Sélectionnez le nom de la destination à afficher.

   ![Sélectionnez des destinations](../assets/ui/details-page/destination-select.png)

1. La page de détails de la destination s’affiche, affichant ses commandes disponibles.

   ![Détails de la destination](../assets/ui/details-page/destination-details.png)

## Rail de droite {#right-rail}

Le rail de droite affiche les informations de base sur la destination sélectionnée.

![rail droit](../assets/ui/details-page/right-sidebar.png)

Le tableau suivant couvre les contrôles et les détails fournis par le rail de droite :

| Élément de rail de droite | Description |
| --- | --- |
| [!UICONTROL Activation des audiences] | Sélectionnez ce contrôle pour modifier les audiences qui sont mappées à la destination, mettre à jour les plannings d’exportation ou ajouter et supprimer des attributs et des identités mappés. Voir les guides sur [activation des données d’audience vers des destinations de diffusion en continu d’audience](./activate-segment-streaming-destinations.md), [activation des données d’audience vers des destinations basées sur un profil de lot](./activate-batch-profile-destinations.md), et [activation des données d’audience vers des destinations basées sur un profil de diffusion en continu](./activate-streaming-profile-destinations.md) pour plus d’informations. |
| [!UICONTROL Supprimer] | Permet de supprimer ce flux de données et annule la correspondance des audiences qui ont été activées auparavant, le cas échéant. |
| [!UICONTROL Nom de la destination] | Ce champ peut être modifié afin de mettre à jour le nom de la destination. |
| [!UICONTROL Description] | Ce champ peut être modifié pour mettre à jour ou ajouter une description facultative à la destination. |
| [!UICONTROL Destination] | Représente la plateforme de destination vers laquelle les audiences sont envoyées. Voir [destinations](../catalog/overview.md) pour plus d’informations. |
| [!UICONTROL Statut] | Indique si la destination est activée ou désactivée. |
| [!UICONTROL Actions marketing] | Indique les actions marketing (cas d’utilisation) qui s’appliquent à cette destination à des fins de gouvernance des données. |
| [!UICONTROL Catégorie] | Indique le type de destination. Voir [destinations](../catalog/overview.md) pour plus d’informations. |
| [!UICONTROL Type de connexion] | Indique le formulaire par lequel vos audiences sont envoyées vers la destination. Les valeurs possibles sont les suivantes : [!UICONTROL Cookie] et [!UICONTROL Basé sur les profils]. |
| [!UICONTROL Fréquence] | Indique la fréquence d’envoi des audiences vers la destination. Les valeurs possibles sont les suivantes : [!UICONTROL Diffusion en continu] et [!UICONTROL Lot]. |
| [!UICONTROL Identité] | Représente l’espace de noms d’identité accepté par la destination, tel que `GAID`, `IDFA`ou `email`. Pour plus d’informations sur les espaces de noms d’identité acceptés, voir [présentation de l’espace de noms d’identité](../../identity-service/namespaces.md). |
| [!UICONTROL Créé par] | Indique l’utilisateur qui a créé cette destination. |
| [!UICONTROL Créé] | Indique la date et l’heure (UTC) de création de cette destination. |

{style="table-layout:auto"}

## [!UICONTROL Activé]/[!UICONTROL Désactivé] basculer {#enabled-disabled-toggle}

Vous pouvez utiliser la variable **[!UICONTROL Activé]/[!UICONTROL Désactivé]** pour démarrer et suspendre toutes les exportations de données vers la destination.

![Activation ou désactivation du basculement de flux de données](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Exécutions de flux de données] {#dataflow-runs}

Le [!UICONTROL Exécutions de flux de données] fournit des données de mesure sur vos flux de données s’exécutent sur des destinations par lot et en flux continu. Voir [Surveiller les flux de données](monitor-dataflows.md) pour plus d’informations et de définitions de mesures.

>[!NOTE]
>
>* La fonctionnalité de surveillance des destinations est actuellement prise en charge pour toutes les destinations dans Experience Platform. *Sauf* la valeur [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), [Personnalisation personnalisée](/help/destinations/catalog/personalization/custom-personalization.md) et [Audiences Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md) destinations.
>* Pour le [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Centre d’événements Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), et [API HTTP](/help/destinations/catalog/streaming/http-destination.md) destinations, les mesures liées aux identités exclues, en échec et activées sont estimées. Des volumes plus importants de données d’activation augmentent la précision des mesures.

![Vue des exécutions du flux de données](../assets/ui/details-page/dataflow-runs.png)

### Durée des exécutions du flux de données {#dataflow-runs-duration}

Il existe une différence dans la durée affichée des exécutions de flux de données entre les destinations en flux continu et celles basées sur des fichiers.

### Destinations de diffusion en continu {#streaming}

Lorsque la variable **[!UICONTROL Durée de traitement]** indiqué pour la plupart des exécutions de flux de données en continu est d’environ quatre heures, comme illustré dans l’image ci-dessous, le temps de traitement réel pour toute exécution de flux de données est beaucoup plus court. Les fenêtres d’exécution du flux de données restent ouvertes pendant plus longtemps si l’Experience Platform doit réessayer d’effectuer des appels vers la destination et s’assurer qu’il ne manque pas de données arrivées tardivement pendant la même période.

![Image de la page Exécution du flux de données avec la colonne Temps de traitement mise en surbrillance pour une destination de diffusion en continu.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-streaming.png)

Pour plus d’informations, reportez-vous à la section [le flux de données s’exécute dans les destinations de diffusion en continu.](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) dans la documentation de surveillance.

### Destinations basées sur des fichiers {#file-based}

Pour les flux de données qui s’exécutent sur des destinations basées sur des fichiers, la variable **[!UICONTROL Durée de traitement]** dépend de la taille des données exportées et de la charge du système. Notez également que le flux de données s’exécute vers des destinations basées sur des fichiers sont ventilés par audience.

![Image de la page Flux de données s’exécutant avec la colonne Temps de traitement mise en surbrillance pour une destination basée sur un fichier.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-file-based.png)

Pour plus d’informations, reportez-vous à la section [le flux de données s’exécute dans des destinations par lots (basées sur des fichiers).](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) dans la documentation de surveillance.

## [!UICONTROL Données d’activation] {#activation-data}

Le [!UICONTROL Données d’activation] affiche une liste des audiences qui ont été mappées à la destination, y compris leur date de début et de fin (le cas échéant), ainsi que d’autres informations pertinentes pour l’exportation des données, telles que le type d’exportation, la planification et la fréquence. Pour afficher les détails d’une audience spécifique, sélectionnez son nom dans la liste.

>[!TIP]
>
>Pour afficher et modifier les détails sur les attributs et les identités mappés à une destination, sélectionnez **[!UICONTROL Activation des audiences]** dans le [rail droit](#right-rail).

![Destination du lot d’affichage des données d’activation](../assets/ui/details-page/activation-data-batch.png)

![Destination de la diffusion en continu de l’affichage des données d’activation](../assets/ui/details-page/activation-data-streaming.png)

>[!NOTE]
>
>Pour plus d’informations sur l’exploration de la page de détails d’une audience, reportez-vous à la section [Présentation de l’interface utilisateur de segmentation](../../segmentation/ui/overview.md#segment-details).
