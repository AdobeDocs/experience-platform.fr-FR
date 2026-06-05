---
title: Plannings de requête
description: Découvrez comment automatiser les exécutions de requête planifiées, modifier les paramètres de planning existants, supprimer ou désactiver un planning de requête et utiliser les options de planification disponibles via l’interface utilisateur de Adobe Experience Platform.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
TQID: https://experienceleague.adobe.com/TazOHQGBFYjSGH0WjggCDoo8YybIJ3Wg61Iz8igpFNk
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: d50a9dc5e0afacd9b61ad5836032c53a6bf32533
workflow-type: tm+mt
source-wordcount: 2824
ht-degree: 7%

---

# Plannings de requête

Vous pouvez automatiser les exécutions de requête en créant des plannings de requête. Les requêtes planifiées s’exécutent à une cadence personnalisée pour gérer vos données en fonction de la fréquence, de la date et de l’heure. Vous pouvez également choisir un jeu de données de sortie pour vos résultats, si nécessaire. Les requêtes qui ont été enregistrées en tant que modèle peuvent être planifiées à partir de Query Editor.

>[!IMPORTANT]
>
>Vous pouvez uniquement ajouter un planning à une requête qui a déjà été créée et enregistrée.

## Exigences de compte pour les requêtes planifiées {#technical-account-user-requirements}

Pour que les requêtes planifiées s’exécutent de manière fiable, Adobe recommande aux administrateurs de configurer un compte technique (à l’aide des informations d’identification de serveur à serveur OAuth) pour créer des requêtes planifiées. Les requêtes planifiées peuvent également être créées avec un compte utilisateur personnel, mais les requêtes créées de cette manière cesseront de s’exécuter si l’accès de cet utilisateur est supprimé ou désactivé.

Pour plus d’informations sur la configuration des comptes techniques et l’attribution des autorisations requises, consultez les [Conditions préalables du guide d’identification](./credentials.md#prerequisites) et [Authentification de l’API](../../landing/api-authentication.md).

Pour plus d’informations sur la création et la configuration d’un compte technique, voir :

- [Configuration de Developer Console &#x200B;](https://experienceleague.adobe.com/fr/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/set-up-developer-console-and-postman) : instructions détaillées pour configurer Adobe Developer Console et obtenir les informations d’identification OAuth.
- [Configuration de compte technique de bout en bout](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/setup) : présentation complète de la création et de la configuration d’un compte technique dans Adobe Experience Platform.

Si vous utilisez uniquement l’interface utilisateur de Query Service, assurez-vous de disposer des autorisations nécessaires ou contactez un administrateur qui gère les comptes techniques. Toutes les requêtes planifiées sont ajoutées à la liste dans l’onglet [!UICONTROL Requêtes planifiées], où vous pouvez surveiller le statut, les détails de la planification et les messages d’erreur de tous les traitements de requête planifiés, ainsi que vous abonner aux alertes. Pour plus d’informations sur la surveillance et la gestion de vos requêtes, consultez le document [surveiller les requêtes planifiées](./monitor-queries.md).

Ce workflow couvre le processus de planification dans l’interface utilisateur de Query Service. Pour savoir comment ajouter des plannings à l’aide de l’API, reportez-vous au guide de point d’entrée [des requêtes planifiées](../api/scheduled-queries.md).

>[!NOTE]
>
>Utilisez un compte technique pour vous assurer que les requêtes planifiées continuent à s’exécuter même si les utilisateurs et utilisatrices quittent l’organisation ou si leurs rôles changent. Choisissez un compte technique chaque fois que cela est possible pour une automatisation ininterrompue des requêtes.

## Créer un planning de requête {#create-schedule}

Pour planifier une requête, sélectionnez un modèle de requête dans l’onglet [!UICONTROL Modèles] ou dans la colonne [!UICONTROL Modèle] de l’onglet [!UICONTROL Requêtes planifiées]. La sélection du nom du modèle vous permet d’accéder au Query Editor.

Si vous accédez à une requête enregistrée à partir du Query Editor, vous pouvez créer un planning pour la requête ou afficher le planning de la requête à partir du panneau des détails.

>[!TIP]
>
>Sélectionnez **[!UICONTROL Afficher le planning]** pour accéder à l’espace de travail des plannings et afficher en un coup d’œil les exécutions de requête planifiées.

![Query Editor avec les options [!UICONTROL Afficher le planning] et [!UICONTROL Ajouter un planning] mises en surbrillance.](../images/ui/query-schedules/view-add-schedule.png)

Sélectionnez **[!UICONTROL Ajouter un planning]** pour accéder à la page [Détails du planning](#schedule-details).

Vous pouvez également sélectionner l’onglet **[!UICONTROL Plannings]** sous le nom de la requête.

![Requêteur avec l’onglet Plannings en surbrillance.](../images/ui/query-schedules/schedules-tab.png)

L’espace de travail des plannings s’affiche. L’interface utilisateur affiche une liste de toutes les exécutions planifiées auxquelles le modèle est associé. Sélectionnez **[!UICONTROL Ajouter un planning]** pour créer un planning.

![Espace de travail Planning du requêteur avec l’option Ajouter un planning mise en surbrillance.](../images/ui/query-schedules/add-schedule.png)

### Ajouter les détails du planning {#schedule-details}

>[!CONTEXTUALHELP]
>id="platform_queryService_querySchedules_noEndDate"
>title="Requête planifiée sans date de fin"
>abstract="Cette requête planifiée n’a pas de date de fin et continue de s’exécuter jusqu’à ce que vous la suspendiez ou la supprimiez manuellement. Vérifiez régulièrement les plannings de longue durée pour éviter toute utilisation inutile des ressources de calcul."

La page Détails du planning s’affiche. Utilisez cette page pour configurer les paramètres de planification de la requête planifiée. Les détails incluent la [fréquence et jour de la semaine de la requête planifiée](#scheduled-query-frequency) l’exécution, les dates de début et de fin, le jeu de données vers lequel exporter les résultats et les [alertes de statut de la requête](#alerts-for-query-status).

>[!IMPORTANT]
>
>La prise en charge des requêtes planifiées sans date de fin est actuellement disponible pour un nombre limité de clients et clientes. Si cette fonctionnalité est activée pour votre organisation, vous pouvez créer des requêtes planifiées qui s’exécutent en continu sans spécifier de date de fin. Dans certaines réponses système et vues de l&#39;interface utilisateur, les plannings sans date de fin peuvent apparaître avec une date à long terme, telle que `31.12.9999`.
>
>Si cette fonctionnalité n’est pas activée pour votre organisation, une date de fin doit être spécifiée. Il n’existe pas de limite supérieure pour la date de fin.

![Le panneau Détails du planning est mis en surbrillance.](../images/ui/query-schedules/schedule-details.png)

#### Périodicité de requête planifiée {#scheduled-query-frequency}

Vous pouvez choisir les options suivantes pour **[!UICONTROL Fréquence]** :

- **[!UICONTROL Par heure]** : la requête planifiée s’exécute toutes les heures pour la période que vous avez sélectionnée.
- **[!UICONTROL Quotidien]** : la requête planifiée s’exécute tous les X jours à l’heure et à la période que vous avez sélectionnées. Notez que l’heure sélectionnée est indiquée en **UTC**, et non dans votre fuseau horaire local.
- **[!UICONTROL Hebdomadaire]** : la requête sélectionnée sera exécutée aux jours de la semaine, à l’heure et à la période que vous avez sélectionnés. Notez que l’heure sélectionnée est indiquée en **UTC**, et non dans votre fuseau horaire local.
- **[!UICONTROL Mensuel]** : la requête sélectionnée s’exécute tous les mois au jour, à l’heure et à la période que vous avez sélectionnés. Notez que l’heure sélectionnée est indiquée en **UTC**, et non dans votre fuseau horaire local.
- **[!UICONTROL Annuel]** : la requête sélectionnée s’exécute chaque année au jour, au mois, à l’heure et à la période que vous avez sélectionnés. Notez que l’heure sélectionnée est indiquée en **UTC**, et non dans votre fuseau horaire local.

### Fournir des détails sur le jeu de données {#dataset-details}

Gérez les résultats de la requête en ajoutant les données à un jeu de données existant ou en créant un nouveau jeu de données et en y ajoutant les données.

Sélectionnez **[!UICONTROL Créer et ajouter dans un nouveau jeu de données]** pour créer un jeu de données lorsque vous exécutez une requête pour la première fois. Les exécutions suivantes continuent d’insérer des données dans ce jeu de données. Enfin, indiquez un nom et une description pour le jeu de données.

>[!IMPORTANT]
>
> Puisque vous utilisez un jeu de données existant ou que vous en créez un nouveau, vous n’avez **pas** besoin d’inclure `INSERT INTO` ou `CREATE TABLE AS SELECT` dans le cadre de la requête, puisque les jeux de données sont déjà définis. L’inclusion de `INSERT INTO` ou `CREATE TABLE AS SELECT` dans le cadre de vos requêtes planifiées entraînera une erreur.

![Le panneau Détails du planning avec les détails du jeu de données et les options [!UICONTROL Créer et ajouter dans un nouveau jeu de données] mises en surbrillance.](../images/ui/query-schedules/dataset-details-create-and-append.png)

Vous pouvez également sélectionner **[!UICONTROL Ajouter à un jeu de données existant]** suivi de l’icône du jeu de données (![Icône du jeu de données.](/help/images/icons/database.png)).

![Le panneau Détails du planning avec les détails du jeu de données et Ajouter dans le jeu de données existant mis en surbrillance.](../images/ui/query-schedules/dataset-details-existing.png)

La boîte de dialogue **[!UICONTROL Sélectionner le jeu de données de sortie]** s’affiche.

Ensuite, parcourez les jeux de données existants ou utilisez le champ de recherche pour filtrer les options. Sélectionnez la ligne du jeu de données que vous souhaitez utiliser. Les détails du jeu de données s’affichent dans le panneau de droite. Sélectionnez **[!UICONTROL Terminé]** pour confirmer votre choix.

![La boîte de dialogue Sélectionner le jeu de données de sortie avec le champ de recherche, une ligne de jeu de données et Terminé en surbrillance.](../images/ui/query-schedules/select-output-dataset-dialog.png)

### Les requêtes en quarantaine en cas d’échec continu {#quarantine}

Lors de la création d’un planning, vous pouvez inscrire votre requête à la fonction de quarantaine afin de protéger les ressources système et d’éviter des perturbations potentielles. La fonction de quarantaine identifie et isole automatiquement les requêtes qui échouent à plusieurs reprises en les plaçant dans un état [!UICONTROL Quarantaine]. En mettant les requêtes en quarantaine après dix échecs consécutifs, vous pouvez intervenir, réviser et corriger les problèmes avant d’autoriser d’autres exécutions. Cela permet de maintenir votre efficacité opérationnelle et l’intégrité des données.

![Espace de travail des plannings de requête avec [!UICONTROL &#x200B; Query Quarantine &#x200B;] en surbrillance et Oui sélectionné.](../images/ui/query-schedules/quarantine-enroll.png)

Une fois qu’une requête est inscrite à la fonction de quarantaine, vous pouvez vous abonner à des alertes pour ce changement de statut de la requête. Si une requête planifiée n’est pas mise en quarantaine, elle n’apparaît pas comme option dans [la boîte de dialogue Alertes](./monitor-queries.md#alert-subscription).

Vous pouvez également inscrire une requête planifiée à la fonction de quarantaine à partir des actions intégrées de l’onglet [!UICONTROL Requêtes planifiées]. Pour plus d’informations, consultez la documentation [surveiller les requêtes](./monitor-queries.md#quarantined-queries).

### Définir des alertes pour le statut d’une requête planifiée {#alerts-for-query-status}

Vous pouvez également vous abonner aux alertes de requêtes dans le cadre des paramètres de vos requêtes planifiées. Vous pouvez configurer vos paramètres pour recevoir des notifications pour diverses situations. Les alertes peuvent être définies pour un statut mis en quarantaine, des retards dans le traitement des requêtes ou un changement de statut de votre requête. Les options d’alerte d’état de requête disponibles incluent le début, la réussite et l’échec. Les alertes peuvent être reçues sous la forme de notifications pop-up ou d’e-mails. Cochez la case pour vous abonner aux alertes concernant ce statut de requête planifiée.

![Panneau Détails du planning avec les options d’alerte mises en surbrillance.](../images/ui/query-editor/alerts.png)

Le tableau ci-dessous décrit les types d’alerte de requête pris en charge :

| Type d’alerte | Description |
|---|---|
| `start` | Cette alerte vous avertit lorsqu’une exécution de requête planifiée est lancée ou commence à être traitée. |
| `success` | Cette alerte vous informe lorsqu’une exécution de requête planifiée se termine avec succès, indiquant que la requête s’est exécutée sans erreur. |
| `failed` | Cette alerte se déclenche lorsqu’une exécution de requête planifiée rencontre une erreur ou ne s’exécute pas correctement. Cela vous aide à identifier et à résoudre les problèmes rapidement. |
| `quarantine` | Cette alerte est activée lorsqu’une exécution de requête planifiée est mise en quarantaine. Une fois qu’une requête est [inscrite dans la fonction de quarantaine](#quarantine), toute requête planifiée qui échoue dix exécutions consécutives passe automatiquement à l’état [!UICONTROL En quarantaine]. Une requête en quarantaine nécessite ensuite votre intervention avant que d’autres exécutions ne puissent avoir lieu. Remarque : les requêtes doivent être inscrites à la fonction de quarantaine pour que vous puissiez vous abonner aux alertes de quarantaine. |
| `delay` | Cette alerte vous avertit en cas de [&#x200B; retard dans le résultat d’une exécution de requête planifiée](./monitor-queries.md#query-run-delay) au-delà d’un seuil spécifié. Vous pouvez définir une heure personnalisée qui déclenche l’alerte lorsque la requête s’exécute pendant cette durée sans terminer ni échouer. Le comportement par défaut définit une alerte pendant 150 minutes après le début du traitement de la requête. |

>[!NOTE]
>
>Si vous choisissez de définir une alerte [!UICONTROL Délai d’exécution des requêtes], vous devez définir le délai souhaité en minutes dans l’interface utilisateur d’Experience Platform. Saisissez la durée en minutes. Le délai maximal est de 24 heures (1 440 minutes).

Pour obtenir un aperçu des alertes dans Adobe Experience Platform, y compris la structure de la définition des règles d’alerte, reportez-vous à la [présentation des alertes](../../observability/alerts/overview.md). Pour obtenir des conseils sur la gestion des alertes et des règles d’alerte dans l’interface utilisateur de Adobe Experience Platform, consultez le [&#x200B; Guide de l’interface utilisateur des alertes](../../observability/alerts/ui.md).

### Définition des paramètres d’une requête paramétrée planifiée {#set-parameters}

Si vous créez une requête planifiée pour une [requête paramétrée](./parameterized-queries.md), vous devez maintenant définir les valeurs de paramètre pour ces exécutions de requête.

![La section Détails du planning du workflow de création du planning avec la section Paramètres de requête mise en surbrillance.](../images/ui/query-schedules/scheduled-query-parameter.png)

Après avoir confirmé les détails de votre planning, sélectionnez **[!UICONTROL Enregistrer]** pour créer un planning. Vous revenez sur l’onglet Plannings de votre modèle. Cet espace de travail affiche les détails du planning nouvellement créé, y compris l’identifiant du planning, le planning lui-même et le jeu de données de sortie du planning.

## Afficher les exécutions de requête planifiées {#scheduled-query-runs}

Dans l’onglet [!UICONTROL Plannings] de votre modèle, sélectionnez l’ID de planning pour accéder à la liste des exécutions de requête pour votre nouvelle requête planifiée.

![Espace de travail des plannings avec le nouveau planning mis en surbrillance.](../images/ui/query-schedules/schedules-workspace.png)

Vous pouvez également afficher la liste des exécutions planifiées d’un modèle de requête en accédant à l’onglet **[!UICONTROL Requêtes planifiées]** et en sélectionnant un nom de modèle dans la liste disponible.

![Onglet Requêtes planifiées avec un modèle nommé mis en surbrillance.](../images/ui/query-schedules/view-scheduled-runs.png)

La liste des exécutions de requête pour cette requête planifiée s’affiche.

### Heures de calcul au niveau de la tâche {#compute-hours}

Effectuez le suivi des heures de calcul consommées au niveau de l’exécution des requêtes pour vos requêtes par lots CTAS/ITAS. Cette fonctionnalité offre des informations sur l’utilisation du calcul, ce qui vous permet d’optimiser l’allocation des ressources et d’améliorer les performances des requêtes.

>[!AVAILABILITY]
>
>La fonctionnalité Heures de calcul est réservée aux utilisateurs qui ont acheté le [SKU de Data Distiller](../data-distiller/overview.md). Contactez votre représentant ou représentante Adobe pour plus d’informations.

![Section de détails de l’espace de travail Requêtes planifiées avec une liste d’exécutions de requête mises en surbrillance pour une requête planifiée.](../images/ui/query-schedules/list-of-scheduled-runs.png)

Le tableau suivant fournit des descriptions de chaque colonne disponible dans la section détails qui répertorie les exécutions de requête planifiées.

| Titre de colonne | Description |
|---------------------|----------------------------------|
| [!UICONTROL ID d’exécution de requête] | Affiche un identifiant unique pour chaque exécution de requête, ce qui vous permet de suivre et de référencer les exécutions individuelles de vos requêtes planifiées. |
| [!UICONTROL Début de l’exécution de la requête] | Indique la date et l’heure de début de l’exécution de la requête afin de vous aider à surveiller le début de chaque exécution. |
| [!UICONTROL Exécution de la requête terminée] | Affiche la date et l’heure d’achèvement de l’exécution de la requête, afin de fournir à insight la durée et le statut d’exécution. |
| [!UICONTROL Statut] | Affiche le statut actuel de l’exécution de la requête, tel que `Completed,` `Running,` ou `Failed,` pour évaluer le résultat rapidement. |
| [!UICONTROL Jeux de données] | Répertorie les jeux de données utilisés dans l’exécution de la requête afin d’indiquer les sources de données impliquées dans l’exécution. |
| [!UICONTROL Heures de calcul] | Affiche le temps de calcul utilisé pour chaque exécution de requête, mesuré en heures. Cela permet de suivre l’utilisation des ressources et d’optimiser les performances des requêtes. |

{style="table-layout:auto"}

>[!NOTE]
>
>Les données des heures de calcul sont disponibles à partir du 08/15/2024. Les données antérieures à cette date apparaissent comme « Non disponibles ».

Consultez le [guide de surveillance des requêtes planifiées](./monitor-queries.md) pour obtenir des informations complètes sur la manière de surveiller le statut de tous les traitements de requêtes via l’interface utilisateur.

Sélectionnez un **[!UICONTROL ID d’exécution de requête]** dans la liste pour accéder à la présentation de l’exécution de requête. Pour obtenir une répartition complète des informations disponibles dans la [présentation de l’exécution des requêtes](./monitor-queries.md#query-run-overview), consultez la documentation sur la surveillance des requêtes planifiées.

Pour surveiller les requêtes planifiées à l’aide de l’API Query Service, consultez le guide [des points d’entrée d’exécution de requête planifiée](../api/runs-scheduled-queries.md).

## Modification d’un planning {#edit-schedule}

Vous pouvez accéder à l’éditeur de planning à partir de l’espace de travail [!UICONTROL Requêtes planifiées], de la page des détails du planning ou de l’éditeur de requêtes. Vous pouvez modifier les paramètres de configuration pris en charge pour une requête planifiée existante sans recréer la planification. La modification d’un planning met uniquement à jour la configuration du planning. Elle ne modifie pas la définition de la requête SQL sous-jacente.

>[!IMPORTANT]
>
>L’option **[!UICONTROL Modifier le planning]** ne s’affiche que pour les plannings éligibles. Les planifications terminées, supprimées ou toujours enregistrées ne peuvent pas être modifiées.

### Accès au workflow de modification {#access-edit-workflow}

Utilisez l’un des chemins suivants de l’onglet **[!UICONTROL Requêtes planifiées]** pour accéder au workflow de modification d’une requête planifiée éligible.

Sélectionnez les points de suspension (**...**) pour le planning que vous souhaitez modifier, puis **[!UICONTROL Modifier le planning]** dans le menu d’actions intégrées. L’éditeur de planning s’ouvre alors directement. Pour plus d’informations, consultez [Gestion des requêtes planifiées avec des actions intégrées](./monitor-queries.md#inline-actions).

![Onglet Requêtes planifiées avec les points de suspension d’action intégrés et Modifier le planning mis en surbrillance dans le menu contextuel.](../images/ui/query-schedules/inline-actions-edit.png)

Vous pouvez également sélectionner un nom de planning dans la table pour ouvrir la page des détails du planning. Sur la page des détails du planning, sélectionnez **[!UICONTROL Modifier le planning]** dans le coin supérieur droit de la page pour ouvrir l’éditeur de planning.

![Page des détails du planning avec le bouton Modifier le planning en surbrillance.](../images/ui/query-schedules/edit-schedule.png)

Vous pouvez également modifier un planning qualifié existant à partir de Query Editor.

1. Ouvrez un modèle de requête dans Query Editor et sélectionnez **[!UICONTROL Afficher le planning]**.
2. Sélectionnez l’ID du planning dans la liste pour ouvrir la page des détails du planning.
3. Sélectionnez **[!UICONTROL Modifier le planning]**.

### Modifier les paramètres du planning {#edit-schedule-settings}

Utilisez l’éditeur de planification pour passer en revue la configuration de planification actuelle et mettre à jour les paramètres pris en charge.

>[!NOTE]
>
>Les champs **[!UICONTROL Date de début]** et **[!UICONTROL Heure de début]** sont fixes lors de la création et ne peuvent pas être modifiés. Pour utiliser une date ou une heure de début différente, [créez une nouvelle planification](#create-schedule).

![L’éditeur de planning affiche les paramètres de planning modifiables, notamment la fréquence, les jours de périodicité, la date de fin, l’heure de fin, l’inscription à la quarantaine de la requête et les abonnements aux alertes. Les champs Date de début et Heure de début sont désactivés et ne peuvent pas être modifiés.](../images/ui/query-schedules/schedule-editor.png)

Les paramètres suivants peuvent être modifiés :

| Paramètre | Description |
|---|---|
| **[!UICONTROL Fréquence]** | Fréquence d’exécution de la requête. Les options incluent **[!UICONTROL Horaire]**, **[!UICONTROL Quotidien]**, **[!UICONTROL Hebdomadaire]**, **[!UICONTROL Mensuel]** et **[!UICONTROL Annuel]**. |
| **[!UICONTROL Jours]** | Jours d’exécution de la requête. Choisissez un ou plusieurs jours de la semaine pour exécuter une cadence hebdomadaire ou un jour spécifique du mois si vous exécutez des fréquences mensuelles ou annuelles. |
| **[!UICONTROL Date de fin]** | Date à laquelle la requête planifiée s’arrête. |
| **[!UICONTROL Heure de fin]** | Heure à laquelle le planning se termine à la date de fin spécifiée. |
| **[!UICONTROL Pas de date de fin]** | Configure le planning pour qu’il s’exécute en continu sans date de fin, si cette option est activée pour votre organisation. |
| **[!UICONTROL Quarantaine de requête]** | Inscrit ou supprime la requête de la fonction de quarantaine. Pour plus d’informations, consultez [Requêtes de quarantaine en cas d’échec continu](#quarantine). |
| **[!UICONTROL Alertes]** | Ajoute, supprime ou modifie les abonnements aux alertes pour cette requête planifiée. Voir [Définir des alertes pour le statut d’une requête planifiée](#alerts-for-query-status) pour connaître les types d’alerte disponibles. |

### Enregistrer les modifications du planning {#save-schedule-changes}

Après avoir mis à jour les paramètres du planning, sélectionnez **[!UICONTROL Enregistrer]** pour appliquer les modifications. Un message de confirmation s’affiche lorsque le planning est correctement mis à jour.

### Vérifier les informations de planning mises à jour {#verify-schedule-updates}

Après l’enregistrement, vérifiez que la configuration de planning mise à jour s’affiche aux emplacements suivants :

- L’onglet **[!UICONTROL Requêtes planifiées]**.
- Panneau **[!UICONTROL Propriétés]** de la page [Détails du planning](./monitor-queries.md#query-runs).

## Activation, désactivation ou suppression d’un planning {#delete-schedule}

Vous pouvez activer, désactiver ou supprimer un planning dans l’espace de travail des plannings d’une requête spécifique ou dans l’espace de travail [!UICONTROL Requêtes planifiées] qui répertorie toutes les requêtes planifiées.

Pour accéder à l’onglet [!UICONTROL Plannings] de la requête de votre choix, vous devez sélectionner le nom d’un modèle de requête dans l’onglet [!UICONTROL Modèles] ou [!UICONTROL Requêtes planifiées]. Cette action permet d’accéder à l’éditeur de requêtes pour cette requête. Dans le Query Editor, sélectionnez **[!UICONTROL Plannings]** pour accéder à l’espace de travail des plannings.

Sélectionnez un planning dans les lignes des plannings disponibles pour remplir le panneau des détails. Utilisez le bouton (bascule) pour désactiver (ou activer) la requête planifiée.

### Supprimer les requêtes désactivées

>[!IMPORTANT]
>
>Vous devez désactiver le planning avant de pouvoir supprimer un planning pour une requête.

![Liste des plannings d’un modèle avec le panneau des détails mis en surbrillance.](../images/ui/query-schedules/schedule-details-panel.png)

Une boîte de dialogue de confirmation s’affiche. Sélectionnez **[!UICONTROL Désactiver]** pour confirmer l’action.

![Boîte de dialogue de confirmation Désactiver le planning.](../images/ui/query-schedules/disable-schedule-confirmation-dialog.png)

Sélectionnez **[!UICONTROL Supprimer un planning]** pour supprimer le planning désactivé.

![Espace de travail des plannings avec l’option Supprimer le planning mise en surbrillance.](../images/ui/query-schedules/delete-schedule.png)

L’onglet [!UICONTROL Requêtes planifiées] propose également une collection d’actions intégrées pour chaque requête planifiée. Les actions intégrées disponibles sont les suivantes : [!UICONTROL Désactiver le planning] ou [!UICONTROL Activer le planning], [!UICONTROL Supprimer le planning] et [!UICONTROL S’abonner] aux alertes pour la requête planifiée. Pour obtenir des instructions complètes sur la suppression ou la désactivation d’une requête planifiée via l’onglet Requêtes planifiées , consultez le guide [surveiller les requêtes planifiées](./monitor-queries.md#inline-actions).
