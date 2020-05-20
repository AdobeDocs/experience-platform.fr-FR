---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Surveiller les comptes et les flux de jeux de données
topic: overview
translation-type: tm+mt
source-git-commit: fc0a406bdea7b31e046d02427805a9deba557e93
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 1%

---


# Surveiller les comptes et les flux de jeux de données

Les connecteurs source d’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour afficher les comptes et les flux de jeux de données existants à partir de l&#39;espace de travail *Sources* .

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [Système](../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
   - [Principes de base de la composition](../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   - [Didacticiel](../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [Profil](../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

## Surveiller les comptes

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’écran *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer des flux de jeux de données de comptes. Chaque source indique le nombre de comptes et de flux de jeux de données existants qui leur sont associés.

Sélectionnez *Comptes* dans l&#39;en-tête supérieur pour vue des comptes existants.

![catalogue](../../images/tutorials/monitor/catalog.png)

Les pages *Comptes* s&#39;affichent. Cette page contient une liste de comptes affichables, y compris des informations sur leur source, leur nom d&#39;utilisateur, le nombre de flux de jeux de données et la date de création.

Sélectionnez l’icône en haut à gauche pour lancer la fenêtre de tri.

![comptes](../../images/tutorials/monitor/accounts-list.png)

Le panneau de tri vous permet d’accéder aux comptes à partir d’une source spécifique. Sélectionnez la source à utiliser et sélectionnez le compte dans la liste de droite.

![comptes-sélectionner](../../images/tutorials/monitor/accounts-sort.png)

Sur la page *Comptes* , vous pouvez vue une liste de flux de jeux de données existants associés au compte auquel vous avez accédé. Sélectionnez le flux de jeux de données à vue.

![comptes-page](../../images/tutorials/monitor/dataset-flows.png)

L’écran activité *de flux de* données s’affiche. Cette page affiche le taux de messages consommés sous forme de graphique.

![dataset-flow-activité](../../images/tutorials/monitor/dataset-flows-activity.png)

## Surveiller les flux de données

Les flux de jeux de données sont accessibles directement à partir de la page *Catalogue* sans afficher *les comptes*. Sélectionnez *Flux* de jeux de données de l’en-tête supérieur à la vue d’une liste de flux de jeux de données existants.

![dataset-flows](../../images/tutorials/monitor/dataset-flows-list.png)

Comme pour les comptes, vous pouvez trier la liste des flux de jeux de données à l’aide de l’icône de tri en haut à gauche. Sélectionnez la source que vous souhaitez vue et sélectionnez le flux du jeu de données dans la liste située à droite.

![select-dataset-flows](../../images/tutorials/monitor/dataset-flows-sort.png)

L’écran activité *de flux de* données s’affiche. Cette page affiche le taux de messages consommés sous forme de graphique.

![dataset-flow-activité](../../images/tutorials/monitor/dataset-flows-activity.png)

Pour plus d&#39;informations sur la surveillance des jeux de données et l&#39;assimilation, consultez le didacticiel sur la [surveillance des flux de données](../../../ingestion/quality/monitor-data-flows.md)en flux continu.

## Étapes suivantes

En suivant ce didacticiel, vous avez accédé avec succès aux flux de comptes et de jeux de données existants à partir de l’espace de travail *Sources* . Les données entrantes peuvent désormais être utilisées par les services Plateforme en aval, tels que le Profil client en temps réel et l’espace de travail Data Science. Pour plus d’informations, voir les documents suivants :

- [Présentation du profil client en temps réel](../../../profile/home.md)
- [Présentation de Data Science Workspace](../../../data-science-workspace/home.md)