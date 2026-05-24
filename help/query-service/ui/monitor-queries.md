---
title: Surveiller les requêtes planifiées
description: Découvrez comment surveiller les requêtes via l’interface utilisateur du service de requête.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
TQID: https://experienceleague.adobe.com/w0AEwVkNeV5Bls6rqmVrb-67dUePifYsaxg8odpQLQE
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 2340
ht-degree: 20%

---

# Surveiller les requêtes planifiées

Adobe Experience Platform offre une meilleure visibilité du statut de toutes les tâches de requête via l’interface utilisateur. Dans l’onglet [!UICONTROL Scheduled Queries] , vous pouvez désormais trouver des informations importantes sur vos exécutions de requête qui incluent le statut, les détails du planning et les messages/codes d’erreur en cas d’échec. Vous pouvez également vous abonner à des alertes pour les requêtes en fonction de leur statut par le biais de l’interface utilisateur pour l’une de ces requêtes via [!UICONTROL Scheduled Queries] onglet .

## [!UICONTROL Scheduled Queries]

L’onglet [!UICONTROL Scheduled Queries] donne un aperçu de toutes vos requêtes CTAS et ITAS planifiées. Vous trouverez des détails sur l’exécution pour toutes les requêtes planifiées, ainsi que des codes d’erreur et des messages pour toutes les requêtes ayant échoué.

Pour accéder à l’onglet [!UICONTROL Scheduled Queries] , sélectionnez **[!UICONTROL Queries]** dans la barre de navigation de gauche, puis **[!UICONTROL Scheduled Queries]**

![Onglet Requêtes planifiées de l’espace de travail Requêtes avec Requêtes planifiées et Requêtes planifiées en surbrillance.](../images/ui/monitor-queries/scheduled-queries.png)

Le tableau ci-dessous décrit chaque colonne disponible.

>[!NOTE]
>
>L’icône d’abonnement aux alertes (![Icône d’abonnement aux alertes.](/help/images/icons/alert-add.png)) est contenu dans chaque ligne d’une colonne sans titre. Consultez la section [Abonnements aux alertes](#alert-subscription) pour plus d’informations.

| Colonne | Description |
|---|---|
| **[!UICONTROL Name]** | Le champ nom correspond soit au nom du modèle, soit aux premiers caractères de votre requête SQL. Toute requête créée à l’aide de l’interface utilisateur avec le requêteur est nommée dès le départ. Si la requête a été créée via l’API, son nom devient un extrait du SQL initial utilisé pour créer la requête. Pour afficher la liste de toutes les exécutions associées à la requête, sélectionnez un élément dans la colonne [!UICONTROL Name]. Pour plus d’informations, voir la section [détails du planning d’exécution des requêtes](#query-runs). |
| **[!UICONTROL Template]** | Nom du modèle de la requête. Sélectionnez un nom de modèle pour accéder au requêteur. Le modèle de requête est affiché dans le requêteur pour plus de commodité. S’il n’existe aucun nom de modèle, la ligne est marquée d’un trait d’union et il n’est pas possible d’effectuer une redirection vers le requêteur pour afficher la requête. |
| **[!UICONTROL SQL]** | Fragment de la requête SQL. |
| **[!UICONTROL Run frequency]** | La cadence d’exécution de votre requête. Les valeurs disponibles sont `Run once` et `Scheduled`. |
| **[!UICONTROL Created by]** | Nom de la personne qui a créé la requête. |
| **[!UICONTROL Created]** | La date et l’heure de création de la requête, au format UTC. |
| **[!UICONTROL Last run timestamp]** | La date et l’heure les plus récentes auxquelles la requête a été exécutée. Cette colonne met en évidence si une requête a été exécutée conformément à son planning actuel. |
| **[!UICONTROL Last run status]** | Statut de la dernière exécution de la requête. Les valeurs de statut sont les suivantes : `Success`, `Failed`, `In progress` et `No runs`. |
| **[!UICONTROL Schedule Status]** | Statut actuel de la requête planifiée. Il existe six valeurs potentielles : [!UICONTROL Registering], [!UICONTROL Active], [!UICONTROL Inactive], [!UICONTROL Deleted], un trait d’union et [!UICONTROL Quarantined].<ul><li>Le statut **[!UICONTROL Registering]** indique que le système est toujours en train de traiter la création du nouveau planning pour la requête. Notez que vous ne pouvez pas désactiver ni supprimer une requête planifiée pendant son enregistrement.</li><li>Le statut **[!UICONTROL Active]** indique que la requête planifiée n’a **pas encore expiré** sa date et son heure de fin.</li><li>Le statut **[!UICONTROL Inactive]** indique que la requête planifiée a **dépassé** sa date et son heure d’achèvement ou qu’elle a été marquée par un utilisateur comme étant inactive.</li><li>Le statut **[!UICONTROL Deleted]** indique que le planning de la requête a été supprimé.</li><li>Le trait d’union indique que la requête planifiée est une requête unique et non récurrente.</li><li>Le statut **[!UICONTROL Quarantined]** indique que la requête a échoué dix exécutions consécutives et nécessite votre intervention avant que d’autres exécutions ne puissent avoir lieu.</li></ul> |

>[!TIP]
>
>Si vous accédez à l’éditeur de requêtes, vous pouvez sélectionner **[!UICONTROL Queries]** pour revenir à l’onglet [!UICONTROL Templates] .

## Personnaliser les paramètres des tableaux pour les requêtes planifiées {#customize-table}

Vous pouvez ajuster les colonnes de l’onglet [!UICONTROL Scheduled Queries] en fonction de vos besoins. Pour ouvrir la boîte de dialogue des paramètres de [!UICONTROL Customize table] et modifier les colonnes disponibles, sélectionnez l’icône des paramètres (![icône des paramètres A.](/help/images/icons/column-settings.png)) en haut à droite de l’écran.

>[!NOTE]
>
>La colonne [!UICONTROL Created] qui fait référence à la date de création de la planification est masquée par défaut.

![Onglet Requêtes planifiées avec l’icône Personnaliser les paramètres du tableau mise en surbrillance.](../images/ui/monitor-queries/customze-table-settings-icon.png)

Activez/désactivez les cases à cocher appropriées pour supprimer ou ajouter une colonne de tableau. Sélectionnez ensuite **[!UICONTROL Apply]** pour confirmer vos choix.

>[!NOTE]
>
>Toute requête créée via l’interface utilisateur devient un modèle nommé dans le cadre du processus de création. Le nom du modèle est indiqué dans la colonne de modèle. Si la requête a été créée via l’API, la colonne de modèle est vide.

![Boîte de dialogue Personnaliser les paramètres du tableau.](../images/ui/monitor-queries/customize-table-dialog.png)

## Gestion des requêtes planifiées avec des actions intégrées {#inline-actions}

La vue [!UICONTROL Scheduled Queries] propose différentes actions intégrées pour gérer toutes vos requêtes planifiées à partir d’un seul emplacement. Les actions intégrées sont indiquées dans chaque ligne par des points de suspension. Sélectionnez les points de suspension d’une requête planifiée que vous souhaitez gérer pour afficher les options disponibles dans un menu pop-up. Les options disponibles sont les suivantes : [[!UICONTROL Disable schedule]](#disable) ou [!UICONTROL Enable schedule], [[!UICONTROL Delete schedule]](#delete), [[!UICONTROL Subscribe]](#alert-subscription) aux alertes de requêtes et [Activer ou [!UICONTROL Disable quarantine]](#quarantined-queries).

![Onglet Requêtes planifiées avec les points de suspension d’action intégrés et le menu contextuel en surbrillance.](../images/ui/monitor-queries/inline-actions.png)

### Désactiver ou activer une requête planifiée {#disable}

Pour désactiver une requête planifiée, sélectionnez les points de suspension de la requête planifiée que vous souhaitez gérer, puis sélectionnez **[!UICONTROL Disable schedule]** dans les options du menu pop-up. Une boîte de dialogue s’affiche pour confirmer votre action. Sélectionnez **[!UICONTROL Disable]** pour confirmer votre paramètre.

Une fois qu’une requête planifiée est désactivée, vous pouvez activer le planning par le même processus. Sélectionnez les points de suspension, puis sélectionnez **[!UICONTROL Enable schedule]** dans les options disponibles.

>[!NOTE]
>
>Si une requête a été mise en quarantaine, vous devez vérifier le code SQL du modèle avant d’activer son planning. Cela évite le gaspillage d’heures de calcul si la requête de modèle présente toujours des problèmes.

### Supprimer une requête planifiée {#delete}

Pour supprimer une requête planifiée, sélectionnez les points de suspension de la requête planifiée que vous souhaitez gérer, puis sélectionnez **[!UICONTROL Delete schedule]** dans les options du menu pop-up. Une boîte de dialogue s’affiche pour confirmer votre action. Sélectionnez **[!UICONTROL Delete]** pour confirmer votre paramètre.

Une fois qu’une requête planifiée est supprimée, elle n’est **pas** supprimée de la liste des requêtes planifiées. Les actions intégrées fournies par les points de suspension sont supprimées et remplacées par l’icône grisée Ajouter un abonnement aux alertes. Vous ne pouvez pas vous abonner aux alertes pour le planning supprimé. La ligne reste dans l’interface utilisateur pour fournir des informations sur les exécutions effectuées dans le cadre de la requête planifiée.

![L’onglet Requêtes planifiées avec une requête planifiée supprimée et l’icône d’abonnement aux alertes grisée en surbrillance.](../images/ui/monitor-queries/post-delete.png)

Si vous souhaitez planifier des exécutions pour ce modèle de requête, sélectionnez le nom du modèle à partir de la ligne appropriée pour accéder à Query Editor, puis suivez les [instructions pour ajouter un planning à une requête](./query-schedules.md#create-schedule) comme décrit dans la documentation.

### S’abonner aux alertes {#alert-subscription}

Pour vous abonner à des alertes pour les exécutions de requête planifiées, sélectionnez l’icône d’abonnement aux `...` (points de suspension) ou aux alertes (![icône d’abonnement aux alertes.](/help/images/icons/alert-add.png)) pour la requête planifiée que vous souhaitez gérer. Le menu déroulant des actions intégrées s’affiche. Sélectionnez ensuite **[!UICONTROL Subscribe]** dans les options disponibles.

![Espace de travail des requêtes planifiées avec des points de suspension, une icône d’abonnement aux alertes et le menu déroulant des actions intégrées en surbrillance.](../images/ui/monitor-queries/subscribe.png)

La boîte de dialogue [!UICONTROL Alerts] s’ouvre. La boîte de dialogue [!UICONTROL Alerts] vous abonne à la fois aux notifications de l’interface utilisateur et aux alertes par e-mail. Plusieurs options d’abonnement aux alertes sont disponibles : `start`, `success`, `failure`, `quarantine` et `delay`. Cochez la ou les cases correspondantes et sélectionnez **[!UICONTROL Save]** pour vous abonner.

![Boîte de dialogue d’abonnement aux alertes.](../images/ui/monitor-queries/alert-subscription-dialog.png)

Le tableau ci-dessous décrit les types d’alerte de requête pris en charge :

| Type d’alerte | Description |
|---|---|
| `start` | Cette alerte vous avertit lorsqu’une exécution de requête planifiée est lancée ou commence à être traitée. |
| `success` | Cette alerte vous informe lorsqu’une exécution de requête planifiée se termine avec succès, indiquant que la requête s’est exécutée sans erreur. |
| `failed` | Cette alerte se déclenche lorsqu’une exécution de requête planifiée rencontre une erreur ou ne s’exécute pas correctement. Cela vous aide à identifier et à résoudre les problèmes rapidement. |
| `quarantine` | Cette alerte est activée lorsqu’une exécution de requête planifiée est mise en quarantaine. Lorsque des requêtes sont inscrites dans la [fonction de quarantaine](#quarantined-queries), toute requête planifiée qui échoue dix exécutions consécutives est automatiquement mise en état de [!UICONTROL Quarantined]. Elles nécessitent ensuite votre intervention avant que d’autres exécutions ne puissent avoir lieu. |
| `delay` | Cette alerte vous avertit en cas de [ retard dans le résultat de l’exécution d’une requête](#query-run-delay) au-delà d’un seuil spécifié. Vous pouvez définir une heure personnalisée qui déclenche l’alerte lorsque la requête s’exécute pendant cette durée sans terminer ni échouer. |

>[!NOTE]
>
>Pour être averti de la mise en quarantaine des exécutions de requête, vous devez d’abord inscrire les exécutions de requête planifiées à la [fonction de quarantaine](#quarantined-queries).

Pour plus d’informations, consultez la [documentation de l’API d’abonnements aux alertes](../api/alert-subscriptions.md).

### Affichage des détails de la requête {#query-details}

Sélectionnez l’icône d’information (![Icône d’information.](/help/images/icons/info.png)) pour afficher le panneau des détails de la requête. Le panneau de détails contient toutes les informations pertinentes sur la requête au-delà des faits inclus dans le tableau des requêtes planifiées. Les informations supplémentaires incluent l’identifiant de la requête, la date de dernière modification, le code SQL de la requête, l’identifiant du planning et le planning défini actuel.

![Onglet Requêtes planifiées avec l’icône d’informations et le panneau de détails mis en surbrillance.](../images/ui/monitor-queries/details-panel.png)

## Requêtes mises en quarantaine {#quarantined-queries}

>[!NOTE]
>
>L’alerte de quarantaine n’est pas disponible pour les requêtes ad hoc « run-once ». L’alerte de quarantaine s’applique uniquement aux requêtes par lots planifiées (CTAS et ITAS).

Lorsqu’elle est inscrite à la fonction de quarantaine, toute requête planifiée qui échoue dix exécutions consécutives passe automatiquement au statut [!UICONTROL Quarantined]. Une requête avec ce statut devient inactive et ne s’exécute pas à sa cadence planifiée. Il nécessite ensuite votre intervention avant que d’autres exécutions ne puissent avoir lieu. Cela permet de préserver les ressources système, car vous devez examiner et corriger les problèmes liés à votre SQL avant que d’autres exécutions ne se produisent.

Pour activer une requête planifiée pour la fonction de quarantaine, sélectionnez les points de suspension (`...`), puis [!UICONTROL Enable quarantine] dans le menu déroulant qui s’affiche.

![Onglet Requêtes planifiées avec les points de suspension et Activer la quarantaine mis en surbrillance dans le menu déroulant des actions intégrées.](../images/ui/monitor-queries/inline-enable.png)

Les requêtes peuvent également être inscrites à la fonction de quarantaine pendant le processus de création du planning. Pour plus d’informations, consultez la [documentation sur les plannings de requête](./query-schedules.md#quarantine).

## Retard d’exécution de la requête {#query-run-delay}

Gardez le contrôle de vos heures de calcul en définissant des alertes pour les retards de requête. Vous pouvez surveiller les performances des requêtes et recevoir des notifications si le statut d’une requête reste inchangé après une période spécifique. Utilisez l’alerte « [!UICONTROL Query Run Delay] » pour être averti si une requête continue à être traitée après une période spécifique sans être terminée.

Lorsque vous vous [abonnez à des alertes](#alert-subscription) pour les exécutions de requête planifiées, l’une des alertes disponibles est la [!UICONTROL Query Run Delay] . Cette alerte nécessite de définir un seuil pour le temps d’exécution. Vous serez alors informé du retard de traitement.

Pour choisir une durée seuil qui déclenche la notification, saisissez un nombre dans le champ de saisie de texte ou utilisez les flèches vers le haut et vers le bas pour augmenter par incréments d’une minute. Comme le seuil est défini en minutes, la durée maximale d’observation d’un délai d’exécution de requête est de 1 440 minutes (24 heures). La période par défaut d’un délai d’exécution est de 150 minutes.

>[!NOTE]
>
>Une exécution de requête ne peut avoir qu’un seul délai d’exécution. Si vous modifiez le seuil de délai, il est également modifié pour l’utilisateur ou l’utilisatrice abonné à l’alerte et pour l’ensemble de l’organisation.

![Boîte de dialogue Alertes de l’onglet Requêtes planifiées avec le champ d’entrée Délai d’exécution de la requête en surbrillance.](../images/ui/monitor-queries/query-run-delay-input.png)

Consultez la section S’abonner aux alertes pour savoir comment [s’abonner aux alertes [!UICONTROL Query Run Delay]](#alert-subscription).

## Filtrer des requêtes {#filter}

Vous pouvez filtrer les requêtes selon la fréquence d’exécution. Dans l’onglet [!UICONTROL Scheduled Queries] , sélectionnez l’icône de filtre (![Icône Filtrer](/help/images/icons/filter.png)) pour ouvrir la barre latérale du filtre.

![Onglet Requêtes planifiées avec l’icône de filtre mise en surbrillance.](../images/ui/monitor-queries/filter-queries.png)

Pour filtrer la liste des requêtes en fonction de leur fréquence d’exécution, cochez les cases de filtrage des **[!UICONTROL Scheduled]** ou des **[!UICONTROL Run once]** .

>[!NOTE]
>
>Toute requête qui a été exécutée mais n’a pas été planifiée est qualifiée de [!UICONTROL Run once].

![Onglet Requêtes planifiées avec la barre latérale de filtrage mise en surbrillance.](../images/ui/monitor-queries/filter-sidebar.png)

Une fois vos critères de filtre activés, sélectionnez **[!UICONTROL Hide Filters]** pour fermer le panneau de filtrage.

## Détails du planning des exécutions de requête {#query-runs}

Pour ouvrir la page des détails du planning, sélectionnez un nom de requête dans l’onglet [!UICONTROL Scheduled Queries] . Cette vue fournit une liste de toutes les exécutions exécutées dans le cadre de cette requête planifiée. Les informations fournies incluent l’heure de début et de fin, le statut et le jeu de données utilisé.

![Page des détails du planning.](../images/ui/monitor-queries/schedule-details.png)

Ces informations apparaissent dans un tableau à cinq colonnes. Chaque ligne indique l’exécution d’une requête.

| Nom de la colonne | Description |
|---|---|
| **[!UICONTROL Query run ID]** | Identifiant d’exécution de requête pour l’exécution quotidienne. Sélectionnez la **[!UICONTROL Query run ID]** pour accéder à la [!UICONTROL Query run overview]. |
| **[!UICONTROL Query run start]** | Date et heure de l’exécution de la requête. La date et l’heure sont au format UTC. |
| **[!UICONTROL Query run complete]** | Date et heure de la fin de la requête. La date et l’heure sont au format UTC. |
| **[!UICONTROL Status]** | Statut de la dernière exécution de la requête. Les valeurs de statut sont les suivantes : `Success`, `Failed`, `In progress` ou `Quarantined`. |
| **[!UICONTROL Dataset]** | Jeu de données présent dans l’exécution. |

Les détails de la requête en cours de planification sont visibles dans le panneau [!UICONTROL Properties]. Ce panneau comprend l’ID de requête initial, le type de client, le nom du modèle, la requête SQL et la cadence du planning.

![Page de détails du planning avec le panneau Propriétés mis en surbrillance.](../images/ui/monitor-queries/properties-panel.png)

Sélectionnez un ID d’exécution de requête pour accéder à la page des détails de l’exécution et afficher les informations de la requête.

![Écran des détails du planning avec un ID d’exécution mis en surbrillance.](../images/ui/monitor-queries/navigate-to-run-details.png)

## Vue d’ensemble de l’exécution de la requête {#query-run-overview}

La [!UICONTROL Query run overview] fournit des informations sur les exécutions individuelles pour cette requête planifiée et une répartition plus détaillée du statut d’exécution. Cette page inclut également les informations sur le client et les détails de toutes les erreurs qui ont pu entraîner l’échec de la requête.

![Écran de détails de l’exécution avec la section de présentation mise en surbrillance.](../images/ui/monitor-queries/query-run-details.png)

La section du statut de la requête indique le code d’erreur et le message correspondant en cas d’échec de la requête.

![Écran de détails de l’exécution avec la section Erreurs mise en surbrillance.](../images/ui/monitor-queries/failed-query.png)

Vous pouvez copier la requête SQL dans le presse-papiers à partir de cette vue. Pour copier la requête, sélectionnez l’icône de copie en haut à droite du fragment de code SQL. Un message contextuel confirme que le code a été copié.

![Écran des détails de l’exécution avec l’icône de copie SQL mise en surbrillance.](../images/ui/monitor-queries/copy-sql.png)

### Exécuter les détails des requêtes avec un bloc anonyme {#anonymous-block-queries}

Les requêtes qui utilisent des blocs anonymes pour comprendre leurs instructions SQL sont séparées dans leurs sous-requêtes individuelles. La séparation en sous-requêtes vous permet d’examiner individuellement les détails d’exécution de chaque bloc de requête.

>[!NOTE]
>
>Les détails d’exécution d’un bloc anonyme qui utilise la commande DROP ne sont **pas** signalés comme une sous-requête distincte. Des détails d’exécution distincts sont disponibles pour les requêtes CTAS, les requêtes ITAS et les instructions COPY utilisées comme sous-requêtes de bloc anonymes. Les détails d’exécution de la commande DROP ne sont actuellement pas pris en charge.

Les blocs anonymes sont signalés par l’utilisation d’un préfixe `$$` avant la requête. Pour en savoir plus sur les blocs anonymes dans Query Service, consultez le document [Bloc anonyme](../key-concepts/anonymous-block.md).

Les sous-requêtes en bloc anonymes comportent des onglets à gauche du statut d’exécution. Sélectionnez un onglet pour afficher les détails de l’exécution.

![Aperçu de l’exécution de la requête affichant une requête en bloc anonyme. Les onglets de requêtes multiples sont mis en surbrillance.](../images/ui/monitor-queries/anonymous-block-overview.png)

Dans le cas où une requête de bloc anonyme échoue, vous pouvez trouver le code d’erreur pour ce bloc spécifique via cette interface utilisateur.

![Présentation de l’exécution de la requête affichant une requête en bloc anonyme avec le code d’erreur d’un seul bloc mis en surbrillance.](../images/ui/monitor-queries/anonymous-block-failed-query.png)

Sélectionnez **[!UICONTROL Query]** pour revenir à l’écran des détails du planning, ou **[!UICONTROL Scheduled Queries]** pour revenir à l’onglet [!UICONTROL Scheduled Queries] .

![L’écran des détails de l’exécution avec la requête mise en surbrillance.](../images/ui/monitor-queries/return-navigation.png)
