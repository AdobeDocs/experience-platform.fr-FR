---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Adobe Analytics dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Création d’un connecteur source Adobe Analytics dans l’interface utilisateur

Ce didacticiel décrit la procédure à suivre pour créer un connecteur source Adobe Analytics dans l’interface utilisateur afin d’importer des données du client dans Adobe Experience Platform.

## Création d’une connexion source avec Adobe Analytics

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail Sources. L’écran *Catalogue* affiche les sources disponibles pour créer des connexions liées avec, et chaque source indique le nombre de connexions existantes qui y sont associées. Sélectionnez l’option pour **Adobe Analytics** , puis cliquez sur **source** pour afficher toutes les connexions intégrées établies à cette source.

![](../../../../images/tutorials/create/analytics/AA-sources_catalog.png)

L’écran   *source* toutes les connexions précédemment établies à Adobe Analytics, vous pouvez créer une nouvelle connexion en cliquant sur **Sélectionner des données**.

>[!NOTE] Vous pouvez établir plusieurs connexions intégrées à une source pour importer différentes données.

![](../../../..//images/tutorials/create/analytics/AA-source_activity.png)

Dans le  des suites de rapports disponibles, sélectionnez celle que vous souhaitez importer dans la plateforme et cliquez sur **Suivant**.

>[!NOTE] Une seule suite de rapports peut être sélectionnée par connexion à la source Analytics. En outre, une seule suite de rapports ne peut exister que dans un sandbox.

![](../../../../images/tutorials/create/analytics/AA-select_data.png)

L’étape *Révision* s’affiche, vous permettant de vérifier votre nouvelle connexion liée Analytics avant de la créer. Les détails de la connexion sont regroupés par , notamment :

* *Détails* de la source : Affiche le type de connexion source et la suite de rapports sélectionnée.
* *Détails* du : Lors de la création d’autres connecteurs source, ce indique dans quel jeu de données les données source sont assimilées, y compris le auquel le jeu de données adhère. Les données Analytics sont automatiquement mises en correspondance et assimilées dans le client en temps réel.

![](../../../../images/tutorials/create/analytics/AA-review.png)

## Étapes suivantes

Une fois la connexion créée, un  et un jeu de données sont automatiquement créés pour contenir les données entrantes. De plus, le renvoi des données se produit et ingère jusqu’à 13 mois de données historiques. Une fois l’assimilation initiale terminée, les données Analytics sont utilisées par les services de plateforme en aval, tels que le service de segmentation et le service de client en temps réel. Pour plus d’informations, reportez-vous au  suivant :

* [Présentation du profil client en temps réel](../../../../../profile/home.md)
* [Présentation du service de segmentation](../../../../../segmentation/home.md)
* [Présentation de l’espace de travail Data Science](../../../../../data-science-workspace/home.md)
* [Présentation du service](../../../../../query-service/home.md)

