---
title: Gestion des scores de piste et de compte prédictifs dans Real-Time CDP B2B
type: Documentation
description: Ce document fournit des informations sur la gestion de la fonctionnalité de notation de compte et de piste prédictive dans la plateforme CDP B2B Experience Platform.
exl-id: fe7eb94e-5cf1-46bf-80e5-affe5735c998
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 5%

---

# Gestion des scores de piste et de compte prédictifs dans Adobe Real-time Customer Data Platform, Édition B2B

>[!NOTE]
>
>Seuls les utilisateurs disposant de l’autorisation Gérer l’IA B2B peuvent créer, modifier et supprimer des objectifs de score.

Ce tutoriel vous guide tout au long des étapes à suivre pour gérer les objectifs de score du service de notation de compte et de prospect prédictif. Les objectifs de score peuvent concerner soit un profil de personne, soit un profil de compte.

## Création d’un score

Pour créer un score, sélectionnez le **[!UICONTROL Services]** dans la barre latérale et sélectionnez **[!UICONTROL Créer un score]**.

![plas-new-score](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

Le **[!UICONTROL Informations de base]** s’affiche, vous invitant à sélectionner un type de profil, à saisir un nom et éventuellement une description. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![plas-enter-basic-information](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

Le **[!UICONTROL Définition de votre objectif]** s’affiche. Sélectionnez la flèche de liste déroulante, puis un type d’objectif dans la fenêtre déroulante qui s’affiche.

![plas-select-a-goal](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

Le **[!UICONTROL Particularités des objectifs]** s’ouvre. Sélectionnez la flèche de liste déroulante, puis le nom du champ cible dans la fenêtre déroulante qui s’affiche.

![plas-select-a-goal-field-name](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

Le **[!UICONTROL Conditions de l’objectif]** s’affiche. Sélectionnez la flèche de liste déroulante, puis sélectionnez une condition dans la fenêtre déroulante qui s’affiche.

![plas-goal-specific-condition](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

Le **[!UICONTROL Valeur de l’objectif]** s’affiche. Ensuite, configurez vos [!UICONTROL Particularités des objectifs]. Sélectionnez la [!UICONTROL Saisir la valeur du champ] et saisissez votre valeur d’objectif.

>[!NOTE]
>
>Plusieurs valeurs d’objectif peuvent être ajoutées.

![plas-goal-specific-field-value](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

Pour ajouter des champs supplémentaires, sélectionnez **[!UICONTROL Ajouter un champ]**.

![plas-goal-specific-add-event](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

Pour configurer la période de prédiction, sélectionnez la flèche de liste déroulante, puis sélectionnez la période de votre choix.

![plas-prediction-timeframe](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

La stratégie de fusion sélectionnée détermine la manière dont les valeurs de champ d’un profil de personne sont sélectionnées. À l’aide de la flèche de liste déroulante, sélectionnez la stratégie de fusion de votre choix, puis sélectionnez **[!UICONTROL Terminer]**.

Le **[!UICONTROL La configuration de notation est terminée.]** s’affiche, confirmant que le nouveau score a été créé. Sélectionnez **[!UICONTROL OK]**.

![plas-score-complete](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>Chaque processus de notation peut prendre jusqu’à 24 heures.

Vous revenez alors au **[!UICONTROL Services]** où vous pouvez voir le nouveau score créé dans la liste des scores.

![plas-score-created](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

Sélectionnez le score pour afficher les détails et des informations supplémentaires sur les détails de la dernière exécution.

![plas-score-additional-information](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

Pour plus d’informations sur les codes d’erreur visibles sous les détails de la dernière exécution, reportez-vous à la section sur [génère les codes d’erreur de pipeline AI.](#leads-ai-pipeline-error-codes) dans ce document.

## Modifier un score

Pour modifier un score, sélectionnez un score dans la **[!UICONTROL Services]** et sélectionnez **[!UICONTROL Modifier]** dans le panneau des détails supplémentaires sur le côté droit de l’écran.

![plas-edit-score](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png)

Le **[!UICONTROL Modifier l’instance]** s’affiche, dans laquelle vous pouvez modifier la description du score. Apportez vos modifications et sélectionnez **[!UICONTROL Enregistrer]**.

![plas-edit-save](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>La configuration du score ne peut pas être modifiée, car cela déclenchera une nouvelle formation et une nouvelle notation du modèle. C&#39;est l&#39;équivalent de la suppression du score et de la création d&#39;un nouveau score. Pour modifier la configuration du score, vous devez cloner ce score ou créer un nouveau score.

Vous revenez alors au **[!UICONTROL Services]** . Sélectionnez le score pour afficher les détails de la description mise à jour dans le panneau des détails supplémentaires sur le côté droit de l’écran.

## Clonage d’un score

Pour cloner un score, sélectionnez un score dans la variable **[!UICONTROL Services]** et sélectionnez **[!UICONTROL Cloner]** dans le panneau des détails supplémentaires sur le côté droit de l’écran.

![plas-clone-score](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

Le **[!UICONTROL Informations de base]** s’affiche. Le type, le nom et la description du profil sont clonés à partir du score d’origine. Modifiez ces détails et sélectionnez **[!UICONTROL Suivant]**.

![plas-clone-basic-info](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

Le **[!UICONTROL Définition de votre objectif]** s’affiche. Suivez la section Objectifs comme vous le feriez lors de la création d’un nouveau score et sélectionnez **[!UICONTROL Terminer]**.

Vous revenez alors au **[!UICONTROL Services]** où vous pouvez voir le score nouvellement cloné dans la liste.

>[!NOTE]
>
>Le **[!UICONTROL Définition de votre objectif]** n’est pas clonée à partir du score d’origine.

## Supprimer un score

Pour supprimer un score, sélectionnez un score dans la **[!UICONTROL Services]** et sélectionnez **[!UICONTROL Supprimer]** dans le panneau des détails supplémentaires sur le côté droit de l’écran.

![plas-delete-score](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

Le **[!UICONTROL Suppression de la documentation]** la boîte de dialogue de confirmation s’affiche. Sélectionnez **[!UICONTROL Supprimer]**.

![plas-delete-score-confirmation](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>La suppression de la définition de score supprimerait également tous les scores prévus sur le profil de la personne ou le profil du compte, mais pas le groupe de champs créé pour la définition de score. Le groupe de champs restera &quot;orphelin&quot; dans le modèle de données.

Vous revenez alors au **[!UICONTROL Services]** où vous ne pouvez plus voir le score dans la liste.

## Leads Codes d’erreur de pipeline AI

| Code d’erreur | Message d’erreur |
| --- | --- |
| 401 | ERREUR 401. Le pipeline Leads AI est arrêté : comptes valides insuffisants pour la notation de compte. Nombre de comptes : {}. |
| 402 | ERREUR 402. Le pipeline Leads AI est arrêté : contacts valides insuffisants pour la notation des contacts. Nombre de contacts : {}. |
| 403 | ERREUR 403. Le pipeline Leads AI est arrêté : volume d’activité insuffisant pour la formation de modèle. Nombre d’événements : {}. |
| 404 | ERREUR 404. Le pipeline Leads AI est arrêté : pas suffisamment de conversions pour la formation de modèle. Nombre de conversions : {}. |
| 405 | ERREUR 405. Le pipeline Leads AI est arrêté : activité trop éparse pour une formation de modèle valide. Seul {} % des comptes ont une activité. |
| 406 | ERREUR 406. Le pipeline Leads AI est arrêté : activité trop éparse pour une formation de modèle valide. Seul {} % des contacts ont une activité. |
| 407 | ERREUR 407. Le pipeline Leads AI est arrêté : les types d’activité de données de notation ne correspondent pas aux données de formation. |
| 408 | ERREUR 408. Le pipeline Leads AI est arrêté : le taux d’absence est trop élevé pour les fonctionnalités d’activité. Taux manquant : {}. |
| 409 | ERREUR 409. Le pipeline Leads AI est arrêté : test auc est trop faible. Test d’auc : {}. |
| 410 | ERREUR 410. Le pipeline Leads AI est arrêté : test auc est trop faible après réglage des paramètres. Test d’auc : {}. |
| 411 | ERREUR 411. Le pipeline Leads AI est arrêté : les données de formation ne disposent pas de suffisamment de conversions pour produire un modèle fiable. de conversions: {}. |
| 412 | ERREUR 412. Le pipeline Leads AI est arrêté : les données de test n’ont aucune conversion pour calculer AUC-ROC. |

| Code d’avertissement/d’information | Message |
| --- | --- |
| 100 | INFO 100. Contrôle la qualité de l’IA : le nombre de comptes est le suivant : {}. |
| 101 | INFO 101. Contrôle la qualité de l’IA : le nombre de contacts est le suivant : {}. |
| 102 | INFO 102. Contrôle la qualité de l’IA : le nombre d’opportunités est le suivant : {}. |
| 103 | INFO 103. Contrôle la qualité de l’IA : test d’auc est faible. Démarrez le réglage des paramètres. Test d’auc : {}. |
| 200 | AVERTISSEMENT 200. Contrôle la qualité de l’IA : le taux de fonctionnalités démographiques est le suivant : {}. |
| 201 | AVERTISSEMENT 201. Contrôle la qualité de l’IA : les fonctionnalités de taux d’activité manquantes sont les suivantes : {}. |

## Étapes suivantes

En suivant ce tutoriel, vous pouvez désormais créer et gérer des scores. Consultez les documents suivants pour plus d’informations :

* [Notation prédictive des prospects et des comptes](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [Surveillance des tâches de notation de compte et de piste prédictives](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)
