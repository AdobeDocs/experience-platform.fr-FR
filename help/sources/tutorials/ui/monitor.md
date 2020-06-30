---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Surveiller les comptes et les flux de jeux de données
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---


# Surveiller les comptes et les flux de jeux de données

Les connecteurs source dans l’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour afficher les comptes et les flux de jeux de données existants à partir de l&#39;espace de travail *[!UICONTROL Sources]* .

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants de l&#39;Adobe Experience Platform :

- [Système](../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   - [Principes de base de la composition](../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   - [Didacticiel](../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [Profil](../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

## Surveiller les comptes

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">l’Adobe Experience Platform</a> , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]* . L’écran *[!UICONTROL Catalogue]* affiche diverses sources pour lesquelles vous pouvez créer des flux de jeux de données de comptes. Chaque source indique le nombre de comptes et de flux de jeux de données existants qui leur sont associés.

Sélectionnez *[!UICONTROL Comptes]* dans l&#39;en-tête supérieur pour vue des comptes existants.

![catalogue](../../images/tutorials/monitor/catalog.png)

Les pages *[!UICONTROL Comptes]* s&#39;affichent. Cette page contient une liste de comptes affichables, y compris des informations sur leur source, leur nom d&#39;utilisateur, le nombre de flux de jeux de données et la date de création.

Sélectionnez l’icône en haut à gauche pour lancer la fenêtre de tri.

![comptes](../../images/tutorials/monitor/accounts-list.png)

Le panneau de tri vous permet d’accéder aux comptes à partir d’une source spécifique. Sélectionnez la source à utiliser et sélectionnez le compte dans la liste de droite.

![comptes-sélectionner](../../images/tutorials/monitor/accounts-sort.png)

Sur la page *[!UICONTROL Comptes]* , vous pouvez vue une liste de flux de jeux de données existants associés au compte auquel vous avez accédé. Sélectionnez le flux de jeux de données à vue.

![comptes-page](../../images/tutorials/monitor/dataset-flows.png)

L’écran activité *[!UICONTROL de flux de]* données s’affiche. Cette page affiche le taux de messages consommés sous forme de graphique.

![dataset-flow-activité](../../images/tutorials/monitor/dataset-flows-activity.png)

## Surveiller les flux de données

Les flux de jeux de données sont accessibles directement à partir de la page *[!UICONTROL Catalogue]* sans afficher *[!UICONTROL les comptes]*. Sélectionnez *[!UICONTROL Flux]* de jeux de données de l’en-tête supérieur à la vue d’une liste de flux de jeux de données existants.

![dataset-flows](../../images/tutorials/monitor/dataset-flows-list.png)

Comme pour les comptes, vous pouvez trier la liste des flux de jeux de données à l’aide de l’icône de tri en haut à gauche. Sélectionnez la source que vous souhaitez vue et sélectionnez le flux du jeu de données dans la liste située à droite.

![select-dataset-flows](../../images/tutorials/monitor/dataset-flows-sort.png)

L’écran activité *[!UICONTROL de flux de]* données s’affiche. Cette page affiche le taux de messages consommés sous forme de graphique.

![dataset-flow-activité](../../images/tutorials/monitor/dataset-flows-activity.png)

Pour plus d&#39;informations sur la surveillance des jeux de données et l&#39;assimilation, consultez le didacticiel sur la [surveillance des flux de données](../../../ingestion/quality/monitor-data-flows.md)en flux continu.

## Étapes suivantes

En suivant ce didacticiel, vous avez accédé avec succès aux flux de comptes et de jeux de données existants à partir de l’espace de travail *[!UICONTROL Sources]* . Les données entrantes peuvent désormais être utilisées par [!DNL Platform] les services en aval tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, voir les documents suivants :

- [Présentation du profil client en temps réel](../../../profile/home.md)
- [Présentation de Data Science Workspace](../../../data-science-workspace/home.md)