---
keywords: Experience Platform;noter un modèle;Data Science Workspace;rubriques populaires;ui;opération de notation;résultats de notation
solution: Experience Platform
title: Notation d’un modèle dans l’interface utilisateur de Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: La notation dans Adobe Experience Platform Data Science Workspace peut être réalisée en alimentant un modèle formé existant avec des données d’entrée. Les résultats de la notation sont ensuite stockés et consultables dans un jeu de données de sortie spécifié sous la forme d’un nouveau lot.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 35%

---

# Notation d’un modèle dans l’interface utilisateur de Data Science Workspace

Notation dans Adobe Experience Platform [!DNL Data Science Workspace] peut être réalisé en alimentant les données d’entrée dans un modèle formé existant. Les résultats de la notation sont ensuite stockés et consultables dans un jeu de données de sortie spécifié sous la forme d’un nouveau lot.

Ce tutoriel présente les étapes requises pour noter un modèle dans la variable [!DNL Data Science Workspace] de l’interface utilisateur.

## Prise en main

Pour suivre ce tutoriel, vous devez avoir accès à [!DNL Experience Platform]. Si vous n’avez pas accès à une organisation IMS dans [!DNL Experience Platform], contactez votre administrateur système avant de continuer.

Ce tutoriel nécessite un modèle formé. Si vous ne disposez pas d’un modèle formé, suivez le tutoriel [Formation et évaluation d’un modèle dans l’interface utilisateur](./train-evaluate-model-ui.md) avant de poursuivre.

## Création d’une opération de notation

Vous pouvez créer une opération de notation l’aide de configurations optimisées provenant d’une opération de formation déjà terminée et évaluée. L’ensemble des configurations optimales d’un modèle est généralement déterminé en examinant les mesures d’évaluation de l’opération de formation.

Trouvez l’opération de formation optimale afin d’utiliser ses configurations pour la notation. Ouvrez ensuite l’opération de formation souhaitée en sélectionnant le lien hypertexte associé à son nom.

![Sélection de l’opération de formation](../images/models-recipes/score/select-run.png)

À partir de l’opération de formation **[!UICONTROL Évaluation]** onglet, sélectionnez **[!UICONTROL Score]** situé en haut à droite de l’écran. Un nouveau workflow de notation commence.

![](../images/models-recipes/score/training_run_overview.png)

Sélectionnez le jeu de données de notation d’entrée et sélectionnez **[!UICONTROL Suivant]**.

![](../images/models-recipes/score/scoring_input.png)

Sélectionnez le jeu de données de notation de sortie. Il s’agit du jeu de données de sortie dédié dans lequel les résultats de la notation sont stockés. Confirmez votre sélection et sélectionnez **[!UICONTROL Suivant]**.

![](../images/models-recipes/score/scoring_results.png)

La dernière étape du processus vous invite à configurer votre opération de notation. Ces configurations sont utilisées par le modèle pour l’opération de notation.
Notez que vous ne pouvez pas supprimer les paramètres hérités qui ont été définis lors de la création des modèles. Vous pouvez modifier ou rétablir des paramètres non hérités en double-cliquant sur la valeur ou en sélectionnant l’icône Rétablir lorsque vous survolez l’entrée.

![configuration](../images/models-recipes/score/configuration.png)

Vérifiez et confirmez les configurations de notation, puis sélectionnez **[!UICONTROL Terminer]**  pour créer et exécuter l’opération de notation. Vous êtes dirigé vers le **[!UICONTROL Opérations de notation]** et la nouvelle opération de notation avec l’onglet **[!UICONTROL En attente]** s’affiche.

![onglet opérations de notation](../images/models-recipes/score/scoring_runs_tab.png)

Une opération de notation peut être affichée avec l’un des états suivants :
- En attente
- Terminée
- Échec
- En cours

Les états sont automatiquement mis à jour. Passez à l’étape suivante si l’état est **[!UICONTROL Terminer]** ou **[!UICONTROL En échec]**.

## Affichage des résultats de la notation

Pour afficher les résultats de la notation, commencez par sélectionner une opération de formation.

![Sélection de l’opération de formation](../images/models-recipes/score/select-run.png)

Vous êtes redirigé vers les opérations de formation. **[!UICONTROL Évaluation]** page. Près de la partie supérieure de la page d’évaluation de l’opération de formation, sélectionnez **[!UICONTROL Opérations de notation]** pour afficher une liste des exécutions de notation existantes.

![page d’évaluation](../images/models-recipes/score/view_scoring_runs.png)

Sélectionnez ensuite une opération de notation pour afficher les détails de l’opération.

![détails de l’exécution](../images/models-recipes/score/view_details.png)

Si l’état de l’opération de notation sélectionnée est &quot;Terminé&quot; ou &quot;Échec&quot;, la variable **[!UICONTROL Affichage des journaux d’activité]** est rendu disponible. Si une opération de notation échoue, les journaux d’exécution peuvent fournir des informations utiles pour déterminer la raison de l’échec. Pour télécharger les logs d&#39;exécution, sélectionnez **[!UICONTROL Affichage des journaux d’activité]**.

![Sélectionner les journaux d’affichage](../images/models-recipes/score/view_logs.png)

Le **[!UICONTROL Afficher les journaux d’activité]** s’affiche. Sélectionnez une URL pour télécharger automatiquement les logs associés.

![](../images/models-recipes/score/activity_logs.png)

Vous avez également la possibilité d’afficher vos résultats de notation en sélectionnant  **[!UICONTROL Aperçu du jeu de données de résultats de notation]**.

![Sélectionner les résultats de l’aperçu](../images/models-recipes/score/view_results.png)

Un aperçu du jeu de données de sortie est fourni.

![aperçu des résultats](../images/models-recipes/score/preview_results.png)

Pour consulter l’ensemble des résultats de la notation, sélectionnez la variable **[!UICONTROL Jeu de données des résultats de notation]** lien situé dans la colonne de droite.

## Étapes suivantes

Ce tutoriel vous a expliqué les étapes à suivre pour noter les données à l’aide d’un modèle formé dans [!DNL Data Science Workspace]. Suivez le tutoriel sur la [publication d’un modèle en tant que service dans l’interface utilisateur](./publish-model-service-ui.md) pour permettre aux utilisateurs de votre organisation de noter des données en leur fournissant un accès facile à un service d’apprentissage automatique.
