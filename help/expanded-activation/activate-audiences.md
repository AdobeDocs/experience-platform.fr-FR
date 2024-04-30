---
title: Activation des audiences d’Audience Manager par le biais d’une activation étendue
description: Découvrez comment activer les audiences d’Audience Manager vers les destinations publicitaires et sociales par le biais de l’activation étendue de l’Audience Manager.
source-git-commit: 19fb369a7faa0c5ac27a34db7b848b0332cb8695
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# Activation des audiences par le biais de l’activation étendue des Audiences Manager

Cette page décrit le processus de bout en bout que vous devez suivre pour activer les audiences depuis l’Audience Manager vers les plateformes de destination prises en charge par l’activation étendue.

## Avant de commencer {#before-you-begin}

Les étapes décrites dans ce guide supposent que vous avez lu le [Page d’aperçu de l’activation étendue](overview.md) et vous avez confirmé que vous remplissez les conditions préalables à l’activation d’audience.

>[!IMPORTANT]
>
>Pour activer des audiences par le biais de [!DNL Expanded Activation], assurez-vous que les audiences de votre Audience Manager sont basées sur **adresses électroniques hachées**. Voir [conditions préalables](overview.md#prerequisites) pour plus d’informations.

## Etape 1 : configuration de la connexion source de l&#39;Audience Manager {#configure-source}

La variable [Connecteur source d’Audience Manager](../sources/connectors/adobe-applications/audience-manager.md) envoie les données d’audience collectées dans Adobe Audience Manager pour activation dans les plateformes de destination prises en charge par l’activation étendue.

Suivez le guide sur la manière de [créer une connexion source d’Audience Manager](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) pour configurer votre connecteur source.

![Image de l’interface utilisateur de Platform montrant l’onglet Sources avec la connexion à la source de l’Audience Manager.](assets/sources-tab.png)

>[!TIP]
>
>Le connecteur source Adobe Audience Manager est le seul connecteur source disponible dans Activation étendue.
>
>Si vous souhaitez ingérer des audiences basées sur des identifiants supplémentaires, vous devez acheter une édition de [Real-Time CDP](../rtcdp/overview.md). Pour plus d’informations, contactez votre représentant d’Adobe.

### Affichage et surveillance des audiences ingérées {#view-audiences}

Les audiences que vous importez dans l’activation étendue à partir de l’Audience Manager sont disponibles dans la **[!UICONTROL Audiences]** tableau de bord.

Pour afficher vos audiences, accédez à **[!UICONTROL Client]** -> **[!UICONTROL Audiences]** -> **[!UICONTROL Parcourir]**.

![Image de l’interface utilisateur de Platform montrant la page Audiences.](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* Les audiences peuvent prendre jusqu’à 48 heures pour être entièrement renseignées dans l’activation étendue. Cela s’applique également aux mises à jour des audiences d’Audience Manager existantes.
>* Les audiences d’Audience Manager nouvellement créées n’apparaissent pas automatiquement dans l’activation étendue. Pour ingérer de nouveaux segments dans l’activation étendue, vous devez les ajouter via le connecteur source d’Audience Manager.

Une fois que vous avez configuré le connecteur source d’Audience Manager, accédez à [étape 2](#create-destination-connection).

## Étape 2 : création d’une connexion de destination {#create-destination-connection}

Avant de pouvoir envoyer les audiences de votre Audience Manager vers votre plateforme de destination de votre choix, vous devez d’abord créer une connexion vers une plateforme de destination.

Dans la barre latérale gauche, accédez à **[!UICONTROL Connexions]** -> **[!UICONTROL Destinations]** -> **[!UICONTROL Catalogue]**.

Catégories de destination disponibles pour [!DNL Expanded Activation] are [publicité](../destinations/catalog/advertising/overview.md) et [social](../destinations/catalog/social/overview.md).

![Image de l’interface utilisateur de Platform montrant le catalogue de destination pour l’activation étendue.](assets/destination-catalog.png)

Pour créer une connexion à une plateforme de destination, suivez le guide sur [comment créer une connexion de destination](../destinations/ui/connect-destination.md). Ensuite, passez à [étape 3](#activate-audiences).

## Étape 3 : activation des audiences vers votre destination {#activate-audiences}

Après avoir réussi [audiences d’Audience Manager ingérées](#configure-source) et [création d’une connexion de destination](#create-destination-connection), vous pouvez désormais activer vos audiences sur la plateforme de destination de votre choix.

![Image de l’interface utilisateur de Platform montrant le catalogue de destination pour l’activation étendue.](assets/activate-audiences.png)

Pour activer les audiences vers votre destination, suivez le guide sur [comment activer des audiences vers des destinations de diffusion en continu](../destinations/ui/activate-segment-streaming-destinations.md).

## Vérification de l’activation de l’audience {#verify}

Vérifiez les [documentation sur la surveillance des destinations](../dataflows/ui/monitor-destinations.md) pour obtenir des informations détaillées sur la manière de surveiller le flux de données vers vos destinations.