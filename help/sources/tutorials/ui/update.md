---
keywords: Experience Platform;home;popular topics;update accounts;
description: null
solution: Experience Platform
title: Mettre à jour les détails du compte dans l’interface utilisateur
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 413687a0d9e790ea3f61a858002e9510216d7c34
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 13%

---


# Mettre à jour les détails du compte dans l’interface utilisateur

Dans certains cas, il peut être nécessaire de mettre à jour les détails d&#39;un compte de sources existantes. L&#39;espace de travail [!UICONTROL Sources] vous permet de modifier, ajouter et supprimer des détails d&#39;un compte, y compris les valeurs de son nom, de sa description et de ses informations d&#39;identification d&#39;authentification.

Ce didacticiel décrit la procédure à suivre pour mettre à jour les détails et les informations d’identification d’un compte existant à partir de l’espace de travail [!UICONTROL Sources] .

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

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