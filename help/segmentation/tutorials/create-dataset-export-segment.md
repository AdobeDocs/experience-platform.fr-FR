---
keywords: Experience Platform ; accueil ; rubriques populaires ; Service de segmentation ; segmentation ; Segmentation ; créer un jeu de données ; exporter un segment d'audience ; exporter un segment ;
solution: Experience Platform
title: Création d’un jeu de données pour l’exportation d’un segment d’Audience
topic-legacy: tutorial
type: Tutorial
description: Ce tutoriel décrit les étapes nécessaires à la création d’un jeu de données qui peut être utilisé pour exporter un segment ciblé à l’aide de l’interface utilisateur d’Experience Platform.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 57%

---

# Création d’un jeu de données pour l’exportation d’un segment ciblé

[!DNL Adobe Experience Platform] vous permet de segmenter facilement les profils client en audiences selon des attributs spécifiques. Une fois les segments créés, vous pouvez exporter cette audience vers un jeu de données où il sera possible d’y accéder et de la manipuler. Pour que l’exportation soit réussie, le jeu de données doit être correctement configuré.

Ce didacticiel décrit les étapes nécessaires à la création d&#39;un jeu de données qui peut être utilisé pour exporter un segment d&#39;audience à l&#39;aide de l&#39;interface utilisateur [!DNL Experience Platform].

Ce tutoriel est directement lié aux étapes décrites dans le tutoriel portant sur l’[évaluation et l’accès aux résultats de segmentation](./evaluate-a-segment.md). Le didacticiel d’évaluation d’un segment décrit les étapes à suivre pour créer un jeu de données à l’aide de l’API [!DNL Catalog Service], tandis que ce didacticiel décrit les étapes à suivre pour créer un jeu de données à l’aide de l’interface utilisateur [!DNL Experience Platform].

## Prise en main

Pour exporter un segment, le jeu de données doit être basé sur [!DNL XDM Individual Profile Union Schema]. Un schéma d&#39;union est un schéma généré par le système et en lecture seule qui agrégat les champs de tous les schémas qui partagent la même classe, dans ce cas c&#39;est la classe [!DNL XDM Individual Profile]. Pour plus d’informations sur la vue d’union des schémas, consultez la [section Real-time Customer Profile du guide de développement du registre des schémas](../../xdm/schema/composition.md#union).

Pour visualiser les schémas d’union dans l’interface utilisateur, cliquez sur **[!UICONTROL Profils]** dans le volet de navigation de gauche, puis cliquez sur l’onglet **[!UICONTROL Schéma d’union]** comme illustré ci-dessous.

![Onglet de schéma d’union dans l’interface utilisateur d’Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Espace de travail des jeux de données

L&#39;espace de travail des jeux de données dans l&#39;interface utilisateur [!DNL Experience Platform] vous permet de vue et de gérer tous les jeux de données créés par votre organisation IMS, ainsi que de en créer de nouveaux.

Pour afficher l’espace de travail des jeux de données, cliquez sur **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche, puis cliquez sur l’onglet **[!UICONTROL Parcourir]**. L&#39;espace de travail des jeux de données contient une liste de jeux de données, y compris des colonnes indiquant le nom, la création (date et heure), la source, le schéma et l&#39;état du dernier lot, ainsi que la date et l&#39;heure de la dernière mise à jour du jeu de données. Selon la largeur de chaque colonne, vous devrez peut-être faire défiler vers la gauche ou la droite pour toutes les afficher.

>[!NOTE]
>
>Cliquez sur l’icône de filtre près de la barre de recherche pour utiliser les fonctionnalités de filtrage afin d’afficher uniquement les jeux de données activés pour [!DNL Real-time Customer Profile].

![Affichage de tous les jeux de données](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Création d’un jeu de données

Pour créer un jeu de données, cliquez sur **[!UICONTROL Créer un jeu de données]** dans le coin supérieur droit de l’espace de travail des jeux de données.****

![Cliquez sur Créer un jeu de données](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Sur l’écran **[!UICONTROL Créer un jeu de données]**, cliquez sur **[!UICONTROL Créer un jeu de données à partir d’un schéma]** pour continuer.

![Sélectionner la source de données](../images/tutorials/segment-export-dataset/create-dataset.png)

## Sélection du schéma d’union XDM Individual Profile

Pour sélectionner le [!DNL XDM Individual Profile Union Schema] à utiliser dans votre jeu de données, recherchez le schéma &quot;[!UICONTROL Profil individuel XDM]&quot; avec un type de &quot;[!UICONTROL Union]&quot; sur l’écran **[!UICONTROL Sélectionner un Schéma]**.

Sélectionnez le bouton radio près de **[!UICONTROL XDM Individual Profile]**, puis cliquez sur **[!UICONTROL Suivant]** dans le coin supérieur droit.

![Sélectionner un schéma](../images/tutorials/segment-export-dataset/select-schema.png)

## Configuration d’un jeu de données

Dans l&#39;écran **[!UICONTROL Configurer le jeu de données]**, vous devrez donner un nom à votre jeu de données et peut également fournir une description du jeu de données.

**Remarques sur les noms des jeux de données :**
- Les noms des jeux de données doivent être courts et descriptifs afin qu’ils puissent être facilement retrouvés par la suite dans la bibliothèque.
- Les noms des jeux de données doivent être uniques, ce qui signifie qu’ils doivent également être suffisamment précis pour ne pas être réutilisés à l’avenir.
- Il est recommandé de fournir des informations supplémentaires sur le jeu de données à l’aide du champ de description, car cela peut aider d’autres utilisateurs à différencier les jeux de données à l’avenir.

Une fois que le jeu de données possède un nom et une description, cliquez sur **[!UICONTROL Terminer]**.

![Configurer un jeu de données](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Activité du jeu de données

Un jeu de données vide a désormais été créé et vous avez été renvoyé à l’onglet **[!UICONTROL Activité du jeu de données]** dans l’espace de travail des jeux de données. **** Vous devriez voir le nom du jeu de données dans le coin supérieur gauche de l’espace de travail, ainsi qu’une notification indiquant « Aucun lot n’a été ajouté ». Cela est normal puisque vous n’avez encore ajouté aucun lot à ce jeu de données.

L&#39;onglet **[!UICONTROL Informations]** situé à droite de l&#39;espace de travail Datasets contient des informations relatives à votre nouveau jeu de données, telles que l&#39;ID, le nom, la description, le nom de la table, le schéma, la diffusion en continu et la source. L&#39;onglet **[!UICONTROL Info]** contient également des informations sur le moment où le jeu de données a été créé et sa date de dernière modification.

Prêtez attention à l’**[!UICONTROL identifiant du jeu de données]** : cette valeur est indispensable pour terminer le workflow d’exportation du segment ciblé.

![Activité du jeu de données](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Étapes suivantes

Maintenant que vous avez créé un jeu de données basé sur [!DNL XDM Individual Profile Union Schema], vous pouvez utiliser l&#39;ID de jeu de données pour continuer le didacticiel [évaluation et accès aux résultats du segment](./evaluate-a-segment.md).

Pour l&#39;instant, veuillez revenir au didacticiel d&#39;évaluation des résultats des segments et prendre connaissance de l&#39;étape [génération de profils pour les membres d&#39;audience](./evaluate-a-segment.md#generate-profiles) du processus d&#39;exportation d&#39;un segment.
