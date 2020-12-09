---
keywords: Experience Platform;home;popular topics;update accounts
description: Dans certains cas, il peut être nécessaire de mettre à jour les détails d'un compte de sources existantes. L’espace de travail Sources vous permet d’ajouter, de modifier et de supprimer des détails d’une connexion existante par lot ou en flux continu, y compris son nom, sa description et ses informations d’identification.
solution: Experience Platform
title: Mettre à jour les détails du compte dans l’interface utilisateur
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 9b48bc1426e6259ea0b2cf9b420b55b92712f7c2
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 4%

---


# Mettre à jour les détails du compte dans l’interface utilisateur

Dans certains cas, il peut être nécessaire de mettre à jour les détails d&#39;un compte de sources existantes. L’espace de travail [!UICONTROL Sources] vous permet d’ajouter, de modifier et de supprimer des détails d’une connexion existante par lot ou en flux continu, y compris son nom, sa description et ses informations d’identification.

Ce didacticiel décrit la procédure à suivre pour mettre à jour les détails et les informations d’identification d’un compte existant à partir de l’espace de travail [!UICONTROL Sources] .

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Sources](../../home.md): L’Experience Platform DNL permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de plate-forme.
- [Sandbox](../../../sandboxes/home.md): DNL Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

## Mettre à jour les comptes

Connectez-vous à l’interface utilisateur [de l’](https://platform.adobe.com) Experience Platform, puis sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources] . Sélectionnez **[!UICONTROL Comptes]** dans l&#39;en-tête supérieur pour vue des comptes existants.

![catalogue](../../images/tutorials/update/catalog.png)

The **[!UICONTROL Accounts]** page appears. Cette page contient une liste de comptes consultables, y compris des informations sur leur source, leur nom d&#39;utilisateur, le nombre de flux de données et la date de création.

Sélectionnez le ![filtre d’icône de filtre](../../images/tutorials/update/filter.png) en haut à gauche pour lancer le panneau de tri.

![comptes-liste](../../images/tutorials/update/accounts-list.png)

Le panneau de tri fournit une liste de toutes les sources. Vous pouvez sélectionner plusieurs sources dans la liste pour accéder à une sélection filtrée de comptes associés à différentes sources.

Sélectionnez la source avec laquelle vous souhaitez travailler pour voir une liste de ses comptes existants. Une fois que vous avez identifié le compte à mettre à jour, sélectionnez les points de suspension (`...`) en regard du nom du compte.

![comptes-tri](../../images/tutorials/update/accounts-sort.png)

Un menu déroulant s’affiche, vous permettant d’ **[!UICONTROL Ajouter des données]**, de **[!UICONTROL modifier des détails]** et de **[!UICONTROL supprimer]**. Sélectionnez **[!UICONTROL Modifier les détails]** dans le menu pour mettre à jour votre compte.

![mettre à jour](../../images/tutorials/update/update.png)

La boîte de dialogue **[!UICONTROL Modifier les détails]** du compte vous permet de mettre à jour le nom, la description et les informations d’identification d’authentification d’un compte. Une fois que vous avez mis à jour les informations de votre choix, sélectionnez **[!UICONTROL Enregistrer]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Après quelques instants, une boîte de confirmation verte s’affiche en bas de l’écran pour confirmer une mise à jour réussie.

![update-confirmé](../../images/tutorials/update/update-confirmed.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez utilisé l’espace de travail [!UICONTROL Sources] pour mettre à jour les informations de compte.

Pour obtenir des instructions sur la façon d’effectuer ces opérations par programmation à l’aide de l’ [!DNL Flow Service] API, consultez le didacticiel sur la [mise à jour des informations de connexion à l’aide de l’API](../../tutorials/api/update.md)Flow Service.