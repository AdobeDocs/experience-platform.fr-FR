---
keywords: Experience Platform;accueil;rubriques populaires;mapper csv;mapper le fichier csv;mapper le fichier csv à xdm;mapper csv à xdm;guide de lʼui;mappeur;mappage;data prep;préparation des données;préparer des données;
solution: Experience Platform
title: Présentation de la préparation des données
description: Ce document présente Data Prep dans Adobe Experience Platform.
exl-id: 9bef5c3b-368d-4492-bdef-64e67fc25bfd
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 100%

---

# Champs calculés

Les champs calculés permettent de créer des valeurs en fonction des attributs du schéma d’entrée. Ces valeurs peuvent ensuite être affectées à des attributs dans le schéma cible. Vous pouvez également leur fournir un nom et une description pour en faciliter la référence.

Pour créer un champ calculé, sélectionnez **[!UICONTROL Ajouter un champ calculé]**.

![](./images/calculated-fields/add-calculated-field.png)

Le panneau **[!UICONTROL Créer un champ calculé]** sʼaffiche. La boîte de dialogue de gauche contient les champs, fonctions et opérateurs pris en charge dans les champs calculés. Sélectionnez lʼun des onglets pour commencer à ajouter des fonctions, des champs ou des opérateurs à lʼéditeur dʼexpression.

![](./images/calculated-fields/create-calculated-field.png)

| Tabulation | Description |
| --- | ----------- |
| Fonction | Lʼonglet Fonctions répertorie les fonctions disponibles pour transformer les données. Pour en savoir plus sur les fonctions que vous pouvez utiliser dans les champs calculés, consultez le guide dʼ [utilisation des fonctions Data Prep (Mapper)](./functions.md). |
| Champ | Lʼonglet Champs répertorie les champs et attributs disponibles dans le schéma source. |
| Opérateur | Lʼonglet Opérateurs répertorie les opérateurs disponibles pour la transformation des données. |

Vous pouvez ajouter manuellement des champs, des fonctions et des opérateurs à lʼaide de lʼéditeur dʼexpression situé au centre. Sélectionnez lʼéditeur pour commencer à créer une expression.

![](./images/calculated-fields/write-calculated-field.png)

Sélectionnez **[!UICONTROL Enregistrer]** pour continuer.

Lʼécran des mappings réapparaît avec le champ source que vous venez de créer. Appliquez le champ cible correspondant et sélectionnez **[!UICONTROL Terminer]** pour terminer le mapping.

![](./images/calculated-fields/new-calculated-field.png)
