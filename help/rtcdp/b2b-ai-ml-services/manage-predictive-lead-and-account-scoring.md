---
title: Gérer la notation prédictive des prospects et des comptes dans Real-Time CDP B2B
type: Documentation
description: Ce document fournit des informations sur la gestion de la fonctionnalité de notation prédictive des prospects et des comptes dans Experience Platform CDP B2B.
feature: Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: fe7eb94e-5cf1-46bf-80e5-affe5735c998
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 4%

---

# Gérer la notation prédictive des prospects et des comptes dans Adobe Real-Time Customer Data Platform, B2B edition

>[!NOTE]
>
>Seuls les utilisateurs disposant d’une autorisation Gérer l’IA B2B peuvent créer, modifier et supprimer des objectifs de score.

Ce tutoriel vous guide tout au long des étapes de gestion des objectifs de score du service de notation prédictive des prospects et des comptes. Les objectifs de score peuvent être attribués au profil d’une personne ou au profil d’un compte

## Créer un nouveau score

Pour créer un nouveau score, sélectionnez le **[!UICONTROL Services]** dans la barre latérale et sélectionnez **[!UICONTROL Create score]**.

![plas-new-score](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

L’écran **[!UICONTROL Basic information]** s’affiche et vous invite à sélectionner un type de profil, à saisir un nom et une description facultative. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Next]**.

![plas-enter-basic-information](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

L’écran **[!UICONTROL Define your goal]** s’affiche. Sélectionnez la flèche déroulante, puis sélectionnez un type d’objectif dans la fenêtre déroulante qui s’affiche.

![plas-select-a-goal](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

La boîte de dialogue **[!UICONTROL Goal specifics]** s’ouvre. Sélectionnez la flèche déroulante, puis sélectionnez nom du champ de l’objectif dans la fenêtre déroulante qui s’affiche.

![plas-select-a-goal-field-name](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

La sélection de **[!UICONTROL Goal conditions]** s’affiche. Sélectionnez la flèche déroulante, puis sélectionnez condition dans la fenêtre déroulante qui s’affiche.

![condition-spécifique-à-l’objectif-plan](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

Le champ **[!UICONTROL Goal value]** s’affiche. Configurez ensuite votre [!UICONTROL Goal specifics]. Sélectionnez le panneau [!UICONTROL Enter Field Value] et saisissez la valeur de votre objectif.

>[!NOTE]
>
>Plusieurs valeurs d’objectif peuvent être ajoutées.

![plas-goal-specific-field-value](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

Pour ajouter des champs supplémentaires, sélectionnez **[!UICONTROL Add field]**.

![plas-goal-specific-add-event](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

Pour configurer le délai de prédiction, sélectionnez la flèche déroulante, puis sélectionnez le délai de votre choix.

![plas-prediction-timeframe](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

La politique de fusion sélectionnée détermine la manière dont les valeurs de champ d’un profil de personne sont sélectionnées. À l’aide de la flèche déroulante, sélectionnez la politique de fusion de votre choix, puis sélectionnez **[!UICONTROL Finish]**.

La boîte de dialogue **[!UICONTROL Scoring setup is complete]** s’affiche, confirmant que le nouveau score a été créé. Sélectionnez **[!UICONTROL OK]**.

![plas-score-complete](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>Chaque processus de notation peut prendre jusqu’à 24 heures.

Vous revenez alors à l’onglet **[!UICONTROL Services]** où vous pouvez voir le nouveau score créé dans la liste des scores.

![plas-score-created](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

Sélectionnez le score pour afficher les détails et des informations supplémentaires sur les détails de la dernière exécution.

![plas-score-additional-information](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

Pour plus d’informations sur les codes d’erreur visibles sous les détails de la dernière exécution, reportez-vous à la section [Codes d’erreur du pipeline de l’IA dédiée aux prospects](#leads-ai-pipeline-error-codes) dans ce document.

## Modifier un score

Pour modifier une note, sélectionnez une note dans l’onglet **[!UICONTROL Services]** et sélectionnez **[!UICONTROL Edit]** dans le panneau des détails supplémentaires sur le côté droit de l’écran.

![plas-edit-score](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png)

La boîte de dialogue **[!UICONTROL Edit instance]** s’affiche et vous pouvez modifier la description du score. Apportez vos modifications et sélectionnez **[!UICONTROL Save]**.

![plas-edit-save](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>La configuration de score ne peut pas être modifiée, car cela déclenchera le recyclage et le re-score du modèle. Cela équivaut à supprimer le score et à créer un nouveau score. Pour modifier la configuration de la note, vous devez cloner cette note ou créer une note.

Vous revenez alors à l’onglet **[!UICONTROL Services]** . Sélectionnez le score pour afficher les détails de la description mise à jour dans le panneau des détails supplémentaires sur le côté droit de l’écran.

## Cloner un score

Pour cloner une note, sélectionnez une note dans l’onglet **[!UICONTROL Services]** et sélectionnez **[!UICONTROL Clone]** dans le panneau des détails supplémentaires sur le côté droit de l’écran.

![plas-clone-score](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

L’écran **[!UICONTROL Basic information]** s’affiche. Le type, le nom et la description du profil sont clonés à partir du score d’origine. Modifiez ces détails et sélectionnez **[!UICONTROL Next]**.

![plas-clone-basic-info](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

L’écran **[!UICONTROL Define your goal]** s’affiche. Renseignez la section des objectifs comme vous le feriez lors de la création d’un nouveau score et sélectionnez **[!UICONTROL Finish]**.

Vous revenez alors à l’onglet **[!UICONTROL Services]** où vous pouvez voir le score nouvellement cloné dans la liste.

>[!NOTE]
>
>La section **[!UICONTROL Define your goal]** n’est pas clonée à partir de la note d’origine.

## Supprimer un score

Pour supprimer une note, sélectionnez une note dans l’onglet **[!UICONTROL Services]** et sélectionnez **[!UICONTROL Delete]** dans le panneau des détails supplémentaires sur le côté droit de l’écran.

![plas-delete-score](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

La boîte de dialogue de confirmation de **[!UICONTROL Delete documentation]** s’affiche. Sélectionnez **[!UICONTROL Delete]**.

![plas-delete-score-confirmation](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>La suppression de la définition de score supprimerait également tous les scores prévus sur le profil de personne ou le profil de compte, mais pas le groupe de champs créé pour la définition de score. Le groupe de champs reste « orphelin » dans le modèle de données.

Vous revenez alors à l’onglet **[!UICONTROL Services]** où vous ne pouvez plus voir le score dans la liste.

## Codes d’erreur du pipeline de l’IA dédiée aux leads

| Code d’erreur | Message d’erreur |
| --- | --- |
| 401 | ERREUR 401. Pipeline d’IA de leads arrêté : comptes valides insuffisants pour la notation du compte. Nombre de comptes : {}. |
| 402 | ERREUR 402. Pipeline d’IA de leads arrêté : pas assez de contacts valides pour la notation des contacts. Nombre de contacts : {}. |
| 403 | ERREUR 403. Pipeline d’IA de leads arrêté : volume d’activité insuffisant pour la formation du modèle. Nombre d’événements : {}. |
| 404 | ERREUR 404. Pipeline d’IA de leads arrêté : pas assez de conversions pour la formation du modèle. Nombre de conversions : {}. |
| 405 | ERREUR 405. Pipeline d’IA de leads arrêté : activité trop clairsemée pour une formation de modèle valide. Seul {} % des comptes ont une activité. |
| 406 | ERREUR 406. Pipeline d’IA de leads arrêté : activité trop clairsemée pour une formation de modèle valide. Seul {} % des contacts ont une activité. |
| 407 | ERREUR 407. Pipeline d’IA dédiée aux leads arrêté : les types d’activité de notation des données ne correspondent pas aux données d’identification. |
| 408 | ERREUR 408. Pipeline d’IA dédiée aux leads arrêté : le taux manquant est trop élevé pour les fonctionnalités d’activité. Taux manquant : {}. |
| 409 | ERREUR 409. Pipeline d’IA de leads arrêté : l’auc de test est trop faible. Auc de test : {}. |
| 410 | ERREUR 410. Pipeline de l’IA dédiée aux leads arrêté : l’auc de test est trop faible après l’optimisation des paramètres. Auc de test : {}. |
| 411 | ERREUR 411. Pipeline de l’IA dédiée aux leads arrêté : les données d’apprentissage n’ont pas suffisamment de conversions pour produire un modèle fiable. Conversions : {}. |
| 412 | ERREUR 412. Pipeline d’IA de leads arrêté : les données de test n’ont aucune conversion pour calculer l’AUC-ROC. |

| Code avertissement/info | Message |
| --- | --- |
| 100 | INFO 100. Vérification de la qualité de l’IA dédiée aux leads : le nombre de comptes est : {}. |
| 101 | INFOS 101. Vérification de la qualité de l’IA dédiée aux leads : le nombre de contacts est : {}. |
| 102 | INFOS 102. Vérification de la qualité de l’IA dédiée aux leads : le nombre d’opportunités est : {}. |
| 103 | INFO 103. Contrôle de qualité de l’IA dédiée aux leads : l’auc de test est faible. Commencez l’optimisation des paramètres. Test de l’auc : {}. |
| 200 | ATTENTION 200. Vérification de la qualité de l’IA dédiée aux leads : le taux manquant de fonctionnalités firmographiques est : {}. |
| 201 | AVERTISSEMENT 201. Vérification de la qualité de l’IA dédiée aux leads : le taux d’activité manquant est : {}. |

## Étapes suivantes

En suivant ce tutoriel, vous pouvez désormais créer et gérer des scores avec succès. Consultez les documents suivants pour plus d’informations :

* [Notation prédictive des prospects et des comptes](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [Surveiller les tâches de notation prédictive des prospects et des comptes](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)
