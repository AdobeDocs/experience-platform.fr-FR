---
title: Activer les audiences Audience Manager par le biais d’une activation étendue
description: Découvrez comment activer les audiences Audience Manager vers des destinations sociales et publicitaires, via l’activation étendue d’Audience Manager.
exl-id: 4105f5c5-db69-414f-9ee4-8630b0a86da7
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Activer des audiences via l’activation étendue d’Audience Manager

Cette page décrit le workflow de bout en bout que vous devez suivre pour activer les audiences d’Audience Manager vers les plateformes de destination prises en charge par l’activation étendue.

## Avant de commencer {#before-you-begin}

Les étapes décrites dans ce guide supposent que vous ayez lu la page [Aperçu de l’activation étendue](overview.md) et que vous ayez confirmé que vous remplissez les conditions préalables à l’activation de l’audience.

>[!IMPORTANT]
>
>Pour activer des audiences par le biais de [!DNL Expanded Activation], assurez-vous que vos audiences Audience Manager sont basées sur des adresses e-mail **hachées**. Voir les [conditions préalables](overview.md#prerequisites) pour plus d’informations.

## Étape 1 : configurer la connexion source Audience Manager {#configure-source}

Le connecteur source [Audience Manager](../sources/connectors/adobe-applications/audience-manager.md) envoie les données d’audience collectées dans Adobe Audience Manager pour activation sur les plateformes de destination prises en charge par l’activation étendue.

Suivez le guide expliquant comment [créer une connexion source Audience Manager](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) pour configurer votre connecteur source.

![Image de l’interface utilisateur d’Experience Platform montrant l’onglet Sources avec la connexion source Audience Manager.](assets/sources-tab.png)

>[!TIP]
>
>Le connecteur source Adobe Audience Manager est le seul connecteur source disponible dans l’activation étendue.
>
>Si vous souhaitez ingérer des audiences en fonction d’identifiants supplémentaires, vous devez acheter une édition de [Real-Time CDP](../rtcdp/overview.md). Contactez votre représentant Adobe pour plus d’informations.

### Affichage et surveillance des audiences ingérées {#view-audiences}

Les audiences que vous importez dans Activation étendue à partir d’Audience Manager peuvent être affichées dans le tableau de bord **[!UICONTROL Audiences]**.

Pour afficher vos audiences, accédez à **[!UICONTROL Client]** -> **[!UICONTROL Audiences]** -> **[!UICONTROL Parcourir]**.

![Image de l’interface utilisateur d’Experience Platform montrant la page Audiences.](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* Il faut parfois jusqu’à 48 heures pour renseigner complètement les audiences dans l’activation étendue. Cela s’applique également aux mises à jour des audiences Audience Manager existantes.
>* Les audiences Audience Manager nouvellement créées n’apparaissent pas automatiquement dans l’activation étendue. Pour ingérer de nouveaux segments dans Activation étendue, vous devez les ajouter via le connecteur source Audience Manager.

Après avoir configuré votre connecteur source Audience Manager, passez à l’[étape 2](#create-destination-connection).

## Étape 2 : créer une connexion de destination {#create-destination-connection}

Avant d’envoyer vos audiences Audience Manager vers la plateforme de destination de votre choix, vous devez d’abord créer une connexion à une plateforme de destination.

Dans la barre latérale gauche, accédez à **[!UICONTROL Connexions]** -> **[!UICONTROL Destinations]** -> **[!UICONTROL Catalogue]**.

Les catégories de destination disponibles pour [!DNL Expanded Activation] sont [publicité](../destinations/catalog/advertising/overview.md) et [social](../destinations/catalog/social/overview.md).

![Image de l’interface utilisateur d’Experience Platform montrant le catalogue de destination pour l’activation étendue.](assets/destination-catalog.png)

Pour créer une connexion à une plateforme de destination, suivez le guide sur [comment créer une connexion de destination](../destinations/ui/connect-destination.md). Passez ensuite à [étape 3](#activate-audiences).

## Étape 3 : activer les audiences vers la destination {#activate-audiences}

Après avoir correctement [ingéré des audiences Audience Manager](#configure-source) et [créé une nouvelle connexion de destination](#create-destination-connection), vous pouvez maintenant activer vos audiences vers la plateforme de destination de votre choix.

![Image de l’interface utilisateur d’Experience Platform montrant le catalogue de destination pour l’activation étendue.](assets/activate-audiences.png)

Pour activer des audiences vers la destination, suivez le guide sur la [Comment activer des audiences vers des destinations de diffusion en streaming](../destinations/ui/activate-segment-streaming-destinations.md).

## Vérifier l’activation de l’audience {#verify}

Consultez la [documentation sur la surveillance des destinations](../dataflows/ui/monitor-destinations.md) pour obtenir des informations détaillées sur la surveillance du flux de données vers les destinations.
