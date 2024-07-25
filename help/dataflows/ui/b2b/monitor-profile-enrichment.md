---
description: Utilisez le tableau de bord [!UICONTROL Enrichissement du profil] pour déterminer si les tâches d’enrichissement de profil ont été exécutées et terminées avec succès et pour afficher les mesures de base permettant d’évaluer l’efficacité des enrichissements.
solution: Experience Platform
title: Surveillance des tâches d’enrichissement de profil
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 4%

---

# Surveillance des tâches d’enrichissement de profil dans l’interface utilisateur {#monitor-profile-enrichment}

Utilisez le tableau de bord [!UICONTROL Enrichissement du profil] pour déterminer si les tâches d’enrichissement de profil ont été exécutées et terminées avec succès et pour afficher les mesures de base permettant d’évaluer l’efficacité des enrichissements.

Dans l’ [ interface utilisateur de Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Surveillance]** dans le volet de navigation de gauche pour accéder au tableau de bord [!UICONTROL Surveillance]. Dans le sélecteur de vue, sélectionnez **Flux B2B** pour afficher les éléments de tableau de bord spécifiques à [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  Le tableau de bord [!UICONTROL Surveillance] comprend les mesures de base de la dernière exécution réussie et l’état de la tâche quotidienne jusqu’à 90 jours dans le passé.

## Enrichissement du profil de comptes associés {#related-accounts}

Le tableau de bord [!UICONTROL Comptes associés] affiche les mesures de base et l’état de la tâche quotidienne spécifique à l’enrichissement du profil [ ](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

![Indication visuelle de la manière d’accéder à l’écran de surveillance des tâches d’enrichissement de profil dans l’interface utilisateur Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Les données de la carte **[!UICONTROL Mesures]** incluent les mesures de base de la dernière exécution réussie de la tâche Comptes associés.

Les mesures suivantes sont disponibles pour les tâches d’enrichissement de profil de comptes connexes :

| Mesure | Description |
| --------- | ---------- |
| **[!UICONTROL Total des profils de compte]** | Indique le nombre total de profils de compte auxquels votre entreprise a accès. |
| **[!UICONTROL Groupes de comptes]** | Indique le nombre de groupes de comptes organisés en grappe par la tâche d’apprentissage automatique des comptes associés. |
| **[!UICONTROL Groupes à compte unique]** | Indique le nombre de comptes qui ne sont pas regroupés avec d’autres comptes. |
| **[!UICONTROL Taille de groupe la plus grande]** | Indique la taille du groupe de comptes associé le plus grand. La taille maximale autorisée pour le groupe est de 30. |
| **[!UICONTROL Taille du groupe médian]** | Indique la taille médiane des groupes de comptes associés dans votre organisation. |
| **[!UICONTROL Dernière exécution réussie]** | Indique la date et l’heure de la dernière tâche de comptes associés réussie. |
| **[!UICONTROL Statut]** | Indique l’état (réussite, échec ou traitement) de la tâche de comptes associée. |
| **[!UICONTROL Message]** | Indique un message d’erreur ou d’avertissement pour une tâche particulière. |

## Conduire à l’enrichissement du profil correspondant au compte {#lead-to-account-matching}

Le tableau de bord [!UICONTROL Correspondance de piste avec le compte] affiche les mesures de base et l’état d’exécution de tâche quotidien spécifiques à l’enrichissement de profil [Correspondance de piste avec le compte](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

![ Piste vers l’enrichissement du profil correspondant](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

Les mesures suivantes sont disponibles pour les tâches d’enrichissement de profil correspondant à un compte :

| Mesure | Description |
| --------- | ---------- |
| **[!UICONTROL Nombre total de personnes avec des comptes]** | Indique le nombre total de personnes associées à un compte. |
| **[!UICONTROL Total comptes]** | Indique le nombre total de comptes. |
| **[!UICONTROL Personnes existantes avec comptes]** | Indique le nombre de personnes déjà associées à un compte à partir des sources de données. |
| **[!UICONTROL Personnes correspondantes]** | Indique le nombre de personnes qui ont été associées à un compte. |
| **[!UICONTROL Personnes sans correspondance]** | Indique le nombre de personnes qui n’ont pas été associées à un compte. |
| **[!UICONTROL Dernière exécution réussie]** | Indique la date et l’heure de la dernière exécution de la tâche de correspondance de compte réussie. |
| **[!UICONTROL Statut]** | Indique l’état (réussite, échec ou traitement) de la tâche de correspondance de compte. |

## Enrichissement prédictif du profil de piste et de notation de compte {#predictive-lead-to-account-scoring}

Le tableau de bord [!UICONTROL Score prédictif de piste et de compte] affiche les mesures de base et l’état d’exécution de la tâche quotidien spécifiques à l’enrichissement de profil [Score prédictif de piste et de compte](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md).

![ Enrichissement prédictif du profil de piste et de notation de compte ](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

Les mesures suivantes sont disponibles pour les tâches d’enrichissement de profil de score de piste et de compte prédictives :

| Mesure | Description |
| --------- | ---------- |
| **[!UICONTROL Démarrage de la tâche]** | Indique la date et l’heure de début de l’exécution de la tâche de notation de compte et de piste prédictive. |
| **[!UICONTROL Temps de traitement]** | Temps total nécessaire à la réalisation de la tâche. |
| **[!UICONTROL Nom du score]** | Nom du score de la tâche. |
| **[!UICONTROL Type de profil]** | Type de score : <ul><li>Personne</li><li>Compte</li></ul>. |
| **[!UICONTROL Type de tâche]** | Type de la tâche :<ul><li>Notation</li><li>Formation</li>. |
| **[!UICONTROL Statut]** | Indique l’état (réussite, échec ou traitement) de la tâche de notation de compte et de piste prédictive. |

## Contrôles de l’interface utilisateur {#ui-controls}

Cette section décrit les différentes options de l’interface utilisateur (IU) de l’interface de surveillance, qui vous permettent de filtrer les mesures affichées sur la page.

Utilisez l’icône de flèche (![icône de flèche](/help/images/icons/chevron-up.png)) pour développer ou ignorer la carte en haut de l’écran, qui affiche des informations en un coup d’oeil sur les tâches d’enrichissement de profil.

![Enregistrement d’écran qui affiche la commande de l’icône de flèche dans l’interface utilisateur.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Utilisez le bouton d’activation/désactivation **[!UICONTROL Mesures et graphiques]** pour ignorer la vue qui affiche les dernières mesures.

![Enregistrement d’écran qui affiche le bouton d’activation/désactivation des mesures et des graphiques.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Utilisez le bouton d’activation/désactivation **[!UICONTROL Afficher les échecs uniquement]** pour afficher uniquement les tâches d’enrichissement de profil ayant échoué.

![Enregistrement d’écran qui affiche le bouton bascule Afficher les échecs uniquement.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous pouvez désormais contrôler et comprendre les mesures des tâches d’enrichissement de profil. Consultez les documents suivants pour plus d’informations :

* [Comptes associés dans Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Section « Comptes associés » du guide de l’interface utilisateur du profil de compte](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Conduire à la correspondance de comptes dans Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Score prédictif de piste et de compte dans Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
