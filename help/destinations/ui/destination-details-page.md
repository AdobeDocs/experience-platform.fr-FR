---
keywords: destinations;destination;page des détails des destinations;page des détails des destinations
title: Affichage des détails de destination
description: 'La page de détails d’une destination individuelle fournit un aperçu des détails de destination. Les détails de la destination incluent le nom de destination, l’identifiant, les segments mappés à la destination et les contrôles permettant de modifier l’activation et d’activer et désactiver le flux de données. '
seo-description: The details page for an individual destination provides an overview of the destination details. Destination details include the destination name, ID, segments mapped to the destination, and controls to edit the activation and to enable and disable the data flow.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 6%

---

# Affichage des détails de destination

## Présentation {#overview}

Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez afficher et surveiller les attributs et les activités de vos destinations. Ces détails incluent le nom et l’identifiant de la destination, des commandes pour activer ou désactiver les destinations, etc. Les détails des destinations par lot incluent également des mesures pour les enregistrements de profil activés et un historique des exécutions de flux de données.

>[!NOTE]
>
>La page des détails des destinations fait partie de l’espace de travail [!UICONTROL Destinations] dans [!DNL Platform] [!DNL UI]. Pour plus d’informations, consultez la [[!UICONTROL Présentation de l’espace de travail Destinations] .](./destinations-workspace.md)

## Affichage des détails de destination {#view-details}

Suivez les étapes ci-dessous pour afficher plus de détails sur une destination existante.

1. Connectez-vous à l’[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Sélectionnez **[!UICONTROL Parcourir]** dans l’en-tête supérieur pour afficher vos destinations existantes.

   ![Parcourir les destinations](../assets/ui/details-page/browse-destinations.png)

1. Sélectionnez l’icône de filtre ![Icône de filtre](../assets/ui/details-page/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrage des destinations](../assets/ui/details-page/filter-destinations.png)

1. Sélectionnez le nom de la destination à afficher.

   ![Sélectionner la destination](../assets/ui/details-page/destination-select.png)

1. La page de détails de la destination s’affiche, affichant ses commandes disponibles. Si vous affichez les détails d’une destination par lot, un tableau de bord de surveillance s’affiche également.

   ![Détails de la destination](../assets/ui/details-page/destination-details.png)

## Rail de droite

Le rail de droite affiche les informations de base sur la destination sélectionnée.

![rail droit](../assets/ui/details-page/right-sidebar.png)

Le tableau suivant couvre les contrôles et les détails fournis par le rail de droite :

| Élément de rail de droite | Description |
| --- | --- |
| [!UICONTROL Activer] | Sélectionnez ce contrôle pour modifier les segments qui sont mappés à la destination. Pour plus d’informations, consultez les guides sur l’[activation des données d’audience vers des destinations de diffusion en continu de segments](./activate-segment-streaming-destinations.md), l’[activation des données d’audience vers des destinations basées sur un profil de lot](./activate-batch-profile-destinations.md) et l’[activation des données d’audience vers des destinations basées sur un profil de diffusion en continu](./activate-streaming-profile-destinations.md) . |
| [!UICONTROL Supprimer] | Permet de supprimer ce flux de données et annule le mappage des segments qui ont été activés auparavant, le cas échéant. |
| [!UICONTROL Nom de la destination] | Ce champ peut être modifié afin de mettre à jour le nom de la destination. |
| [!UICONTROL Description] | Ce champ peut être modifié pour mettre à jour ou ajouter une description facultative à la destination. |
| [!UICONTROL Destination] | Représente la plateforme de destination vers laquelle les audiences sont envoyées. Pour plus d’informations, consultez le [catalogue des destinations](../catalog/overview.md) . |
| [!UICONTROL État] | Indique si la destination est activée ou désactivée. |
| [!UICONTROL Actions marketing] | Indique les actions marketing (cas d’utilisation) qui s’appliquent à cette destination à des fins de gouvernance des données. |
| [!UICONTROL Catégorie] | Indique le type de destination. Pour plus d’informations, consultez le [catalogue des destinations](../catalog/overview.md) . |
| [!UICONTROL Type de connexion] | Indique le formulaire par lequel vos audiences sont envoyées vers la destination. Les valeurs possibles sont [!UICONTROL Cookie] et [!UICONTROL Basé sur un profil]. |
| [!UICONTROL Fréquence] | Indique la fréquence d’envoi des audiences vers la destination. Les valeurs possibles sont [!UICONTROL Diffusion en continu] et [!UICONTROL Lot]. |
| [!UICONTROL Identité] | Représente l’espace de noms d’identité accepté par la destination, par exemple `GAID`, `IDFA` ou `email`. Pour plus d’informations sur les espaces de noms d’identité acceptés, consultez la [présentation des espaces de noms d’identité](../../identity-service/namespaces.md). |
| [!UICONTROL Créé par] | Indique l’utilisateur qui a créé cette destination. |
| [!UICONTROL Créé] | Indique la date et l’heure (UTC) de création de cette destination. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Activé]/ Désactivé

Vous pouvez utiliser le bouton d’activation **[!UICONTROL Activé]/[!UICONTROL Désactivé]** pour démarrer et suspendre toutes les exportations de données vers la destination.

![Activer la désactivation du bouton](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Exécutions de flux de données]

L’onglet [!UICONTROL Flux de données s’exécute] fournit des données de mesure sur vos flux de données s’exécutent vers des destinations par lot. Pour plus d’informations, voir [Surveiller les flux de données](monitor-dataflows.md) .

## [!UICONTROL Données d’activation] {#activation-data}

L’onglet [!UICONTROL Données d’activation] affiche la liste des segments qui ont été mappés à la destination, y compris leur date de début et leur date de fin (le cas échéant). Pour afficher les détails d’un segment particulier, sélectionnez son nom dans la liste.

![Données d’activation](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Pour plus d’informations sur l’exploration de la page de détails d’un segment, reportez-vous à la [Présentation de l’interface utilisateur de segmentation](../../segmentation/ui/overview.md#segment-details).
