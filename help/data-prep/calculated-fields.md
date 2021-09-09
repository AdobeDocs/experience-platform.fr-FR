---
keywords: Experience Platform;accueil;rubriques populaires;mapper csv;mapper le fichier csv;mapper le fichier csv à xdm;mapper csv à xdm;guide de lʼui;mappeur;mappage;data prep;préparation des données;préparer des données;
solution: Experience Platform
title: Présentation de Data Prep
topic-legacy: overview
description: Ce document présente Data Prep dans Adobe Experience Platform.
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 19%

---


# Les champs calculés

Les champs calculés permettent de créer des valeurs en fonction des attributs du schéma d’entrée. Ces valeurs peuvent ensuite être affectées à des attributs dans le schéma cible et recevoir un nom et une description pour faciliter la référence.

Pour créer un champ calculé, sélectionnez **[!UICONTROL Ajouter un champ calculé]**.

![](./images/calculated-fields/add-calculated-field.png)

Le panneau **[!UICONTROL Créer un champ calculé]** s’affiche. La boîte de dialogue de gauche contient les champs, fonctions et opérateurs pris en charge dans les champs calculés. Sélectionnez l&#39;un des onglets pour commencer à ajouter des fonctions, des champs ou des opérateurs dans l&#39;éditeur d&#39;expression.

![](./images/calculated-fields/create-calculated-field.png)

| Tabulation | Description |
| --- | ----------- |
| Fonction | L’onglet Fonctions répertorie les fonctions disponibles pour transformer les données. Pour en savoir plus sur les fonctions que vous pouvez utiliser dans les champs calculés, consultez le guide sur [l’utilisation des fonctions de préparation de données (mappeur)](./functions.md). |
| Champ | L&#39;onglet Champs répertorie les champs et attributs disponibles dans le schéma source. |
| Opérateur | L&#39;onglet Opérateurs répertorie les opérateurs disponibles pour la transformation des données. |

Vous pouvez ajouter manuellement des champs, des fonctions et des opérateurs à l’aide de l’éditeur d’expression situé au centre. Sélectionnez l&#39;éditeur pour commencer la création d&#39;une expression.

![](./images/calculated-fields/write-calculated-field.png)

Sélectionnez **[!UICONTROL Enregistrer]** pour continuer.

L’écran de mappage réapparaît avec le champ source que vous venez de créer. Appliquez le champ cible correspondant et sélectionnez **[!UICONTROL Terminer]** pour terminer le mapping.

![](./images/calculated-fields/new-calculated-field.png)