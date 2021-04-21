---
keywords: Experience Platform ; accueil ; sujets populaires ; supprimer des flux de données
description: L’espace de travail sources vous permet de supprimer les flux de données par lot et en flux continu existants qui contiennent des erreurs ou qui sont devenus obsolètes.
solution: Experience Platform
title: Suppression de flux de données dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 5%

---

# Suppression de flux de données dans l’interface utilisateur

L&#39;espace de travail [!UICONTROL Sources] vous permet de supprimer les flux de données de traitement par lot et de diffusion en flux continu existants qui contiennent des erreurs ou sont devenus obsolètes.

Ce didacticiel décrit les étapes à suivre pour supprimer des flux de données à l’aide de l’espace de travail [!UICONTROL Sources].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Sources](../../home.md) :  [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
- [Sandbox](../../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

## Supprimer des flux de données

Dans l&#39;[interface utilisateur Experience Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l&#39;espace de travail [!UICONTROL Sources], puis sélectionnez **[!UICONTROL Flux de données]** dans l&#39;en-tête supérieur.

![catalogue](../../images/tutorials/delete/catalog.png)

La page **[!UICONTROL Flux de données]** s&#39;affiche. Cette page contient une liste de flux de données affichables, y compris des informations sur leur jeu de données de cible, leur source, leur nom de compte et leur date de création.

Sélectionnez l’icône de filtre (![filter-icon](../../images/tutorials/delete/filter.png)) en haut à gauche pour lancer le panneau de tri.

![flux de données](../../images/tutorials/delete/dataflows.png)

Le panneau de tri fournit une liste de toutes les sources. Vous pouvez sélectionner plusieurs sources dans la liste pour accéder à une sélection filtrée de flux de données associés aux sources particulières que vous avez sélectionnées.

Sélectionnez la source à utiliser pour afficher une liste de ses flux de données existants. Une fois que vous avez identifié le flux de données à supprimer, sélectionnez les ellipses (`...`) en regard du nom du flux de données.

![filtre de flux de données](../../images/tutorials/delete/dataflows-filter.png)

Un menu déroulant s&#39;affiche, vous offrant des options pour modifier la planification de votre flux de données, désactiver le flux de données ou le supprimer entièrement.

Sélectionnez **[!UICONTROL Supprimer]** pour supprimer le flux de données.

![Supprimez](../../images/tutorials/delete/delete.png)

Une boîte de dialogue de confirmation finale s’affiche. Sélectionnez **[!UICONTROL Supprimer]** pour terminer le processus.

![confirm](../../images/tutorials/delete/confirm.png)

Après quelques instants, une boîte de confirmation s’affiche en bas de l’écran pour confirmer une suppression réussie.

![confirmé](../../images/tutorials/delete/confirmed.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à utiliser l&#39;espace de travail [!UICONTROL Sources] pour supprimer un flux de données existant.

Consultez le didacticiel sur la [suppression de flux de données à l’aide de l’API Flow Service](../../tutorials/api/delete-dataflows.md) pour connaître les étapes à suivre pour effectuer ces opérations par programmation à l’aide d’appels d’API.
