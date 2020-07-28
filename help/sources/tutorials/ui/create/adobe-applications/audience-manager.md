---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Adobe Audience Manager dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 13%

---


# Création d’un connecteur source Adobe Audience Manager dans l’interface utilisateur

Ce didacticiel vous guide tout au long des étapes de création d’un connecteur source pour l’Adobe Audience Manager afin d’importer les données du Événement d’expérience de consommation dans Platform à l’aide de l’interface utilisateur.

## Créer une connexion source avec l&#39;Adobe Audience Manager

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">l’Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail sources. L’écran *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer des connexions source et chaque source affiche le nombre de connexions existantes qui lui sont associées.

Sous la catégorie des applications *d’* Adobe, sélectionnez **Adobe Audience Manager** pour afficher une barre d’informations sur la droite de l’écran. La barre d&#39;informations fournit une brève description de la source sélectionnée ainsi que des options permettant de vue de sa documentation ou de se connecter à la source.

Pour créer un connecteur source pour l’Adobe Audience Manager, cliquez sur **Connecter la source**.

![](../../../../images/tutorials/create/aam/aam_catalog.png)

Une boîte de dialogue s’affiche. Cliquez sur **Se connecter** pour créer la connexion.

![](../../../../images/tutorials/create/aam/aam_connect_full.png)

Si une connexion source avec l&#39;Adobe Audience Manager est établie, la page activité ** source du connecteur d&#39;Audience Manager s&#39;affiche.

![](../../../../images/tutorials/create/aam/aam_flow.png)

Si vous souhaitez suspendre les données d’Audience Manager entrantes, vous pouvez le faire en cliquant sur la liste de flux de données et en faisant basculer son *état* dans la colonne *Propriétés* appropriée.

![](../../../../images/tutorials/create/aam/aam_flow_disable.png)

## Étapes suivantes

Lorsqu’un flux de données d’Audience Manager est actif, les données entrantes sont automatiquement ingérées dans les Profils client en temps réel. Vous pouvez désormais utiliser ces données entrantes et créer des segments d’audience à l’aide de Platform Segmentation Service. Pour plus d’informations, voir les documents suivants :

- [Présentation du profil client en temps réel](../../../../../profile/home.md)
- [Présentation du service de segmentation](../../../../../segmentation/home.md)