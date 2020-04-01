---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Création d’un jeu de données pour l’exportation d’un segment  '
topic: tutorial
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea

---


# Création d’un jeu de données pour l’exportation d’un segment  

Adobe Experience Platform vous permet de segmenter facilement les  de clients en  en fonction d’attributs spécifiques. Une fois les segments créés, vous pouvez exporter ce   vers un jeu de données dans lequel il est possible d’y accéder et d’y agir. Pour que l&#39;exportation soit réussie, le jeu de données doit être configuré correctement.

Ce didacticiel décrit les étapes nécessaires à la création d’un jeu de données qui peut être utilisé pour exporter un segment de   à l’aide de l’interface utilisateur de la plateforme d’expérience.

Ce didacticiel est directement lié aux étapes décrites dans le didacticiel pour [évaluer les résultats](./evaluate-a-segment.md)des segments et y accéder. Le didacticiel sur l’évaluation d’un segment décrit les étapes de création d’un jeu de données à l’aide de l’API Catalogue, tandis que ce didacticiel décrit les étapes de création d’un jeu de données à l’aide de l’interface utilisateur de la plateforme d’expérience.

## Prise en main

Pour exporter un segment, le jeu de données doit être basé sur le individuel XDM   lede. Un   est ungénéré par le système et en lecture seule qui permet de les champs de tous lespartageant la même classe, dans ce cas la classe de la classe de l’XDM Individuel. Pour plus d&#39;informations sur   [](../../xdm/schema/composition.md#union)de l&#39;, veuillez consulter la section de l&#39;en temps réel du guidedu développeur du registre desclients.

Pour   de l&#39;de **dans l&#39;interface utilisateur, cliquez sur** dans la barre de navigation de gauche, puis cliquez sur l&#39;onglet *de l&#39;* ensemble dede l&#39;onglet, comme illustré ci-dessous.

![onglet  de  de l’interface utilisateur de la plateforme d’expérience](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Espace de travail Datasets

L’espace de travail des jeux de données dans l’interface utilisateur de la plateforme d’expérience vous permet de  et de gérer tous les jeux de données créés par votre organisation IMS, ainsi que de créer de nouveaux jeux.

Pour  l’espace de travail Jeu de données, cliquez sur **Jeu de données** dans le volet de navigation de gauche, puis cliquez sur l’onglet *Parcourir* . The datasets workspace contains a list of datasets, including columns showing *Name*, *Created* (date and time), *Source*, *Schema*, and *Last Batch Status*, as well as the date and time the dataset was *Last Updated*. Selon la largeur de chaque colonne, vous devrez peut-être faire défiler vers la gauche ou la droite pour afficher toutes les colonnes.

>[!NOTE] Cliquez sur l’icône de filtre en regard de la barre de recherche pour utiliser les fonctionnalités de filtrage afin de ne  que les jeux de données activés pour le de clients en temps réel.

![tous les jeux de données](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Création d’un jeu de données

Pour créer un jeu de données, cliquez sur **Créer un jeu** de données dans le coin supérieur droit de l’espace de travail Jeux de données.

![Cliquez sur Créer un jeu de données](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Dans l’écran *Créer un jeu* de données, cliquez sur **Créer un jeu de données à partir du** pour continuer.

![Sélectionner la source de données](../images/tutorials/segment-export-dataset/create-dataset.png)

## Sélectionner un XDM individuel    de

Pour sélectionner le XDM Individuel   *de* à utiliser dans votre jeu de données, recherchez le &quot;XDM Individuel&quot; avec un type de &quot;de disque&quot; dans l’écranSélectionner unde disque dur.

Sélectionnez le bouton radio en regard de XDM Individuel **, puis cliquez sur** Suivant **** dans le coin supérieur droit.

![Sélectionner](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurer un jeu de données

Dans l’écran **Configurer le jeu de données** , vous devrez attribuer un *nom* à votre jeu de données et vous pouvez également fournir une *description* du jeu de données.

**Remarques sur les noms des jeux de données :**
- Les noms des jeux de données doivent être courts et descriptifs afin que le jeu de données puisse être facilement retrouvé dans la bibliothèque ultérieurement.
- Les noms des jeux de données doivent être uniques, ce qui signifie qu’ils doivent être suffisamment spécifiques pour ne pas être réutilisés à l’avenir.
- Il est recommandé de fournir des informations supplémentaires sur le jeu de données à l’aide du champ de description, car cela peut aider d’autres utilisateurs à différencier les jeux de données à l’avenir.

Une fois que le jeu de données a un nom et une description, cliquez sur **Terminer**.

![Configurer un jeu de données](../images/tutorials/segment-export-dataset/configure-dataset.png)

##  de données 

Un jeu de données vide a maintenant été créé et vous avez été renvoyé à l&#39;onglet  de jeu de *données* dans l&#39;espace de travail Jeu de données. Vous devriez voir le nom du jeu de données dans le coin supérieur gauche de l’espace de travail, ainsi qu’une notification indiquant qu’aucun lot n’a été ajouté. Vous devez vous y attendre, car vous n’avez encore ajouté aucun lot à ce jeu de données.

Sur le côté droit de l’espace de travail Jeu de données, l’onglet **Infos** contient des informations relatives à votre nouveau jeu de données, telles que l’ID *du jeu de données, le* nom *, la**description, le nomTable, le, leStreaminget leSource.********* L’onglet Infos contient également des informations sur le moment où le jeu de données a été *créé* et sa date de *dernière modification* .

Veuillez prendre note de l&#39;ID **du jeu de** données, car cette valeur est requise pour terminer le flux de travail   d&#39;exportation de segments.

![de données](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Étapes suivantes

Maintenant que vous avez créé un jeu de données basé sur le XDM individuel   **de, vous pouvez utiliser l’ID** du jeu de [données pour continuer le didacticiel d’](./evaluate-a-segment.md) évaluation et d’accès aux résultatsdes segments.

Pour l’instant, veuillez revenir au didacticiel sur les résultats des segments d’évaluation et prendre connaissance de l’étape [Générer un XDM individuel pour  membres](./evaluate-a-segment.md#generate-profiles-for-audience-members) de l’étape d’ [exportation d’un segment](./evaluate-a-segment.md#export-a-segment) du flux de travail.
