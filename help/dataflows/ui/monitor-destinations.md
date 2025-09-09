---
description: Découvrez comment surveiller les flux de données pour les destinations à l’aide de l’interface utilisateur d’Experience Platform.
solution: Experience Platform
title: Surveillance des flux de données pour les destinations dans l’interface utilisateur
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 9d92999df8e35ac6223986ece8a98af72ab6ace8
workflow-type: tm+mt
source-wordcount: '3623'
ht-degree: 11%

---

# Surveillance des flux de données pour les destinations dans l’interface utilisateur

Utilisez les différentes destinations du catalogue Experience Platform pour activer vos données d’Experience Platform vers d’innombrables partenaires externes. Experience Platform facilite le processus de suivi du flux de données vers les destinations en offrant de la transparence aux flux de données.

Le tableau de bord de surveillance vous fournit une représentation visuelle du parcours d’un flux de données, y compris la destination vers laquelle les données sont activées, le type de données que vous consultez, les données exportées par exécution de flux de données, etc.

Ce tutoriel vous explique comment surveiller les flux de données directement dans l’espace de travail des destinations ou utiliser le tableau de bord de surveillance pour surveiller les flux de données vers vos destinations à l’aide de l’interface utilisateur d’Experience Platform.

## Prise en main {#getting-started}

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [Flux de données](../home.md) : les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Experience Platform. Les flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers des jeux de données cibles, vers [!DNL Identity] et [!DNL Profile], et vers [!DNL Destinations].
   - [Exécutions de flux de données](../../sources/notifications.md) : les exécutions de flux de données sont les tâches planifiées récurrentes en fonction de la configuration de la fréquence des flux de données sélectionnés.
- [Destinations](../../destinations/home.md) : les destinations sont des intégrations préconfigurées aux applications couramment utilisées. Elles permettent l’activation transparente des données d’Experience Platform pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.
- [Sandbox](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Surveillance des flux de données dans l’espace de travail des destinations {#monitor-dataflows-in-the-destinations-workspace}

Dans l’espace de travail **[!UICONTROL Destinations]** de l’interface utilisateur d’Experience Platform, accédez à l’onglet **[!UICONTROL Parcourir]** et sélectionnez le nom d’une destination que vous souhaitez afficher.

![Sélectionner la vue de destination avec une connexion de destination mise en surbrillance](../assets/ui/monitor-destinations/select-destination.png)

Une liste des flux de données existants s’affiche. Sur cette page, vous trouverez une liste des flux de données visibles, y compris des informations sur leur destination, leur nom d’utilisateur, le nombre de flux de données et leur statut.

Pour plus d’informations sur les statuts, consultez le tableau suivant :

| État | Description |
| ------ | ----------- |
| Activé | Le statut `Enabled` indique qu’un flux de données est actif et exporte les données selon le planning qui lui a été fourni. |
| Désactivé | Le statut `Disabled` indique qu’un flux de données est inactif et n’exporte aucune donnée. |
| En cours de traitement | Le statut `Processing` indique qu’un flux de données n’est pas encore actif. Ce statut se rencontre souvent immédiatement après la création d’un nouveau flux de données. |
| Erreur | Le statut `Error` indique que le processus d’activation d’un flux de données a été interrompu. |

### Exécutions de flux de données pour les destinations de diffusion en continu {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="Détails de l’exécution du flux de données"
>abstract="Les détails de l’exécution du flux de données de destination contiennent des informations sur le statut d’activation d’une audience et et des mesures obtenues à partir du profil client en temps réel pour générer des identités uniques. Pour en savoir plus, consultez le guide des définitions des mesures."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="Profils reçus"
>abstract="Nombre total de profils reçus dans le flux de données. Cette valeur est mise à jour toutes les 60 minutes."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="Identités activées"
>abstract="Le nombre d&#39;identités de profil individuel activées avec succès vers la destination sélectionnée. Cette mesure inclut les identités qui sont créées, mises à jour et supprimées dans les audiences exportées."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="Identités exclues"
>abstract="Le nombre d&#39;enregistrements de profil individuel exclus de l&#39;activation pour la destination sélectionnée en fonction des attributs manquants et de la violation du consentement."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="Identités ayant échoué"
>abstract="Le nombre d&#39;identités de profil individuel qui ont échoué pour la destination sélectionnée. Pour plus d&#39;informations, consultez les diagnostics d&#39;erreur."

Pour les destinations de diffusion en continu, l’onglet [!UICONTROL Exécutions de flux de données] fournit une mise à jour horaire des données de mesure sur vos exécutions de flux de données. Les statistiques les plus importantes étiquetées concernent les identités.

Les identités représentent les différentes facettes d’un profil. Par exemple, si un profil contient à la fois un numéro de téléphone et une adresse e-mail, ce profil possède deux identités.

Une liste d’exécutions individuelles et de leurs mesures spécifiques s’affiche, ainsi que les totaux suivants pour les identités :

- **[!UICONTROL Identités activées]** : nombre total d’identités de profil activées vers la destination sélectionnée. Cette mesure inclut les identités qui sont créées, mises à jour et supprimées dans les audiences exportées.
- **[!UICONTROL Identités exclues]** : nombre total d’identités de profil qui sont ignorées pour l’activation en fonction des attributs manquants et de la violation du consentement.
- **[!UICONTROL Identités en échec]** : nombre total d’identités de profil qui ne sont pas activées vers la destination en raison d’erreurs.

![Le flux de données exécute les détails des destinations de diffusion en streaming.](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Chaque exécution de flux de données affiche les détails suivants :

- **[!UICONTROL Démarrage de l’exécution du flux de données]** : heure de démarrage de l’exécution du flux de données. Pour les exécutions de flux de données en continu, Experience Platform capture les mesures en fonction du début de l’exécution du flux de données, sous la forme de mesures horaires. Cela signifie que pour les exécutions de flux de données en continu, si une exécution de flux de données a démarré, par exemple à 10 :30PM, la mesure affiche l’heure de début à 10 :00 dans l’interface utilisateur.
- **[!UICONTROL Temps de traitement]** : temps nécessaire à l’exécution du flux de données.
   - Pour les exécutions **[!UICONTROL terminées]**, la mesure Temps de traitement affiche toujours une heure.
   - Pour les exécutions de flux de données qui sont toujours à l’état **[!UICONTROL traitement]**, la fenêtre permettant de capturer toutes les mesures reste ouverte pendant plus d’une heure, afin de traiter toutes les mesures qui correspondent à l’exécution du flux de données. Par exemple, une exécution de flux de données ayant démarré à 9 :30 peut rester en état de traitement pendant une heure et trente minutes pour capturer et traiter toutes les mesures. Ensuite, une fois la fenêtre de traitement fermée et le statut de l’exécution du flux de données mis à jour sur **terminé**, le temps de traitement affiché est remplacé par une heure.
- **[!UICONTROL Profils reçus]** : nombre total de profils reçus dans le flux de données.
- **[!UICONTROL Identités activées]** : nombre total d’identités de profil qui ont été activées avec succès vers la destination sélectionnée dans le cadre de l’exécution du flux de données. Cette mesure inclut les identités qui sont créées, mises à jour et supprimées dans les audiences exportées.
- **[!UICONTROL Identités exclues]** : nombre total d’identités de profil qui sont exclues de l’activation en fonction des attributs manquants et de la violation du consentement.
- **[!UICONTROL Identités ayant échoué]** Nombre total d’identités de profil qui ne sont pas activées vers la destination en raison d’erreurs.

  >[!IMPORTANT]
  >
  > Depuis mars 2025, Adobe propose une mise à jour améliorant la précision des rapports pour les destinations de streaming. Cette amélioration assure un meilleur alignement entre les rapports dans Experience Platform et les plateformes de destination.
  >
  > Avant cette mise à jour, **[!UICONTROL Identités en échec]** incluait toutes les reprises d’activation. Après cette mise à jour, seule la dernière reprise d’activation est incluse dans le nombre total.
  > 
  > Cette amélioration s’applique à toutes les destinations de diffusion en continu.
  > Suite à cette amélioration, les utilisateurs des destinations de diffusion en continu peuvent voir une baisse attendue de leur nombre d’**[!UICONTROL identités en échec]**.


- **[!UICONTROL Taux d’activation]** : pourcentage d’identités reçues qui ont été activées avec succès. La formule suivante montre comment cette valeur est calculée :
  ![Formule du taux d’activation.](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Statut]** : représente le statut du flux de données : [!UICONTROL Terminé] ou [!UICONTROL Traitement]. [!UICONTROL Terminé] signifie que toutes les identités pour l’exécution du flux de données correspondant ont été exportées au cours d’une période d’une heure. [!UICONTROL Traitement] signifie que l’exécution du flux de données n’est pas encore terminée.

Pour afficher les détails d’une exécution de flux de données spécifique, sélectionnez l’heure de début de l’exécution dans la liste.

La page de détails d’une exécution de flux de données contient des informations supplémentaires, telles que le nombre de profils reçus, le nombre d’identités activées, le nombre d’identités ayant échoué et le nombre d’identités exclues.

![Détails du flux de données pour les destinations de diffusion en streaming.](../assets/ui/monitor-destinations/dataflow-details-stream.png)

La page de détails affiche également une liste des identités ayant échoué et des identités ayant été exclues. Des informations sur les identités en échec et exclues s’affichent, notamment le code d’erreur, le nombre d’identités et la description. Par défaut, la liste affiche les identités en échec. Pour afficher les identités ignorées, activez le bouton (bascule) **[!UICONTROL Identités exclues]**.

![Enregistrements de flux de données pour les destinations de diffusion en continu avec un message d’erreur en surbrillance.](../assets/ui/monitor-destinations/dataflow-records-stream.png)

#### [!BADGE Beta &#x200B;]{type=Informative} Surveillance de l’exécution du flux de données au niveau de l’audience pour les destinations de diffusion en streaming {#audience-level-dataflow-runs-for-streaming-destinations}

Vous pouvez afficher des informations sur les identités activées, exclues ou en échec réparties au niveau de l’audience, pour chaque audience qui fait partie du flux de données.

La surveillance au niveau de l’audience pour les destinations de diffusion en streaming est actuellement disponible uniquement pour les destinations suivantes :

- [Connexion [!DNL (API) Oracle Eloqua]](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)
- [[!DNL (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)
- [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md)
- [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)
- [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)
- [[!DNL Google Customer Match + Display & Video 360]](../../destinations/catalog/advertising/google-customer-match-dv360.md)
- [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md)
- [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md)
- [[!DNL Magnite: Real-time]](../../destinations/catalog/advertising/magnite-streaming.md)
- [[!DNL Marketo Engage Person Sync]](../../destinations/catalog/adobe/marketo-engage-person-sync.md)
- [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md)
- [[!DNL Moengage]](../../destinations/catalog/mobile-engagement/moengage.md)
- [[!DNL Outreach]](../../destinations/catalog/crm/outreach.md)
- [[!DNL PubMatic Connect]](../../destinations/catalog/advertising/pubmatic.md)
- [[!DNL PubMatic Connect (Custom Audience ID Mapping)]](../../destinations/catalog/advertising/pubmatic.md)
- [[!DNL Qualtrics Automations]](../../destinations/catalog/survey/qualtrics-automations.md)
- [[!DNL RainFocus Attendee Profiles]](../../destinations/catalog/marketing-automation/rainfocus.md)
- [[!DNL SAP Commerce]](../../destinations/catalog/ecommerce/sap-commerce.md)
- [[!DNL Snowflake]](../../destinations/catalog/cloud-storage/snowflake.md)
- [[!DNL Yahoo DataX]](../../destinations/catalog/advertising/datax.md)
- [[!DNL Zendesk]](../../destinations/catalog/crm/zendesk.md)

![Surveillance au niveau de l’audience pour les destinations de diffusion en streaming.](/help/dataflows/assets/ui/monitor-destinations/audience-level-monitoring-streaming.png)

>[!NOTE]
>
>Le nombre **[!UICONTROL Profils reçus]** de l’onglet **[!UICONTROL Audiences]** peut ne pas toujours correspondre au nombre de profils reçus pour l’exécution du flux de données. Cela est dû au fait qu’un profil donné peut faire partie de plusieurs audiences activées dans l’exécution du flux de données.

### Exécutions de flux de données pour les destinations par lots {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="Détails de l’exécution du flux de données"
>abstract="Les détails de l’exécution du flux de données de destination contiennent des informations sur le statut d’activation d’une audience et et des mesures obtenues à partir du profil client en temps réel pour générer des identités uniques. Pour en savoir plus, consultez le guide des définitions des mesures."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-destinations.html?lang=fr#dataflow-runs-for-streaming-destinations" text="Exécutions de flux de données pour les destinations de diffusion en continu"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="Profils reçus"
>abstract="Nombre total de profils reçus dans le flux de données. Cette valeur est mise à jour toutes les 60 minutes."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="Identités activées"
>abstract="Le nombre d&#39;identités de profil individuel activées avec succès vers la destination sélectionnée. Cette mesure inclut les identités qui sont créées, mises à jour et supprimées dans les audiences exportées."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="Identités exclues"
>abstract="Le nombre d&#39;enregistrements de profil individuel exclus de l&#39;activation pour la destination sélectionnée en fonction des attributs manquants et de la violation du consentement."

Pour les destinations par lots, l’onglet [!UICONTROL Exécutions de flux de données] fournit des données de mesure sur vos exécutions de flux de données. Une liste d’exécutions individuelles et de leurs mesures spécifiques s’affiche, ainsi que les totaux suivants pour les identités :

- **[!UICONTROL Identités activées]** : nombre total d’identités de profil activées vers la destination sélectionnée. Cette mesure inclut les identités qui sont créées, mises à jour et supprimées dans les audiences exportées.
- **[!UICONTROL Identités exclues]** : nombre d’identités de profils individuels exclues de l’activation pour la destination sélectionnée, en fonction des attributs manquants et de la violation du consentement.

![Vue Exécutions de flux de données pour les destinations par lots.](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Chaque exécution de flux de données affiche les détails suivants :

- **[!UICONTROL Démarrage de l’exécution du flux de données]** : heure de démarrage de l’exécution du flux de données.
- **[!UICONTROL Audience]** : nom de l’audience associée à chaque exécution du flux de données.
- **[!UICONTROL Temps de traitement]** : temps nécessaire au traitement de l’exécution du flux de données.
- **[!UICONTROL Profils reçus]** : nombre total de profils reçus dans le flux de données. Cette valeur est mise à jour toutes les 60 minutes.
- **[!UICONTROL Identités activées]** : nombre total d’identités de profil qui ont été activées avec succès vers la destination sélectionnée dans le cadre de l’exécution du flux de données. Cette mesure inclut les identités qui sont créées, mises à jour et supprimées dans les audiences exportées.
- **[!UICONTROL Identités exclues]** : nombre total d’identités de profil qui sont exclues de l’activation en fonction des attributs manquants et de la violation du consentement.
- **[!UICONTROL Statut]** : représente le statut du flux de données. Il peut s’agir de l’un des trois états suivants : [!UICONTROL &#x200B; Succès &#x200B;], [!UICONTROL &#x200B; Échec &#x200B;] et [!UICONTROL &#x200B; Traitement &#x200B;]. [!UICONTROL Succès] signifie que le flux de données est actif et exporte les données selon son planning fourni. [!UICONTROL &#x200B; Échec &#x200B;] signifie que l’activation des données a été suspendue en raison d’erreurs. Le [!UICONTROL Traitement] signifie que le flux de données n’est pas encore actif et qu’il est généralement rencontré lors de la création d’un nouveau flux de données.

Pour afficher les détails d’une exécution de flux de données spécifique, sélectionnez l’heure de début de l’exécution dans la liste.

>[!NOTE]
>
>Les exécutions de flux de données sont générées en fonction de la fréquence de planification du flux de données de destination. Une exécution de flux de données distincte est effectuée pour chaque [politique de fusion](../../profile/merge-policies/overview.md) appliquée à une audience.

La page de détails d’un flux de données, en plus des détails affichés dans la liste des flux de données, affiche des informations plus spécifiques sur le flux de données :

- **[!UICONTROL Taille des données]** : la taille du flux de données en cours d’exportation.
- **[!UICONTROL Nombre total de fichiers]** : nombre total de fichiers exportés dans le flux de données.
- **[!UICONTROL Dernière mise à jour]** : heure de la dernière mise à jour de l’exécution du flux de données.

![Détails d’exécution du flux de données pour les destinations par lots.](../assets/ui/monitor-destinations/dataflow-batch.png)

La page de détails affiche également une liste des identités ayant échoué et des identités ayant été exclues. Des informations sur les identités en échec et exclues s’affichent, y compris le code et la description de l’erreur. Par défaut, la liste affiche les identités en échec. Pour afficher les identités exclues, activez le bouton (bascule) **[!UICONTROL Identités exclues]**.

![Enregistrements de flux de données pour les destinations par lots avec un message d’erreur en surbrillance.](../assets/ui/monitor-destinations/dataflow-records-batch.png)

### Afficher dans la surveillance {#view-in-monitoring}

Vous pouvez également choisir d’afficher des informations riches sur un certain flux de données et son exécution dans le tableau de bord de surveillance. Pour afficher des informations sur un flux de données dans le tableau de bord de surveillance :

1. Accédez à l’onglet **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]**
2. Accédez au flux de données à inspecter.
3. Sélectionnez le symbole représentant des points de suspension et ![icône de surveillance](/help/images/icons/monitoring.png) **[!UICONTROL Afficher dans la surveillance]**.

![Sélectionnez Afficher dans la surveillance dans le workflow des destinations pour obtenir plus d’informations sur un flux de données.](/help/dataflows/assets/ui/monitor-destinations/view-in-monitoring.png)

>[!SUCCESS]
>
>Vous pouvez désormais afficher des informations sur le flux de données et les exécutions de flux de données associées dans le tableau de bord de surveillance. Lisez la section ci-dessous pour plus d’informations.

## Tableau de bord de surveillance des destinations {#monitoring-destinations-dashboard}

>[!NOTE]
>
>La fonctionnalité de surveillance des destinations est actuellement prise en charge pour toutes les destinations dans Experience Platform *à l’exception* destinations [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) et [Personnalisation personnalisée](/help/destinations/catalog/personalization/custom-personalization.md).

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="Activation"
>abstract="La vue d’activation de destination contient des informations sur le statut d’activation d’une audience et des mesures obtenues à partir du profil client en temps réel pour générer des identités uniques."

Pour accéder au tableau de bord [!UICONTROL Surveillance], sélectionnez **[!UICONTROL Surveillance]** (![icône de surveillance](/help/images/icons/monitoring.png)) dans le volet de navigation de gauche. Une fois sur la page [!UICONTROL Surveillance], sélectionnez [!UICONTROL Destinations]. Le tableau de bord [!UICONTROL Surveillance] contient des mesures et des informations sur les tâches d’exécution de destination.

Utilisez le tableau de bord [!UICONTROL Destinations] pour avoir une idée globale de l’intégrité de vos flux d’activation. Commencez par obtenir des informations à un niveau agrégé pour toutes les destinations par lots et de diffusion en continu, puis explorez les vues détaillées pour les flux de données, les exécutions de flux de données et les audiences activées pour une analyse approfondie de vos données d’activation. Les écrans du tableau de bord [!UICONTROL Surveillance] fournissent des informations exploitables par le biais de mesures et de descriptions d’erreur afin de vous aider à résoudre les problèmes susceptibles de se produire dans vos scénarios d’activation.

Vous pouvez filtrer les informations affichées par type de données : clients, comptes (pour le B2B edition Adobe Real-Time CDP uniquement), prospects et enrichissement du compte. Pour en savoir plus sur ces options, consultez le [ guide du tableau de bord de surveillance ](/help/dataflows/ui/monitor.md#monitoring-dashboard-overview).

![Filtre de type de données mis en surbrillance dans la vue du tableau de bord de surveillance.](/help/dataflows/assets/ui/monitor-destinations/add-data-filter.png)

Au centre du tableau de bord se trouve le panneau [!UICONTROL Activation], qui contient des mesures et des graphiques qui affichent des données sur le taux d’activation des données exportées vers des destinations de diffusion en continu, ainsi que sur les exécutions de flux de données par lots ayant échoué vers des destinations par lots.

![Graphiques d’activation par flux et par lots mis en surbrillance dans la vue de surveillance.](../assets/ui/monitor-destinations/dashboard-graph.png)


Par défaut, les données affichées contiennent les informations d’activation des dernières 24 heures. Sélectionnez **[!UICONTROL Dernières 24 heures]** pour ajuster la période des enregistrements affichés. Les options disponibles sont les suivantes : **[!UICONTROL 24 dernières heures]**, **[!UICONTROL 7 derniers jours]** et **[!UICONTROL 30 derniers jours]**. Vous pouvez également sélectionner les dates dans la fenêtre pop-up du calendrier qui s’affiche. Une fois les dates sélectionnées, sélectionnez **[!UICONTROL Appliquer]** pour ajuster la période des informations affichées.

>[!NOTE]
>
>La capture d’écran suivante montre le taux d’activation et l’exécution du flux de données par lots au cours des 30 derniers jours au lieu des dernières 24 heures. Vous pouvez ajuster la période en sélectionnant **[!UICONTROL 30 derniers jours]**.

![Modification de la commande de période de recherche arrière mise en surbrillance pour les destinations activées](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

Utilisez l’icône de flèche (![icône de flèche](/help/images/icons/chevron-up.png)) pour développer ou ignorer les cartes en haut de l’écran, qui affichent en un coup d’œil les informations sur les détails d’activation, en fonction du type de destination : diffusion en continu ou lot :

- **[!UICONTROL Taux d’activation en flux continu]** : représente le pourcentage d’identités reçues qui ont été activées avec succès ou ignorées. La formule utilisée pour calculer ce pourcentage est décrite plus haut sur cette page, dans la section [Exécutions de flux de données pour les destinations de diffusion en streaming](#dataflow-runs-for-streaming-destinations).
- **[!UICONTROL Exécutions de flux de données par lot ayant échoué]** : représente le nombre d’exécutions de flux de données ayant échoué dans l’intervalle de temps sélectionné.

![Afficher ou ignorer les vignettes en haut de la page.](../assets/ui/monitor-destinations/monitoring-destinations-toggle-arrow.gif)

Le graphique **[!UICONTROL Activation]** s’affiche par défaut et vous pouvez le désactiver pour développer la liste des destinations ci-dessous. Sélectionnez le bouton (bascule) **[!UICONTROL Mesures et graphiques]** pour désactiver les graphiques.

Le panneau **[!UICONTROL Activation]** affiche une liste des destinations qui contiennent au moins un compte existant. Cette liste inclut également des informations sur les profils reçus, les identités activées, les identités ayant échoué, les identités exclues, le taux d’activation, le nombre total de flux de données ayant échoué et la date de la dernière mise à jour de ces destinations. Toutes les mesures ne sont pas disponibles pour tous les types de destination. Le tableau ci-dessous décrit les mesures et les informations disponibles par type de destination.

| Mesure | Type de destination |
|--------------------------------------|-----------------------|
| **[!UICONTROL Enregistrements reçus]** | Diffusion en continu et par lots |
| **[!UICONTROL Enregistrements activés]** | Diffusion en continu et par lots |
| **[!UICONTROL Échec des enregistrements]** | Diffusion en continu |
| **[!UICONTROL Enregistrements ignorés]** | Diffusion en continu et par lots |
| **[!UICONTROL Type de données]** | Diffusion en continu et par lots |
| **[!UICONTROL Taux d’activation]** | Diffusion en continu |
| **[!UICONTROL Nombre total de flux de données ayant échoué]** | Lot |
| **[!UICONTROL Dernière mise à jour]** | Diffusion en continu et par lots |

{style="table-layout:auto"}

![Tableau de bord de surveillance avec toutes les destinations activées mises en surbrillance.](../assets/ui/monitor-destinations/dashboard-destinations.png)

Vous pouvez également filtrer votre liste de destinations pour n’afficher que la catégorie de destinations sélectionnée. Sélectionnez la liste déroulante **[!UICONTROL Mes destinations]**, puis sélectionnez la [catégorie de destination](/help/destinations/destination-types.md#categories) sur laquelle vous souhaitez appliquer un filtre.

![Filtrer des destinations à l’aide du sélecteur de liste déroulante](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

De plus, vous pouvez saisir une destination dans la barre de recherche pour vous isoler vers une seule destination. Si vous souhaitez afficher les flux de données de la destination, vous pouvez sélectionner le filtre ![filtre](/help/images/icons/filter-add.png) en regard pour afficher la liste de ses flux de données actifs.

![Filtrez les destinations à l’aide de la barre de recherche mise en surbrillance dans la vue de surveillance.](../assets/ui/monitor-destinations/filtered-destinations.png)

Si vous souhaitez afficher tous les flux de données existants sur toutes les destinations, sélectionnez **[!UICONTROL Flux de données]**.

Une liste de flux de données s’affiche, triés selon la dernière exécution du flux de données. Pour afficher des détails supplémentaires sur un flux de données spécifique, localisez la destination à surveiller, sélectionnez le filtre ![filtre](/help/images/icons/filter-add.png) en regard, puis sélectionnez le filtre ![filtre](/help/images/icons/filter-add.png) en regard du flux de données sur lequel vous souhaitez obtenir des informations supplémentaires.

![Tous les flux de données mis en surbrillance dans le tableau de bord de surveillance.](../assets/ui/monitor-destinations/dashboard-dataflows.png)

Une fois que vous avez sélectionné un flux de données pour une inspection plus approfondie, la page de détails du flux de données contient un bouton (bascule) qui vous permet d’afficher les données activées dans le flux de données, réparties par exécution de flux de données ou audience.

### Vue des exécutions de flux de données {#dataflow-runs-view}

Lorsque l’option **[!UICONTROL Exécutions de flux de données]** est sélectionnée, vous pouvez voir une liste d’exécutions de flux de données pour le flux de données sélectionné et des informations supplémentaires sur chaque exécution.

>[!INFO]
>
>Pour les flux de données vers des destinations de diffusion en continu, une exécution de flux de données est divisée en fenêtres horaires. Chaque fenêtre horaire génère un identifiant d’exécution de flux de données correspondant.
>
>Pour les flux de données vers des destinations par lots, une exécution de flux de données correspondante est générée pour chaque audience, en fonction de la fréquence planifiée d’activation des audiences. Par exemple, si vous configurez une activation planifiée quotidienne pour cinq audiences dans le même flux de données de destination, cinq exécutions de flux de données distinctes seront générées chaque jour.

![Panneau exécutions de flux de données avec plusieurs exécutions mises en surbrillance.](../assets/ui/monitor-destinations/dashboard-flow-runs-view.png)

Utilisez le bouton (bascule) **[!UICONTROL Afficher les échecs uniquement]** pour n’afficher que les exécutions ayant échoué pour un flux de données.

![Vue des exécutions de flux de données avec le bouton (bascule) Afficher les échecs uniquement mis en surbrillance](../assets/ui/monitor-destinations/dataflow-runs-show-failures-only.gif)

### Vue au niveau de l’audience {#segment-level-view}

Lorsque l’option **[!UICONTROL Audiences]** est sélectionnée, la liste des audiences qui ont été activées dans le flux de données sélectionné s’affiche, au cours de la période sélectionnée. Cet écran comprend des informations au niveau de l’audience sur les enregistrements activés, les enregistrements exclus, ainsi que le statut et l’heure de la dernière exécution du flux de données. En examinant les mesures pour les enregistrements exclus et activés, vous pouvez vérifier si une audience a été activée ou non.

Par exemple, vous activez une audience appelée « Membres du programme de fidélité en Californie » vers une destination Amazon S3 « Membres du programme de fidélité en Californie en décembre ». Supposons qu’il y ait 100 profils dans l’audience sélectionnée, mais que seuls 80 enregistrements sur 100 contiennent des attributs d’ID de fidélité et que vous ayez défini les règles de mappage d’exportation selon `loyalty.id` besoin. Dans ce cas, au niveau de l’audience, vous verrez 80 enregistrements activés et 20 enregistrements exclus.

>[!IMPORTANT]
>
>Notez les limites actuelles liées aux mesures au niveau de l’audience :
>
>- La vue au niveau de l’audience est actuellement disponible pour les destinations répertoriées ci-dessous. Le déploiement est prévu pour d’autres destinations de diffusion en continu.
>
>   - [[!DNL (API) Oracle Eloqua] Connexion](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)
>   - [[!DNL (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)
>   - [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md)
>   - [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)
>   - [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)
>   - [[!DNL Google Customer Match + Display & Video 360]](../../destinations/catalog/advertising/google-customer-match-dv360.md)
>   - [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md)
>   - [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md)
>   - [[!DNL Magnite: Real-time]](../../destinations/catalog/advertising/magnite-streaming.md)
>   - [[!DNL Marketo Engage Person Sync]](../../destinations/catalog/adobe/marketo-engage-person-sync.md)
>   - [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md)
>   - [[!DNL Moengage]](../../destinations/catalog/mobile-engagement/moengage.md)
>   - [[!DNL Outreach]](../../destinations/catalog/crm/outreach.md)
>   - [[!DNL PubMatic Connect]](../../destinations/catalog/advertising/pubmatic.md)
>   - [[!DNL PubMatic Connect (Custom Audience ID Mapping)]](../../destinations/catalog/advertising/pubmatic.md)
>   - [[!DNL Qualtrics Automations]](../../destinations/catalog/survey/qualtrics-automations.md)
>   - [[!DNL RainFocus Attendee Profiles]](../../destinations/catalog/marketing-automation/rainfocus.md)
>   - [[!DNL SAP Commerce]](../../destinations/catalog/ecommerce/sap-commerce.md)
>   - [[!DNL Snowflake]](../../destinations/catalog/cloud-storage/snowflake.md)
>   - [[!DNL Yahoo DataX]](../../destinations/catalog/advertising/datax.md)
>   - [[!DNL Zendesk]](../../destinations/catalog/crm/zendesk.md)
>   - Destinations de lot (basées sur des fichiers)
> 
>- Pour les destinations par lots, les mesures au niveau de l’audience sont actuellement enregistrées pour les exécutions de flux de données réussies uniquement. Elles ne sont pas enregistrées pour les exécutions de flux de données ayant échoué et les enregistrements exclus. Pour les exécutions de flux de données vers des destinations de diffusion en continu, les mesures sont capturées et affichées pour les enregistrements activés et exclus.

![Audiences mises en surbrillance dans le panneau flux de données.](../assets/ui/monitor-destinations/dashboard-segments-view.png)

Dans la vue au niveau de l’audience, les mesures sont agrégées sur plusieurs exécutions de flux de données au cours de la période sélectionnée. S’il existe plusieurs exécutions de flux de données, vous pouvez effectuer une analyse en profondeur à partir du niveau de l’audience pour afficher la répartition de chaque exécution de flux de données, filtrée par l’audience sélectionnée.
Utilisez le bouton de filtre ![filter](/help/images/icons/filter-add.png) pour accéder à la vue d’exécution du flux de données pour chaque audience du flux de données.

### Page Exécutions de flux de données {#dataflow-runs-page}

La page exécutions de flux de données affiche des informations sur vos exécutions de flux de données, notamment l’heure de début de l’exécution du flux de données, le temps de traitement, les enregistrements reçus, les enregistrements activés, les enregistrements exclus, les enregistrements en échec, le taux d’activation et le statut.

Lorsque vous analysez la page exécutions de flux de données à partir de la [vue au niveau de l’audience](#segment-level-view), vous avez la possibilité de filtrer les exécutions de flux de données à l’aide des options suivantes :

- **[!UICONTROL Le flux de données s’exécute avec des enregistrements en échec]** : pour l’audience sélectionnée, cette option répertorie toutes les exécutions de flux de données qui ont échoué pour activation. Pour examiner les raisons pour lesquelles les enregistrements d’une certaine exécution de flux de données ont échoué, consultez la page [détails de l’exécution du flux de données](#dataflow-run-details-page) de cette exécution de flux de données.
- **[!UICONTROL Exécutions de flux de données avec enregistrements exclus]** : pour l’audience sélectionnée, cette option répertorie toutes les exécutions de flux de données pour lesquelles certains enregistrements n’ont pas été entièrement activés et certains profils ont été ignorés. Pour vérifier pourquoi les enregistrements d’une certaine exécution de flux de données ont été ignorés, reportez-vous à la page [détails de l’exécution du flux de données](#dataflow-run-details-page) pour cette exécution de flux de données.
- **[!UICONTROL Exécutions de flux de données avec des enregistrements activés]** : pour l’audience sélectionnée, cette option répertorie toutes les exécutions de flux de données contenant des enregistrements activés.

![Boutons radio indiquant comment filtrer les exécutions de flux de données pour les audiences.](/help/dataflows/assets/ui/monitor-destinations/dataflow-runs-segment-filter.png)

Pour afficher plus d’informations sur une exécution de flux de données spécifique, sélectionnez le filtre ![filtre](/help/images/icons/filter-add.png) à côté de l’heure de début de l’exécution du flux de données pour afficher la page des détails de l’exécution du flux de données.

![Le flux de données exécute un filtre dans le tableau de bord de surveillance pour analyser plus d’informations pour une certaine exécution du flux de données.](../assets/ui/monitor-destinations/dataflow-runs-filter.png)

### Page Détails de l’exécution du flux de données {#dataflow-run-details-page}

La page des détails de l’exécution du flux de données, en plus des détails affichés dans la liste des exécutions de flux de données, affiche des informations plus spécifiques sur le flux de données :

- **[!UICONTROL ID d’exécution du flux de données]** : ID du flux de données.
- **[!UICONTROL ID d’organisation IMS]** : organisation à laquelle appartient le flux de données.
- **[!UICONTROL Dernière mise à jour]** : heure de la dernière mise à jour de l’exécution du flux de données.

La page de détails comporte également un bouton (bascule) pour basculer entre les erreurs d’exécution du flux de données et les audiences. Cette option est disponible uniquement pour les exécutions de flux de données dans les destinations par lots et pour la destination de diffusion en continu [Google Customer Match DV 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md).

La vue Erreurs d’exécution du flux de données affiche une liste des enregistrements ayant échoué et des enregistrements ayant été ignorés. Les informations relatives aux enregistrements ayant échoué et ignorés s’affichent, y compris le code d’erreur, le nombre d’identités et la description. Par défaut, la liste affiche les enregistrements ayant échoué. Pour afficher les enregistrements ignorés, activez le bouton (bascule) **[!UICONTROL Enregistrements ignorés]**.

![ Basculement des identités exclues mis en surbrillance dans la vue de surveillance](../assets/ui/monitor-destinations/identities-excluded.png)

Lorsque **[!UICONTROL Audiences]** est sélectionné, la liste des audiences qui ont été activées dans l’exécution du flux de données sélectionné s’affiche. Cet écran comprend des informations au niveau de l’audience sur les enregistrements activés, les enregistrements exclus, ainsi que le statut et l’heure de la dernière exécution du flux de données.

![Vue Audiences de l’écran Détails de l’exécution du flux de données.](../assets/ui/monitor-destinations/dataflow-run-segments-view.png)

## Étapes suivantes {#next-steps}

En suivant ce guide, vous savez désormais comment surveiller les flux de données pour les destinations par lots et de diffusion en continu, y compris toutes les informations pertinentes telles que le temps de traitement, le taux d’activation et le statut. Pour en savoir plus sur les flux de données dans Experience Platform, consultez la [présentation des flux de données](../home.md). Pour en savoir plus sur les destinations, lisez la [présentation des destinations](../../destinations/home.md).