---
keywords: Experience Platform;home;popular topics;Audience manager source connector;Audience Manager;audience manager connector
solution: Experience Platform
title: Création d’un connecteur source Adobe Audience Manager dans l’interface utilisateur
topic: overview
type: Tutorial
description: Ce didacticiel vous guide tout au long des étapes nécessaires pour créer des connecteurs source pour Adobe Audience Manager afin d’importer les données du Événement d’expérience de consommation dans la plate-forme à l’aide de l’interface utilisateur.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 11%

---


# Création d’un connecteur source Adobe Audience Manager dans l’interface utilisateur

Ce didacticiel vous guide tout au long des étapes nécessaires pour créer des connecteurs source pour Adobe Audience Manager afin d’importer les données du Événement d’expérience de consommation dans la plate-forme à l’aide de l’interface utilisateur.

## Création d’une connexion source avec Adobe Audience Manager

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail sources. L’écran **Catalogue** affiche diverses sources pour lesquelles vous pouvez créer des connexions source et chaque source affiche le nombre de connexions existantes qui lui sont associées.

Sous la catégorie des applications **d’** Adobe, sélectionnez **Adobe Audience Manager** pour afficher une barre d’informations sur la droite de l’écran. La barre d&#39;informations fournit une brève description de la source sélectionnée ainsi que des options permettant de vue de sa documentation ou de se connecter à la source.

Pour créer un connecteur source pour Adobe Audience Manager, cliquez sur **Ajouter des données**.

![](../../../../images/tutorials/create/aam/catalog.png)

Une boîte de dialogue s’affiche. Cliquez sur **Se connecter** pour créer la connexion.

![](../../../../images/tutorials/create/aam/connect_full.png)

Si une connexion source avec Adobe Audience Manager est établie, la page activité **** source du connecteur d&#39;Audience Manager s&#39;affiche.

![](../../../../images/tutorials/create/aam/flow.png)

Si vous souhaitez suspendre les données d’Audience Manager entrantes, vous pouvez le faire en cliquant sur la liste de flux de données et en faisant basculer son *état* dans la colonne *Propriétés* appropriée.

![](../../../../images/tutorials/create/aam/flow_disable.png)

## Étapes suivantes

Lorsqu’un flux de données d’Audience Manager est principal, les données entrantes sont automatiquement assimilées aux Profils client en temps réel. Vous pouvez désormais utiliser ces données entrantes et créer des segments d’audience à l’aide du service de segmentation de plate-forme. Pour plus d’informations, voir les documents suivants :

- [Présentation du profil client en temps réel](../../../../../profile/home.md)
- [Présentation du service de segmentation](../../../../../segmentation/home.md)