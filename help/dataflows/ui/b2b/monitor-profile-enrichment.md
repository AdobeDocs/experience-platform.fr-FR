---
description: Utilisez le tableau de bord [!UICONTROL Enrichissement du profil] pour déterminer si les tâches d’enrichissement du profil ont été exécutées et terminées avec succès et pour afficher les mesures de base permettant d’évaluer l’efficacité des enrichissements.
solution: Experience Platform
title: Surveillance des tâches d’enrichissement des profils
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 4%

---

# Surveiller les tâches d’enrichissement de profil dans l’interface utilisateur {#monitor-profile-enrichment}

Utilisez le tableau de bord [!UICONTROL Enrichissement du profil] pour déterminer si les tâches d’enrichissement du profil ont été exécutées et terminées avec succès et pour afficher les mesures de base permettant d’évaluer l’efficacité des enrichissements.

Dans l’interface utilisateur [Experience Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Surveillance]** dans le volet de navigation de gauche pour accéder au tableau de bord [!UICONTROL Surveillance]. Dans le sélecteur d’affichage, sélectionnez **Flux B2B** pour afficher les éléments de tableau de bord spécifiques à [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  Le tableau de bord [!UICONTROL Surveillance] comprend les mesures de base de la dernière exécution réussie et le statut quotidien des tâches jusqu’à 90 jours auparavant.

## Enrichissement du profil des comptes associés {#related-accounts}

Le tableau de bord [!UICONTROL Comptes associés] affiche les mesures de base et le statut du traitement quotidien spécifique à l’enrichissement du profil [Comptes associés](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

![Indication visuelle de la manière d’accéder à l’écran de surveillance des tâches d’enrichissement du profil dans l’interface utilisateur d’Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Les données de la carte **[!UICONTROL Mesures]** incluent les mesures de base de la dernière exécution réussie de la tâche Comptes associés.

Les mesures suivantes sont disponibles pour les tâches d’enrichissement de profil de comptes associées :

| Mesure | Description |
| --------- | ---------- |
| **[!UICONTROL Nombre total de profils de compte]** | Indique le nombre total de profils de compte auxquels votre organisation a accès. |
| **[!UICONTROL Groupes de comptes]** | Indique le nombre de groupes de comptes mis en cluster par la tâche de machine learning de comptes associés. |
| **[!UICONTROL Groupes à compte unique]** | Indique le nombre de comptes qui ne sont pas regroupés avec d’autres comptes. |
| **[!UICONTROL Taille du groupe le plus grand]** | Indique la taille du plus grand groupe de comptes associés. La taille de groupe maximale autorisée est de 30. |
| **[!UICONTROL Taille médiane du groupe]** | Indique la taille médiane des groupes de comptes associés dans votre organisation. |
| **[!UICONTROL Dernière exécution réussie]** | Indique la date et l’heure de la dernière exécution réussie de la tâche de comptes associés. |
| **[!UICONTROL Statut]** | Indique le statut (réussi, en échec ou en cours de traitement) de la tâche de comptes associée. |
| **[!UICONTROL Message]** | Indique un message d’erreur ou d’avertissement pour une exécution de tâche spécifique. |

## Enrichissement du profil correspondant du lead au compte {#lead-to-account-matching}

Le tableau de bord [!UICONTROL Correspondance entre les prospects et les comptes] affiche les mesures de base et le statut d’exécution de tâche quotidien spécifiques à l’enrichissement de profil [Correspondance entre les prospects et les comptes](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

![Enrichissement du profil correspondant du prospect au compte](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

Les mesures suivantes sont disponibles pour les tâches d’enrichissement de profil correspondant au compte de prospect :

| Mesure | Description |
| --------- | ---------- |
| **[!UICONTROL Nombre total de personnes ayant un compte]** | Indique le nombre total de personnes associées à un compte. |
| **[!UICONTROL Total des comptes]** | Indique le nombre total de comptes. |
| **[!UICONTROL Personnes existantes ayant des comptes]** | Indique le nombre de personnes déjà associées à un compte à partir des sources de données. |
| **[!UICONTROL Personnes appariées]** | Indique le nombre de personnes qui ont été associées à un compte. |
| **[!UICONTROL Personnes sans correspondance]** | Indique le nombre de personnes qui n’ont pas été associées à un compte. |
| **[!UICONTROL Dernière exécution réussie]** | Indique la date et l’heure de la dernière exécution réussie de la tâche de correspondance de prospect et de compte. |
| **[!UICONTROL Statut]** | Indique le statut (réussi, en échec ou en cours de traitement) de la tâche de correspondance entre le prospect et le compte. |

## Enrichissement prédictif du profil de notation des prospects et des comptes {#predictive-lead-to-account-scoring}

Le tableau de bord [!UICONTROL Notation prédictive des prospects et des comptes] affiche les mesures de base et le statut d’exécution quotidien des tâches spécifiques à l’enrichissement de profil [Notation prédictive des prospects et des comptes](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md).

![Enrichissement prédictif du profil de notation des prospects et des comptes](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

Les mesures suivantes sont disponibles pour les tâches d’enrichissement des profils de notation prédictive des prospects et des comptes :

| Mesure | Description |
| --------- | ---------- |
| **[!UICONTROL Début du traitement]** | Indique la date et l’heure de début de l’exécution de la tâche de notation prédictive des prospects et des comptes. |
| **[!UICONTROL Temps de traitement]** | Durée totale nécessaire à l’exécution de la tâche. |
| **[!UICONTROL Nom du score]** | Nom de score de la tâche. |
| **[!UICONTROL Type de profil]** | Le type du score : <ul><li>Personne</li><li>Compte</li></ul>. |
| **[!UICONTROL Type de traitement]** | Type de la tâche :<ul><li>Notation</li><li>Formation</li>. |
| **[!UICONTROL Statut]** | Indique le statut (réussi, en échec ou en cours de traitement) de la tâche de notation prédictive des prospects et des comptes. |

## Contrôles de l’interface utilisateur {#ui-controls}

Cette section décrit diverses options de l’interface utilisateur de la surveillance. Ces options vous permettent de filtrer les mesures affichées sur la page.

Utilisez l’icône de flèche (![icône de flèche](/help/images/icons/chevron-up.png)) pour développer ou ignorer la carte en haut de l’écran, qui affiche des informations d’un coup d’œil sur les tâches d’enrichissement de profil.

![Enregistrement d’écran affichant le contrôle de l’interface utilisateur de l’icône de flèche.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Utilisez le bouton (bascule) **[!UICONTROL Mesures et graphiques]** pour ignorer la vue qui affiche les dernières mesures.

![Enregistrement d’écran affichant le bouton (bascule) Mesures et graphiques.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Utilisez le bouton (bascule) **[!UICONTROL Afficher les échecs uniquement]** pour afficher uniquement les tâches d’enrichissement de profil ayant échoué.

![Enregistrement d’écran affichant uniquement le bouton Afficher les échecs.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous pouvez désormais surveiller et comprendre les mesures des tâches d’enrichissement de profil. Consultez les documents suivants pour plus d’informations :

* [Comptes associés dans Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Section « Comptes associés » du guide de l’interface utilisateur du profil de compte](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Correspondance des prospects et des comptes dans Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Notation prédictive des prospects et des comptes dans Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
