---
keywords: Experience Platform;accueil;rubriques les plus consultées;surveiller les profils;surveiller les flux de données;flux de données;profil;profil client en temps réel;
description: Le profil client en temps réel offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Ce tutoriel explique comment surveiller les flux de données avec les profils à l’aide de l’interface utilisateur d’Experience Platform.
title: Surveillance des flux de données pour les profils dans l’interface utilisateur
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: 1d60afdf486642398a2d31302db339eb9cb45130
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 11%

---

# Surveillance des flux de données pour les profils dans l’interface utilisateur

Le profil client en temps réel offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le profil vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

Le tableau de bord de surveillance vous fournit une représentation visuelle de l’activité des données dans Profile, y compris le statut des profils de vos données. Ce tutoriel explique comment utiliser le tableau de bord de surveillance pour surveiller les profils de vos données à l’aide de l’interface utilisateur d’Experience Platform, ce qui vous permet de suivre l’état du traitement des profils.

## Prise en main {#getting-started}

Ce guide nécessite une compréhension professionnelle des composants suivants d&#39;Adobe Experience Platform :

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

Pour accéder au tableau de bord **[!UICONTROL Profiles]**, sélectionnez **[!UICONTROL Monitoring]** dans le volet de navigation de gauche. Une fois sur la page **[!UICONTROL Monitoring]**, sélectionnez la carte **[!UICONTROL Profiles]** .

![Carte Profils . Des informations sur le nombre d’enregistrements reçus, le nombre de fragments de profil créés et mis à jour, ainsi que le taux de succès s’affichent.](../assets/ui/monitor-profiles/focus-card.png)

Dans le tableau de bord de **[!UICONTROL Profiles]** principal, la carte de **[!UICONTROL Profiles]** affiche des informations sur le nombre total d’enregistrements reçus, le nombre de fragments de profil créés et mis à jour, ainsi que le taux de succès des fragments de profil créés et mis à jour.

Le tableau de bord lui-même contient des mesures sur le traitement des profils. Par défaut, le tableau de bord affiche les détails du traitement des profils pour les sources de votre organisation au cours des dernières 24 heures.

![Le tableau de bord Profils . Des informations sur le nombre d’enregistrements de profil reçus par source s’affichent.](../assets/ui/monitor-profiles/sources.png)

La page [!UICONTROL Profile processing] contient des informations sur les enregistrements ingérés dans [!DNL Profile], notamment le nombre de fragments de profil créés, mis à jour et le nombre total de fragments de profil.

Les mesures suivantes sont disponibles pour cette vue de tableau de bord :

| Mesure | Description |
| -------| ----------- |
| **[!UICONTROL Source name]** | Nom de la source. |
| **[!UICONTROL Records received]** | Nombre d’enregistrements reçus du lac de données. |
| **[!UICONTROL Records failed]** | Nombre d’enregistrements ingérés, mais non intégrés dans [!DNL Profile] en raison d’erreurs. |
| **[!UICONTROL Profile fragments created]** | Nombre de nouveaux fragments de [!DNL Profile] nets ajoutés. |
| **[!UICONTROL Profile fragments updated]** | Nombre de fragments de [!DNL Profile] existants mis à jour. |
| **[!UICONTROL Total Profile fragments]** | Nombre total d’enregistrements écrits dans [!DNL Profile], y compris tous les fragments de [!DNL Profile] existants mis à jour et les nouveaux fragments de [!DNL Profile] créés. |
| **[!UICONTROL Total failed dataflows]** | Nombre d’exécutions de flux de données ayant échoué. |

Vous pouvez sélectionner l’icône de filtre ![icône de filtre](/help/images/icons/filter.png) à côté du nom de la source pour afficher les informations de traitement du profil pour les flux de données de cette source sélectionnée.

Vous pouvez également sélectionner **[!UICONTROL Dataflows]** sur le bouton (bascule) pour afficher les détails du traitement du profil pour les flux de données de votre entreprise au cours des dernières 24 heures.

![Le tableau de bord Profils . Des informations sur le nombre d’enregistrements de profil reçus par flux de données s’affichent.](../assets/ui/monitor-profiles/dataflows.png)

Les mesures suivantes sont disponibles pour cette vue de tableau de bord :

| Mesure | Description |
| -------| ----------- |
| **[!UICONTROL Dataflow]** | Nom du flux de données. |
| **[!UICONTROL Dataset]** | Nom du jeu de données vers lequel le flux de données est inséré. |
| **[!UICONTROL Source name]** | Nom de la source à laquelle appartient le flux de données. |
| **[!UICONTROL Data type]** | Type de données reçu du jeu de données. |
| **[!UICONTROL Records received**] | Nombre d’enregistrements reçus du lac de données. |
| **[!UICONTROL Records failed]** | Nombre d’enregistrements ingérés, mais non intégrés dans [!DNL Profile] en raison d’erreurs. |
| **[!UICONTROL Profile fragments created]** | Nombre de nouveaux fragments de [!DNL Profile] nets ajoutés. |
| **[!UICONTROL Profile fragments updated]** | Nombre de fragments de [!DNL Profile] existants mis à jour |
| **[!UICONTROL Total Profile fragments]** | Nombre total d’enregistrements écrits dans [!DNL Profile], y compris tous les fragments de [!DNL Profile] existants mis à jour et les nouveaux fragments de [!DNL Profile] créés. |
| **[!UICONTROL Total failed flow runs]** | Nombre d’exécutions de flux de données ayant échoué. |
| **[!UICONTROL Last active]** | Date et heure de la dernière exécution du flux de données. |

Sélectionnez l’icône de filtre ![filtre](/help/images/icons/filter.png) à côté de l’heure de début de l’exécution du flux de données pour afficher plus d’informations sur votre exécution de flux de données [!DNL Profile].

Un tableau de bord affichant toutes les exécutions de flux de données s’affiche. Ce tableau de bord contient des mesures sur les exécutions de flux de données ainsi que des graphiques qui montrent le taux de succès, les fragments de profil créés et les fragments de profil mis à jour.

![Le flux de données exécute le tableau de bord. Des informations sur les exécutions de flux de données s’affichent.](../assets/ui/monitor-profiles/dataflow-run.png)

Les mesures suivantes sont disponibles pour cette vue de tableau de bord :

>[!NOTE]
>
>Lorsque l’exécution du flux de données est à l’état **[!UICONTROL Processing]**, vous pouvez consulter des informations sur la préparation en consultant les statuts des points de contrôle dans le processus d’ingestion.
>
>![La bulle de préparation à l’ingestion du profil s’affiche.](../assets/ui/monitor-profiles/profile-ingestion-readiness.png){zoomable="yes" width="300"}

| Mesure | Description |
| ------ | ----------- |
| **[!UICONTROL Dataflow run start]** | Heure à laquelle l’exécution du flux de données a démarré en UTC. |
| **[!UICONTROL Data type]** | Type de données reçu par le flux de données. |
| **[!UICONTROL Records received]** | Nombre d’enregistrements reçus du lac de données. |
| **[!UICONTROL Records failed]** | Nombre d’enregistrements ingérés, mais non intégrés dans [!DNL Profile] en raison d’erreurs. |
| **[!UICONTROL Profile fragments created]** | Nombre de nouveaux fragments de [!DNL Profile] nets ajoutés. |
| **[!UICONTROL Profile fragments updated]** | Nombre de fragments de [!DNL Profile] existants mis à jour. |
| **[!UICONTROL Total profile fragments]** | Nombre total d’enregistrements écrits dans [!DNL Profile], y compris tous les fragments de [!DNL Profile] existants mis à jour et les nouveaux fragments de [!DNL Profile] créés. |
| **[!UICONTROL Processing time]** | Temps nécessaire à l’exécution du flux de données pour le traitement. |
| **[!UICONTROL Status]** | Statut de l’exécution du flux de données. Les valeurs possibles sont [!UICONTROL Success], [!UICONTROL Failed], [!UICONTROL Queued] et [!UICONTROL Processing]. |
| **[!UICONTROL Ready for customer segmentation]** | Un statut indiquant si les enregistrements ingérés sont prêts à être utilisés dans la segmentation client. Les valeurs possibles sont [!UICONTROL Yes], [!UICONTROL Failed], [!UICONTROL Queued] et [!UICONTROL Processing]. Même si le **Statut** du flux de données est en cours de traitement, si la valeur de ce champ est Oui, vous pouvez utiliser les profils dans la segmentation de la clientèle. |
| **[!UICONTROL Ready for lookup]** | Statut indiquant si les enregistrements ingérés sont prêts à être utilisés dans la recherche Adobe Journey Optimizer.  Les valeurs possibles sont [!UICONTROL Yes], [!UICONTROL Failed], [!UICONTROL Queued] et [!UICONTROL Processing]. Même si le **Statut** du flux de données est en cours de traitement, si la valeur de ce champ est Oui, vous pouvez utiliser les profils dans la recherche Journey Optimizer. |

La page [!UICONTROL Dataflow run details] affiche plus d’informations sur votre exécution de flux de données [!DNL Profile], y compris son identifiant d’organisation et son identifiant d’exécution de flux de données. Cette page affiche également le code d’erreur et le message d’erreur correspondants fournis par [!DNL Profile] en cas d’erreur dans le processus d’ingestion.

![Un tableau de bord présentant des informations détaillées sur le flux de données sélectionné s’affiche.](../assets/ui/monitor-profiles/dataflow-run-details.png)

Les mesures suivantes sont disponibles pour cette vue de tableau de bord :

| Mesure | Description |
| -------| ----------- |
| **[!UICONTROL Records received]** | Nombre d’enregistrements reçus du lac de données. |
| **[!UICONTROL Records failed]** | Nombre d’enregistrements ingérés, mais non intégrés dans [!DNL Profile] en raison d’erreurs. |
| **[!UICONTROL Profile fragments created]** | Nombre de nouveaux fragments de [!DNL Profile] nets ajoutés. |
| **[!UICONTROL Profile fragments updated]** | Nombre de fragments de [!DNL Profile] existants mis à jour. |
| **[!UICONTROL Status]** | Définit le statut global d’un flux de données. Les valeurs de statut possibles sont les suivantes : <ul><li>`Success` : indique qu’un flux de données est actif et ingère des données en fonction du planning qui lui a été fourni.</li><li>`Failed` : indique que le processus d’activation d’un flux de données a été interrompu en raison d’erreurs. </li><li>`Processing` : indique que le flux de données n’est pas encore actif. Ce statut se rencontre souvent immédiatement après la création d’un nouveau flux de données.</li></ul> |
| **[!UICONTROL Dataflow run start]** | Date et heure auxquelles le flux de données a commencé à s’exécuter. |
| **[!UICONTROL Last updated]** | Date et heure de la dernière mise à jour du flux de données. |
| **[!UICONTROL Error summary]** | Si l’exécution du flux de données a échoué, un code d’erreur et un résumé des raisons de l’échec de l’exécution du flux de données s’affichent. |
| **[!UICONTROL Dataflow run ID]** | Identifiant de l’exécution du flux de données. |
| **[!UICONTROL IMS org ID]** | Identifiant d’organisation auquel appartient l’exécution du flux de données. |

De plus, vous pouvez sélectionner le bouton (bascule) pour afficher les enregistrements ayant échoué ou les enregistrements ayant été ignorés. La section Erreurs comprend des détails sur le code d’erreur et le nombre d’enregistrements ayant échoué ou exclus.
