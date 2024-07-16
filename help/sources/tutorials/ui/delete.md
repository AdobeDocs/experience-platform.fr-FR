---
keywords: Experience Platform;accueil;rubriques les plus consultées ; supprimer des flux de données
description: L’espace de travail des sources vous permet de supprimer les flux de données par lots et en flux continu existants qui contiennent des erreurs ou qui sont devenus obsolètes.
solution: Experience Platform
title: Suppression de flux de données dans l’interface utilisateur
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 18%

---

# Suppression de flux de données dans l’interface utilisateur

L’espace de travail [!UICONTROL Sources] vous permet de supprimer les flux de données de lot et de diffusion en continu existants qui contiennent des erreurs ou qui sont devenus obsolètes.

Ce tutoriel décrit les étapes à suivre pour supprimer des flux de données à l’aide de l’espace de travail [!UICONTROL Sources] .

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Sources ](../../home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
- [Sandbox](../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Supprimer des flux de données

Dans l’ [ interface utilisateur Experience Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources], puis sélectionnez **[!UICONTROL Flux de données]** dans l’en-tête supérieur.

![catalogue](../../images/tutorials/delete/catalog.png)

La page **[!UICONTROL Flux de données]** s’affiche. Cette page contient une liste de flux de données affichables, y compris des informations sur leur jeu de données cible, leur source, leur nom de compte et leur date de création.

Sélectionnez l’icône de filtre (![filter-icon](../../images/tutorials/delete/filter.png)) en haut à gauche pour lancer le panneau de tri.

![dataflows](../../images/tutorials/delete/dataflows.png)

Le panneau de tri fournit une liste de toutes les sources. Vous pouvez sélectionner plusieurs sources dans la liste pour accéder à une sélection filtrée de flux de données associés aux sources spécifiques que vous avez sélectionnées.

Sélectionnez la source que vous souhaitez utiliser pour afficher la liste de ses flux de données existants. Une fois que vous avez identifié le flux de données à supprimer, sélectionnez les ellipses (`...`) en regard du nom du flux de données.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Un menu déroulant s’affiche, vous fournissant des options pour modifier le planning de votre flux de données, désactiver le flux de données ou le supprimer entièrement.

Sélectionnez **[!UICONTROL Supprimer]** pour supprimer le flux de données.

![delete](../../images/tutorials/delete/delete.png)

Une boîte de dialogue de confirmation finale s’affiche. Sélectionnez **[!UICONTROL Supprimer]** pour terminer le processus.

![confirm](../../images/tutorials/delete/confirm.png)

Au bout de quelques instants, une boîte de confirmation s’affiche en bas de l’écran pour confirmer une suppression réussie.

![confirmé](../../images/tutorials/delete/confirmed.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez réussi à utiliser l’espace de travail [!UICONTROL Sources] pour supprimer un flux de données existant.

Consultez le tutoriel sur la [suppression de flux de données à l’aide de l’API Flow Service](../../tutorials/api/delete-dataflows.md) pour savoir comment effectuer ces opérations par programmation à l’aide d’appels API.
