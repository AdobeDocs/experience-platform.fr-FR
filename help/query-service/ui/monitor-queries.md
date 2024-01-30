---
title: Surveillance des requêtes planifiées
description: Découvrez comment surveiller les requêtes via l’interface utilisateur de Query Service.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: 7e0259f8807e96118dbcd1085d8b3b3186fc8317
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 37%

---

# Surveiller les requêtes planifiées

Adobe Experience Platform offre une meilleure visibilité du statut de toutes les tâches de requête via l’interface utilisateur. Dans la [!UICONTROL Requêtes planifiées] , vous pouvez maintenant trouver des informations importantes sur les exécutions de votre requête qui incluent l’état, les détails de planification et les messages/codes d’erreur en cas d’échec. Vous pouvez également vous abonner à des alertes pour les requêtes en fonction de leur statut par le biais de l’interface utilisateur pour l’une de ces requêtes via l’onglet [!UICONTROL Requêtes planifiées].

## [!UICONTROL Requêtes planifiées]

La variable [!UICONTROL Requêtes planifiées] fournit un aperçu de toutes vos requêtes CTAS et ITAS planifiées. Vous trouverez des détails sur l’exécution pour toutes les requêtes planifiées, ainsi que des codes d’erreur et des messages pour toutes les requêtes ayant échoué.

Pour accéder à l’onglet [!UICONTROL Requêtes planifiées], sélectionnez **[!UICONTROL Requêtes]** dans la barre de navigation de gauche, suivi de **[!UICONTROL Requêtes planifiées]**

![Onglet Requêtes planifiées de l’espace de travail Requêtes avec surbrillance Requêtes planifiées et Requêtes.](../images/ui/monitor-queries/scheduled-queries.png)

Le tableau ci-dessous décrit chaque colonne disponible.

>[!NOTE]
>
>L’icône d’abonnement aux alertes apparaît dans chaque ligne dans une colonne sans titre. Consultez la section [Abonnements aux alertes](#alert-subscription) pour plus d’informations.

| Colonne | Description |
|---|---|
| **[!UICONTROL Nom]** | Le champ nom correspond soit au nom du modèle, soit aux premiers caractères de votre requête SQL. Toute requête créée à l’aide de l’interface utilisateur avec le Query Editor est nommée dès le départ. Si la requête a été créée via l’API, son nom devient un fragment de code SQL initial utilisé pour créer la requête. Pour afficher la liste de toutes les exécutions associées à la requête, sélectionnez un élément dans la [!UICONTROL Nom] colonne . Pour plus d’informations, voir [détails du planning des exécutions de requête](#query-runs) . |
| **[!UICONTROL Modèle]** | Nom du modèle de la requête. Sélectionnez un nom de modèle pour accéder à l’éditeur de requêtes. Le modèle de requête est affiché dans l’éditeur de requêtes pour plus de commodité. S’il n’existe aucun nom de modèle, la ligne est marquée d’un trait d’union et il n’est pas possible d’effectuer une redirection vers l’éditeur de requêtes pour afficher la requête. |
| **[!UICONTROL SQL]** | Fragment de la requête SQL. |
| **[!UICONTROL Fréquence d’exécution]** | La cadence d’exécution de votre requête. Les valeurs disponibles sont `Run once` et `Scheduled`. Les requêtes peuvent être filtrées en fonction de leur fréquence d’exécution. |
| **[!UICONTROL Créé par]** | Nom de la personne qui a créé la requête. |
| **[!UICONTROL Créé]** | La date et l’heure de création de la requête, au format UTC. |
| **[!UICONTROL Horodatage de la dernière exécution]** | La date et l’heure les plus récentes auxquelles la requête a été exécutée. Cette colonne met en évidence si une requête a été exécutée conformément à son planning actuel. |
| **[!UICONTROL État de la dernière exécution]** | Statut de la dernière exécution de la requête. Les valeurs d’état sont les suivantes : `Success`, `Failed`, `In progress`, et `No runs`. |
| **[!UICONTROL État de la planification]** | État actuel de la requête planifiée. Il existe cinq valeurs potentielles, [!UICONTROL Enregistrement], [!UICONTROL Actif], [!UICONTROL Inactif], [!UICONTROL Supprimé]et un trait d’union. <ul><li>Le trait d’union indique que la requête planifiée est une requête ponctuelle non récurrente.</li><li>La variable [!UICONTROL Enregistrement] Le statut indique que le système traite toujours la création du nouveau planning pour la requête. Remarque : vous ne pouvez pas désactiver ou supprimer une requête planifiée lors de son enregistrement.</li><li>La variable [!UICONTROL Actif] le statut indique que la requête planifiée possède **pas encore passé** date et heure d’achèvement.</li><li>La variable [!UICONTROL Inactif] le statut indique que la requête planifiée possède **transmis** date et heure d’achèvement.</li><li>La variable [!UICONTROL Supprimé] Le statut indique que le planning de requête a été supprimé.</li></ul> |

>[!TIP]
>
>Si vous accédez à l’éditeur de requêtes, vous pouvez sélectionner **[!UICONTROL Requêtes]** pour revenir à l’onglet [!UICONTROL Modèles].

## Personnaliser les paramètres des tableaux pour les requêtes planifiées {#customize-table}

Vous pouvez ajuster les colonnes de l’onglet [!UICONTROL Requêtes planifiées] à vos besoins. Pour ouvrir la [!UICONTROL Personnalisation du tableau] la boîte de dialogue paramètres et modifiez les colonnes disponibles, sélectionnez l’icône paramètres (![Icône Paramètres .](../images/ui/monitor-queries/settings-icon.png)) en haut à droite de l’écran.

>[!NOTE]
>
>La variable [!UICONTROL Créé] qui fait référence à la date de création du planning est masquée par défaut.

![L’onglet Requêtes planifiées avec l’icône Personnaliser les paramètres du tableau en surbrillance.](../images/ui/monitor-queries/customze-table-settings-icon.png)

Activez/désactivez les cases à cocher appropriées pour supprimer ou ajouter une colonne de tableau. Ensuite, sélectionnez **[!UICONTROL Appliquer]** pour confirmer vos choix.

>[!NOTE]
>
>Toute requête créée via l’interface utilisateur devient un modèle nommé dans le cadre du processus de création. Le nom du modèle est indiqué dans la colonne de modèle. Si la requête a été créée via l’API, la colonne de modèle est vide.

![Boîte de dialogue Personnaliser les paramètres du tableau.](../images/ui/monitor-queries/customize-table-dialog.png)

## Gestion des requêtes planifiées avec des actions intégrées {#inline-actions}

La variable [!UICONTROL Requêtes planifiées] view propose diverses actions intégrées pour gérer toutes vos requêtes planifiées à partir d’un seul emplacement. Les actions intégrées sont indiquées par des points de suspension dans chaque ligne. Sélectionnez les points de suspension d’une requête planifiée que vous souhaitez gérer pour afficher les options disponibles dans un menu contextuel. Les options disponibles incluent [[!UICONTROL Désactiver le planning]](#disable) ou [!UICONTROL Activation du planning], [[!UICONTROL Supprimer le planning]](#delete), et [[!UICONTROL Abonner]](#alert-subscription) pour interroger des alertes.

![L’onglet Requêtes planifiées avec les ellipses d’action intégrées et le menu contextuel en surbrillance.](../images/ui/monitor-queries/disable-inline.png)

### Désactivation ou activation d’une requête planifiée {#disable}

Pour désactiver une requête planifiée, sélectionnez les points de suspension d’une requête planifiée que vous souhaitez gérer, puis sélectionnez **[!UICONTROL Désactiver le planning]** dans les options du menu contextuel. Une boîte de dialogue s’affiche pour confirmer votre action. Sélectionner **[!UICONTROL Désactiver]** pour confirmer votre paramètre.

Une fois qu’une requête planifiée est désactivée, vous pouvez activer le planning par le biais du même processus. Sélectionnez les points de suspension, puis sélectionnez **[!UICONTROL Activation du planning]** dans les options disponibles.

### Suppression d’une requête planifiée {#delete}

Pour supprimer une requête planifiée, sélectionnez les points de suspension d’une requête planifiée que vous souhaitez gérer, puis sélectionnez **[!UICONTROL Supprimer le planning]** dans les options du menu contextuel. Une boîte de dialogue s’affiche pour confirmer votre action. Sélectionner **[!UICONTROL Supprimer]** pour confirmer votre paramètre.

Une fois une requête planifiée supprimée, elle est **not** supprimé de la liste des requêtes planifiées. Les actions intégrées fournies par les ellipses sont supprimées et remplacées par l’icône d’alerte d’ajout grisé. Vous ne pouvez pas vous abonner à des alertes pour le planning supprimé. La ligne reste dans l’interface utilisateur pour fournir des informations sur les exécutions effectuées dans le cadre de la requête planifiée.

![L’onglet Requêtes planifiées avec une requête planifiée supprimée et l’icône d’alerte grisée mise en surbrillance.](../images/ui/monitor-queries/post-delete.png)

Si vous souhaitez planifier des exécutions pour ce modèle de requête, sélectionnez le nom du modèle dans la ligne appropriée pour accéder à l’éditeur de requêtes, puis suivez le [instructions pour ajouter un planning à une requête](./query-schedules.md#create-schedule) comme décrit dans la documentation.

### S’abonner aux alertes {#alert-subscription}

Pour vous abonner aux alertes pour les exécutions de requête planifiées, sélectionnez les points de suspension d’une requête planifiée à gérer, puis sélectionnez **[!UICONTROL Abonner]** dans les options du menu contextuel.

La variable [!UICONTROL Alertes] s’ouvre. La variable [!UICONTROL Alertes] vous abonne aux notifications de l’interface utilisateur et aux alertes par courrier électronique. Les alertes reposent sur le statut de la requête. Trois options sont disponibles : `start`, `success` et `failure`. Cochez la ou les cases correspondantes et sélectionnez **[!UICONTROL Enregistrer]** pour vous abonner. Vous pouvez vous abonner à des alertes tant qu’elles n’ont pas de [!UICONTROL Horodatage de la dernière exécution] .

![Boîte de dialogue d’abonnement aux alertes.](../images/ui/monitor-queries/alert-subscription-dialog.png)

Voir [documentation de l’API d’abonnements des alertes](../api/alert-subscriptions.md) pour plus d’informations.

### Afficher les détails de la requête {#query-details}

Sélectionnez l’icône d’information (![Icône d’informations.](../images/ui/monitor-queries/information-icon.png)) pour afficher le panneau des détails de la requête. Le panneau Détails contient toutes les informations pertinentes sur la requête, au-delà des faits inclus dans le tableau des requêtes planifiées. Les informations supplémentaires incluent l’identifiant de la requête, la date de dernière modification, le code SQL de la requête, l’identifiant de planification et le planning défini actuel.

![L’onglet Requêtes planifiées avec l’icône d’informations et le panneau Détails surligné.](../images/ui/monitor-queries/details-panel.png)

## Filtrer des requêtes {#filter}

Vous pouvez filtrer les requêtes selon la fréquence d’exécution. Dans l’onglet [!UICONTROL Requêtes planifiées], sélectionnez l’icône de filtre (![Icône Filtrer](../images/ui/monitor-queries/filter-icon.png)) pour ouvrir la barre latérale du filtre.

![Onglet Requêtes planifiées avec l’icône de filtre mise en surbrillance.](../images/ui/monitor-queries/filter-queries.png)

Pour filtrer la liste des requêtes selon leur fréquence d’exécution, sélectionnez l’une des options suivantes : **[!UICONTROL Planifié]** ou **[!UICONTROL Exécuter une seule fois]** des cases à cocher de filtre.

>[!NOTE]
>
>Toute requête qui a été exécutée mais n’a pas été planifiée est qualifiée selon l’option [!UICONTROL Exécuter une fois].

![Onglet Requêtes planifiées avec la barre latérale de filtrage mise en surbrillance.](../images/ui/monitor-queries/filter-sidebar.png)

Une fois que vos critères de filtre sont activés, sélectionnez **[!UICONTROL Masquer les filtres]** pour fermer le panneau de filtrage.

## Détails du planning des exécutions de requête {#query-runs}

Pour ouvrir la page des détails du planning, sélectionnez un nom de requête dans le [!UICONTROL Requêtes planifiées] . Cette vue fournit une liste de toutes les exécutions exécutées dans le cadre de cette requête planifiée. Les informations fournies incluent l’heure de début et de fin, le statut et le jeu de données utilisé.

![Page des détails du planning.](../images/ui/monitor-queries/schedule-details.png)

Ces informations apparaissent dans un tableau à cinq colonnes. Chaque ligne indique l’exécution d’une requête.

| Nom de la colonne | Description |
|---|---|
| **[!UICONTROL Identifiant d’exécution de requête]** | Identifiant d’exécution de requête pour l’exécution quotidienne. Sélectionnez la variable **[!UICONTROL Identifiant d’exécution de requête]** pour accéder au [!UICONTROL Présentation de l’exécution de requête]. |
| **[!UICONTROL Démarrage de l’exécution de requête]** | Date et heure de l’exécution de la requête. L’horodatage est au format UTC. |
| **[!UICONTROL Fin de l’exécution de requête]** | Date et heure de la fin de la requête. L’horodatage est au format UTC. |
| **[!UICONTROL Statut]** | Statut de la dernière exécution de la requête. Les trois valeurs de statut sont les suivantes : `successful` `failed` ou `in progress`. |
| **[!UICONTROL Jeu de données]** | Jeu de données présent dans l’exécution. |

Les détails de la requête en cours de planification sont visibles dans le panneau [!UICONTROL Propriétés]. Ce panneau comprend l’ID de requête initial, le type de client, le nom du modèle, la requête SQL et la cadence du planning.

![Page de détails du planning avec le panneau Propriétés mis en surbrillance.](../images/ui/monitor-queries/properties-panel.png)

Sélectionnez un ID d’exécution de requête pour accéder à la page des détails de l’exécution et afficher les informations de la requête.

![Écran des détails du planning avec un ID d’exécution mis en surbrillance.](../images/ui/monitor-queries/navigate-to-run-details.png)

## Présentation de l’exécution de requête {#query-run-overview}

La variable [!UICONTROL Présentation de l’exécution de requête] fournit des informations sur les exécutions individuelles pour cette requête planifiée et une ventilation plus détaillée de l’état d’exécution. Cette page contient également les informations sur le client et les détails des erreurs qui ont pu entraîner l’échec de la requête.

![Écran de détails de l’exécution avec la section de présentation mise en surbrillance.](../images/ui/monitor-queries/query-run-details.png)

La section du statut de la requête indique le code d’erreur et le message correspondant en cas d’échec de la requête.

![Écran de détails de l’exécution avec la section Erreurs mise en surbrillance.](../images/ui/monitor-queries/failed-query.png)

Vous pouvez copier la requête SQL dans le presse-papiers à partir de cette vue. Pour copier la requête, sélectionnez l’icône de copie en haut à droite du fragment de code SQL. Un message contextuel confirme que le code a été copié.

![Écran des détails de l’exécution avec l’icône de copie SQL mise en surbrillance.](../images/ui/monitor-queries/copy-sql.png)

### Exécution des détails des requêtes avec bloc anonyme {#anonymous-block-queries}

Les requêtes qui utilisent des blocs anonymes pour comprendre leurs instructions SQL sont séparées dans leurs sous-requêtes individuelles. La séparation en sous-requêtes vous permet d’examiner individuellement les détails d’exécution de chaque bloc de requête.

>[!NOTE]
>
>Les détails d&#39;exécution d&#39;un bloc anonyme qui utilise la commande DROP sont **not** être signalée en tant que sous-requête distincte. Des détails d’exécution distincts sont disponibles pour les requêtes CTAS, les requêtes ITAS et les instructions COPY utilisées comme sous-requêtes de bloc anonymes. Les détails d’exécution de la commande DROP ne sont actuellement pas pris en charge.

Les blocs anonymes sont identifiés à l’aide d’une `$$` avant la requête. Pour en savoir plus sur les blocs anonymes dans le service de requête, voir la section [document de bloc anonyme](../key-concepts/anonymous-block.md).

Les sous-requêtes de bloc anonymes ont des onglets à gauche de l’état d’exécution. Sélectionnez un onglet pour afficher les détails de l’exécution.

![La vue d&#39;ensemble Exécution de la requête affiche une requête bloquée anonyme. Les onglets de requête multiples sont mis en surbrillance.](../images/ui/monitor-queries/anonymous-block-overview.png)

En cas d’échec d’une requête bloquée anonyme, vous pouvez trouver le code d’erreur correspondant à ce bloc spécifique via cette interface utilisateur.

![La vue d&#39;ensemble Exécution de la requête affiche une requête bloquée anonyme avec le code d&#39;erreur pour un seul bloc en surbrillance.](../images/ui/monitor-queries/anonymous-block-failed-query.png)

Sélectionnez **[!UICONTROL Requête]** pour revenir à l’écran des détails du planning, ou **[!UICONTROL Requêtes planifiées]** pour revenir à l’onglet [!UICONTROL Requêtes planifiées].

![L’écran des détails de l’exécution avec la requête mise en surbrillance.](../images/ui/monitor-queries/return-navigation.png)
