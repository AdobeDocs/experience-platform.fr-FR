---
solution: Experience Platform
title: Création d’un jeu de données pour l’exportation d’une audience
type: Tutorial
description: Découvrez comment créer un jeu de données qui peut être utilisé pour exporter une audience à l’aide de l’interface utilisateur de l’Experience Platform.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 15%

---

# Création d’un jeu de données pour l’exportation d’une audience

[!DNL Adobe Experience Platform] vous permet de segmenter les profils client en audiences en fonction d’attributs spécifiques. Une fois qu’une définition de segment est créée, vous pouvez exporter l’audience obtenue vers un jeu de données où elle peut être accessible et sur lequel vous pouvez agir. Pour que l’exportation soit réussie, le jeu de données doit être correctement configuré.

Ce tutoriel décrit les étapes nécessaires à la création d’un jeu de données qui peut être utilisé pour exporter une audience à l’aide de l’interface utilisateur [!DNL Experience Platform].

Ce tutoriel est directement lié aux étapes décrites dans le tutoriel sur l’ [évaluation et accès aux résultats de la segmentation](./evaluate-a-segment.md). Le tutoriel d’évaluation de la définition de segment décrit les étapes à suivre pour créer un jeu de données à l’aide de l’API [!DNL Catalog Service], tandis que ce tutoriel décrit les étapes à suivre pour créer un jeu de données à l’aide de l’interface utilisateur [!DNL Experience Platform].

## Commencer

Pour exporter une audience, le jeu de données doit être basé sur le [!DNL XDM Individual Profile Union Schema]. Un schéma d’union est un schéma en lecture seule généré par le système qui agrège les champs de tous les schémas qui partagent la même classe. Pour plus d’informations sur les schémas d’union, consultez le guide sur [les principes de base de la composition des schémas](../../xdm/schema/composition.md#union).

Pour afficher les schémas d’union dans l’interface utilisateur, sélectionnez **[!UICONTROL Profils]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Schéma d’union]** comme illustré ci-dessous.

![L’onglet de schéma d’union est surligné.](../images/tutorials/segment-export-dataset/union.png)

## Espace de travail des jeux de données

L’espace de travail [!UICONTROL Jeux de données] vous permet d’afficher et de gérer tous les jeux de données pour votre organisation.

Sélectionnez **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche pour accéder à l’espace de travail, puis sélectionnez **[!UICONTROL Parcourir]**. Cet onglet affiche une liste des jeux de données et leurs détails. Selon la largeur de chaque colonne, vous devrez peut-être faire défiler vers la gauche ou la droite pour toutes les afficher.

>[!NOTE]
>
>Sélectionnez l’icône de filtre en regard de la barre de recherche pour utiliser les fonctionnalités de filtrage afin de n’afficher que les jeux de données activés pour [!DNL Real-Time Customer Profile].

![L’espace de travail des jeux de données s’affiche.](../images/tutorials/segment-export-dataset/browse.png)

## Créer un jeu de données

Pour créer un jeu de données, sélectionnez **[!UICONTROL Créer un jeu de données]**.

![Le bouton Créer un jeu de données est mis en surbrillance.](../images/tutorials/segment-export-dataset/create-dataset.png)

Sur l’écran suivant, sélectionnez **[!UICONTROL Créer un jeu de données à partir d’un schéma]**.

![&#x200B; L’option Créer un jeu de données à partir d’un schéma est mise en surbrillance.](../images/tutorials/segment-export-dataset/create-from-schema.png)

## Sélection du schéma d’union XDM Individual Profile

Pour sélectionner le [!DNL XDM Individual Profile Union Schema] à utiliser dans votre jeu de données, recherchez le schéma &quot;[!UICONTROL XDM Individual Profile]&quot; sur l’écran **[!UICONTROL Sélectionner le schéma]**. Une fois que vous avez sélectionné le schéma, vous pouvez confirmer s’il s’agit du schéma d’union sous **[!UICONTROL Utilisation de l’API]** dans le rail de droite. Si le chemin d’accès [!UICONTROL Schema] se termine par `_union`, il s’agit d’un schéma d’union.

>[!NOTE]
>
>Bien que les schémas d’union participent par définition à Real-Time Customer Profile, ils sont répertoriés comme &quot;Non activé&quot; en raison du fait qu’ils ne sont pas activés pour Profile de la même manière que les schémas traditionnels.

Sélectionnez le bouton radio en regard de **[!UICONTROL XDM Individual Profile]**, puis sélectionnez **[!UICONTROL Next]**.

![Le schéma XDM Individual Profile est mis en surbrillance.](../images/tutorials/segment-export-dataset/select-schema.png)

## Configuration d’un jeu de données

Sur l’écran suivant, vous devez donner un nom à votre jeu de données. Vous pouvez également ajouter une description facultative.

**Remarques sur les noms des jeux de données :**

* Les noms des jeux de données doivent être courts et descriptifs afin qu’ils puissent être facilement retrouvés par la suite dans la bibliothèque.
* Les noms des jeux de données doivent être uniques, ce qui signifie qu’ils doivent également être suffisamment précis pour ne pas être réutilisés à l’avenir.
* Vous devez fournir des informations supplémentaires sur le jeu de données à l’aide du champ de description, car cela peut aider d’autres utilisateurs à différencier les jeux de données à l’avenir.

Une fois que le jeu de données a un nom et une description, sélectionnez **[!UICONTROL Terminer]**.

![La page Configurer le jeu de données s’affiche. Les options de configuration sont mises en surbrillance.](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Activité du jeu de données

Une fois le jeu de données créé, la page d’activité de ce jeu de données s’affiche. Vous devriez voir le nom du jeu de données dans le coin supérieur gauche de l’espace de travail, ainsi qu’une notification indiquant « Aucun lot n’a été ajouté ». Cela est normal puisque vous n’avez encore ajouté aucun lot à ce jeu de données.

Le rail de droite contient des informations relatives à votre nouveau jeu de données, telles que l’identifiant du jeu de données, le nom, la description, le schéma, etc. Veuillez noter l’**[!UICONTROL identifiant du jeu de données]**, car cette valeur est nécessaire pour terminer le workflow d’exportation de l’audience.

![La page de l’activité du jeu de données s’affiche. L’identifiant du jeu de données est mis en surbrillance, car cette valeur doit être notée pour les étapes suivantes.](../images/tutorials/segment-export-dataset/activity.png)

## Étapes suivantes

Maintenant que vous avez créé un jeu de données basé sur [!DNL XDM Individual Profile Union Schema], vous pouvez utiliser l’identifiant du jeu de données pour continuer le tutoriel [portant sur l’évaluation et l’accès aux résultats de définition de segment](./evaluate-a-segment.md).

Pour l’instant, revenez au tutoriel portant sur l’évaluation des résultats de définition de segment et intéressez-vous à l’étape [génération de profils pour les membres de l’audience](./evaluate-a-segment.md#generate-profiles) du workflow d’exportation d’une audience.
