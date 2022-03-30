---
description: Utilisez la variable [!UICONTROL Enrichissement du profil] tableau de bord pour comprendre si les tâches d’enrichissement de profil ont été exécutées et terminées avec succès et pour afficher les mesures de base afin d’évaluer l’efficacité des enrichissements.
solution: Experience Platform
title: Surveillance des tâches d’enrichissement de profil
type: Tutorial
source-git-commit: f3389ef2c2bd9ff52ecde2a4f5fd55e5b86783fc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Surveillance des tâches d’enrichissement de profil dans l’interface utilisateur

Utilisez la variable [!UICONTROL Enrichissement du profil] tableau de bord pour comprendre si les tâches d’enrichissement de profil ont été exécutées et terminées avec succès et pour afficher les mesures de base afin d’évaluer l’efficacité des enrichissements.

Dans le [Interface utilisateur de Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Surveillance]** dans le volet de navigation de gauche pour accéder à la fonction [!UICONTROL Surveillance] tableau de bord. Dans le sélecteur de mode, sélectionnez **Flux B2B** pour afficher les éléments du tableau de bord spécifiques à [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  Le [!UICONTROL Surveillance] Le tableau de bord comprend les mesures de base de la dernière exécution réussie et l’état de la tâche quotidienne jusqu’à 90 jours auparavant. Le [!UICONTROL Comptes associés] Le tableau de bord affiche les mesures de base et l’état de la tâche quotidienne spécifiques à la variable [Comptes associés](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) enrichissement de profil.

![Une indication visuelle de la façon d’accéder à l’écran de surveillance des tâches d’enrichissement de profil dans l’interface utilisateur Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Les données de la variable **[!UICONTROL Mesures]** La carte comprend les mesures de base de la dernière exécution réussie de la tâche Comptes associés.

Les mesures suivantes sont disponibles pour les tâches d’enrichissement de profil de comptes connexes :

| Mesure | Description |
---------|----------|
| **[!UICONTROL Profils de compte totaux]** | Indique le nombre total de profils de compte auxquels votre entreprise a accès. |
| **[!UICONTROL Groupes de comptes]** | Indique le nombre de groupes de comptes organisés en grappe par la tâche d’apprentissage automatique Comptes associés. |
| **[!UICONTROL Groupes à compte unique]** | Indique le nombre de comptes qui ne sont pas regroupés avec d’autres comptes. |
| **[!UICONTROL Taille de groupe la plus grande]** | Indique la taille du groupe de comptes associé le plus grand. La taille maximale autorisée pour le groupe est de 30. |
| **[!UICONTROL Taille médiane du groupe]** | Indique la taille médiane des groupes de comptes associés dans votre organisation. |
| **[!UICONTROL Dernière exécution réussie]** | Indique la date et l’heure de la dernière exécution de la tâche Comptes associés réussie. |
| **[!UICONTROL État]** | Indique l’état (réussite, échec ou traitement) de la tâche Comptes associés. |
| **[!UICONTROL Message]** | Indique un message d’erreur ou d’avertissement pour une tâche particulière. |

## Contrôles de l’interface utilisateur {#ui-controls}

Cette section décrit les différentes options de l’interface utilisateur (IU) de l’interface de surveillance, qui vous permettent de filtrer les mesures affichées sur la page.

Utilisez l’icône de flèche (![icône de flèche](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) pour développer ou supprimer la carte en haut de l’écran, qui affiche des informations en un coup d’oeil sur les tâches d’enrichissement de profil.

![Enregistrement d’écran qui affiche la commande d’IU de l’icône de flèche.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Utilisez la variable **[!UICONTROL Mesures et graphiques]** bascule pour fermer la vue qui affiche les dernières mesures.

![Enregistrement d’écran qui affiche le bouton d’activation/désactivation des mesures et des graphiques.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Utilisez la variable **[!UICONTROL Afficher uniquement les échecs]** bascule pour afficher uniquement les tâches d’enrichissement de profil ayant échoué.

![Enregistrement d’écran qui affiche le bouton d’activation/désactivation Afficher les échecs uniquement.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous pouvez désormais contrôler et comprendre les mesures des tâches d’enrichissement de profil de comptes associés. Pour plus d’informations, consultez les documents suivants :

* [Comptes associés dans la plateforme CDP B2B en temps réel](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Onglet Comptes associés dans le guide d’interface utilisateur du profil de compte](/help/rtcdp/accounts/account-profile-ui-guide.md)