---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Surveiller et supprimer les flux de données
topic: overview
translation-type: tm+mt
source-git-commit: f08ad2c9cc48c08bcdc0e278481992e8789000b5
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 12%

---


# Surveiller et supprimer les flux de données

Les connecteurs source dans l’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour afficher les comptes et flux de données existants à partir de l&#39;espace de travail *[!UICONTROL Sources]* . Ce didacticiel décrit également les étapes à suivre pour supprimer des flux de données de l&#39;espace de travail *[!UICONTROL Sources]* .

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Système de modèle de données d’expérience (XDM)](../../../xdm/home.md)[!DNL Experience Platform] : cadre normalisé selon lequel organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [Real-time Customer Profile](../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

## Surveiller les comptes

Connectez-vous à [l’Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]* . L’écran *[!UICONTROL Catalogue]* affiche diverses sources pour lesquelles vous pouvez créer des comptes et des flux de données. Chaque source indique le nombre de comptes et de flux de données existants qui leur sont associés.

Sélectionnez *[!UICONTROL Comptes]* dans l&#39;en-tête supérieur pour vue des comptes existants.

![catalogue](../../images/tutorials/monitor/catalog.png)

Les pages *[!UICONTROL Comptes]* s&#39;affichent. Cette page contient une liste de comptes consultables, y compris des informations sur leur source, leur nom d&#39;utilisateur, le nombre de flux de données et la date de création.

Sélectionnez l&#39;icône d&#39;entonnoir en haut à gauche pour lancer la fenêtre de tri.

![comptes](../../images/tutorials/monitor/accounts-list.png)

Le panneau de tri vous permet d’accéder aux comptes à partir d’une source spécifique. Sélectionnez la source à utiliser et sélectionnez le compte dans la liste de droite.

![comptes-sélectionner](../../images/tutorials/monitor/accounts-sort.png)

Sur la page *[!UICONTROL Comptes]* , vous pouvez vue une liste de flux de données existants associés au compte auquel vous avez accédé. Sélectionnez le flux de données à vue.

![comptes-page](../../images/tutorials/monitor/dataflows.png)

L’écran activité ** de flux de données s’affiche. Cette page affiche le taux de messages consommés sous forme de graphique.

![dataset-flow-activité](../../images/tutorials/monitor/dataflow-activity.png)

## Surveiller les flux de données

Les flux de données sont accessibles directement à partir de la page *[!UICONTROL Catalogue]* sans afficher *[!UICONTROL les comptes]*. Sélectionnez *[!UICONTROL Flux de données]* dans l&#39;en-tête supérieur pour vue d&#39;une liste de flux de données existants.

![catalogue-flux de données](../../images/tutorials/monitor/catalog-dataflows.png)

Une liste de flux de données existants s’affiche. Cette page contient une liste de flux de données affichables, y compris des informations sur leur source, leur nom d&#39;utilisateur, leur nombre de flux de données et leur état. Sélectionnez l’icône d’entonnoir en haut à gauche pour effectuer le tri.

![flux de données-liste](../../images/tutorials/monitor/dataflows-list.png)

Le panneau de tri s’affiche. Sélectionnez la source à laquelle vous souhaitez accéder dans le menu de défilement et sélectionnez le flux de données dans la liste située à droite.

![sort-données-flux](../../images/tutorials/monitor/dataflows-sort.png)

L’écran activité ** de flux de données s’affiche. Cette page affiche le taux de messages consommés sous forme de graphique.

![dataset-flow-activité](../../images/tutorials/monitor/dataflow-activity.png)

Pour plus d&#39;informations sur la surveillance des flux de données et l&#39;assimilation, consultez le didacticiel sur la [surveillance des flux de données](../../../ingestion/quality/monitor-data-flows.md)en flux continu.

## Suppression d’un flux de données

Vous pouvez supprimer des flux de données créés incorrectement ou qui ne sont plus nécessaires en accédant à l’écran des flux de données. Localisez le flux de données que vous souhaitez supprimer à l&#39;aide de l&#39;icône d&#39;entonnoir de tri et sélectionnez-le pour ouvrir le panneau **[!UICONTROL Propriétés]** .

Pour supprimer un flux de données, sélectionnez **[!UICONTROL Supprimer]** dans les propriétés situées en haut à droite.

![delete-dataflows](../../images/tutorials/monitor/dataflows-sort-delete.png)

Un message de confirmation final s’affiche. Sélectionnez **[!UICONTROL Supprimer]** pour confirmer.

![verify-delete](../../images/tutorials/monitor/confirm-delete.png)

Après quelques instants, une boîte de confirmation verte s’affiche en bas de l’écran pour confirmer une suppression réussie.

![delete-success](../../images/tutorials/monitor/deletion-confirmed.png)

Vous pouvez également supprimer un flux de données de l’écran *[!UICONTROL Comptes]* . Localisez le compte auquel vous souhaitez accéder à l&#39;aide de l&#39;icône d&#39;entonnoir de tri et sélectionnez le compte dans la liste.

![comptes-sélectionner](../../images/tutorials/monitor/accounts-sort.png)

The *[!UICONTROL Accounts]* page appears. Sélectionnez le flux de données à supprimer, puis sélectionnez **[!UICONTROL Supprimer]** dans le panneau Propriétés pour terminer le processus.

![comptes-supprimer](../../images/tutorials/monitor/accounts-delete.png)

Suivez les étapes de confirmation décrites ci-dessus pour terminer le processus.

## Étapes suivantes

En suivant ce didacticiel, vous avez accédé à des comptes et flux de données existants à partir de l’espace de travail *[!UICONTROL Sources]* . Les données entrantes peuvent désormais être utilisées par [!DNL Platform] les services en aval tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, voir les documents suivants :

- [Présentation du profil client en temps réel](../../../profile/home.md)
- [Présentation de Data Science Workspace](../../../data-science-workspace/home.md)