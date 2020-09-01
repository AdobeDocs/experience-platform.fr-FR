---
keywords: Experience Platform;home;popular topics;Segmentation Service;segmentation;Segmentation;create a dataset;export audience segment;export segment;
solution: Experience Platform
title: Création d’un jeu de données pour l’exportation d’un segment ciblé
topic: tutorial
translation-type: tm+mt
source-git-commit: d2f098cb9e4aaf5beaad02173a22a25a87a43756
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 71%

---


# Création d’un jeu de données pour l’exportation d’un segment ciblé

[!DNL Adobe Experience Platform] vous permet de segmenter facilement les profils client en audiences selon des attributs spécifiques. Une fois les segments créés, vous pouvez exporter cette audience vers un jeu de données où il sera possible d’y accéder et de la manipuler. Pour que l’exportation soit réussie, le jeu de données doit être correctement configuré.

This tutorial walks through the steps required to create a dataset that can be used for exporting an audience segment using the [!DNL Experience Platform] UI.

Ce tutoriel est directement lié aux étapes décrites dans le tutoriel portant sur l’[évaluation et l’accès aux résultats de segmentation](./evaluate-a-segment.md). The evaluating a segment tutorial provides steps for creating a dataset using the [!DNL Catalog Service] API, whereas this tutorial outlines steps to create a dataset using the [!DNL Experience Platform] UI.

## Prise en main

Pour exporter un segment, le jeu de données doit être basé sur le [!DNL XDM Individual Profile Union Schema]. A union schema is a system-generated, read-only schema that aggregates the fields of all schemas that share the same class, in this case that is the [!DNL XDM Individual Profile] class. Pour plus d’informations sur la vue d’union des schémas, consultez la [section Real-time Customer Profile du guide de développement du registre des schémas](../../xdm/schema/composition.md#union).

Pour visualiser les schémas d’union dans l’interface utilisateur, cliquez sur **[!UICONTROL Profils]** dans le volet de navigation de gauche, puis cliquez sur l’onglet **[!UICONTROL Schéma d’union]** comme illustré ci-dessous.

![Onglet de schéma d’union dans l’interface utilisateur d’Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Espace de travail des jeux de données

The datasets workspace within the [!DNL Experience Platform] UI allows you to view and manage all of the datasets that your IMS organization has made, as well as create new ones.

Pour afficher l’espace de travail des jeux de données, cliquez sur **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche, puis cliquez sur l’onglet **[!UICONTROL Parcourir]**. L’espace de travail des jeux de données contient une liste de jeux de données, y compris des colonnes indiquant le **[!UICONTROL nom]**, la date et l’heure de **[!UICONTROL création]**, la **[!UICONTROL source]**, le **[!UICONTROL schéma]** et l’**[!UICONTROL état du dernier lot]**, ainsi que la date et l’heure de la **[!UICONTROL dernière mise à jour]** du jeu de données. Selon la largeur de chaque colonne, vous devrez peut-être faire défiler vers la gauche ou la droite pour toutes les afficher.

>[!NOTE]
>
>Cliquez sur l’icône de filtre près de la barre de recherche pour utiliser les fonctionnalités de filtrage afin d’afficher uniquement les jeux de données activés pour [!DNL Real-time Customer Profile].

![Affichage de tous les jeux de données](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Création d’un jeu de données

Pour créer un jeu de données, cliquez sur **[!UICONTROL Créer un jeu de données]** dans le coin supérieur droit de l’espace de travail des jeux de données.

![Cliquez sur Créer un jeu de données](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Sur l’écran **[!UICONTROL Créer un jeu de données]**, cliquez sur **[!UICONTROL Créer un jeu de données à partir d’un schéma]** pour continuer.

![Sélectionner la source de données](../images/tutorials/segment-export-dataset/create-dataset.png)

## Sélection du schéma d’union XDM Individual Profile

To select the [!DNL XDM Individual Profile Union Schema] for use in your dataset, find the &quot;[!UICONTROL XDM Individual Profile]&quot; schema with a type of &quot;[!UICONTROL Union]&quot; on the **[!UICONTROL Select Schema]** screen.

Sélectionnez le bouton radio près de **[!UICONTROL XDM Individual Profile]**, puis cliquez sur **[!UICONTROL Suivant]** dans le coin supérieur droit.

![Sélectionner un schéma](../images/tutorials/segment-export-dataset/select-schema.png)

## Configuration d’un jeu de données

Dans l’écran **[!UICONTROL Configurer le jeu de données]**, vous devrez attribuer un **[!UICONTROL nom]** à votre jeu de données et pourrez également fournir une **[!UICONTROL description]** pour celui-ci.

**Remarques sur les noms des jeux de données :**
- Les noms des jeux de données doivent être courts et descriptifs afin qu’ils puissent être facilement retrouvés par la suite dans la bibliothèque.
- Les noms des jeux de données doivent être uniques, ce qui signifie qu’ils doivent également être suffisamment précis pour ne pas être réutilisés à l’avenir.
- Il est recommandé de fournir des informations supplémentaires sur le jeu de données à l’aide du champ de description, car cela peut aider d’autres utilisateurs à différencier les jeux de données à l’avenir.

Une fois que le jeu de données possède un nom et une description, cliquez sur **[!UICONTROL Terminer]**.

![Configurer un jeu de données](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Activité du jeu de données

Un jeu de données vide a désormais été créé et vous avez été renvoyé à l’onglet **[!UICONTROL Activité du jeu de données]** dans l’espace de travail des jeux de données.  Vous devriez voir le nom du jeu de données dans le coin supérieur gauche de l’espace de travail, ainsi qu’une notification indiquant « Aucun lot n’a été ajouté ». Cela est normal puisque vous n’avez encore ajouté aucun lot à ce jeu de données.

Sur le côté droit de l’espace de travail des jeux de données, l’onglet **[!UICONTROL Informations]** contient des informations relatives à votre nouveau jeu de données, telles que l’**[!UICONTROL identifiant du jeu de données]**, le **[!UICONTROL nom]**, la **[!UICONTROL description]**, le **[!UICONTROL nom du tableau]**, le **[!UICONTROL schéma]**, le **[!UICONTROL Streaming]** et la **[!UICONTROL Source]**. The [!UICONTROL Info] tab also includes information about when the dataset was **[!UICONTROL Created]** and its **[!UICONTROL Last Modified]** date.

Prêtez attention à l’**[!UICONTROL identifiant du jeu de données]** : cette valeur est indispensable pour terminer le workflow d’exportation du segment ciblé.

![Activité du jeu de données](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Étapes suivantes

Now that you have created a dataset based on the [!DNL XDM Individual Profile Union Schema], you can use the **[!UICONTROL Dataset ID]** to continue the [evaluating and accessing segment results](./evaluate-a-segment.md) tutorial.

At this time, please return to the evaluating segment results tutorial and pick up from the [generating profiles for audience members](./evaluate-a-segment.md#generate-profiles) step of the exporting a segment workflow.
