---
keywords: Experience Platform;home;popular topics;customer attributes
solution: Experience Platform
title: Création d’un connecteur source d’attributs du client dans l’interface utilisateur
topic: overview
type: Tutorial
description: Ce didacticiel décrit les étapes à suivre pour créer un connecteur source dans l’interface utilisateur afin de collecter les données du profil des attributs du client dans Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 8%

---


# Création d’un connecteur source d’attributs du client dans l’interface utilisateur

Ce didacticiel décrit les étapes à suivre pour créer un connecteur source dans l’interface utilisateur afin de collecter les données du profil des attributs du client dans Adobe Experience Platform. Pour plus d’informations sur les attributs du client, voir le document [de](https://docs.adobe.com/content/help/fr-FR/core-services/interface/customer-attributes/attributes.html)présentation.

## Création d’une connexion source

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail sources. L’écran **[!UICONTROL Catalogue]** affiche les sources disponibles pour créer des connexions entrantes avec, et chaque source affiche le nombre de connexions existantes qui y sont associées. Sélectionnez l’option Attributs **** du client, puis sélectionnez **[!UICONTROL Ajouter les données]**. Prévoyez un certain temps pour établir la connexion, vous serez redirigé si une connexion est établie.

>[!NOTE]
>
>Si vous avez déjà établi un connecteur source pour les données du profil des attributs du client, l’option de connexion à la source est désactivée.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

L&#39;écran activité **** source liste toutes les connexions précédemment établies pour les données du profil des attributs du client. Vous pouvez créer une nouvelle connexion en cliquant sur **Sélectionner les données**.

>[!NOTE]
>
>Plusieurs connexions entrantes à une source peuvent être établies pour apporter différentes données.

![](../../../../images/tutorials/create/customer-attributes/source_activity.png)

Dans la liste des jeux de données de profil d&#39;attributs du client disponibles, sélectionnez celui dans lequel vous souhaitez importer [!DNL Platform] et cliquez sur **Suivant**.

>[!NOTE]
>
>Un seul jeu de données peut être sélectionné par connexion à la source des attributs du client.

![](../../../../images/tutorials/create/customer-attributes/select_data.png)

L’étape **Révision** s’affiche, vous permettant de vérifier votre nouvelle connexion entrante avant de la créer. Les détails de la connexion sont regroupés par catégorie, notamment :

* **Détails** de la source : Affiche le type de connexion source et les données source sélectionnées.
* **Détails** de la cible : Lors de la création d’autres connecteurs source, ce conteneur indique dans quel jeu de données les données source sont imbriquées, y compris le schéma auquel adhère le jeu de données. Les données du profil des attributs du client sont automatiquement mises en correspondance et ingérées dans les Profils client en temps réel.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## Étapes suivantes

Une fois la connexion créée, un schéma et un jeu de données cibles sont automatiquement créés pour contenir les données entrantes. Une fois l’assimilation initiale terminée, les données du profil des attributs du client peuvent être utilisées par [!DNL Platform] les services en aval, tels que [!DNL Real-time Customer Profile] et [!DNL Segmentation Service]. Pour plus d’informations, voir les documents suivants :

* [[!DNL Real-time Customer Profile] aperçu](../../../../../profile/home.md)
* [[!DNL Segmentation Service] aperçu](../../../../../segmentation/home.md)
