---
keywords: Experience Platform;accueil;rubriques les plus consultées;profils de surveillance;flux de données de surveillance;flux de données;profil;profil client en temps réel ;
description: Real-Time Customer Profile vous permet d’obtenir une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment en ligne, hors ligne, CRM et tiers. Ce tutoriel explique comment surveiller les flux de données avec des profils à l’aide de l’interface utilisateur de l’Experience Platform.
title: Surveillance des flux de données pour les profils dans l’interface utilisateur
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 9%

---

# Surveillance des flux de données pour les profils dans l’interface utilisateur

Real-Time Customer Profile vous permet d’obtenir une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment en ligne, hors ligne, CRM et tiers. Le Profil vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

Le tableau de bord de surveillance vous fournit une représentation visuelle de l’activité des données dans Profile, y compris l’état des profils de vos données. Ce tutoriel explique comment utiliser le tableau de bord de surveillance pour surveiller les profils de vos données à l’aide de l’interface utilisateur de l’Experience Platform, ce qui vous permet de suivre l’état du traitement des profils.

## Prise en main {#getting-started}

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [Flux de données](../home.md) : les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Platform. Les flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers des jeux de données cibles, vers [!DNL Identity] et [!DNL Profile], et vers [!DNL Destinations].
   - [Exécutions de flux de données](../../sources/notifications.md): Les exécutions de flux de données sont les tâches planifiées récurrentes en fonction de la configuration de fréquence des flux de données sélectionnés.
- [Profil client en temps réel](../../profile/home.md): Fournit un profil client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
- [Sandbox](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuelles qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Tableau de bord des profils de surveillance {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="Traitement des profils"
>abstract="La vue Traitement des profils contient des informations sur les enregistrements ingérés dans le service Profile, notamment le nombre de fragments de profil créés, de fragments de profil mis à jour et le nombre total de fragments de profil."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="Détails de l’exécution du flux de données"
>abstract="La page Détails de l’exécution du flux de données affiche plus d’informations sur votre exécution de flux de données de profil, y compris son identifiant d’organisation et son identifiant d’exécution de flux de données."

Pour accéder au **[!UICONTROL Profils]** tableau de bord, sélectionnez **[!UICONTROL Surveillance]** dans le volet de navigation de gauche. Une fois sur le **[!UICONTROL Surveillance]** , sélectionnez **[!UICONTROL Profils]** carte.

![La carte Profils . Informations sur le nombre d&#39;enregistrements reçus, le nombre de fragments de profil créés et mis à jour, et le taux de succès s&#39;affiche.](../assets/ui/monitor-profiles/focus-card.png)

Sur la page principale **[!UICONTROL Profils]** tableau de bord, le **[!UICONTROL Profils]** La carte affiche des informations sur le nombre total d’enregistrements reçus, le nombre de fragments de profil créés et mis à jour, ainsi que le taux de succès des fragments de profil créés et mis à jour.

Le tableau de bord lui-même contient des mesures relatives au traitement des profils. Par défaut, le tableau de bord affiche les détails du traitement des profils pour les sources de votre entreprise au cours des dernières 24 heures.

![Le tableau de bord Profils . Les informations sur le nombre d&#39;enregistrements de profil reçus par source s&#39;affichent.](../assets/ui/monitor-profiles/sources.png)

Le [!UICONTROL Traitement des profils] contient des informations sur les enregistrements ingérés dans [!DNL Profile], notamment le nombre de fragments de profil créés, de fragments de profil mis à jour et le nombre total de fragments de profil.

Les mesures suivantes sont disponibles pour cette vue de tableau de bord :

| Mesure | Description |
| -------| ----------- |
| **[!UICONTROL Nom de source]** | Nom de la source. |
| **[!UICONTROL Enregistrements reçus]** | Nombre d’enregistrements reçus du lac de données. |
| **[!UICONTROL Enregistrements échoués]** | Nombre d’enregistrements ingérés, mais pas dans [!DNL Profile] en raison d’erreurs. |
| **[!UICONTROL Fragments de profil créés]** | Nombre de nouvelles nettes [!DNL Profile] fragments ajoutés. |
| **[!UICONTROL Fragments de profil mis à jour]** | Le nombre de [!DNL Profile] fragments mis à jour. |
| **[!UICONTROL Fragments de profil totaux]** | Le nombre total d&#39;enregistrements écrits dans [!DNL Profile], y compris toutes les [!DNL Profile] fragments mis à jour et nouveaux [!DNL Profile] fragments créés. |
| **[!UICONTROL Total des flux de données ayant échoué]** | Nombre d’exécutions de flux de données ayant échoué. |

Vous pouvez sélectionner l’icône de filtre ![Icône Filtrer](../assets/ui/monitor-profiles/filter.png) en regard du nom de la source pour afficher les informations de traitement de profil pour les flux de données de cette source sélectionnée.

![L’icône de filtre est mise en surbrillance. La sélection de cette icône vous permet d’afficher les flux de données de la source sélectionnée.](../assets/ui/monitor-profiles/sources-filter.png)

Vous pouvez également sélectionner **[!UICONTROL Flux de données]** sur le bouton d’activation/désactivation pour afficher les détails du traitement de profil pour les flux de données de votre entreprise au cours des dernières 24 heures.

![Le tableau de bord Profils . Des informations sur le nombre d’enregistrements de profil reçus par flux de données s’affichent.](../assets/ui/monitor-profiles/dataflows.png)

Les mesures suivantes sont disponibles pour cette vue de tableau de bord :

| Mesure | Description |
| -------| ----------- |
| **[!UICONTROL Flux de données]** | Nom du flux de données. |
| **[!UICONTROL Jeu de données]** | Nom du jeu de données auquel le flux de données est en cours d’insertion. |
| **[!UICONTROL Nom de source]** | Nom de la source à laquelle le flux de données appartient. |
| **[!UICONTROL Enregistrements reçus**] | Nombre d’enregistrements reçus du lac de données. |
| **[!UICONTROL Enregistrements échoués]** | Nombre d’enregistrements ingérés, mais pas dans [!DNL Profile] en raison d’erreurs. |
| **[!UICONTROL Fragments de profil créés]** | Nombre de nouvelles nettes [!DNL Profile] fragments ajoutés. |
| **[!UICONTROL Fragments de profil mis à jour]** | Le nombre de [!DNL Profile] fragments mis à jour |
| **[!UICONTROL Fragments de profil totaux]** | Le nombre total d&#39;enregistrements écrits dans [!DNL Profile], y compris toutes les [!DNL Profile] fragments mis à jour et nouveaux [!DNL Profile] fragments créés. |
| **[!UICONTROL Nombre total d’exécutions de flux ayant échoué]** | Nombre d’exécutions de flux de données ayant échoué. |
| **[!UICONTROL Dernière principale]** | Horodatage de la dernière exécution du flux de données. |

Icône Sélectionner le filtre ![filter](../assets/ui/monitor-profiles/filter.png) en regard de l’heure de début d’exécution du flux de données pour afficher plus d’informations sur votre [!DNL Profile] dataflow s’exécute.

![L’icône de filtre est mise en surbrillance. La sélection de cette icône vous permet d’afficher les détails du flux de données sélectionné.](../assets/ui/monitor-profiles/dataflows-filter.png)

Le [!UICONTROL Détails de l’exécution du flux de données] affiche plus d’informations sur votre [!DNL Profile] les flux de données s’exécutent, y compris leur identifiant d’organisation et l’identifiant d’exécution de flux de données. Cette page affiche également le code d’erreur et le message d’erreur correspondants fournis par [!DNL Profile], en cas d’erreur dans le processus d’ingestion.

![Un tableau de bord présentant des informations détaillées sur le flux de données sélectionné s’affiche.](../assets/ui/monitor-profiles/dataflow-run-details.png)

Les mesures suivantes sont disponibles pour cette vue de tableau de bord :

| Mesure | Description |
| -------| ----------- |
| **[!UICONTROL Enregistrements reçus]** | Nombre d’enregistrements reçus du lac de données. |
| **[!UICONTROL Enregistrements échoués]** | Nombre d’enregistrements ingérés, mais pas dans [!DNL Profile] en raison d’erreurs. |
| **[!UICONTROL Fragments de profil créés]** | Nombre de nouvelles nettes [!DNL Profile] fragments ajoutés. |
| **[!UICONTROL Fragments de profil mis à jour]** | Le nombre de [!DNL Profile] fragments mis à jour. |
| **[!UICONTROL Statut]** | Définit l’état global d’un flux de données. Les valeurs d’état possibles sont les suivantes : <ul><li>`Success`: Indique qu’un flux de données est principal et ingère des données selon le planning selon lequel il a été fourni.</li><li>`Failed`: Indique que le processus d’activation d’un flux de données a été interrompu en raison d’erreurs. </li><li>`Processing`: Indique que le flux de données n’est pas encore principal. Cet état est souvent rencontré immédiatement après la création d’un nouveau flux de données.</li></ul> |
| **[!UICONTROL Démarrage de l’exécution du flux de données]** | Date et heure auxquelles le flux de données a commencé à s’exécuter. |
| **[!UICONTROL Dernière mise à jour]** | Date et heure de la dernière mise à jour du flux de données. |
| **[!UICONTROL Synthèse des erreurs]** | Si l’exécution du flux de données a échoué, un code d’erreur s’affiche et un résumé des raisons de l’échec de l’exécution du flux de données. |
| **[!UICONTROL Identifiant d’exécution du flux de données]** | L’identifiant de l’exécution du flux de données. |
| **[!UICONTROL Identifiant de l’organisation IMS]** | ID d’organisation auquel appartient le flux de données. |

De plus, vous pouvez sélectionner le bouton bascule pour afficher les enregistrements en échec ou ignorés. La section Erreurs comprend des détails sur le code d’erreur et le nombre d’enregistrements ayant échoué ou exclus.
