---
keywords: Experience Platform ; accueil ; rubriques populaires ; mettre à jour les comptes
description: Dans certains cas, il peut être nécessaire de mettre à jour les détails d'un compte de sources existantes. L’espace de travail Sources vous permet d’ajouter, de modifier et de supprimer des détails d’une connexion existante par lot ou en flux continu, y compris son nom, sa description et ses informations d’identification.
solution: Experience Platform
title: Mettre à jour les détails du compte de connexion à la source dans l’interface utilisateur
topic: aperçu
type: Tutoriel
translation-type: tm+mt
source-git-commit: 4a7405e2c8c97442d2781295dd827c6940aa33eb
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 10%

---


# Mettre à jour les détails du compte dans l’interface utilisateur

Dans certains cas, il peut être nécessaire de mettre à jour les détails d&#39;un compte de sources existantes. L&#39;espace de travail [!UICONTROL Sources] vous permet d&#39;ajouter, de modifier et de supprimer des détails d&#39;une connexion existante par lot ou en flux continu, y compris son nom, sa description et ses informations d&#39;identification.

Ce didacticiel décrit les étapes de mise à jour des détails et des informations d’identification d’un compte existant à partir de l’espace de travail [!UICONTROL Sources].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Sources](../../home.md) : Experience Platform permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de plate-forme.
- [Environnements de test](../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Mettre à jour les comptes

Connectez-vous à l&#39;[interface utilisateur Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l&#39;espace de travail [!UICONTROL Sources]. Sélectionnez **[!UICONTROL Comptes]** de l&#39;en-tête supérieur à la vue des comptes existants.

![catalogue](../../images/tutorials/update/catalog.png)

La page **[!UICONTROL Comptes]** s&#39;affiche. Cette page contient une liste de comptes consultables, y compris des informations sur leur source, leur nom d&#39;utilisateur, le nombre de flux de données et la date de création.

Sélectionnez l’icône de filtre ![filter](../../images/tutorials/update/filter.png) en haut à gauche pour lancer le panneau de tri.

![comptes-liste](../../images/tutorials/update/accounts-list.png)

Le panneau de tri fournit une liste de toutes les sources. Vous pouvez sélectionner plusieurs sources dans la liste pour accéder à une sélection filtrée de comptes associés à différentes sources.

Sélectionnez la source avec laquelle vous souhaitez travailler pour voir une liste de ses comptes existants. Une fois que vous avez identifié le compte à mettre à jour, sélectionnez les points de suspension (`...`) en regard du nom du compte.

![comptes-tri](../../images/tutorials/update/accounts-sort.png)

Un menu déroulant s’affiche, vous offrant des options pour **[!UICONTROL Ajouter les données]**, **[!UICONTROL Modifier les détails]** et **[!UICONTROL Supprimer]**. Sélectionnez **[!UICONTROL Modifier les détails]** dans le menu pour mettre à jour votre compte.

![mettre à jour](../../images/tutorials/update/update.png)

La boîte de dialogue **[!UICONTROL Modifier les détails du compte]** vous permet de mettre à jour le nom, la description et les informations d&#39;identification d&#39;authentification d&#39;un compte. Une fois que vous avez mis à jour les informations de votre choix, sélectionnez **[!UICONTROL Enregistrer]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Après quelques instants, une boîte de confirmation s’affiche en bas de l’écran pour confirmer une mise à jour réussie.

![update-confirmé](../../images/tutorials/update/update-confirmed.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez utilisé l&#39;espace de travail [!UICONTROL Sources] pour mettre à jour les informations d&#39;un compte source existant.

Pour savoir comment exécuter ces opérations par programmation à l&#39;aide de l&#39;API [!DNL Flow Service], consultez le didacticiel sur la [mise à jour des informations de connexion à l&#39;aide de l&#39;API Flow Service](../../tutorials/api/update.md).