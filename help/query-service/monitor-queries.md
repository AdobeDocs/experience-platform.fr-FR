---
title: Surveiller les requêtes
description: Découvrez comment surveiller les requêtes via l’interface utilisateur de Query Service.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 1%

---

# Surveillance des requêtes

Adobe Experience Platform offre une meilleure visibilité de l’état de toutes les tâches de requête via l’interface utilisateur. De [!UICONTROL Requêtes planifiées] vous pouvez maintenant trouver des informations importantes sur les exécutions de votre requête qui incluent l’état, les détails de planification et les messages/codes d’erreur en cas d’échec. Vous pouvez également vous abonner à des alertes pour les requêtes en fonction de leur état via l’interface utilisateur pour l’une de ces requêtes via [!UICONTROL Requêtes planifiées] .

## [!UICONTROL Requêtes planifiées]

Le [!UICONTROL Requêtes planifiées] fournit un aperçu des requêtes exécutées et planifiées. L’espace de travail contient toutes vos requêtes CTAS et ITAS qui sont planifiées pour s’exécuter ou qui ont été exécutées au moins une fois. Vous trouverez des détails sur l’exécution pour toutes les requêtes planifiées, ainsi que des codes d’erreur et des messages pour les requêtes en échec.

Pour accéder au [!UICONTROL Requêtes planifiées] onglet, sélectionnez **[!UICONTROL Requêtes]** dans la barre de navigation de gauche, suivie de **[!UICONTROL Requêtes planifiées]**

![L’onglet Requêtes planifiées de l’espace de travail Requêtes .](./images/monitor-queries/scheduled-queries.png)

Le tableau ci-dessous décrit chaque colonne disponible.

>[!NOTE]
>
>L’icône d’abonnement aux alertes se trouve dans chaque ligne d’une colonne sans titre. Voir [abonnements aux alertes](#alert-subscription) pour plus d’informations.

| Colonne | Description |
|---|---|
| Nom | Le champ name correspond au nom du modèle ou aux premiers caractères de votre requête SQL. Toute requête créée à l’aide de l’interface utilisateur avec Query Editor est nommée dès le départ. Si la requête a été créée via l’API, alors le nom de la requête est un extrait de code SQL initial utilisé pour créer la requête. |
| Modèle | Nom du modèle de la requête. Sélectionnez un nom de modèle pour accéder à l’éditeur de requêtes. Le modèle de requête est affiché dans Query Editor à des fins pratiques. S’il n’existe aucun nom de modèle, la ligne est marquée d’un trait d’union et il n’est pas possible de rediriger vers l’éditeur de requêtes pour afficher la requête. |
| SQL | Fragment de la requête SQL. |
| Fréquence d’exécution | Il s’agit de la cadence d’exécution de votre requête. Les valeurs disponibles sont les suivantes : `Run once` et `Scheduled`. Les requêtes peuvent être filtrées en fonction de leur fréquence d’exécution. |
| Créé par | Nom de l’utilisateur qui a créé la requête. |
| Créé | Horodatage de création de la requête, au format UTC. |
| Horodatage de la dernière exécution | Horodatage le plus récent lors de l’exécution de la requête. Cette colonne indique si une requête a été exécutée conformément à son planning actuel. |
| État de la dernière exécution | Etat de la dernière exécution de la requête. Les trois valeurs d’état sont les suivantes : `successful` `failed` ou `in progress`. |

>[!TIP]
>
>Si vous accédez à l’éditeur de requêtes, vous pouvez sélectionner **[!UICONTROL Requêtes]** pour revenir au [!UICONTROL Modèles] .

### Personnalisation des paramètres de tableau pour les requêtes planifiées

Vous pouvez ajuster les colonnes du [!UICONTROL Requêtes planifiées] à vos besoins. Cliquez sur l’icône des paramètres (![Icône Paramètres .](./images/monitor-queries/settings-icon.png)) pour ouvrir le [!UICONTROL Personnalisation du tableau] et modifiez les colonnes disponibles.

![Icône Personnaliser les paramètres du tableau .](./images/monitor-queries/customze-table-settings-icon.png)

Activez/désactivez les cases à cocher appropriées pour supprimer ou ajouter une colonne de tableau. Ensuite, sélectionnez **[!UICONTROL Appliquer]** pour confirmer vos choix.

>[!NOTE]
>
>Toute requête créée via l’interface utilisateur devient un modèle nommé dans le cadre du processus de création. Le nom du modèle s’affiche dans la colonne Modèle. Si la requête a été créée via l’API, la colonne de modèle est vide.

![Boîte de dialogue Personnaliser les paramètres du tableau .](./images/monitor-queries/customize-table-dialog.png)

### S’abonner aux alertes {#alert-subscription}

Vous pouvez vous abonner à des alertes à l’aide du [!UICONTROL Requêtes planifiées] . Sélectionnez l’icône de notification d’alerte (![Icône d’alerte.](./images/monitor-queries/alerts-icon.png)) en regard d’un nom de requête pour ouvrir la variable [!UICONTROL Alertes] boîte de dialogue. Le [!UICONTROL Alertes] s’abonne aux notifications de l’interface utilisateur et aux alertes par courrier électronique. Les alertes reposent sur l’état de la requête. Trois options sont disponibles : `start`, `success`, et `failure`. Cochez la ou les cases correspondantes et sélectionnez **[!UICONTROL Enregistrer]** pour vous abonner.

<!-- This dialog will be updated before release. THe image below will need to be updated inline with these changes. -->

![Boîte de dialogue d’inscription des alertes.](./images/monitor-queries/alert-subscription-dialog.png)

<!-- Link to alert subscriptions doc when available -->

### Filtrage des requêtes

Vous pouvez filtrer les requêtes selon la fréquence d’exécution. Dans la [!UICONTROL Requêtes planifiées] , sélectionnez l’icône de filtre (![Icône Filtrer](./images/monitor-queries/filter-icon.png)) pour ouvrir la barre latérale du filtre.

![Onglet Requêtes planifiées avec l’icône de filtre mise en surbrillance.](./images/monitor-queries/filter-queries.png)

Sélectionnez l’une des options suivantes : **[!UICONTROL Planifié]** ou **[!UICONTROL Exécuter une seule fois]** cochez les cases de filtrage des fréquences d’exécution pour filtrer la liste des requêtes.

>[!NOTE]
>
>Toute requête qui a été exécutée mais n’a pas été planifiée est considérée comme [!UICONTROL Exécuter une seule fois].

![Onglet Requêtes planifiées avec la barre latérale de filtrage mise en surbrillance.](./images/monitor-queries/filter-sidebar.png)

Une fois que vous avez activé vos critères de filtre, sélectionnez **[!UICONTROL Masquer les filtres]** pour fermer le panneau de filtrage.

## Détails du planning des exécutions de requête

Sélectionnez un nom de requête pour accéder à la page des détails du planning. Cette vue fournit une liste de toutes les exécutions exécutées dans le cadre de cette requête planifiée. Les informations fournies incluent l’heure de début et de fin, l’état et le jeu de données utilisé.

![La page des détails du planning.](./images/monitor-queries/schedule-details.png)

Ces informations sont fournies dans un tableau à cinq colonnes. Chaque ligne indique l’exécution d’une requête.

| Nom de la colonne | Description |
|---|---|
| Identifiant d’exécution de requête | Identifiant d’exécution de requête pour l’exécution quotidienne. |
| Démarrage de l’exécution de requête | Horodatage de l’exécution de la requête. Il est au format UTC. |
| Fin de l’exécution de requête | Horodatage à l’issue de la requête. Il est au format UTC. |
| État | Etat de la dernière exécution de la requête. Les trois valeurs d’état sont les suivantes : `successful` `failed` ou `in progress`. |
| Jeu de données | Jeu de données impliqué dans l’exécution. |

Les détails de la requête en cours de planification sont visibles dans la [!UICONTROL Propriétés] du panneau. Ce panneau comprend l’ID de requête initial, le type de client, le nom du modèle, la requête SQL et la cadence du planning.

![La page Détails de la planification avec le panneau Propriétés surligné.](./images/monitor-queries/properties-panel.png)

### Détails de l’exécution

Sélectionnez un identifiant d’exécution de requête pour accéder à la page des détails de l’exécution et afficher les informations de la requête.

![L’écran des détails du planning avec un identifiant d’exécution mis en surbrillance.](./images/monitor-queries/navigate-to-run-details.png)

Cette vue fournit des informations sur les exécutions individuelles pour cette requête planifiée et une ventilation plus détaillée de l’état d’exécution. Cette page inclut également les informations sur le client et les détails des erreurs qui ont provoqué l’échec de la requête.

![L’écran de détails de l’exécution avec la section de présentation mise en surbrillance.](./images/monitor-queries/query-run-details.png)

La section d’état de la requête fournit le code d’erreur et le message d’erreur en cas d’échec de la requête.

![L’écran de détails de l’exécution avec la section Erreurs mise en surbrillance.](./images/monitor-queries/failed-query.png)

Vous pouvez copier la requête SQL dans le presse-papiers à partir de cette vue. Sélectionnez l’icône de copie en haut à droite du fragment de code SQL pour copier la requête. Un message contextuel confirme que le code a été copié.

![L’écran de détails de l’exécution avec l’icône de copie SQL mise en surbrillance.](./images/monitor-queries/copy-sql.png)

Sélectionner **[!UICONTROL Requête]** pour revenir à l’écran des détails du planning, ou **[!UICONTROL Requêtes planifiées]** pour revenir au [!UICONTROL Requêtes planifiées] .

![L’écran des détails de l’exécution avec la requête mise en surbrillance.](./images/monitor-queries/return-navigation.png)
