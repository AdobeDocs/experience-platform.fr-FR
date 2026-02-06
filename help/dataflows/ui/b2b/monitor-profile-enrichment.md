---
description: Utilisez le tableau de bord [!UICONTROL Profile Enrichment] pour déterminer si les tâches d’enrichissement de profil ont été exécutées et terminées avec succès, et pour afficher les mesures de base permettant d’évaluer l’efficacité des enrichissements.
solution: Experience Platform
title: Surveillance des tâches d’enrichissement des profils
type: Tutorial
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 0e993f7d0791f5f6f9dce63eb3848609d892e788
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 4%

---

# Surveiller les tâches d’enrichissement de profil dans l’interface utilisateur {#monitor-profile-enrichment}

Utilisez le tableau de bord [!UICONTROL Profile Enrichment] pour déterminer si les tâches d’enrichissement de profil ont été exécutées et terminées avec succès, et pour afficher les mesures de base permettant d’évaluer l’efficacité des enrichissements.

Dans l’[interface utilisateur d’Experience Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Monitoring]** dans le volet de navigation de gauche pour accéder au tableau de bord [!UICONTROL Monitoring]. Dans le sélecteur d’affichage, sélectionnez **Flux B2B** pour afficher les éléments de tableau de bord spécifiques à [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  Le tableau de bord [!UICONTROL Monitoring] inclut les mesures de base de la dernière exécution réussie et le statut quotidien des tâches jusqu’à 90 jours auparavant.

## Enrichissement du profil des comptes associés {#related-accounts}

Le tableau de bord [!UICONTROL Related accounts] affiche les mesures de base et le statut du traitement quotidien spécifique à l’enrichissement du profil [Comptes associés](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

![Indication visuelle de la manière d’accéder à l’écran de surveillance des tâches d’enrichissement du profil dans l’interface utilisateur d’Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Les données de la carte **[!UICONTROL Metrics]** incluent les mesures de base de la dernière exécution réussie de la tâche Comptes associés.

Les mesures suivantes sont disponibles pour les tâches d’enrichissement de profil de comptes associées :

| Mesure | Description |
| --------- | ---------- |
| **[!UICONTROL Total account profiles]** | Indique le nombre total de profils de compte auxquels votre organisation a accès. |
| **[!UICONTROL Account groups]** | Indique le nombre de groupes de comptes mis en cluster par la tâche de machine learning de comptes associés. |
| **[!UICONTROL Single-account groups]** | Indique le nombre de comptes qui ne sont pas regroupés avec d’autres comptes. |
| **[!UICONTROL Largest group size]** | Indique la taille du plus grand groupe de comptes associés. La taille de groupe maximale autorisée est de 30. |
| **[!UICONTROL Median group size]** | Indique la taille médiane des groupes de comptes associés dans votre organisation. |
| **[!UICONTROL Last successful run]** | Indique la date et l’heure de la dernière exécution réussie de la tâche de comptes associés. |
| **[!UICONTROL Status]** | Indique le statut (réussi, en échec ou en cours de traitement) de la tâche de comptes associée. |
| **[!UICONTROL Message]** | Indique un message d’erreur ou d’avertissement pour une exécution de tâche spécifique. |

## Enrichissement du profil correspondant du lead au compte {#lead-to-account-matching}

Le tableau de bord [!UICONTROL Lead to account matching] affiche les mesures de base et le statut d’exécution quotidien des tâches spécifiques à l’enrichissement de profil [Correspondance des prospects et des comptes](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

![Enrichissement du profil correspondant du prospect au compte](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

Les mesures suivantes sont disponibles pour les tâches d’enrichissement de profil correspondant au compte de prospect :

| Mesure | Description |
| --------- | ---------- |
| **[!UICONTROL Total persons with accounts]** | Indique le nombre total de personnes associées à un compte. |
| **[!UICONTROL Total accounts]** | Indique le nombre total de comptes. |
| **[!UICONTROL Existing persons with accounts]** | Indique le nombre de personnes déjà associées à un compte à partir des sources de données. |
| **[!UICONTROL Persons matched]** | Indique le nombre de personnes qui ont été associées à un compte. |
| **[!UICONTROL Persons unmatched]** | Indique le nombre de personnes qui n’ont pas été associées à un compte. |
| **[!UICONTROL Last successful run]** | Indique la date et l’heure de la dernière exécution réussie de la tâche de correspondance de prospect et de compte. |
| **[!UICONTROL Status]** | Indique le statut (réussi, en échec ou en cours de traitement) de la tâche de correspondance entre le prospect et le compte. |

## Enrichissement prédictif du profil de notation des prospects et des comptes {#predictive-lead-to-account-scoring}

Le tableau de bord [!UICONTROL Predictive lead and account scoring] affiche les mesures de base et le statut d’exécution quotidien des tâches spécifiques à l’enrichissement de profil [Notation prédictive des prospects et des comptes](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md).

![Enrichissement prédictif du profil de notation des prospects et des comptes](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

Les mesures suivantes sont disponibles pour les tâches d’enrichissement des profils de notation prédictive des prospects et des comptes :

| Mesure | Description |
| --------- | ---------- |
| **[!UICONTROL Job start]** | Indique la date et l’heure de début de l’exécution de la tâche de notation prédictive des prospects et des comptes. |
| **[!UICONTROL Processing time]** | Durée totale nécessaire à l’exécution de la tâche. |
| **[!UICONTROL Score name]** | Nom de score de la tâche. |
| **[!UICONTROL Profile type]** | Le type du score : <ul><li>Personne</li><li>Compte</li></ul>. |
| **[!UICONTROL Job type]** | Type de la tâche :<ul><li>Notation</li><li>Formation</li>. |
| **[!UICONTROL Status]** | Indique le statut (réussi, en échec ou en cours de traitement) de la tâche de notation prédictive des prospects et des comptes. |

## Contrôles de l’interface utilisateur {#ui-controls}

Cette section décrit diverses options de l’interface utilisateur de la surveillance. Ces options vous permettent de filtrer les mesures affichées sur la page.

Utilisez l’icône de flèche (![icône de flèche](/help/images/icons/chevron-up.png)) pour développer ou ignorer la carte en haut de l’écran, qui affiche des informations d’un coup d’œil sur les tâches d’enrichissement de profil.

![Enregistrement d’écran affichant le contrôle de l’interface utilisateur de l’icône de flèche.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Utilisez le bouton **[!UICONTROL Metrics and graphs]** pour ignorer la vue qui affiche les dernières mesures.

![Enregistrement d’écran affichant le bouton (bascule) Mesures et graphiques.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Utilisez le bouton **[!UICONTROL Show failures only]** pour afficher uniquement les tâches d’enrichissement de profil ayant échoué.

![Enregistrement d’écran affichant uniquement le bouton Afficher les échecs.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous pouvez désormais surveiller et comprendre les mesures des tâches d’enrichissement de profil. Consultez les documents suivants pour plus d’informations :

* [Comptes associés dans Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Section « Comptes associés » du guide de l’interface utilisateur du profil de compte](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Correspondance des prospects et des comptes dans Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Notation prédictive des prospects et des comptes dans Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
