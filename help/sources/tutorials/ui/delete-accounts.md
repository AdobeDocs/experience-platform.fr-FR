---
keywords: Experience Platform ; accueil ; sujets populaires ; supprimer des comptes
description: Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour supprimer des comptes de l'espace de travail Sources.
solution: Experience Platform
title: Suppression de comptes de connexion source dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 12%

---

# Suppression de comptes de connexion source

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour supprimer des comptes de l&#39;espace de travail **[!UICONTROL Sources]**.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organiser les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

## Suppression de comptes à l’aide de l’interface utilisateur

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer des comptes et des flux de données. Chaque source indique le nombre de comptes et de flux de données existants qui leur sont associés.

Sélectionnez **[!UICONTROL Comptes]** pour accéder à la page **[!UICONTROL Comptes]**.

![catalogue-comptes](../../images/tutorials/delete-accounts/catalog.png)

Une liste de comptes existants s’affiche. Cette page contient une liste d&#39;informations pouvant être triées pour les comptes existants, tels que la source, le nom d&#39;utilisateur, les flux de données associés et la date de création. Sélectionnez l&#39;icône **entonnoir** en haut à gauche pour trier.

![flux de données-liste](../../images/tutorials/delete-accounts/accounts.png)

Le panneau de tri s’affiche sur le côté gauche de l’écran, avec une liste de sources disponibles. Vous pouvez sélectionner plusieurs sources à l’aide de la fonction de tri.

Sélectionnez la source à laquelle vous souhaitez accéder et localisez le compte que vous avez l&#39;intention de supprimer de la liste des comptes dans l&#39;interface principale. Dans l&#39;exemple, la source sélectionnée est **[!DNL Azure Blob Storage]** et le nom du compte est **[!UICONTROL blobTestConnector]**. Lors de la sélection de plusieurs sources dans le panneau de tri, les comptes que vous avez créés le plus récemment apparaissent en premier, car la liste est triée par date de création.

Sélectionnez le compte que vous souhaitez supprimer.

![flux de données-tri](../../images/tutorials/delete-accounts/sort.png)

Le panneau **[!UICONTROL Propriétés]** s&#39;affiche sur le côté droit de l&#39;écran et contient des informations concernant le compte sélectionné.

Sélectionnez les points de suspension (`...`) en regard du nom du compte que vous souhaitez supprimer. Un panneau contextuel s’affiche, fournissant des options pour **[!UICONTROL Ajouter les données]**, **[!UICONTROL Modifier les détails]** et **[!UICONTROL Supprimer]**. Sélectionnez **[!UICONTROL Supprimer]** pour supprimer le compte.

![flux de données-tri](../../images/tutorials/delete-accounts/delete.png)

Une boîte de dialogue de confirmation finale s’affiche, sélectionnez **[!UICONTROL Supprimer]** pour terminer le processus.

![Supprimez](../../images/tutorials/delete-accounts/confirm.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez utilisé l&#39;espace de travail **[!UICONTROL Sources]** pour supprimer des comptes existants.

Pour savoir comment exécuter ces opérations par programmation à l&#39;aide de l&#39;API [!DNL Flow Service], reportez-vous au didacticiel de [suppression de connexions à l&#39;aide de l&#39;API Flow Service](../../tutorials/api/delete.md).
