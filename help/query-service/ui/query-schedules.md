---
title: Planifications de requête
description: Découvrez comment automatiser les exécutions de requêtes planifiées, supprimer ou désactiver un planning de requêtes et utiliser les options de planification disponibles via l’interface utilisateur de Adobe Experience Platform.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 7d2027bf315ae6e354c906e4aabf6371a92e4148
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 39%

---

# Plannings de requête

Vous pouvez automatiser les exécutions de requêtes en créant des plannings de requête. Les requêtes planifiées s’exécutent sur une cadence personnalisée pour gérer vos données en fonction de la fréquence, de la date et de l’heure. Vous pouvez également choisir un jeu de données de sortie pour vos résultats, si nécessaire. Les requêtes qui ont été enregistrées en tant que modèle peuvent être planifiées à partir de l’éditeur de requêtes.

>[!IMPORTANT]
>
>Vous pouvez uniquement ajouter un planning à une requête qui a déjà été créée, enregistrée et exécutée.

Toutes les requêtes planifiées sont ajoutées à la liste dans la variable [!UICONTROL Requêtes planifiées] . Depuis cet espace de travail, vous pouvez surveiller l’état de toutes les tâches de requête planifiées via l’interface utilisateur. Sur le [!UICONTROL Requêtes planifiées] vous pouvez trouver des informations importantes sur vos exécutions de requête et vous abonner à des alertes. Les informations disponibles incluent l’état, les détails de planification et les codes/messages d’erreur en cas d’échec de l’exécution. Voir [Surveiller le document des requêtes planifiées](./monitor-queries.md) pour plus d’informations.

Ce workflow couvre le processus de planification dans l’interface utilisateur de Query Service. Pour savoir comment ajouter des plannings à l’aide de l’API, veuillez lire le [guide de point d’entrée des requêtes planifiées](../api/scheduled-queries.md).

## Créer un planning de requête {#create-schedule}

Pour planifier une requête, sélectionnez un modèle de requête dans l’une des options suivantes : [!UICONTROL Modèles] ou le [!UICONTROL Modèle] de la colonne [!UICONTROL Requêtes planifiées] . Lorsque vous sélectionnez le nom du modèle, vous accédez à l’éditeur de requêtes.

Si vous accédez à une requête enregistrée à partir de l’éditeur de requêtes, vous pouvez créer un planning pour la requête ou afficher le planning de la requête à partir du panneau Détails.

>[!TIP]
>
>Sélectionner **[!UICONTROL Afficher le planning]** pour accéder à l’espace de travail des plannings et afficher les exécutions de requête planifiées en un coup d’oeil.

![L’éditeur de requêtes avec [!UICONTROL Afficher le planning] et [!UICONTROL Ajouter un planning] surlignée.](../images/ui/query-schedules/view-add-schedule.png)

Sélectionner **[!UICONTROL Ajouter un planning]** pour accéder au [page détails du planning](#schedule-details).

Vous pouvez également sélectionner la variable **[!UICONTROL Planifications]** sous le nom de la requête.

![Query Editor avec l’onglet Plannings en surbrillance.](../images/ui/query-schedules/schedules-tab.png)

L’espace de travail des plannings s’affiche. Sélectionnez **[!UICONTROL Ajouter un planning]** pour créer un planning.

![Espace de travail Planning du Query Editor avec l’option Ajouter un planning mise en surbrillance.](../images/ui/query-schedules/add-schedule.png)

### Modifier les détails du planning {#schedule-details}

La page Détails du planning s’affiche. Sur cette page, vous pouvez choisir la fréquence de la requête planifiée, la date de début et de fin, le jour de la semaine où la requête planifiée sera exécutée, ainsi que le jeu de données vers lequel exporter la requête.

![Le panneau Détails du planning est mis en surbrillance.](../images/ui/query-schedules/schedule-details.png)

Vous pouvez choisir les options suivantes pour **[!UICONTROL Fréquence]** :

- **[!UICONTROL Horaire]** : la requête planifiée s’exécute toutes les heures pour la période que vous avez sélectionnée.
- **[!UICONTROL Quotidien]** : la requête planifiée s’exécute tous les X jours à l’heure et à la période que vous avez sélectionnées. Notez que l’heure sélectionnée est indiquée en **UTC**, et non dans votre fuseau horaire local.
- **[!UICONTROL Hebdomadaire]** : la requête sélectionnée sera exécutée aux jours de la semaine, à l’heure et à la période que vous avez sélectionnés. Notez que l’heure sélectionnée est indiquée en **UTC**, et non dans votre fuseau horaire local.
- **[!UICONTROL Mensuel]** : la requête sélectionnée s’exécute tous les mois au jour, à l’heure et à la période que vous avez sélectionnés. Notez que l’heure sélectionnée est indiquée en **UTC**, et non dans votre fuseau horaire local.
- **[!UICONTROL Annuel]** : la requête sélectionnée s’exécute chaque année au jour, au mois, à l’heure et à la période que vous avez sélectionnés. Notez que l’heure sélectionnée est indiquée en **UTC**, et non dans votre fuseau horaire local.

Pour le jeu de données de sortie, vous avez la possibilité d’utiliser l’option Ajouter dans un jeu de données existant ou créer et ajouter dans un nouveau jeu de données. La deuxième option signifie que si vous exécutez une requête pour la première fois et créez un jeu de données, toutes les exécutions suivantes continueront à insérer des données dans ce jeu de données.

>[!IMPORTANT]
>
> Puisque vous utilisez un jeu de données existant ou que vous en créez un nouveau, vous n’avez **pas** besoin d’inclure `INSERT INTO` ou `CREATE TABLE AS SELECT` dans le cadre de la requête, puisque les jeux de données sont déjà définis. L’inclusion de `INSERT INTO` ou `CREATE TABLE AS SELECT` dans le cadre de vos requêtes planifiées entraînera une erreur.

Si vous n’avez pas accès aux requêtes paramétrées, passez à la [suppression ou désactivation d’une planification](#delete-schedule) .

### Définir les paramètres d’une requête planifiée planifiée {#set-parameters}

>[!IMPORTANT]
>
>La fonction d’IU de requête paramétrée est actuellement disponible dans une **version limitée uniquement** et n’est pas disponible pour tous les clients.

Si vous créez une requête planifiée pour une requête paramétrée, vous devez maintenant définir les valeurs des paramètres pour ces exécutions de requête.

![La section Détails de la planification du workflow de création de la planification avec la section Paramètres de requête mise en surbrillance.](../images/ui/query-schedules/scheduled-query-parameter.png)

Après avoir confirmé tous ces détails, sélectionnez **[!UICONTROL Enregistrer]** pour créer un planning. L’espace de travail des plannings affiche les détails du planning nouvellement créé, y compris l’ID du planning, le planning lui-même et le jeu de données de sortie du planning. Vous pouvez utiliser l’ID de planning pour rechercher plus d’informations sur les exécutions de la requête planifiée elle-même. Pour en savoir plus, veuillez lire le [guide des points d’entrée d’exécution de requête planifiée](../api/runs-scheduled-queries.md).

![Espace de travail des plannings avec le nouveau planning mis en surbrillance.](../images/ui/query-schedules/schedules-workspace.png)

## Afficher les exécutions de requête planifiées {#scheduled-query-runs}

Pour afficher la liste des exécutions planifiées d’un modèle de requête, accédez au [!UICONTROL Requêtes planifiées] et sélectionnez un nom de modèle dans la liste disponible.

![L&#39;onglet Requêtes planifiées avec un modèle nommé en surbrillance.](../images/ui/query-schedules/view-scheduled-runs.png)

La liste des exécutions de requête pour cette requête planifiée s’affiche.

![La section Détails de l’espace de travail Requêtes planifiées avec une liste d’exécutions de requête mise en surbrillance pour une requête planifiée.](../images/ui/query-schedules/list-of-scheduled-runs.png)

Voir [guide de suivi des requêtes planifiées](./monitor-queries.md#inline-actions) pour obtenir des informations complètes sur la manière de surveiller l’état de toutes les tâches de requête via l’interface utilisateur.

## Supprimer ou désactiver un planning {#delete-schedule}

Vous pouvez supprimer ou désactiver un planning dans l’espace de travail des plannings d’une requête spécifique ou dans l’ [!UICONTROL Requêtes planifiées] Workspace qui répertorie toutes les requêtes planifiées.

Pour accéder au [!UICONTROL Planifications] de la requête choisie, vous devez sélectionner le nom d&#39;un modèle de requête parmi les [!UICONTROL Modèles] ou le [!UICONTROL Requêtes planifiées] . L’éditeur de requêtes de cette requête est alors accessible. Dans Query Editor, sélectionnez **[!UICONTROL Planifications]** pour accéder à l’espace de travail des plannings.

Sélectionnez un planning dans les lignes des plannings disponibles. Vous pouvez activer ou désactiver la requête planifiée à l’aide du bouton d’activation.

>[!IMPORTANT]
>
>Vous devez désactiver le planning avant de pouvoir supprimer un planning pour une requête.

Sélectionnez **[!UICONTROL Supprimer un planning]** pour supprimer le planning désactivé.

![L’espace de travail des plannings avec l’option Désactiver le planning et Supprimer le planning est en surbrillance.](../images/ui/query-schedules/delete-schedule.png)

Vous pouvez également utiliser la variable [!UICONTROL Requêtes planifiées] tab propose une collection d’actions intégrées pour chaque requête planifiée. Les actions intégrées disponibles sont les suivantes : [!UICONTROL Désactiver le planning] ou [!UICONTROL Activation du planning], [!UICONTROL Supprimer le planning], et [!UICONTROL Abonner] aux alertes pour la requête planifiée. Pour obtenir des instructions complètes sur la suppression ou la désactivation d’une requête planifiée via l’onglet Requêtes planifiées, voir la section [guide de suivi des requêtes planifiées](./monitor-queries.md#inline-actions).
