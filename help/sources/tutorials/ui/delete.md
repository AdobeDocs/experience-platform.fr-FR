---
keywords: Experience Platform;accueil;rubriques les plus consultées ; supprimer des flux de données
description: L’espace de travail des sources vous permet de supprimer les flux de données par lots et en flux continu existants qui contiennent des erreurs ou qui sont devenus obsolètes.
solution: Experience Platform
title: Suppression de flux de données dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 19%

---

# Suppression de flux de données dans l’interface utilisateur

Le [!UICONTROL Sources] workspace vous permet de supprimer les flux de données de lot et de flux existants qui contiennent des erreurs ou sont devenus obsolètes.

Ce tutoriel décrit les étapes à suivre pour supprimer des flux de données à l’aide de la méthode [!UICONTROL Sources] workspace.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Sources ](../../home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
- [Sandbox](../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuelles qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Supprimer des flux de données

Dans le [Interface utilisateur Experience Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à la fonction [!UICONTROL Sources] workspace, puis sélectionnez **[!UICONTROL Flux de données]** dans l’en-tête supérieur.

![catalogue](../../images/tutorials/delete/catalog.png)

Le **[!UICONTROL Flux de données]** s’affiche. Cette page contient une liste de flux de données affichables, y compris des informations sur leur jeu de données cible, leur source, leur nom de compte et leur date de création.

Sélectionnez l’icône de filtre (![filter-icon](../../images/tutorials/delete/filter.png)) en haut à gauche pour lancer le panneau de tri.

![flux de données](../../images/tutorials/delete/dataflows.png)

Le panneau de tri fournit une liste de toutes les sources. Vous pouvez sélectionner plusieurs sources dans la liste pour accéder à une sélection filtrée de flux de données associés aux sources spécifiques que vous avez sélectionnées.

Sélectionnez la source que vous souhaitez utiliser pour afficher la liste de ses flux de données existants. Une fois que vous avez identifié le flux de données à supprimer, sélectionnez les ellipses (`...`) en regard du nom du flux de données.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Un menu déroulant s’affiche, vous fournissant des options pour modifier le planning de votre flux de données, désactiver le flux de données ou le supprimer entièrement.

Sélectionner **[!UICONTROL Supprimer]** pour supprimer le flux de données.

![delete](../../images/tutorials/delete/delete.png)

Une boîte de dialogue de confirmation finale s’affiche. Sélectionner **[!UICONTROL Supprimer]** pour terminer le processus.

![confirm](../../images/tutorials/delete/confirm.png)

Au bout de quelques instants, une boîte de confirmation s’affiche en bas de l’écran pour confirmer une suppression réussie.

![confirm](../../images/tutorials/delete/confirmed.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez utilisé avec succès la méthode [!UICONTROL Sources] espace de travail pour supprimer un flux de données existant.

Voir le tutoriel sur [suppression de flux de données à l’aide de l’API Flow Service](../../tutorials/api/delete-dataflows.md) pour savoir comment effectuer ces opérations par programmation à l’aide d’appels API.
