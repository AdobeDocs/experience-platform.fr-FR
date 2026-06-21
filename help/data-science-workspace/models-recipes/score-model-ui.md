---
keywords: Experience Platform;noter un modèle;Workspace de science des données;rubriques populaires;interface utilisateur;exécution de notation;résultats de notation
solution: Experience Platform
title: Notation d’un modèle dans l’interface utilisateur de Workspace de science des données
type: Tutorial
description: La notation dans l’espace de travail de science des données d’Adobe Experience Platform peut être réalisée en alimentant un modèle formé existant avec des données d’entrée. Les résultats de la notation sont ensuite stockés et consultables dans un jeu de données de sortie spécifié sous la forme d’un nouveau lot.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
TQID: https://experienceleague.adobe.com/x-LrZ8VzNiLMR8qWGhQ9Wmw4XWZsdayKFSz9zDbrkeM
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 623
ht-degree: 30%

---

# Notation d’un modèle dans l’interface utilisateur de Workspace de science des données

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

La notation dans Adobe Experience Platform [!DNL Data Science Workspace] peut être réalisée en alimentant un modèle formé existant avec des données d’entrée. Les résultats de la notation sont ensuite stockés et consultables dans un jeu de données de sortie spécifié sous la forme d’un nouveau lot.

Ce tutoriel décrit les étapes requises pour noter un modèle dans l’interface utilisateur [!DNL Data Science Workspace].

## Prise en main

Pour suivre ce tutoriel, vous devez avoir accès à [!DNL Experience Platform]. Si vous n’avez pas accès à une organisation dans [!DNL Experience Platform], contactez votre administrateur système avant de continuer.

Ce tutoriel nécessite un modèle formé. Si vous ne disposez pas d’un modèle formé, suivez le tutoriel [Formation et évaluation d’un modèle dans l’interface utilisateur](./train-evaluate-model-ui.md) avant de poursuivre.

## Création d’une opération de notation

Vous pouvez créer une opération de notation l’aide de configurations optimisées provenant d’une opération de formation déjà terminée et évaluée. L’ensemble des configurations optimales d’un modèle est généralement déterminé en examinant les mesures d’évaluation de l’opération de formation.

Trouvez l’opération de formation optimale afin d’utiliser ses configurations pour la notation. Ouvrez ensuite l’exécution de formation souhaitée en sélectionnant le lien hypertexte associé à son nom.

![Sélectionner l’exécution de formation](../images/models-recipes/score/select-run.png)

Dans l’onglet Exécution de la formation **[!UICONTROL Évaluation]**, sélectionnez **[!UICONTROL Score]** dans la partie supérieure droite de l’écran. Un nouveau workflow de notation commence.

![](../images/models-recipes/score/training_run_overview.png)

Sélectionnez le jeu de données de notation d’entrée et sélectionnez **[!UICONTROL Suivant]**.

![](../images/models-recipes/score/scoring_input.png)

Sélectionnez le jeu de données de notation de sortie. Il s’agit du jeu de données de sortie dédié dans lequel les résultats de la notation sont stockés. Confirmez votre sélection et sélectionnez **[!UICONTROL Suivant]**.

![](../images/models-recipes/score/scoring_results.png)

La dernière étape du workflow vous invite à configurer l’exécution de notation. Ces configurations sont utilisées par le modèle pour l’exécution de notation.
Notez que vous ne pouvez pas supprimer les paramètres hérités qui ont été définis lors de la création des modèles. Vous pouvez modifier ou rétablir des paramètres non hérités en double-cliquant sur la valeur ou en sélectionnant l’icône Rétablir lors du survol de l’entrée.

![configuration](../images/models-recipes/score/configuration.png)

Passez en revue et confirmez les configurations de notation et sélectionnez **[!UICONTROL Terminer]** pour créer et exécuter l’exécution de notation. Vous accédez à l’onglet **[!UICONTROL Exécutions de notation]** et la nouvelle exécution de notation avec le statut **[!UICONTROL En attente]** s’affiche.

![onglet exécutions de notation](../images/models-recipes/score/scoring_runs_tab.png)

Une exécution de notation peut être affichée avec l’un des statuts suivants :

- En attente
- Terminée
- Échec
- En cours d’exécution

Les statuts sont mis à jour automatiquement. Passez à l’étape suivante si le statut est **[!UICONTROL Terminé]** ou **[!UICONTROL Échec]**.

## Affichage des résultats de la notation

Pour afficher les résultats de notation, commencez par sélectionner une exécution de formation.

![Sélectionner l’exécution de formation](../images/models-recipes/score/select-run.png)

Vous êtes redirigé vers la page exécutions de formation **[!UICONTROL Évaluation]**. En haut de la page d’évaluation des exécutions de formation, sélectionnez l’onglet **[!UICONTROL Exécutions de notation]** pour afficher la liste des exécutions de notation existantes.

![page d’évaluation](../images/models-recipes/score/view_scoring_runs.png)

Sélectionnez ensuite une exécution de notation pour afficher les détails de l’exécution.

![détails de l’exécution](../images/models-recipes/score/view_details.png)

Si le statut de l’exécution de notation sélectionnée est défini sur « Terminé » ou « Échec », le lien **[!UICONTROL Afficher les journaux d’activité]** devient disponible. Si l’exécution d’une notation échoue, les journaux d’exécution peuvent fournir des informations utiles pour déterminer la raison de l’échec. Pour télécharger les journaux d’exécution, sélectionnez **[!UICONTROL Afficher les journaux d’activité]**.

![Sélectionnez Afficher les journaux](../images/models-recipes/score/view_logs.png)

La fenêtre contextuelle **[!UICONTROL Afficher les journaux d’activité]** s’affiche. Sélectionnez une URL pour télécharger automatiquement les journaux associés.

![](../images/models-recipes/score/activity_logs.png)

Vous avez également la possibilité d’afficher vos résultats de notation en sélectionnant **[!UICONTROL Prévisualiser le jeu de données de résultats de notation]**.

![Sélectionnez Aperçu des résultats](../images/models-recipes/score/view_results.png)

Un aperçu du jeu de données de sortie est fourni.

![prévisualiser les résultats](../images/models-recipes/score/preview_results.png)

Pour obtenir l’ensemble complet des résultats de notation, cliquez sur le lien **[!UICONTROL Jeu de données des résultats de notation]** situé dans la colonne de droite.

## Étapes suivantes

Ce tutoriel vous a guidé à travers les étapes pour noter des données à l’aide d’un modèle formé dans [!DNL Data Science Workspace]. Suivez le tutoriel sur la [publication d’un modèle en tant que service dans l’interface utilisateur](./publish-model-service-ui.md) pour permettre aux utilisateurs de votre organisation de noter des données en leur fournissant un accès facile à un service de machine learning.
