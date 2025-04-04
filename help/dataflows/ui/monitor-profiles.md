---
keywords: Experience Platform;accueil;rubriques les plus consultées;surveiller les profils;surveiller les flux de données;flux de données;profil;profil client en temps réel;
description: Le profil client en temps réel offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Ce tutoriel explique comment surveiller les flux de données avec les profils à l’aide de l’interface utilisateur d’Experience Platform.
title: Surveillance des flux de données pour les profils dans l’interface utilisateur
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 12%

---

# Surveillance des flux de données pour les profils dans l’interface utilisateur

Le profil client en temps réel offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le profil vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

Le tableau de bord de surveillance vous fournit une représentation visuelle de l’activité des données dans Profile, y compris le statut des profils de vos données. Ce tutoriel explique comment utiliser le tableau de bord de surveillance pour surveiller les profils de vos données à l’aide de l’interface utilisateur d’Experience Platform, ce qui vous permet de suivre l’état du traitement des profils.

## Prise en main {#getting-started}

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [Flux de données](../home.md) : les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Experience Platform. Les flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers des jeux de données cibles, vers [!DNL Identity] et [!DNL Profile], et vers [!DNL Destinations].
   - [Exécutions de flux de données](../../sources/notifications.md) : les exécutions de flux de données sont les tâches planifiées récurrentes en fonction de la configuration de la fréquence des flux de données sélectionnés.
- [Profil client en temps réel](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [Sandbox](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Tableau de bord de surveillance des profils {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="Traitement des profils"
>abstract="La vue Traitement des profils contient des informations sur les enregistrements ingérés dans le service Profil, notamment le nombre de fragments de profil créés, mis à jour et le nombre total de fragments de profil."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="Détails de l’exécution du flux de données"
>abstract="La page Détails de l&#39;exécution du flux de données affiche plus d&#39;informations sur votre exécution du flux de données de Profil, y compris son identifiant d&#39;organisation et son identifiant d&#39;exécution du flux de données."

Pour accéder au tableau de bord **[!UICONTROL Profils]**, sélectionnez **[!UICONTROL Surveillance]** dans le volet de navigation de gauche. Une fois sur la page **[!UICONTROL Surveillance]**, sélectionnez la vignette **[!UICONTROL Profils]**.

![Carte Profils . Des informations sur le nombre d’enregistrements reçus, le nombre de fragments de profil créés et mis à jour, ainsi que le taux de succès s’affichent.](../assets/ui/monitor-profiles/focus-card.png)

Dans le tableau de bord principal **[!UICONTROL Profils]**, la carte **[!UICONTROL Profils]** affiche des informations sur le nombre total d’enregistrements reçus, le nombre de fragments de profil créés et mis à jour, ainsi que le taux de succès des fragments de profil créés et mis à jour.

Le tableau de bord lui-même contient des mesures sur le traitement des profils. Par défaut, le tableau de bord affiche les détails du traitement des profils pour les sources de votre organisation au cours des dernières 24 heures.

![Le tableau de bord Profils . Des informations sur le nombre d’enregistrements de profil reçus par source s’affichent.](../assets/ui/monitor-profiles/sources.png)

La page [!UICONTROL Traitement des profils] contient des informations sur les enregistrements ingérés dans [!DNL Profile], notamment le nombre de fragments de profil créés, mis à jour et le nombre total de fragments de profil.

Les mesures suivantes sont disponibles pour cette vue de tableau de bord :

| Mesure | Description |
| -------| ----------- |
| **[!UICONTROL Nom du Source]** | Nom de la source. |
| **[!UICONTROL Enregistrements reçus]** | Nombre d’enregistrements reçus du lac de données. |
| **[!UICONTROL Échec des enregistrements]** | Nombre d’enregistrements ingérés, mais non intégrés dans [!DNL Profile] en raison d’erreurs. |
| **[!UICONTROL Fragments de profil créés]** | Nombre de nouveaux fragments de [!DNL Profile] nets ajoutés. |
| **[!UICONTROL Fragments de profil mis à jour]** | Nombre de fragments de [!DNL Profile] existants mis à jour. |
| **[!UICONTROL Nombre total de fragments de profil]** | Nombre total d’enregistrements écrits dans [!DNL Profile], y compris tous les fragments de [!DNL Profile] existants mis à jour et les nouveaux fragments de [!DNL Profile] créés. |
| **[!UICONTROL Nombre total de flux de données ayant échoué]** | Nombre d’exécutions de flux de données ayant échoué. |

Vous pouvez sélectionner l’icône de filtre ![icône de filtre](/help/images/icons/filter.png) à côté du nom de la source pour afficher les informations de traitement du profil pour les flux de données de cette source sélectionnée.

![L’icône de filtre est mise en surbrillance. En sélectionnant cette icône, vous pouvez afficher les flux de données de la source sélectionnée.](../assets/ui/monitor-profiles/sources-filter.png)

Vous pouvez également sélectionner **[!UICONTROL Flux de données]** sur le bouton (bascule) pour afficher les détails du traitement du profil pour les flux de données de votre entreprise au cours des dernières 24 heures.

![Le tableau de bord Profils . Des informations sur le nombre d’enregistrements de profil reçus par flux de données s’affichent.](../assets/ui/monitor-profiles/dataflows.png)

Les mesures suivantes sont disponibles pour cette vue de tableau de bord :

| Mesure | Description |
| -------| ----------- |
| **[!UICONTROL Flux de données]** | Nom du flux de données. |
| **[!UICONTROL Jeu de données]** | Nom du jeu de données vers lequel le flux de données est inséré. |
| **[!UICONTROL Nom du Source]** | Nom de la source à laquelle appartient le flux de données. |
| **[!UICONTROL Enregistrements reçus**] | Nombre d’enregistrements reçus du lac de données. |
| **[!UICONTROL Échec des enregistrements]** | Nombre d’enregistrements ingérés, mais non intégrés dans [!DNL Profile] en raison d’erreurs. |
| **[!UICONTROL Fragments de profil créés]** | Nombre de nouveaux fragments de [!DNL Profile] nets ajoutés. |
| **[!UICONTROL Fragments de profil mis à jour]** | Nombre de fragments de [!DNL Profile] existants mis à jour |
| **[!UICONTROL Nombre total de fragments de profil]** | Nombre total d’enregistrements écrits dans [!DNL Profile], y compris tous les fragments de [!DNL Profile] existants mis à jour et les nouveaux fragments de [!DNL Profile] créés. |
| **[!UICONTROL Nombre total d’exécutions de flux ayant échoué]** | Nombre d’exécutions de flux de données ayant échoué. |
| **[!UICONTROL Dernière active]** | Date et heure de la dernière exécution du flux de données. |

Sélectionnez l’icône de filtre ![filtre](/help/images/icons/filter.png) à côté de l’heure de début de l’exécution du flux de données pour afficher plus d’informations sur votre exécution de flux de données [!DNL Profile].

![L’icône de filtre est mise en surbrillance. En sélectionnant cette icône, vous pouvez afficher des détails sur le flux de données sélectionné.](../assets/ui/monitor-profiles/dataflows-filter.png)

La page [!UICONTROL Détails de l’exécution du flux de données] affiche plus d’informations sur votre exécution de flux de données [!DNL Profile], y compris son identifiant d’organisation et son identifiant d’exécution de flux de données. Cette page affiche également le code d’erreur et le message d’erreur correspondants fournis par [!DNL Profile] en cas d’erreur dans le processus d’ingestion.

![Un tableau de bord présentant des informations détaillées sur le flux de données sélectionné s’affiche.](../assets/ui/monitor-profiles/dataflow-run-details.png)

Les mesures suivantes sont disponibles pour cette vue de tableau de bord :

| Mesure | Description |
| -------| ----------- |
| **[!UICONTROL Enregistrements reçus]** | Nombre d’enregistrements reçus du lac de données. |
| **[!UICONTROL Échec des enregistrements]** | Nombre d’enregistrements ingérés, mais non intégrés dans [!DNL Profile] en raison d’erreurs. |
| **[!UICONTROL Fragments de profil créés]** | Nombre de nouveaux fragments de [!DNL Profile] nets ajoutés. |
| **[!UICONTROL Fragments de profil mis à jour]** | Nombre de fragments de [!DNL Profile] existants mis à jour. |
| **[!UICONTROL Statut]** | Définit le statut global d’un flux de données. Les valeurs de statut possibles sont les suivantes : <ul><li>`Success` : indique qu’un flux de données est actif et ingère des données en fonction du planning qui lui a été fourni.</li><li>`Failed` : indique que le processus d’activation d’un flux de données a été interrompu en raison d’erreurs. </li><li>`Processing` : indique que le flux de données n’est pas encore actif. Ce statut se rencontre souvent immédiatement après la création d’un nouveau flux de données.</li></ul> |
| **[!UICONTROL Démarrage de l’exécution du flux de données]** | Date et heure auxquelles le flux de données a commencé à s’exécuter. |
| **[!UICONTROL Dernière mise à jour]** | Date et heure de la dernière mise à jour du flux de données. |
| **[!UICONTROL Résumé des erreurs]** | Si l’exécution du flux de données a échoué, un code d’erreur et un résumé des raisons de l’échec de l’exécution du flux de données s’affichent. |
| **[!UICONTROL ID d’exécution du flux de données]** | Identifiant de l’exécution du flux de données. |
| **[!UICONTROL ID d’organisation IMS]** | Identifiant d’organisation auquel appartient l’exécution du flux de données. |

De plus, vous pouvez sélectionner le bouton (bascule) pour afficher les enregistrements ayant échoué ou les enregistrements ayant été ignorés. La section Erreurs comprend des détails sur le code d’erreur et le nombre d’enregistrements ayant échoué ou exclus.
