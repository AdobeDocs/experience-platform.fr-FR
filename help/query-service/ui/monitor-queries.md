---
title: Surveillance des requêtes planifiées
description: Découvrez comment surveiller les requêtes via l’interface utilisateur de Query Service.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: 5e6fa112ccca7405c3dfd0653d3d6cad8b9ed2af
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 74%

---

# Surveillance des requêtes planifiées

Adobe Experience Platform offre une meilleure visibilité du statut de toutes les tâches de requête via l’interface utilisateur. Depuis l’onglet [!UICONTROL Requêtes planifiées], vous pouvez désormais trouver des informations importantes sur vos exécutions de requêtes qui incluent le statut, les détails de la planification et les messages/codes d’erreur en cas d’échec. Vous pouvez également vous abonner à des alertes pour les requêtes en fonction de leur statut par le biais de l’interface utilisateur pour l’une de ces requêtes via l’onglet [!UICONTROL Requêtes planifiées].

## [!UICONTROL Requêtes planifiées]

Le [!UICONTROL Requêtes planifiées] fournit un aperçu de toutes vos requêtes CTAS et ITAS planifiées. Vous trouverez des détails sur l’exécution pour toutes les requêtes planifiées, ainsi que des codes d’erreur et des messages pour toutes les requêtes ayant échoué.

Pour accéder à l’onglet [!UICONTROL Requêtes planifiées], sélectionnez **[!UICONTROL Requêtes]** dans la barre de navigation de gauche, suivi de **[!UICONTROL Requêtes planifiées]**

![L’onglet Requêtes planifiées de l’espace de travail Requêtes.](../images/ui/monitor-queries/scheduled-queries.png)

Le tableau ci-dessous décrit chaque colonne disponible.

>[!NOTE]
>
>L’icône d’abonnement aux alertes apparaît dans chaque ligne dans une colonne sans titre. Consultez la section [Abonnements aux alertes](#alert-subscription) pour plus d’informations.

| Colonne | Description |
|---|---|
| **[!UICONTROL Nom]** | Le champ nom correspond soit au nom du modèle, soit aux premiers caractères de votre requête SQL. Toute requête créée à l’aide de l’interface utilisateur avec le Query Editor est nommée dès le départ. Si la requête a été créée via l’API, son nom devient un fragment de code SQL initial utilisé pour créer la requête. Sélectionnez un élément dans la [!UICONTROL Nom] pour voir la liste de toutes les exécutions associées à la requête. Pour plus d’informations, voir [détails du planning des exécutions de requête](#query-runs) . |
| **[!UICONTROL Modèle]** | Nom du modèle de la requête. Sélectionnez un nom de modèle pour accéder à l’éditeur de requêtes. Le modèle de requête est affiché dans l’éditeur de requêtes pour plus de commodité. S’il n’existe aucun nom de modèle, la ligne est marquée d’un trait d’union et il n’est pas possible d’effectuer une redirection vers l’éditeur de requêtes pour afficher la requête. |
| **[!UICONTROL SQL]** | Fragment de la requête SQL. |
| **[!UICONTROL Fréquence d’exécution]** | Il s’agit de la cadence d’exécution de votre requête. Les valeurs disponibles sont `Run once` et `Scheduled`. Les requêtes peuvent être filtrées en fonction de leur fréquence d’exécution. |
| **[!UICONTROL Créé par]** | Nom de la personne qui a créé la requête. |
| **[!UICONTROL Créé]** | La date et l’heure de création de la requête, au format UTC. |
| **[!UICONTROL La date et l’heure de la dernière exécution]** | La date et l’heure les plus récentes auxquelles la requête a été exécutée. Cette colonne met en évidence si une requête a été exécutée conformément à son planning actuel. |
| **[!UICONTROL Statut de la dernière exécution]** | Statut de la dernière exécution de la requête. Les valeurs d’état sont les suivantes : `Success`, `Failed`, `In progress`, et `No runs`. |

>[!TIP]
>
>Si vous accédez à l’éditeur de requêtes, vous pouvez sélectionner **[!UICONTROL Requêtes]** pour revenir à l’onglet [!UICONTROL Modèles].

### Personnaliser les paramètres des tableaux pour les requêtes planifiées

Vous pouvez ajuster les colonnes de l’onglet [!UICONTROL Requêtes planifiées] à vos besoins. Sélectionnez l’icône des paramètres (![A icône des paramètres.](../images/ui/monitor-queries/settings-icon.png)) pour ouvrir la boîte de dialogue paramètres [!UICONTROL Personnalisation du tableau] et modifier les colonnes disponibles.

![Icône Personnaliser les paramètres du tableau.](../images/ui/monitor-queries/customze-table-settings-icon.png)

Activez/désactivez les cases à cocher appropriées pour supprimer ou ajouter une colonne de tableau. Ensuite, sélectionnez **[!UICONTROL Appliquer]** pour confirmer vos choix.

>[!NOTE]
>
>Toute requête créée via l’interface utilisateur devient un modèle nommé dans le cadre du processus de création. Le nom du modèle est indiqué dans la colonne de modèle. Si la requête a été créée via l’API, la colonne de modèle est vide.

![Boîte de dialogue Personnaliser les paramètres du tableau.](../images/ui/monitor-queries/customize-table-dialog.png)

### S’abonner aux alertes {#alert-subscription}

Vous pouvez vous abonner à des alertes à partir de l’onglet [!UICONTROL Requêtes planifiées]. Sélectionnez l’icône de notification d’alerte (![Icône d’alerte.](../images/ui/monitor-queries/alerts-icon.png)) à côté d’un nom de requête pour ouvrir la boîte de dialogue [!UICONTROL Alertes]. La boîte de dialogue [!UICONTROL Alertes] permet de s’abonner aux notifications de l’interface utilisateur et aux alertes envoyées par e-mail. Les alertes reposent sur le statut de la requête. Trois options sont disponibles : `start`, `success` et `failure`. Cochez la ou les cases correspondantes et sélectionnez **[!UICONTROL Enregistrer]** pour vous abonner.

![Boîte de dialogue d’abonnement aux alertes.](../images/ui/monitor-queries/alert-subscription-dialog.png)

Voir [documentation de l’API d’abonnements des alertes](../api/alert-subscriptions.md) pour plus d’informations.

### Filtrer des requêtes {#filter}

Vous pouvez filtrer les requêtes selon la fréquence d’exécution. Dans l’onglet [!UICONTROL Requêtes planifiées], sélectionnez l’icône de filtre (![Icône Filtrer](../images/ui/monitor-queries/filter-icon.png)) pour ouvrir la barre latérale du filtre.

![Onglet Requêtes planifiées avec l’icône de filtre mise en surbrillance.](../images/ui/monitor-queries/filter-queries.png)

Sélectionnez l’une des cases de filtrage des fréquences d’exécution suivantes : **[!UICONTROL Planifié]** ou **[!UICONTROL Exécuter une seule fois]** pour filtrer la liste des requêtes.

>[!NOTE]
>
>Toute requête qui a été exécutée mais n’a pas été planifiée est qualifiée selon l’option [!UICONTROL Exécuter une fois].

![Onglet Requêtes planifiées avec la barre latérale de filtrage mise en surbrillance.](../images/ui/monitor-queries/filter-sidebar.png)

Une fois que vos critères de filtre sont activés, sélectionnez **[!UICONTROL Masquer les filtres]** pour fermer le panneau de filtrage.

## Détails du planning des exécutions de requête {#query-runs}

Sélectionnez un nom de requête pour accéder à la page des détails du planning. Cette vue fournit une liste de toutes les exécutions exécutées dans le cadre de cette requête planifiée. Les informations fournies incluent l’heure de début et de fin, le statut et le jeu de données utilisé.

![Page des détails du planning.](../images/ui/monitor-queries/schedule-details.png)

Ces informations apparaissent dans un tableau à cinq colonnes. Chaque ligne indique l’exécution d’une requête.

| Nom de la colonne | Description |
|---|---|
| **[!UICONTROL ID d’exécution de requête]** | ID pour l’exécution de requête quotidienne. Sélectionnez la **[!UICONTROL Identifiant d’exécution de requête]** pour accéder au [!UICONTROL Présentation de l’exécution de requête]. |
| **[!UICONTROL Démarrage de l’exécution de requête]** | Date et heure de l’exécution de la requête. Affichée au format UTC. |
| **[!UICONTROL Fin de l’exécution de requête]** | Date et heure de la fin de la requête. Affichée au format UTC. |
| **[!UICONTROL Statut]** | Statut de la dernière exécution de la requête. Les trois valeurs de statut sont les suivantes : `successful` `failed` ou `in progress`. |
| **[!UICONTROL Jeu de données]** | Jeu de données présent dans l’exécution. |

Les détails de la requête en cours de planification sont visibles dans le panneau [!UICONTROL Propriétés]. Ce panneau comprend l’ID de requête initial, le type de client, le nom du modèle, la requête SQL et la cadence du planning.

![Page de détails du planning avec le panneau Propriétés mis en surbrillance.](../images/ui/monitor-queries/properties-panel.png)

Sélectionnez un ID d’exécution de requête pour accéder à la page des détails de l’exécution et afficher les informations de la requête.

![Écran des détails du planning avec un ID d’exécution mis en surbrillance.](../images/ui/monitor-queries/navigate-to-run-details.png)

## Présentation de l’exécution de requête {#query-run-overview}

Le [!UICONTROL Présentation de l’exécution de requête] fournit des informations sur les exécutions individuelles pour cette requête planifiée et une ventilation plus détaillée de l’état d’exécution. Cette page contient également les informations sur le client et les détails des erreurs qui ont pu entraîner l’échec de la requête.

![Écran de détails de l’exécution avec la section de présentation mise en surbrillance.](../images/ui/monitor-queries/query-run-details.png)

La section du statut de la requête indique le code d’erreur et le message correspondant en cas d’échec de la requête.

![Écran de détails de l’exécution avec la section Erreurs mise en surbrillance.](../images/ui/monitor-queries/failed-query.png)

Vous pouvez copier la requête SQL dans le presse-papiers à partir de cette vue. Sélectionnez l’icône de copie en haut à droite du fragment de code SQL pour copier la requête. Un message contextuel confirme que le code a été copié.

![Écran des détails de l’exécution avec l’icône de copie SQL mise en surbrillance.](../images/ui/monitor-queries/copy-sql.png)

### Exécution des détails des requêtes avec bloc anonyme {#anonymous-block-queries}

Les requêtes qui utilisent des blocs anonymes pour comprendre leurs instructions SQL sont séparées dans leurs requêtes individuelles. Vous pouvez ainsi inspecter individuellement les détails de l’exécution pour chaque bloc de requête.

Les blocs anonymes sont identifiés à l’aide d’une `$$` avant la requête. Voir [document de bloc anonyme](../essential-concepts/anonymous-block.md) pour en savoir plus sur les blocs anonymes dans query service.

Les requêtes de bloc anonymes ont des onglets à gauche de l’état d’exécution. Sélectionnez un onglet pour afficher les détails de l’exécution.

![La vue d&#39;ensemble Exécution de la requête affiche une requête bloquée anonyme. Les onglets de requête multiples sont mis en surbrillance.](../images/ui/monitor-queries/anonymous-block-overview.png)

En cas d’échec d’une requête bloquée anonyme, vous pouvez trouver le code d’erreur correspondant à ce bloc spécifique via cette interface utilisateur.

![La vue d&#39;ensemble Exécution de la requête affiche une requête bloquée anonyme avec le code d&#39;erreur pour un seul bloc en surbrillance.](../images/ui/monitor-queries/anonymous-block-failed-query.png)

Sélectionnez **[!UICONTROL Requête]** pour revenir à l’écran des détails du planning, ou **[!UICONTROL Requêtes planifiées]** pour revenir à l’onglet [!UICONTROL Requêtes planifiées].

![L’écran des détails de l’exécution avec la requête mise en surbrillance.](../images/ui/monitor-queries/return-navigation.png)
