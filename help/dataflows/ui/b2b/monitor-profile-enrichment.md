---
description: Utilisez la variable [!UICONTROL Enrichissement du profil] tableau de bord pour comprendre si les tâches d’enrichissement de profil ont été exécutées et terminées avec succès et pour afficher les mesures de base afin d’évaluer l’efficacité des enrichissements.
solution: Experience Platform
title: Surveillance des tâches d’enrichissement de profil
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 6811e3032abe569b1f00d757553eb6862e4e3354
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 4%

---

# Surveillance des tâches d’enrichissement de profil dans l’interface utilisateur (#monitor-profile-enrichment)

Utilisez la variable [!UICONTROL Enrichissement du profil] tableau de bord pour comprendre si les tâches d’enrichissement de profil ont été exécutées et terminées avec succès et pour afficher les mesures de base afin d’évaluer l’efficacité des enrichissements.

Dans le [Interface utilisateur de Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Surveillance]** dans le volet de navigation de gauche pour accéder à la fonction [!UICONTROL Surveillance] tableau de bord. Dans le sélecteur de mode, sélectionnez **Flux B2B** pour afficher les éléments du tableau de bord spécifiques à [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  Le [!UICONTROL Surveillance] Le tableau de bord comprend les mesures de base de la dernière exécution réussie et l’état de la tâche quotidienne jusqu’à 90 jours auparavant.

## Enrichissement du profil des comptes associés (#related-accounts)

Le [!UICONTROL Comptes associés] Le tableau de bord affiche les mesures de base et l’état de la tâche quotidienne spécifique à l’ [Comptes associés](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) enrichissement de profil.

![Une indication visuelle de la façon d’accéder à l’écran de surveillance des tâches d’enrichissement de profil dans l’interface utilisateur Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Les données de la variable **[!UICONTROL Mesures]** La carte comprend les mesures de base de la dernière exécution réussie de la tâche Comptes associés.

Les mesures suivantes sont disponibles pour les tâches d’enrichissement de profil de comptes connexes :

| Mesure | Description |
| --------- | ---------- |
| **[!UICONTROL Profils de compte totaux]** | Indique le nombre total de profils de compte auxquels votre entreprise a accès. |
| **[!UICONTROL Groupes de comptes]** | Indique le nombre de groupes de comptes organisés en grappe par la tâche d’apprentissage automatique des comptes associés. |
| **[!UICONTROL Groupes à compte unique]** | Indique le nombre de comptes qui ne sont pas regroupés avec d’autres comptes. |
| **[!UICONTROL Taille de groupe la plus grande]** | Indique la taille du groupe de comptes associé le plus grand. La taille maximale autorisée pour le groupe est de 30. |
| **[!UICONTROL Taille médiane du groupe]** | Indique la taille médiane des groupes de comptes associés dans votre organisation. |
| **[!UICONTROL Dernière exécution réussie]** | Indique la date et l’heure de la dernière tâche de comptes associés réussie. |
| **[!UICONTROL Statut]** | Indique l’état (réussite, échec ou traitement) de la tâche de comptes associée. |
| **[!UICONTROL Message]** | Indique un message d’erreur ou d’avertissement pour une tâche particulière. |

## Enrichissement du profil correspondant au compte (#lead-to-account-matching)

Le [!UICONTROL Correspondance de piste avec le compte] Le tableau de bord affiche les mesures de base et l’état d’exécution quotidienne des tâches spécifique à la variable [Correspondance de piste avec le compte](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) enrichissement de profil.

![Conduire à l’enrichissement du profil correspondant au compte](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

Les mesures suivantes sont disponibles pour les tâches d’enrichissement de profil correspondant à un compte :

| Mesure | Description |
| --------- | ---------- |
| **[!UICONTROL Nombre total de personnes disposant d’un compte]** | Indique le nombre total de personnes associées à un compte. |
| **[!UICONTROL Comptes totaux]** | Indique le nombre total de comptes. |
| **[!UICONTROL Personnes existantes avec comptes]** | Indique le nombre de personnes déjà associées à un compte à partir des sources de données. |
| **[!UICONTROL Personnes correspondantes]** | Indique le nombre de personnes qui ont été associées à un compte. |
| **[!UICONTROL Personnes inégalées]** | Indique le nombre de personnes qui n’ont pas été associées à un compte. |
| **[!UICONTROL Dernière exécution réussie]** | Indique la date et l’heure de la dernière exécution de la tâche de correspondance de compte réussie. |
| **[!UICONTROL Statut]** | Indique l’état (réussite, échec ou traitement) de la tâche de correspondance de compte. |

## Contrôles de l’interface utilisateur {#ui-controls}

Cette section décrit les différentes options de l’interface utilisateur (IU) de l’interface de surveillance, qui vous permettent de filtrer les mesures affichées sur la page.

Utilisez l’icône de flèche (![icône de flèche](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) pour développer ou supprimer la carte en haut de l’écran, qui affiche des informations en un coup d’oeil sur les tâches d’enrichissement de profil.

![Enregistrement d’écran qui affiche la commande d’IU de l’icône de flèche.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Utilisez la variable **[!UICONTROL Mesures et graphiques]** bascule pour fermer la vue qui affiche les dernières mesures.

![Enregistrement d’écran qui affiche le bouton d’activation/désactivation des mesures et des graphiques.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Utilisez la variable **[!UICONTROL Afficher uniquement les échecs]** bascule pour afficher uniquement les tâches d’enrichissement de profil ayant échoué.

![Enregistrement d’écran qui affiche le bouton d’activation/désactivation Afficher les échecs uniquement.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous pouvez désormais contrôler et comprendre les mesures des tâches d’enrichissement de profil. Consultez les documents suivants pour plus d’informations :

* [Comptes associés dans la plateforme CDP B2B en temps réel](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Section « Comptes associés » du guide de l’interface utilisateur du profil de compte](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Conduire à la correspondance de comptes dans la plateforme CDP B2B en temps réel](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
