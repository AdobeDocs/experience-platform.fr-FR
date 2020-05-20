---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’une connexion en flux continu à l’aide de l’interface utilisateur
topic: tutorial
translation-type: tm+mt
source-git-commit: 181719e729748adcde62199c9406a97b7a807182
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# Création d’une connexion en flux continu à l’aide de l’interface utilisateur

Ce guide d’interface utilisateur vous aidera à créer une connexion de flux continu à l’aide d’Adobe Experience Platform.

## Prise en main

Pour début des données en flux continu sur la plateforme d’expérience, vous devez d’abord créer une connexion HTTP en flux continu. Lors de la création d’une connexion en flux continu, vous devez fournir des détails clés tels que la source des données en flux continu et indiquer si vous avez l’intention d’envoyer des données à partir d’une source approuvée (authentifiée) ou non approuvée (non authentifiée).

Après avoir enregistré une connexion de diffusion en continu, vous disposez d’une URL unique qui peut être utilisée pour diffuser des données sur la plate-forme.

Veuillez noter que pour compléter ce guide, vous devrez accéder à Adobe Experience Platform. Si vous n&#39;avez pas accès à Platform, contactez votre administrateur système avant de continuer.

## Création d’une connexion en flux continu

Après vous être connecté à l’interface utilisateur de la plateforme d’expérience, cliquez sur **Sources** pour ouvrir l’onglet *Catalogue* . Cette page affiche les types de source disponibles sous forme de cartes individuelles, chaque carte contenant une bulle qui affiche le nombre de flux de données créés à partir de connexions en flux continu vers des jeux de données.

![](../images/streaming-ingestion/ui/click-sources.png)

Sur la page *Sources* , cliquez sur API **** HTTP, puis **Connectez la source**.

![](../images/streaming-ingestion/ui/click-connect-source.png)

L’écran *Connexion à HTTP* s’affiche. Sous Détails *du* service, indiquez à la fois le **nom** et une **description** de votre nouvelle connexion de diffusion en continu.

Sous *Authentification* du compte, sélectionnez les propriétés de configuration suivantes pour votre connexion de flux continu :

- **Authentification :** Indique si la connexion en flux continu nécessite ou non une authentification. L’authentification permet de s’assurer que les données sont collectées à partir de sources approuvées. Il est recommandé d’activer cette option si vous traitez d’informations d’identification personnelle.
- **Compatibilité des Schémas XDM :** Indique si cette connexion de flux continu envoie ou non des événements compatibles avec les schémas XDM. Par défaut, cette propriété est activée ****.

Une fois que vous avez terminé de sélectionner vos propriétés de configuration, cliquez sur **Se connecter**. Votre connexion HTTP en flux continu est maintenant créée et peut désormais être affichée sous l’onglet *Parcourir* de l’espace de travail *Sources* .

![](../images/streaming-ingestion/ui/http-sources-details.png)

Dans l&#39;onglet *Parcourir* , vous pouvez cliquer sur votre nouvelle connexion HTTP en flux continu et vue les détails de cette connexion.

![](../images/streaming-ingestion/ui/browse-sources.png)

En cliquant sur l&#39;hyperlien du nom de la connexion, vous pouvez sélectionner les données à afficher en configurant le jeu de données connecté, en cliquant sur *Sélectionner les données*.

![](../images/streaming-ingestion/ui/select-data.png)

Vous pouvez soit [créer un nouveau jeu](#create-a-new-dataset) de données, soit [utiliser un jeu de données](#use-an-existing-dataset)existant.

### Créer un jeu de données

Pour créer un nouveau jeu de données, indiquez le **nom**, la **description**, ainsi que le **Schéma** de cible du jeu de données.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

Après avoir inséré tous les détails et cliqué sur **Suivant**, vous pouvez consulter les détails fournis avant de cliquer sur **Terminer** pour connecter le jeu de données à votre connexion HTTP en flux continu.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### Utiliser un jeu de données existant

Pour utiliser un jeu de données existant, sélectionnez le nom **du jeu de données** Output.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

Après avoir cliqué sur **Suivant**, vous pouvez examiner les détails avant de cliquer sur **Terminer** pour connecter le jeu de données sélectionné à votre connexion HTTP en flux continu.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez créé une connexion HTTP en flux continu, ce qui vous permet d&#39;utiliser le point de terminaison de flux continu pour accéder à diverses API d&#39;importation de données. Pour obtenir des instructions sur la création d’une connexion en flux continu dans l’API, consultez le didacticiel [](../tutorials/create-streaming-connection.md)Création d’une connexion en flux continu.
