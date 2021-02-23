---
keywords: Experience Platform ; accueil ; rubriques populaires ; comptes de surveillance ; flux de données de surveillance ; flux de données ; sources
description: Ce didacticiel décrit les étapes à suivre pour surveiller votre flux de données, en utilisant à la fois la vue de surveillance agrégée et la surveillance interservices.
solution: Experience Platform
title: Surveillance des flux de données pour les sources dans l’interface utilisateur
topic: aperçu
type: Tutoriel
translation-type: tm+mt
source-git-commit: 4c668a47e62ba7736dd2d7afe4e71fd015198356
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 6%

---


# Surveiller les flux de données pour les sources dans l’interface utilisateur

Au Adobe Experience Platform, les données sont ingérées à partir d&#39;une grande variété de sources, analysées dans l&#39;Experience Platform et activées vers une grande variété de destinations. La plate-forme facilite le processus de suivi de ce flux de données potentiellement non linéaire en fournissant de la transparence avec les flux de données.

Le tableau de bord de surveillance vous fournit une représentation visuelle du parcours d’un flux de données. Vous pouvez utiliser une vue de surveillance agrégée et naviguer verticalement du niveau source à un flux de données et à une exécution de flux de données, ce qui vous permet de vue des mesures correspondantes qui contribuent à la réussite ou à l&#39;échec d&#39;un flux de données. Vous pouvez également utiliser la capacité de surveillance interservices du tableau de bord de surveillance pour surveiller le parcours d&#39;un flux de données depuis une source, jusqu&#39;à [!DNL Identity Service] et [!DNL Profile].

Ce didacticiel décrit les étapes à suivre pour surveiller votre flux de données, en utilisant à la fois la vue de surveillance agrégée et la surveillance interservices.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Flux](../home.md) de données : Les flux de données sont une représentation des tâches de données qui déplacent les données entre les plateformes. Les flux de données sont configurés entre différents services, ce qui permet de déplacer les données des connecteurs source vers des jeux de données de cible, vers [!DNL Identity] et [!DNL Profile] et vers [!DNL Destinations].
   * [Flux de données s’exécute](../../sources/notifications.md) : Les exécutions de flux de données sont les tâches planifiées récurrentes en fonction de la configuration de fréquence des flux de données sélectionnés.
* [Sources](../../sources/home.md) : Experience Platform permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de plate-forme.
* [Identity Service](../../identity-service/home.md) : profitez d’une meilleure compréhension de vos clients et de leurs comportements en rapprochant des identités entre appareils et systèmes.
* [Real-time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Environnements de test](../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Vue de surveillance agrégée

Dans l&#39;[interface utilisateur de la plate-forme](https://platform.adobe.com), sélectionnez **[!UICONTROL Surveillance]** dans le volet de navigation de gauche pour accéder au tableau de bord [!UICONTROL Surveillance]. Le tableau de bord [!UICONTROL Surveillance] contient des mesures et des informations sur tous les flux de données de sources, y compris des informations sur l&#39;état du trafic de données d&#39;une source à [!DNL Identity Service] et à [!DNL Profile].

Au centre du tableau de bord se trouve le panneau [!UICONTROL Origine assimilée], qui contient des mesures et des graphiques qui affichent les données sur les enregistrements ingérés et les enregistrements ayant échoué.

![tableau de bord de surveillance](../assets/ui/monitor-sources/monitoring-dashboard.png)

Par défaut, les données affichées contiennent les taux d’assimilation des dernières 24 heures. Sélectionnez **[!UICONTROL Dernières 24 heures]** pour ajuster la période des enregistrements affichés.

![change-date](../assets/ui/monitor-sources/change-date.png)

Une fenêtre contextuelle de calendrier s&#39;affiche, vous offrant des options pour d&#39;autres périodes d&#39;assimilation. Sélectionnez **[!UICONTROL 30 derniers jours]**, puis **[!UICONTROL Appliquer]**.

![période d&#39;ajustement](../assets/ui/monitor-sources/adjust-timeframe.png)

Les graphiques sont activés par défaut et vous pouvez les désactiver pour développer la liste des sources ci-dessous. Sélectionnez la bascule **[!UICONTROL Mesures et graphiques]** pour désactiver les graphiques.

![mesures et graphiques](../assets/ui/monitor-sources/metrics-graphs.png)

| Exportation de source | Description |
| ---------------- | ----------- |
| [!UICONTROL Enregistrements ingérés  ] | Nombre total d’enregistrements ingérés. |
| [!UICONTROL Échec des enregistrements] | Nombre total d’enregistrements qui n’ont pas été ingérés en raison d’erreurs dans les données. |
| [!UICONTROL Nombre total de flux de données ayant échoué] | Nombre total de flux de données avec un état `failed`. |

La liste d&#39;assimilation source affiche toutes les sources qui contiennent au moins un compte existant. La liste comprend également des informations sur le taux d&#39;assimilation de chaque source, le nombre d&#39;enregistrements ayant échoué et le nombre total de flux de données ayant échoué, en fonction de la période que vous avez appliquée.

![source-assimilation](../assets/ui/monitor-sources/source-ingestion.png)

Pour trier à travers la liste des sources, sélectionnez **[!UICONTROL Mes sources]**, puis sélectionnez votre catégorie de choix dans le menu déroulant. Par exemple, pour vous concentrer sur les enregistrements de cloud, sélectionnez **[!UICONTROL enregistrement de cloud]**.

![tri-par-catégorie](../assets/ui/monitor-sources/sort-by-category.png)

Pour vue de tous les flux de données existants dans toutes les sources, sélectionnez **[!UICONTROL Flux de données]**.

![vue-tous-flux de données](../assets/ui/monitor-sources/view-all-dataflows.png)

Vous pouvez également entrer une source dans la barre de recherche pour isoler une source unique. Une fois votre source identifiée, sélectionnez l’icône de filtre ![filter](../assets/ui/monitor-sources/filter.png) en regard de celle-ci pour afficher une liste de ses flux de données principaux.

![rechercher](../assets/ui/monitor-sources/search.png)

Une liste de flux de données s’affiche. Pour restreindre la liste et se concentrer sur les flux de données contenant des erreurs, sélectionnez **[!UICONTROL Afficher uniquement les échecs]**.

![affichage-échecs-uniquement](../assets/ui/monitor-sources/show-failures-only.png)

Localisez le flux de données à surveiller, puis sélectionnez l’icône de filtre ![filter](../assets/ui/monitor-sources/filter.png) située à côté de celui-ci pour afficher plus d’informations sur son état d’exécution.

![flux de données](../assets/ui/monitor-sources/dataflow.png)

La page d’exécution de flux de données affiche des informations sur la date de début d’exécution de votre flux de données, la taille des données, l’état ainsi que la durée de traitement. Sélectionnez l’icône de filtre ![filter](../assets/ui/monitor-sources/filter.png) en regard de l’heure de début d’exécution du flux de données pour afficher ses détails d’exécution.

![début d&#39;exécution de flux de données](../assets/ui/monitor-sources/dataflow-run-start.png)

La page [!UICONTROL Détails de l&#39;exécution du flux de données] affiche des informations sur les métadonnées du flux de données, l&#39;état d&#39;assimilation partielle et le résumé de l&#39;erreur. Le résumé de l&#39;erreur contient l&#39;erreur de niveau supérieur spécifique qui indique à quelle étape le processus d&#39;assimilation a rencontré une erreur.

Faites défiler l&#39;écran vers le bas pour afficher des informations plus spécifiques sur l&#39;erreur qui s&#39;est produite.

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

Le panneau [!UICONTROL Erreurs d&#39;exécution de flux de données] affiche l&#39;erreur et le code d&#39;erreur spécifiques qui ont provoqué l&#39;échec d&#39;assimilation du flux de données. Dans ce scénario, une erreur de transformation du mappeur s&#39;est produite, entraînant l&#39;échec de 24 enregistrements.

Sélectionnez **[!UICONTROL Fichiers]** pour plus d’informations.

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

Le panneau [!UICONTROL Fichiers] contient des informations sur le nom et le chemin du fichier.

Pour une représentation plus détaillée de l&#39;erreur, sélectionnez **[!UICONTROL diagnostics d&#39;erreur de Prévisualisation]**.

![files](../assets/ui/monitor-sources/files.png)

La fenêtre [!UICONTROL prévisualisation des diagnostics d&#39;erreur] s&#39;affiche, affichant une prévisualisation allant jusqu&#39;à 100 erreurs dans le flux de données. Vous pouvez sélectionner **[!UICONTROL Télécharger]** pour récupérer une commande curl, qui vous permet ensuite de télécharger les diagnostics d&#39;erreur.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Fermer]**.

![erreurs-diagnostics](../assets/ui/monitor-sources/error-diagnostics.png)

Vous pouvez utiliser le chemin de navigation dans l’en-tête supérieur pour revenir au tableau de bord [!UICONTROL Surveillance]. Sélectionnez **[!UICONTROL Exécuter le début : 14/02/2021, 09:47 PM]** pour revenir à la page précédente, puis sélectionnez **[!UICONTROL Flux de données : Démonstration de l&#39;ingestion des données de fidélité : échec]** du retour à la page des flux de données.

![fil d&#39;Ariane](../assets/ui/monitor-sources/breadcrumbs.png)

## Surveillance interservices

La partie supérieure du tableau de bord contient une représentation du flux d&#39;assimilation du niveau source, à [!DNL Identity Service] et à [!DNL Profile]. Chaque cellule comprend un marqueur de point qui indique la présence d’erreurs survenues à ce stade d’assimilation. Un point vert signifie une ingestion sans erreur, tandis qu&#39;un point rouge signifie qu&#39;une erreur s&#39;est produite à ce stade particulier de l&#39;assimilation.

![surveillance inter-services](../assets/ui/monitor-sources/cross-service-monitoring.png)

Dans la page des flux de données, recherchez un flux de données réussi et sélectionnez l’icône de filtre ![filter](../assets/ui/monitor-sources/filter.png) à côté de celui-ci pour afficher ses informations d’exécution de flux de données.

![dataflow-success](../assets/ui/monitor-sources/dataflow-success.png)

La page d&#39;[!UICONTROL assimilation de la source] contient des informations qui confirment la réussite de l&#39;assimilation de votre flux de données. À partir de là, vous pouvez début surveiller le parcours de votre flux de données depuis le niveau source jusqu&#39;à [!DNL Identity Service], puis jusqu&#39;à [!DNL Profile].

Sélectionnez **[!UICONTROL Identités]** pour afficher l&#39;assimilation à l&#39;étape [!UICONTROL Identités].

![sources](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] metrics

La page [!UICONTROL Traitement des identités] contient des informations sur les enregistrements assimilés à [!DNL Identity Service], y compris le nombre d&#39;identités ajoutées, les graphiques créés et les graphiques mis à jour.

Sélectionnez l&#39;icône de filtre ![filter](../assets/ui/monitor-sources/filter.png) en regard de l&#39;heure de début d&#39;exécution du flux de données pour afficher plus d&#39;informations sur votre exécution du flux de données [!DNL Identity].

![identités](../assets/ui/monitor-sources/identities.png)

| Mesures d’identité | Description |
| ---------------- | ----------- |
| [!UICONTROL Enregistrements reçus] | Nombre d&#39;enregistrements reçus de [!DNL Data Lake]. |
| [!UICONTROL Échec des enregistrements] | Nombre d’enregistrements qui n’ont pas été ingérés dans la plate-forme en raison d’erreurs dans les données. |
| [!UICONTROL Enregistrements ignorés] | Nombre d&#39;enregistrements qui ont été ingérés, mais pas dans [!DNL Identity Service] car il n&#39;y avait qu&#39;un seul identifiant dans la ligne d&#39;enregistrement. |
| [!UICONTROL Enregistrements ingérés] | Nombre d&#39;enregistrements ingérés dans [!DNL Identity Service]. |
| [!UICONTROL Total des enregistrements] | Nombre total de tous les enregistrements, y compris les enregistrements ayant échoué, les enregistrements ignorés, [!DNL Identities] ajoutés et les enregistrements dupliqués. |
| [!UICONTROL Identités ajoutées] | Nombre de nouveaux identifiants nets ajoutés à [!DNL Identity Service]. |
| [!UICONTROL Graphiques créés] | Nombre de nouveaux graphiques d&#39;identité nets créés dans [!DNL Identity Service]. |
| [!UICONTROL Graphiques mis à jour] | Nombre de graphiques d&#39;identité existants mis à jour avec de nouveaux bords. |
| [!UICONTROL Exécutions de flux de données ayant échoué] | Nombre d’exécutions de flux de données ayant échoué. |
| [!UICONTROL Durée du traitement] | Horodatage du début de l’assimilation jusqu’à la fin. |
| [!UICONTROL État] | Définit l’état général d’un flux de données. Les valeurs d’état possibles sont les suivantes : <ul><li>`Success`: Indique qu’un flux de données est principal et qu’il ingère des données en fonction du planning indiqué.</li><li>`Failed`: Indique que le processus d’activation d’un flux de données a été interrompu en raison d’erreurs. </li><li>`Processing`: Indique que le flux de données n’est pas encore principal. Cet état est souvent rencontré immédiatement après la création d’un nouveau flux de données.</li></ul> |

La page [!UICONTROL Détails de l&#39;exécution de flux de données] affiche plus d&#39;informations sur votre exécution de flux de données [!DNL Identity], y compris son ID d&#39;organisation IMS et son ID d&#39;exécution de flux de données. Cette page affiche également le code d&#39;erreur et le message d&#39;erreur correspondants fournis par [!DNL Identity Service], en cas d&#39;erreur dans le processus d&#39;assimilation.

Sélectionnez **[!UICONTROL Exécuter le début : 14/02/2021, 21:47 PM]** pour revenir à la page précédente.

![identities-dataflow-run](../assets/ui/monitor-sources/identities-dataflow-run.png)

Dans la page [!UICONTROL Traitement d&#39;identité], sélectionnez **[!UICONTROL Profils]** pour afficher l&#39;état d&#39;assimilation des enregistrements à l&#39;étape [!UICONTROL Profils].

![profils sélectionnés](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] mesures

La page [!UICONTROL Profil processing] contient des informations sur les enregistrements ingérés dans [!DNL Profile], notamment le nombre de fragments de profil créés, les fragments de profil mis à jour et le nombre total de fragments de profil.

Sélectionnez l&#39;icône de filtre ![filter](../assets/ui/monitor-sources/filter.png) en regard de l&#39;heure de début d&#39;exécution du flux de données pour afficher plus d&#39;informations sur votre exécution du flux de données [!DNL Profile].

![profils](../assets/ui/monitor-sources/profiles.png)

| Mesures de profil | Description |
| --------------- | ----------- |
| [!UICONTROL Enregistrements reçus] | Nombre d&#39;enregistrements reçus de [!DNL Data Lake]. |
| [!UICONTROL Échec des enregistrements  ] | Nombre d&#39;enregistrements qui ont été ingérés, mais pas dans [!DNL Profile] en raison d&#39;erreurs. |
| [!UICONTROL Fragments de profil ajoutés] | Nombre de nouveaux fragments [!DNL Profile] nets ajoutés. |
| [!UICONTROL Profil de fragments mis à jour] | Nombre de fragments [!DNL Profile] existants mis à jour |
| [!UICONTROL Nombre total de fragments de Profil] | Nombre total d’enregistrements écrits dans [!DNL Profile], y compris tous les fragments [!DNL Profile] existants mis à jour et les nouveaux fragments [!DNL Profile] créés. |
| [!UICONTROL Exécutions de flux de données ayant échoué] | Nombre d’exécutions de flux de données ayant échoué. |
| [!UICONTROL Durée du traitement] | Horodatage du début de l’assimilation jusqu’à la fin. |
| [!UICONTROL État] | Définit l’état général d’un flux de données. Les valeurs d’état possibles sont les suivantes : <ul><li>`Success`: Indique qu’un flux de données est principal et qu’il ingère des données en fonction du planning indiqué.</li><li>`Failed`: Indique que le processus d’activation d’un flux de données a été interrompu en raison d’erreurs. </li><li>`Processing`: Indique que le flux de données n’est pas encore principal. Cet état est souvent rencontré immédiatement après la création d’un nouveau flux de données.</li></ul> |

La page [!UICONTROL Détails de l&#39;exécution de flux de données] affiche plus d&#39;informations sur votre exécution de flux de données [!DNL Profile], y compris son ID d&#39;organisation IMS et son ID d&#39;exécution de flux de données. Cette page affiche également le code d&#39;erreur et le message d&#39;erreur correspondants fournis par [!DNL Profile], en cas d&#39;erreur dans le processus d&#39;assimilation.

![profils-flux de données exécutés](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez suivi avec succès le flux de données d’assimilation du niveau source à [!DNL Identity Service] et à [!DNL Profile], en utilisant le tableau de bord **[!UICONTROL Surveillance]**. Vous avez également identifié avec succès des erreurs qui ont contribué à l&#39;échec des flux de données pendant le processus d&#39;assimilation. Pour plus d’informations, voir les documents suivants :

* [Présentation du profil client en temps réel](../../profile/home.md)
* [Présentation de Data Science Workspace](../../data-science-workspace/home.md)
