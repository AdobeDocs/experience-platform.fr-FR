---
keywords: Experience Platform;accueil;rubriques les plus consultées;mettre à jour des comptes
description: Dans certains cas, il peut être nécessaire de mettre à jour les détails d’un compte de sources existant. L’espace de travail Sources vous permet d’ajouter, de modifier et de supprimer des détails sur un lot ou une connexion en continu existante, y compris son nom, sa description et ses informations d’identification.
solution: Experience Platform
title: Mise à jour des détails du compte de connexion Source dans l’interface utilisateur
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 16%

---

# Mise à jour des détails du compte dans l’interface utilisateur

Dans certains cas, il peut être nécessaire de mettre à jour les détails d’un compte de sources existant. L’espace de travail [!UICONTROL Sources] vous permet d’ajouter, de modifier et de supprimer les détails d’un lot ou d’une connexion en continu existante, y compris son nom, sa description et ses informations d’identification.

Ce tutoriel décrit les étapes à suivre pour mettre à jour les détails et les informations d’identification d’un compte existant à partir de l’espace de travail [!UICONTROL Sources] .

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
- [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Mettre à jour des comptes

Connectez-vous à l’[interface utilisateur Experience Platform](https://platform.adobe.com) et sélectionnez ensuite **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Sélectionnez **[!UICONTROL Comptes]** dans l’en-tête supérieur pour afficher les comptes existants.

![catalogue](../../images/tutorials/update/catalog.png)

La page **[!UICONTROL Comptes]** s’affiche. Cette page contient une liste des comptes consultables, y compris des informations sur leur source, leur nom d’utilisateur, le nombre de flux de données et la date de création.

Sélectionnez l’icône de filtre ![filter](/help/images/icons/filter.png) en haut à gauche pour lancer le panneau de tri.

![accounts-list](../../images/tutorials/update/accounts-list.png)

Le panneau de tri fournit une liste de toutes les sources. Vous pouvez sélectionner plusieurs sources dans la liste pour accéder à une sélection filtrée de comptes associés à différentes sources.

Sélectionnez la source que vous souhaitez utiliser pour afficher la liste de ses comptes existants. Une fois que vous avez identifié le compte à mettre à jour, sélectionnez les points de suspension (`...`) en regard du nom du compte.

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

Un menu déroulant s’affiche, vous fournissant des options pour **[!UICONTROL Ajouter des données]**, **[!UICONTROL Modifier les détails]** et **[!UICONTROL Supprimer]**. Sélectionnez **[!UICONTROL Modifier les détails]** dans le menu pour mettre à jour votre compte.

![Mettre à jour](../../images/tutorials/update/update.png)

La boîte de dialogue **[!UICONTROL Modifier les détails du compte]** vous permet de mettre à jour le nom, la description et les informations d’authentification d’un compte. Une fois que vous avez mis à jour les informations souhaitées, sélectionnez **[!UICONTROL Enregistrer]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Au bout de quelques instants, une boîte de confirmation s’affiche en bas de l’écran pour confirmer une mise à jour réussie.

![update-confirm](../../images/tutorials/update/update-confirmed.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez utilisé l’espace de travail [!UICONTROL Sources] pour mettre à jour les informations d’un compte source existant.

Pour savoir comment effectuer ces opérations par programmation à l’aide de l’API [!DNL Flow Service], reportez-vous au tutoriel sur la [mise à jour des informations de connexion à l’aide de l’API Flow Service](../../tutorials/api/update.md).
