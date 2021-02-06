---
keywords: Experience Platform ; accueil ; rubriques populaires ; connexion en flux continu ; créer une connexion en flux continu ; guide ui ; didacticiel ; créer une connexion en flux continu ; assimilation en flux continu ; assimilation ;
solution: Experience Platform
title: Création d’une connexion de diffusion en continu à l’aide de l’interface utilisateur
topic: tutorial
type: Tutorial
description: Ce guide de l’interface utilisateur vous aidera à créer une connexion en continu à l’aide d’Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 73%

---


# Création d’une connexion en continu à l’aide de l’interface utilisateur

Ce guide de l’interface utilisateur vous aidera à créer une connexion en continu à l’aide d’Adobe Experience Platform.

## Prise en main

Pour début des données en flux continu à [!DNL Experience Platform], vous devez d’abord créer une connexion HTTP en flux continu. Lors de la création d’une connexion en continu, vous devez fournir des détails clés, tels que la source des données en flux continu, et indiquer si vous prévoyez d’envoyer des données à partir d’une source approuvée (authentifiée) ou non approuvée (non authentifiée).

Après avoir enregistré une connexion en continu, vous disposerez d’une URL unique avec laquelle vous pourrez transmettre des données en continu à [!DNL Platform].

Veuillez noter que pour compléter ce guide, vous devez avoir accès à Adobe Experience Platform. Si vous n&#39;avez pas accès à [!DNL Platform], contactez votre administrateur système avant de continuer.

## Création d’une connexion en continu

Après vous être connecté à l&#39;interface utilisateur [!DNL Experience Platform], cliquez sur **[!UICONTROL Sources]** pour ouvrir l&#39;onglet **[!UICONTROL Catalogue]**. Cette page affiche les types de source disponibles sous forme de cartes individuelles, chaque carte contenant une bulle qui indique le nombre de flux de données créés à partir de connexions en continu à des jeux de données.

![](../images/streaming-ingestion/ui/click-sources.png)

Sur la page **[!UICONTROL Sources]**, cliquez sur **[!UICONTROL API HTTP]**, puis sur **[!UICONTROL Connecter une source]**.

![](../images/streaming-ingestion/ui/click-connect-source.png)

L’écran **[!UICONTROL Se connecter avec le protocole HTTP]** s’affiche. Dans **[!UICONTROL Informations sur le service]**, indiquez le nom et une description de votre nouvelle connexion en continu.

Sous **[!UICONTROL Authentification du compte]**, sélectionnez les propriétés de configuration suivantes pour votre connexion en continu :

- **[!UICONTROL Authentification] :** si la connexion en flux continu nécessite une authentification. L’authentification garantit que les données sont collectées auprès de sources approuvées. Il est recommandé de l’activer si vous traitez des informations d’identification personnelle (PII).
- **[!UICONTROL Compatibilité] des Schémas XDM :** si cette connexion de flux continu va envoyer des événements compatibles avec les schémas XDM. Par défaut, cette propriété est **activée**.

Une fois les propriétés de configuration sélectionnées, cliquez sur **[!UICONTROL Se connecter]**. Votre connexion HTTP en continu est maintenant créée. Vous pouvez désormais la visualiser sous l’onglet **[!UICONTROL Parcourir]** de l’espace de travail **[!UICONTROL Sources]**.

![](../images/streaming-ingestion/ui/http-sources-details.png)

Dans l’onglet **[!UICONTROL Parcourir]**, vous pouvez cliquer sur votre nouvelle connexion HTTP en continu et voir les détails de cette dernière.

![](../images/streaming-ingestion/ui/browse-sources.png)

En cliquant sur le lien hypertexte du nom de la connexion, vous pouvez sélectionner les données à afficher en configurant le jeu de données connecté, via le bouton **[!UICONTROL Sélectionner les données]**.

![](../images/streaming-ingestion/ui/select-data.png)

Vous pouvez soit [créer un nouveau jeu de données](#create-a-new-dataset), soit [utiliser un jeu de données existant](#use-an-existing-dataset).

### Création d’un nouveau jeu de données

Pour créer un nouveau jeu de données, indiquez le nom, la description ainsi que le schéma de cible du jeu de données.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

Après avoir saisi tous les détails et cliqué sur **[!UICONTROL Suivant]**, vous pouvez consulter les informations fournies avant de cliquer sur **[!UICONTROL Terminer]** pour connecter le jeu de données à votre connexion HTTP en continu.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### Utilisation d’un jeu de données existant

Pour utiliser un jeu de données existant, sélectionnez le **[!UICONTROL nom du jeu de données de sortie]**.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

Après avoir cliqué sur **[!UICONTROL Suivant]**, vous pouvez consulter les informations avant de cliquer sur **[!UICONTROL Terminer]** pour connecter le jeu de données sélectionné à votre connexion HTTP en continu.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion HTTP en flux continu, ce qui vous permet d’utiliser le point de terminaison de flux continu pour accéder à diverses API [!DNL Data Ingestion]. Pour savoir comment créer une connexion en continu dans l’API, consultez le [tutoriel sur la création d’une connexion en continu](../tutorials/create-streaming-connection.md).
