---
keywords: Experience Platform;accueil;rubriques les plus consultées; supprimer des comptes
description: Les connecteurs Source de Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour supprimer des comptes de l’espace de travail Sources .
solution: Experience Platform
title: Suppression des comptes de connexion Source dans l’interface utilisateur
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
TQID: https://experienceleague.adobe.com/1HxgbCfzsf7otxyMJVr-cxSuQ4hmqfsAXNh-aI-YNcI
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 493
ht-degree: 19%

---

# Supprimer les comptes de connexion source

Les connecteurs Source de Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour supprimer des comptes de l’espace de travail **[!UICONTROL Sources]**.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Tutoriel sur l’éditeur de schémas](../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

## Supprimer des comptes à l’aide de l’interface utilisateur

>[!TIP]
>
>Avant de supprimer le compte source, vous devez d’abord supprimer les flux de données existants associés à ce compte source. Pour supprimer des flux de données existants, reportez-vous au tutoriel sur la [suppression de flux de données sources dans l’interface utilisateur](./delete.md).

Connectez-vous à [&#128279;](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer des comptes et des flux de données. Chaque source affiche le nombre de comptes et de flux de données existants qui leur sont associés.

Sélectionnez **[!UICONTROL Comptes]** pour accéder à la page **[!UICONTROL Comptes]**.

![comptes-catalogue](../../images/tutorials/delete-accounts/catalog.png)

Une liste des comptes existants s’affiche. Sur cette page, vous trouverez une liste d’informations triables pour les comptes existants tels que la source, le nom d’utilisateur, les flux de données associés et la date de création. Sélectionnez l’icône **&#x200B;**&#x200B;en haut à gauche pour trier.

![dataflows-list](../../images/tutorials/delete-accounts/accounts.png)

Le panneau de tri s’affiche dans la partie gauche de l’écran et contient la liste des sources disponibles. Vous pouvez sélectionner plusieurs sources à l’aide de la fonction de tri.

Sélectionnez la source à laquelle vous souhaitez accéder et localisez le compte que vous souhaitez supprimer dans la liste des comptes de l&#39;interface principale. Dans l’exemple, la source sélectionnée est **[!DNL Azure Blob Storage]** et le nom du compte est **[!UICONTROL blobTestConnector]**. Lorsque vous sélectionnez plusieurs sources dans le panneau de tri, les comptes créés le plus récemment apparaissent en premier, car la liste est triée par date de création.

Sélectionnez le compte que vous souhaitez supprimer.

![dataflows-sort](../../images/tutorials/delete-accounts/sort.png)

Le panneau **[!UICONTROL Propriétés]** s’affiche dans la partie droite de l’écran et contient des informations sur le compte sélectionné.

Sélectionnez les points de suspension (`...`) à côté du nom du compte que vous souhaitez supprimer. Un panneau pop-up s’affiche, fournissant des options pour **[!UICONTROL Ajouter des données]**, **[!UICONTROL Modifier les détails]** et **[!UICONTROL Supprimer]**. Sélectionnez **[!UICONTROL Supprimer]** pour supprimer le compte.

![dataflows-sort](../../images/tutorials/delete-accounts/delete.png)

Une boîte de dialogue de confirmation finale s’affiche. Sélectionnez **[!UICONTROL Supprimer]** pour terminer le processus.

![delete](../../images/tutorials/delete-accounts/confirm.png)

## Étapes suivantes

Ce tutoriel vous a permis d’utiliser l’espace de travail **[!UICONTROL Sources]** pour supprimer des comptes existants.

Pour savoir comment effectuer ces opérations par programmation à l’aide de l’API [!DNL Flow Service], reportez-vous au tutoriel [Supprimer des connexions à l’aide de l’API Flow Service](../../tutorials/api/delete.md)
