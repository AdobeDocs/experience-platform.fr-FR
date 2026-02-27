---
title: Gestion des sessions Query Service dans Adobe Experience Platform
description: Découvrez comment les administrateurs peuvent afficher, surveiller et mettre fin aux sessions Query Service actives pour libérer de la capacité inactive et maintenir des workflows Data Distiller fiables.
keywords: Experience Platform;Query Service;sessions;gestion de session;Distiller de données;admin
solution: Experience Platform
source-git-commit: 1d2a8ef649c4454da7cf0949192b8b1eb3696e5a
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 1%

---

# Gestion des sessions Query Service

Utilisez ce guide pour gérer les sessions Query Service actives à partir de l’interface utilisateur de Adobe Experience Platform. La gestion des sessions permet aux administrateurs de surveiller les sessions Query Editor simultanées dans les sandbox et de libérer de la capacité lorsque les utilisateurs laissent les sessions ouvertes.

## Autorisations requises pour la gestion des sessions {#permissions}

>[!AVAILABILITY]
>
>La gestion des sessions n’est disponible que pour les organisations disposant de droits Data Distiller.

>[!IMPORTANT]
>
>Cette fonctionnalité est destinée aux administrateurs. Les utilisateurs finaux exécutant des requêtes ne peuvent pas gérer les sessions.

Pour afficher et terminer des sessions, vous devez appartenir à une organisation avec un accès à Data Distiller et disposer de l’autorisation **[!UICONTROL Manage Query Session]**. Les utilisateurs ne disposant pas des autorisations requises peuvent accéder à Query Service, mais ne peuvent pas afficher ni gérer les sessions actives.

## Afficher les sessions actives {#view-active-sessions}

Les administrateurs peuvent afficher toutes les sessions Query Service actives dans les sandbox de votre organisation. Dans Experience Platform, sélectionnez **[!UICONTROL Queries]** dans le volet de navigation de gauche pour ouvrir l’espace de travail de Query Service, puis sélectionnez l’onglet **[!UICONTROL Admin]** pour accéder à la gestion des sessions.

![Espace de travail de Query Service avec l’onglet Admin sélectionné. Le tableau Gestion des sessions s’affiche et répertorie les sessions actives et inactives sur plusieurs sandbox de votre organisation.](../images/ui/session-management/session-management-admin-tab.png)

Le tableau de gestion des sessions se met automatiquement à jour en temps réel et répertorie toutes les sessions qui consomment actuellement de la capacité de session simultanée de Query Service affectée à votre organisation. Chaque ligne représente une seule session ouverte dans le Query Editor.

## Statut de la session et temps d’inactivité {#session-status}

Le tableau de session fournit des informations pour vous aider à décider si une session peut se terminer en toute sécurité.

| Colonne | Description |
| --- | --- |
| Identifiant utilisateur | Adobe ID de l’utilisateur propriétaire de la session |
| Nom de l’utilisateur ou de l’utilisatrice | Nom associé à l’Adobe ID |
| Sandbox | Indique le sandbox dans lequel la session est en cours d’exécution |
| Statut de la session | Indique si la session est **[!UICONTROL Active]** ou **[!UICONTROL Inactive]** |
| Durée d’inactivité | Affiche la durée d’ouverture de la session sans interaction |
| Durée restante de la session | Indique la durée pendant laquelle la session peut rester ouverte avant expiration automatique |

### Statut de la session

**[!UICONTROL Inactive]** indique que l’utilisateur n’exécute pas activement une requête ; ces sessions peuvent être terminées. **[!UICONTROL Active]** indique qu’une requête est en cours d’exécution ; le contrôle **[!UICONTROL End session]** n’est pas disponible tant que l’exécution de la requête n’est pas terminée.

### Durée d’inactivité et durée restante de la session

Le Temps inactif indique la durée d’ouverture d’une session sans interaction de l’utilisateur. La durée restante de la session indique combien de temps la session peut rester ouverte avant d’être automatiquement fermée par le système. Les sessions expirent automatiquement après la durée maximale autorisée (deux heures d’inactivité). Cette durée est définie par le système et ne peut pas être configurée.

## Terminer les sessions inactives {#end-idle-sessions}

Vous pouvez mettre fin aux sessions inactives afin de libérer de la capacité de session simultanée pour d’autres utilisateurs. Envisagez de terminer les sessions avec un temps d’inactivité élevé lorsque les utilisateurs ne travaillent plus activement.

Dans le tableau Gestion des sessions , sélectionnez **[!UICONTROL End session]** pour choisir la session inactive à terminer.

![Tableau de gestion de session présentant une session inactive avec la fin de session mise en surbrillance.](../images/ui/session-management/end-session.png)

Une boîte de dialogue de confirmation s’affiche pour empêcher toute interruption accidentelle. Sélectionnez **[!UICONTROL End session]** dans la boîte de dialogue pour confirmer l’action.

![La boîte de dialogue de confirmation de fin de session affiche un message d’avertissement et met fin à la session en surbrillance.](../images/ui/session-management/end-session-confirmation-dialog.png)

Une fois la session terminée, elle est supprimée du tableau, la capacité est immédiatement disponible et l’action est enregistrée pour contrôle.

>[!NOTE]
>
>Les sessions avec le statut **[!UICONTROL Active]** ne peuvent pas être terminées. Cette protection empêche l’interruption des charges de travail en cours.

## Comportement de la session après l’arrêt {#session-behavior-after-termination}

Lorsqu’un administrateur met fin à une session, le code de l’utilisateur concerné reste dans l’éditeur sans perdre de travail. Si l’utilisateur ou l’utilisatrice tente d’exécuter une requête après la terminaison, le système détecte la session terminée, rétablit automatiquement la connexion et conserve le contenu de Query Editor intact.

Ce comportement permet de s’assurer que les utilisateurs ne perdent pas le travail écrit dans l’éditeur et peuvent continuer une fois qu’une nouvelle session est établie.

## Journaux d’audit pour la gestion des sessions {#audit-logs}

Le système consigne les actions de gestion de session pour offrir visibilité et responsabilité. Les journaux d’audit enregistrent l’ID de session, l’utilisateur dont la session a pris fin, l’administrateur qui a exécuté l’action et l’heure de l’action.

Utilisez les journaux d’audit pour consulter l’historique de fermeture de session et rechercher les déconnexions inattendues.

Pour plus d’informations sur l’affichage des journaux d’audit, consultez le [guide du journal d’audit de Query Service](../data-governance/audit-log-guide.md).

## Étapes suivantes {#next-steps}

Tenez compte des points suivants pour étendre votre utilisation de Query Service et de Data Distiller :

* [Découvrez comment les utilisateurs créent et exécutent des requêtes dans le guide d’utilisation de Query Editor](user-guide.md)
* [Surveillez les charges de travail planifiées en utilisant la documentation de surveillance des requêtes planifiées](monitor-queries.md)

