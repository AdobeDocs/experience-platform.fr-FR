---
keywords: Experience Platform;accueil;rubriques les plus consultées;comptes de contrôle;flux de données de surveillance;flux de données;destinations
description: Les destinations vous permettent d’activer vos données de Adobe Experience Platform vers d’innombrables partenaires externes. Ce tutoriel explique comment surveiller les flux de données pour vos destinations à l’aide de l’interface utilisateur de l’Experience Platform.
solution: Experience Platform
title: Surveillance des flux de données pour les destinations dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 4a9511f055854ab574aca46f44acf155b0c16af6
workflow-type: tm+mt
source-wordcount: '3211'
ht-degree: 2%

---

# Surveillance des flux de données pour les destinations dans l’interface utilisateur

Les destinations vous permettent d’activer vos données de Adobe Experience Platform vers d’innombrables partenaires externes. Platform facilite le processus de suivi du flux de données vers vos destinations en fournissant de la transparence avec les flux de données.

Le tableau de bord de surveillance fournit une représentation visuelle du parcours d’un flux de données, y compris la destination vers laquelle les données sont activées. Ce tutoriel explique comment surveiller les flux de données directement dans l’espace de travail des destinations ou utiliser le tableau de bord de surveillance pour surveiller les flux de données pour vos destinations à l’aide de l’interface utilisateur Experience Platform.

## Prise en main {#getting-started}

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [Flux de données](../home.md) : les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Platform. Les flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers des jeux de données cibles, vers [!DNL Identity] et [!DNL Profile], et vers [!DNL Destinations].
   - [Exécutions de flux de données](../../sources/notifications.md): Les exécutions de flux de données sont les tâches planifiées récurrentes en fonction de la configuration de fréquence des flux de données sélectionnés.
- [Destinations](../../destinations/home.md): Les destinations sont des intégrations préconfigurées aux applications courantes qui permettent l’activation transparente des données de Platform pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.
- [Sandbox](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuelles qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Surveillance des flux de données dans l’espace de travail des destinations {#monitor-dataflows-in-the-destinations-workspace}

Dans le **[!UICONTROL Destinations]** dans l’interface utilisateur de Platform, accédez à la **[!UICONTROL Parcourir]** et sélectionnez le nom d’une destination que vous souhaitez afficher.

![Sélectionner la vue de destination](../assets/ui/monitor-destinations/select-destination.png)

Une liste des flux de données existants s’affiche. Sur cette page se trouve une liste de flux de données affichables, y compris des informations sur leur destination, leur nom d’utilisateur, le nombre de flux de données et leur état.

Pour plus d’informations sur les statuts, voir le tableau suivant :

| État | Description |
| ------ | ----------- |
| Activé | Le `Enabled` Le statut indique qu’un flux de données est principal et qu’il exporte des données en fonction du planning selon lequel il a été fourni. |
| Désactivé | Le `Disabled` L’état indique qu’un flux de données est inactif et n’exporte aucune donnée. |
| En cours de traitement | Le `Processing` Le statut indique qu’un flux de données n’est pas encore principal. Cet état est souvent rencontré immédiatement après la création d’un nouveau flux de données. |
| Erreur | Le `Error` Le statut indique que le processus d’activation d’un flux de données a été interrompu. |

### Exécutions de flux de données pour les destinations de diffusion en continu {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="Détails de l’exécution du flux de données"
>abstract="Les détails de l’exécution du flux de données de destination contiennent des informations sur l’état d’activation du segment et des mesures provenant de Real-time Customer Profile pour générer des identités uniques. Pour en savoir plus, consultez le guide des définitions de mesure."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="Profils reçus"
>abstract="Nombre total de profils reçus dans le flux de données. Cette valeur est mise à jour toutes les 60 minutes."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="Identités activées"
>abstract="Nombre d’identités de profil individuelles activées avec succès vers la destination sélectionnée. Cette mesure inclut les identités qui sont créées, mises à jour et supprimées des segments exportés."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="Identités exclues"
>abstract="Le nombre d’enregistrements de profil individuels exclus de l’activation pour la destination sélectionnée en fonction des attributs manquants et de la violation du consentement."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="Identités en échec"
>abstract="Le nombre d’identités de profil individuelles qui ont échoué pour la destination sélectionnée. Pour plus d’informations, consultez les diagnostics d’erreur."

Pour les destinations de diffusion en continu, la variable [!UICONTROL Exécutions de flux de données] Cet onglet fournit une mise à jour horaire des données de mesure lors de l’exécution de votre flux de données. Les statistiques les plus en vue sont celles portant sur les identités.

Les identités représentent les différentes facettes d’un profil. Par exemple, si un profil contient à la fois un numéro de téléphone et une adresse électronique, il aura deux identités.

Une liste des exécutions individuelles et de leurs mesures spécifiques s’affiche, ainsi que les totaux suivants pour les identités :

- **[!UICONTROL Identités activées]**: Nombre total d’identités de profil activées vers la destination sélectionnée. Cette mesure inclut les identités qui sont créées, mises à jour et supprimées des segments exportés.
- **[!UICONTROL Identités exclues]**: Nombre total d’identités de profil qui sont ignorées pour activation en fonction des attributs manquants et de la violation du consentement.
- **[!UICONTROL Identités en échec]**: Nombre total d’identités de profil qui ne sont pas activées vers la destination en raison d’erreurs.

![Détails des exécutions de flux de données pour les destinations de diffusion en continu](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Chaque exécution de flux de données individuelle affiche les détails suivants :

- **[!UICONTROL Démarrage de l’exécution du flux de données]**: Heure à laquelle le flux de données a commencé. Pour les exécutions de flux de données en continu, Experience Platform capture les mesures en fonction du début de l’exécution du flux de données, sous la forme de mesures horaires. Pour les exécutions de flux de données en continu, si une exécution de flux de données a commencé, par exemple à 22 h 30, la mesure affiche l’heure de début sur 22 h dans l’interface utilisateur.
- **[!UICONTROL Temps de traitement]**: Le temps nécessaire au traitement du flux de données.
   - Pour **[!UICONTROL terminé]** s’exécute, la mesure de temps de traitement affiche toujours une heure.
   - Pour les exécutions de flux de données qui se trouvent toujours dans une **[!UICONTROL traitement]** , la fenêtre permettant de capturer toutes les mesures reste ouverte pendant plus d’une heure, afin de traiter toutes les mesures qui correspondent à l’exécution du flux de données. Par exemple, une exécution de flux de données démarrée à 9h30 peut rester en état de traitement pendant une heure et demie pour capturer et traiter toutes les mesures. Ensuite, lorsque la fenêtre de traitement se ferme et que l’état du flux de données s’exécute, la fonction **terminé**, le temps de traitement affiché est remplacé par une heure.
- **[!UICONTROL Profils reçus]**: Nombre total de profils reçus dans le flux de données.
- **[!UICONTROL Identités activées]**: Nombre total d’identités de profil qui ont été activées avec succès vers la destination sélectionnée dans le cadre de l’exécution du flux de données. Cette mesure inclut les identités qui sont créées, mises à jour et supprimées des segments exportés.
- **[!UICONTROL Identités exclues]**: Nombre total d’identités de profil qui sont exclues de l’activation en fonction d’attributs manquants et de la violation du consentement.
- **[!UICONTROL Identités en échec]** Nombre total d’identités de profil qui ne sont pas activées vers la destination en raison d’erreurs.
- **[!UICONTROL Taux d&#39;activation]**: Pourcentage d’identités reçues qui ont été activées ou ignorées avec succès. La formule suivante illustre le mode de calcul de cette valeur :
   ![Formule de taux d&#39;activation](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL État]**: Représente l’état dans lequel se trouve le flux de données : both [!UICONTROL Terminé] ou [!UICONTROL Traitement]. [!UICONTROL Terminé] signifie que toutes les identités de l’exécution de flux de données correspondante ont été exportées au cours de la période d’une heure. [!UICONTROL Traitement] signifie que l’exécution du flux de données n’est pas encore terminée.

Pour afficher les détails d’une exécution de flux de données spécifique, sélectionnez l’heure de début de l’exécution dans la liste.

La page des détails d’une exécution de flux de données contient des informations supplémentaires telles que le nombre de profils reçus, le nombre d’identités activées, le nombre d’identités ayant échoué et le nombre d’identités exclues.

![Détails du flux de données pour les destinations de diffusion en continu](../assets/ui/monitor-destinations/dataflow-details-stream.png)

La page Détails affiche également une liste des identités qui ont échoué et des identités qui ont été exclues. Les informations relatives aux identités ayant échoué et exclues s’affichent, notamment le code d’erreur, le nombre d’identités et la description. Par défaut, la liste affiche les identités ayant échoué. Pour afficher les identités ignorées, sélectionnez la variable **[!UICONTROL Identités exclues]** bascule.

![Enregistrements de flux de données pour les destinations de diffusion en continu](../assets/ui/monitor-destinations/dataflow-records-stream.png)

### Les flux de données s’exécutent pour les destinations par lots. {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="Détails de l’exécution du flux de données"
>abstract="Les détails de l’exécution du flux de données de destination contiennent des informations sur l’état d’activation du segment et des mesures provenant de Real-time Customer Profile pour générer des identités uniques. Pour en savoir plus, consultez le guide des définitions de mesure."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-destinations.html#dataflow-runs-for-streaming-destinations" text="Exécutions de flux de données pour les destinations de diffusion en continu"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="Profils reçus"
>abstract="Nombre total de profils reçus dans le flux de données. Cette valeur est mise à jour toutes les 60 minutes."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="Identités activées"
>abstract="Nombre d’identités de profil individuelles activées avec succès vers la destination sélectionnée. Cette mesure inclut les identités qui sont créées, mises à jour et supprimées des segments exportés."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="Identités exclues"
>abstract="Le nombre d’enregistrements de profil individuels exclus de l’activation pour la destination sélectionnée en fonction des attributs manquants et de la violation du consentement."

Pour les destinations par lot, la variable [!UICONTROL Exécutions de flux de données] fournit des données de mesure sur vos exécutions de flux de données. Une liste des exécutions individuelles et de leurs mesures spécifiques s’affiche, ainsi que les totaux suivants pour les identités :

- **[!UICONTROL Identités activées]**: Nombre total d’identités de profil activées vers la destination sélectionnée. Cette mesure inclut les identités qui sont créées, mises à jour et supprimées des segments exportés.
- **[!UICONTROL Identités exclues]**: Le nombre d’identités de profil individuelles exclues de l’activation pour la destination sélectionnée, en fonction des attributs manquants et de la violation du consentement.

![Le flux de données s’exécute en vue des destinations par lots](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Chaque exécution de flux de données individuelle affiche les détails suivants :

- **[!UICONTROL Démarrage de l’exécution du flux de données]**: Heure à laquelle le flux de données a commencé.
- **[!UICONTROL Segment]**: Nom du segment associé à chaque exécution de flux de données.
- **[!UICONTROL Temps de traitement]**: Le temps nécessaire au traitement du flux de données.
- **[!UICONTROL Profils reçus]**: Nombre total de profils reçus dans le flux de données. Cette valeur est mise à jour toutes les 60 minutes.
- **[!UICONTROL Identités activées]**: Nombre total d’identités de profil qui ont été activées avec succès vers la destination sélectionnée dans le cadre de l’exécution du flux de données. Cette mesure inclut les identités qui sont créées, mises à jour et supprimées des segments exportés.
- **[!UICONTROL Identités exclues]**: Nombre total d’identités de profil qui sont exclues de l’activation en fonction d’attributs manquants et de la violation du consentement.
- **[!UICONTROL État]**: Représente l’état dans lequel se trouve le flux de données. Il peut s’agir de l’un des trois états suivants : [!UICONTROL Succès], [!UICONTROL En échec], et [!UICONTROL Traitement]. [!UICONTROL Succès] signifie que le flux de données est principal et qu’il exporte des données selon le planning indiqué. [!UICONTROL En échec] signifie que l’activation des données a été suspendue en raison d’erreurs. [!UICONTROL Traitement] signifie que le flux de données n’est pas encore principal et qu’il est généralement rencontré lors de la création d’un nouveau flux de données.

Pour afficher les détails d’une exécution de flux de données spécifique, sélectionnez l’heure de début de l’exécution dans la liste.

>[!NOTE]
>
>Les exécutions de flux de données sont générées en fonction de la fréquence de planification du flux de données de destination. Une exécution de flux de données distincte est créée pour chaque [stratégie de fusion](../../profile/merge-policies/overview.md) appliquée à un segment.

La page de détails d’un flux de données, en plus des détails affichés dans la liste des flux de données, affiche des informations plus spécifiques sur le flux de données :

- **[!UICONTROL Taille des données]**: Taille du flux de données en cours d’exportation.
- **[!UICONTROL Fichiers totaux]**: Nombre total de fichiers exportés dans le flux de données.
- **[!UICONTROL Dernière mise à jour]**: Heure de la dernière mise à jour du flux de données.

![Détails de l’exécution du flux de données pour les destinations par lots](../assets/ui/monitor-destinations/dataflow-batch.png)

La page Détails affiche également une liste des identités qui ont échoué et des identités qui ont été exclues. Les informations relatives aux identités ayant échoué et exclues s’affichent, y compris le code d’erreur et la description. Par défaut, la liste affiche les identités ayant échoué. Pour afficher les identités exclues, sélectionnez la variable **[!UICONTROL Identités exclues]** bascule.

![Enregistrements de flux de données pour les destinations par lots](../assets/ui/monitor-destinations/dataflow-records-batch.png)

## Tableau de bord de surveillance des destinations {#monitoring-destinations-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="Activation"
>abstract="La vue d’activation de destination contient des informations sur l’état d’activation du segment et des mesures provenant de Real-time Customer Profile pour générer des identités uniques."

>[!NOTE]
>
>- La fonctionnalité de surveillance des destinations est actuellement prise en charge pour toutes les destinations dans Experience Platform. *Sauf* la valeur [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) et [Personnalisation personnalisée](/help/destinations/catalog/personalization/custom-personalization.md) destinations.
>- Pour le [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Centre d’événements Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), et [API HTTP](/help/destinations/catalog/streaming/http-destination.md) destinations, les identités exclues ne sont actuellement pas affichées.


Pour accéder au [!UICONTROL Surveillance] tableau de bord, sélectionnez **[!UICONTROL Surveillance]** (![icône de surveillance](../assets/ui/monitor-destinations/monitoring-icon.png)) dans le volet de navigation de gauche. Une fois sur le [!UICONTROL Surveillance] page, sélectionnez [!UICONTROL Destinations]. Le [!UICONTROL Surveillance] Le tableau de bord contient des mesures et des informations sur les tâches d’exécution de destination.

Utilisez la variable [!UICONTROL Destinations] tableau de bord pour obtenir une idée générale de l’état de vos flux d’activation. Commencez par obtenir des informations sur un niveau agrégé pour toutes les destinations de lot et de diffusion en continu, puis explorez les vues détaillées des flux de données, des exécutions de flux de données et des segments activés afin d’obtenir un aperçu détaillé de vos données d’activation. Les écrans du [!UICONTROL Surveillance] Le tableau de bord fournit des informations exploitables au moyen de mesures et de descriptions d’erreur afin de vous aider à résoudre les problèmes qui peuvent se produire dans vos scénarios d’activation.

Au centre du tableau de bord se trouve l’objet [!UICONTROL Activation] qui contient des mesures et des graphiques qui affichent des données sur le taux d’activation des données exportées vers des destinations de diffusion en continu, ainsi que sur les exécutions de flux de données par lots ayant échoué vers des destinations par lot.

![Graphiques d’activation par flux et par lot](../assets/ui/monitor-destinations/dashboard-graph.png)


Par défaut, les données affichées contiennent les informations d&#39;activation des dernières 24 heures. Sélectionner **[!UICONTROL 24 dernières heures]** pour ajuster la période des enregistrements affichés. Les options disponibles incluent : **[!UICONTROL 24 dernières heures]**, **[!UICONTROL 7 derniers jours]**, et **[!UICONTROL 30 derniers jours]**. Vous pouvez également sélectionner les dates dans la fenêtre contextuelle du calendrier qui s’affiche. Une fois que vous avez sélectionné des dates, sélectionnez **[!UICONTROL Appliquer]** pour ajuster la période des informations affichées.

>[!NOTE]
>
>La capture d’écran suivante montre le taux d’activation et le flux de données par lots s’exécutent pendant les 30 derniers jours au lieu des 24 dernières heures. Vous pouvez ajuster la période en sélectionnant **[!UICONTROL 30 derniers jours]**.

![Modification de la période de recherche en amont pour les destinations activées](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

Utilisez l’icône de flèche (![icône de flèche](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) pour développer ou ignorer les cartes en haut de l’écran, qui affichent des informations en un coup d’oeil sur les détails de l’activation, en fonction du type de destination (diffusion en continu ou lot) :

- **[!UICONTROL Taux d’activation par flux]**: Représente le pourcentage d’identités reçues qui ont été activées ou ignorées avec succès. La formule utilisée pour calculer ce pourcentage est décrite plus haut sur cette page, dans la variable [Exécutions de flux de données pour les destinations de diffusion en continu](#dataflow-runs-for-streaming-destinations) .
- **[!UICONTROL Exécution de flux de données en échec du lot]**: Représente le nombre d’exécutions de flux de données ayant échoué dans l’intervalle de temps sélectionné.

![Afficher ou ignorer les cartes en haut de la page](../assets/ui/monitor-destinations/monitoring-destinations-toggle-arrow.gif)

Le **[!UICONTROL Activation]** le graphique s’affiche par défaut et vous pouvez le désactiver pour développer la liste des destinations ci-dessous. Sélectionnez la **[!UICONTROL Mesures et graphiques]** pour désactiver les graphiques.

Le **[!UICONTROL Activation]** affiche une liste des destinations qui contiennent au moins un compte existant. Cette liste contient également des informations sur les profils reçus, les identités activées, les identités ayant échoué, les identités exclues, le taux d’activation, le nombre total de flux de données ayant échoué et la date de dernière mise à jour pour ces destinations. Toutes les mesures ne sont pas disponibles pour tous les types de destinations. Le tableau ci-dessous indique les mesures disponibles par type de destination, diffusion en continu ou lot.

| Mesure | Type de destination |
---------|----------|
| **[!UICONTROL Profils reçus]** | Diffusion en continu et par lots |
| **[!UICONTROL Identités activées]** | Diffusion en continu et par lots |
| **[!UICONTROL Identités en échec]** | Diffusion en continu |
| **[!UICONTROL Identités exclues]** | Diffusion en continu et par lots |
| **[!UICONTROL Taux d&#39;activation]** | Diffusion en continu |
| **[!UICONTROL Total des flux de données ayant échoué]** | Lot |
| **[!UICONTROL Dernière mise à jour]** | Diffusion en continu et par lots |

![Tableau de bord de toutes les destinations activées](../assets/ui/monitor-destinations/dashboard-destinations.png)

Vous pouvez également filtrer votre liste de destinations pour n’afficher que la catégorie sélectionnée de destinations. Sélectionnez la **[!UICONTROL Mes destinations]** , puis sélectionnez la variable [catégorie de destination](/help/destinations/destination-types.md#categories) que vous souhaitez filtrer.

![Filtrage des destinations à l’aide du sélecteur de liste déroulante](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

De plus, vous pouvez saisir une destination dans la barre de recherche pour l’isoler vers une seule destination. Si vous souhaitez afficher les flux de données de la destination, vous pouvez sélectionner le filtre ![filter](../assets/ui/monitor-destinations/filter-add.png) en regard de pour afficher la liste de ses principaux flux de données.

![Filtrage des destinations à l’aide de la barre de recherche](../assets/ui/monitor-destinations/filtered-destinations.png)

Si vous souhaitez afficher tous les flux de données existants sur toutes les destinations, sélectionnez **[!UICONTROL Flux de données]**.

Une liste de flux de données s’affiche, triée par la dernière exécution de flux de données. Vous pouvez afficher des détails supplémentaires pour un flux de données spécifique en recherchant la destination à surveiller, en sélectionnant le filtre ![filter](../assets/ui/monitor-destinations/filter-add.png) en regard de l’élément, puis en sélectionnant le filtre ![filter](../assets/ui/monitor-destinations/filter-add.png) en regard du flux de données dont vous souhaitez obtenir plus d’informations.

![Tous les flux de données mis en surbrillance dans le tableau de bord de surveillance](../assets/ui/monitor-destinations/dashboard-dataflows.png)

Une fois que vous avez sélectionné un flux de données pour une inspection plus approfondie, la page des détails du flux de données contient un bouton d’activation qui vous permet de voir les données activées dans le flux de données, ventilées par exécutions ou segments de flux de données.

### Vue des exécutions du flux de données {#dataflow-runs-view}

When **[!UICONTROL Exécutions de flux de données]** est sélectionné, vous pouvez afficher une liste des exécutions de flux de données pour le flux de données sélectionné, ainsi que des informations supplémentaires sur chaque exécution.

>[!INFO]
>
>Pour les flux de données vers des destinations de diffusion en continu, une exécution de flux de données est ventilée en fenêtres horaires. Chaque fenêtre horaire génère un identifiant d’exécution de flux de données correspondant.
>
>Pour les flux de données vers les destinations par lot, chaque segment a une exécution de flux de données correspondante générée, en fonction de la fréquence planifiée de l’activation du segment. Par exemple, si vous configurez une activation planifiée quotidienne pour cinq segments dans le même flux de données de destination, cinq exécutions de flux de données distinctes seront générées chaque jour.

![Panneau d’exécutions de flux](../assets/ui/monitor-destinations/dashboard-flow-runs-view.png)

Utilisez la variable **[!UICONTROL Afficher uniquement les échecs]** bascule pour afficher uniquement les exécutions ayant échoué pour un flux de données.

![Exécutions de flux de données : bascule Afficher les échecs uniquement](../assets/ui/monitor-destinations/dataflow-runs-show-failures-only.gif)

### Vue au niveau du segment {#segment-level-view}

When **[!UICONTROL Segments]** est sélectionné, une liste des segments qui ont été activés dans le flux de données sélectionné s’affiche, dans la période sélectionnée. Cet écran comprend des informations au niveau du segment sur les identités activées, les identités exclues, ainsi que l’état et l’heure de la dernière exécution du flux de données. En examinant les mesures des identités exclues et activées, vous pouvez vérifier si un segment a été activé ou non.

Par exemple, vous activez un segment appelé &quot;Loyalty Members in California&quot; vers une destination Amazon S3 &quot;Loyalty Members California December&quot;. Supposons qu’il y ait 100 profils dans le segment sélectionné, mais que seuls 80 des 100 profils contiennent des attributs d’identifiant de fidélité et que vous ayez défini les règles de mappage d’exportation comme `loyalty.id` est obligatoire. Dans ce cas, au niveau du segment, 80 identités sont activées et 20 identités exclues.

>[!IMPORTANT]
>
>Notez les limites actuelles liées aux mesures au niveau du segment :
>- Actuellement, la vue au niveau du segment n’est disponible que pour les destinations par lot.
>- Les mesures au niveau du segment sont actuellement enregistrées uniquement pour les exécutions de flux de données réussies. Ils ne sont pas enregistrés pour les exécutions de flux de données ayant échoué et les enregistrements exclus.


![Segments dans le panneau du flux de données](../assets/ui/monitor-destinations/dashboard-segments-view.png)

Dans la vue au niveau du segment, les mesures sont agrégées sur plusieurs exécutions de flux de données au cours de la période sélectionnée. S’il existe plusieurs exécutions de flux de données, vous pouvez descendre au niveau du segment afin d’afficher la ventilation pour chaque exécution de flux de données, filtrée selon le segment sélectionné.
Utiliser le bouton de filtrage ![filter](../assets/ui/monitor-destinations/filter-add.png) pour accéder à la vue d’exécution du flux de données pour chaque segment du flux de données.

### Page Exécution du flux de données {#dataflow-runs-page}

La page des exécutions du flux de données affiche des informations sur vos exécutions de flux de données, notamment l’heure de début de l’exécution du flux de données, l’heure de traitement, les profils reçus, les identités activées, les identités exclues, les identités ayant échoué, le taux d’activation et l’état.

Lorsque vous explorez la page d’exécution du flux de données à partir du [vue au niveau du segment](#segment-level-view), vous avez la possibilité de filtrer les exécutions du flux de données selon les options suivantes :

- **[!UICONTROL Le flux de données s’exécute avec des identités qui ont échoué.]**: Pour le segment sélectionné, cette option répertorie toutes les exécutions de flux de données qui ont échoué pour l’activation. Pour examiner pourquoi les identités d’un certain flux de données ont échoué, reportez-vous à la section [page des détails de l’exécution du flux de données](#dataflow-run-details-page) pour cette exécution de flux de données.
- **[!UICONTROL Le flux de données s’exécute avec des identités ignorées.]**: Pour le segment sélectionné, cette option répertorie toutes les exécutions de flux de données où certaines identités n’ont pas été entièrement activées et certains profils ont été ignorés. Pour déterminer pourquoi les identités d’une certaine exécution de flux de données ont été ignorées, reportez-vous à la section [page des détails de l’exécution du flux de données](#dataflow-run-details-page) pour cette exécution de flux de données.
- **[!UICONTROL Le flux de données s’exécute avec les identités activées.]**: Pour le segment sélectionné, cette option répertorie toutes les exécutions de flux de données avec des identités qui ont été activées avec succès.

![Filtrage des exécutions de flux de données pour les segments](/help/dataflows/assets/ui/monitor-destinations/dataflow-runs-segment-filter.png)

Pour afficher plus d’informations sur une exécution de flux de données spécifique, sélectionnez le filtre . ![filter](../assets/ui/monitor-destinations/filter-add.png) en regard de l’heure de début d’exécution du flux de données pour afficher la page détails d’exécution du flux de données.

![Filtre des exécutions de flux de données dans le tableau de bord de surveillance](../assets/ui/monitor-destinations/dataflow-runs-filter.png)

### Page Détails de l’exécution du flux de données {#dataflow-run-details-page}

La page des détails de l’exécution du flux de données, en plus des détails affichés sur la liste des exécutions du flux de données, affiche des informations plus spécifiques sur le flux de données :

- **[!UICONTROL Identifiant d’exécution du flux de données]**: L’identifiant du flux de données.
- **[!UICONTROL Identifiant de l’organisation IMS]**: L’organisation IMS à laquelle le flux de données appartient.
- **[!UICONTROL Dernière mise à jour]**: Heure de la dernière mise à jour du flux de données.

La page Détails comporte également un bouton bascule permettant de basculer entre les erreurs d’exécution de flux de données et les segments. Cette option est disponible uniquement pour les exécutions de flux de données dans les destinations par lots.

La vue des erreurs d’exécution du flux de données affiche une liste des identités qui ont échoué et des identités qui ont été exclues. Les informations relatives aux identités ayant échoué et exclues s’affichent, notamment le code d’erreur, le nombre d’identités et la description. Par défaut, la liste affiche les identités ayant échoué. Pour afficher les identités ignorées, sélectionnez la variable **[!UICONTROL Identités exclues]** bascule.

![Bascule des identités exclues](../assets/ui/monitor-destinations/identities-excluded.png)

When **[!UICONTROL Segments]** est sélectionné, une liste des segments qui ont été activés dans l’exécution de flux de données sélectionnée s’affiche. Cet écran comprend des informations au niveau du segment sur les identités activées, les identités exclues, ainsi que l’état et l’heure de la dernière exécution du flux de données.

![Exécution du flux de données - vue des segments](../assets/ui/monitor-destinations/dataflow-run-segments-view.png)

## Étapes suivantes {#next-steps}

En suivant ce guide, vous savez maintenant comment surveiller les flux de données pour les destinations par lots et en flux continu, y compris toutes les informations pertinentes telles que le temps de traitement, le taux d’activation et l’état. Pour en savoir plus sur les flux de données dans Platform, veuillez lire le [présentation des flux de données](../home.md). Pour en savoir plus sur les destinations, veuillez lire le [présentation des destinations](../../destinations/home.md).