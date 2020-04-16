---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source d’attributs du client dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Création d’un connecteur source d’attributs du client dans l’interface utilisateur

Ce didacticiel décrit la procédure à suivre pour créer un connecteur source dans l’interface utilisateur afin de collecter les attributs du client  les données dans Adobe Experience Platform. Pour plus d’informations sur les attributs du client, reportez-vous à la [d’aperçu](https://docs.adobe.com/content/help/fr-FR/core-services/interface/customer-attributes/attributes.html).

## Création d’une connexion source

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail Sources. L’écran *Catalogue* affiche les sources disponibles pour créer des connexions entrantes avec, et chaque source indique le nombre de connexions existantes qui y sont associées. Sélectionnez l’option Attributs **du** client, puis cliquez sur **Connecter la source**. Prévoyez un certain temps pour que la connexion soit établie, vous serez redirigé si une connexion est établie.

>[!NOTE] Si vous avez déjà établi un connecteur source pour les données du des attributs du client, l’option de connexion à la source est désactivée.

![](../../../../images/tutorials/create/customer-attributes/CA-sources_catalog.png)

L’écran   *source* toutes les connexions précédemment établies pour les données de l’des attributs du client, vous pouvez créer une nouvelle connexion en cliquant sur **Sélectionner les données**.

>[!NOTE] Vous pouvez établir plusieurs connexions entrantes vers une source pour importer différentes données.

![](../../../../images/tutorials/create/customer-attributes/CA-source_activity.png)

Dans le des jeux de données de d’attributs du client disponibles, sélectionnez celui que vous souhaitez importer dans la plateforme et cliquez sur **Suivant**.

>[!NOTE] Un seul jeu de données peut être sélectionné par connexion à la source des attributs du client.

![](../../../../images/tutorials/create/customer-attributes/CA-select_data.png)

L’étape *Révision* s’affiche, vous permettant de vérifier votre nouvelle connexion entrante avant de la créer. Les détails de la connexion sont regroupés par , notamment :

* *Détails* de la source : Affiche le type de connexion source et les données source sélectionnées.
* *Détails* du : Lors de la création d’autres connecteurs source, ce indique dans quel jeu de données les données source sont assimilées, y compris le auquel le jeu de données adhère. Les attributs du client  données sont automatiquement mises en correspondance et assimilées dans le  client en temps réel.

![](../../../../images/tutorials/create/customer-attributes/CA-review.png)

## Étapes suivantes

Une fois la connexion créée, un  et un jeu de données sont automatiquement créés pour contenir les données entrantes. Une fois l’assimilation initiale terminée, les données d’attributs du client  peuvent être utilisées par les services de plateforme en aval, tels que l’ du client en temps réel et le service de segmentation. Pour plus d’informations, reportez-vous au  suivant :

* [Présentation du profil client en temps réel](../../../../../profile/home.md)
* [Présentation du service de segmentation](../../../../../segmentation/home.md)
