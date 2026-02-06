---
title: Notation prédictive des prospects et des comptes dans Real-Time CDP B2B
type: Documentation
description: Présentation et plus d’informations sur la fonctionnalité de notation prédictive des prospects et des comptes dans Experience Platform CDP B2B.
feature: Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 11%

---

# Notation prédictive des prospects et des comptes dans Real-Time CDP B2B

Les spécialistes du marketing B2B sont confrontés à de multiples défis au sommet du funnel marketing. Pour être efficaces, les marketeurs B2B ont besoin d’une méthode automatisée pour qualifier le grand nombre de personnes afin qu’elles puissent se concentrer sur les cibles à forte valeur ajoutée. La qualification doit être alignée sur le résultat final de la vente, et pas seulement sur la conversion marketing.

Les comptes sont les entités ultimes qui achètent des produits et services B2B. Afin de commercialiser et de vendre efficacement, les spécialistes du marketing B2B doivent connaître non seulement la probabilité d’achat de l’individu, mais également celle du compte.

Le marketing basé sur les comptes, en particulier, permet de définir les comptes stratégiques comme cibles marketing. Les scores de propension à acheter du compte aident grandement les spécialistes du marketing B2B à établir des priorités parmi les comptes afin de maximiser leur retour sur investissement.

Le service de notation prédictive des prospects et des comptes résout les problèmes ci-dessus en tirant parti des événements de conversion de l’étape d’opportunité, en les prédisant et en agrégeant les activités de personne au niveau du compte pour produire les notes de compte. Les scores sont facilement disponibles en tant que champs personnalisés sur les profils de personne et de compte, et peuvent facilement être inclus en tant que critères de segment pour affiner votre audience. Les principaux facteurs d’influence sont également disponibles au niveau des agrégats et des unités afin d’aider les spécialistes du marketing B2B à mieux comprendre les éléments qui ont motivé les scores.

## Comprendre la notation prédictive des prospects et des comptes {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] source de données est actuellement requise, car il s’agit de la seule source de données pouvant fournir les événements de conversion au niveau du profil de la personne.

La notation prédictive des prospects et des comptes utilise une méthode de machine learning basée sur les arbres de décision (forêt aléatoire/boosting de gradients) pour créer le modèle de notation prédictive des prospects.

Les administrateurs ont la possibilité de configurer plusieurs objectifs de notation de profil, également appelés modèles, un pour chaque événement de conversion configuré, ce qui permet de générer des scores distincts pour chaque objectif configuré.

La notation prédictive des prospects et des comptes prend en charge les types et champs d’objectif de conversion suivants :

| Type d’objectif | Champs |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>Exemple : `opportunityEvent.dataValueChanges.attributeName` est égal à `Stage` et `opportunityEvent.dataValueChanges.newValue` à `Contract`</ul> |

L’algorithme prend en compte les attributs et données d’entrée suivants :

* Profil de la personne

| Champ XDM | Obligatoire/ Facultatif |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | Obligatoire |
| `workAddress.country` | Facultatif |
| `extSourceSystemAudit.createdDate` | Obligatoire |
| `extendedWorkDetails.jobTitle` | Facultatif |

>[!NOTE]
> 
>L’algorithme inspecte uniquement `sourceAccountKey.sourceKey` champ du groupe de champs Personne:personComponents.

* Profil de compte

| Champ XDM | Obligatoire/ Facultatif |
| --- | --- |
| `accountKey.sourceKey` | Obligatoire |
| `extSourceSystemAudit.createdDate` | Obligatoire |
| `accountOrganization.industry` | Facultatif |
| `accountOrganization.numberOfEmployees` | Facultatif |
| `accountOrganization.annualRevenue.amount` | Facultatif |

* Événement d’expérience

| Champ XDM | Obligatoire/ Facultatif |
| --- | --- |
| `_id` | Obligatoire |
| `personKey.sourceKey` | Obligatoire |
| `timestamp` | Obligatoire |
| `eventType` | Obligatoire |

Plusieurs modèles sont pris en charge, avec les limites strictes suivantes mises en place :

* Chaque sandbox de production a droit à cinq modèles.
* Chaque sandbox de développement a droit à un modèle.

Les exigences en matière de qualité des données sont les suivantes :

* Idéalement, il existe deux années de données les plus récentes à des fins de formation.
* La longueur minimale requise des données est de six mois plus la fenêtre de prédiction.
* Pour chaque objectif de prédiction, au moins 10 événements de conversion qualifiés sont requis.

Les tâches de notation sont exécutées quotidiennement et les résultats sont enregistrés en tant qu’attributs de profil et attributs de compte, qui peuvent ensuite être utilisés dans les définitions de segment et la personnalisation. Les informations d’analyse prêtes à l’emploi sont également disponibles sur le tableau de bord de présentation du compte.

Consultez la documentation pour plus d’informations sur la [gestion du service de notation prédictive des prospects et des comptes](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md).

## Afficher les résultats de notation prédictive des prospects et des comptes {#how-to-view}

Après l’exécution de la tâche, les résultats sont enregistrés dans un nouveau jeu de données système pour chaque modèle sous le nom `LeadsAI.Scores` - ***nom du score***. Chaque groupe de champs de score peut être localisé à l’adresse `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`.

| Attribut | Description |
| --- | --- |
| Score | Probabilité relative qu’un profil atteigne l’objectif prévu dans la période définie. Cette valeur ne doit pas être traitée comme un pourcentage de probabilité, mais plutôt comme la probabilité d’un profil par rapport à la population globale. Ce score est compris entre 0 et 100. |
| Percentile | Cette valeur fournit des informations concernant la performance d’un profil par rapport à d’autres profils aux notes similaires. Les percentiles sont compris entre 1 et 100. |
| Type de modèle | Le type de modèle sélectionné indique s’il s’agit d’un score de personne ou de compte. |
| Date de la note | Date à laquelle la notation a eu lieu. |
| Facteurs d’influence | Raisons prédites pour lesquelles un profil est susceptible de procéder à la conversion. Les facteurs se composent des attributs suivants :<ul><li>Code : le profil ou l’attribut comportemental qui influencent positivement le score prévu d’un profil.</li><li>Valeur : la valeur du profil ou de l’attribut comportemental.</li><li>Importance : indique le poids que le profil ou l’attribut comportemental a sur le score prévu (faible, moyen, élevé).</li></ul> |

### Afficher les scores du profil client

Pour afficher les scores prédictifs d’un profil de personne, sélectionnez **[!UICONTROL Profiles]** sous la section client du panneau de gauche, puis saisissez l’espace de noms d’identité et la valeur d’identité. Une fois l’opération terminée, sélectionnez **[!UICONTROL View]**.

Sélectionnez ensuite le profil dans la liste.

![Profil client](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

La page **[!UICONTROL Detail]** inclut désormais les scores prédictifs. Cliquez sur l’icône de graphique en regard du score prédictif.

![Score prédictif du profil client](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

Une boîte de dialogue contextuelle affiche le score, la distribution globale du score, les principaux facteurs d’influence de ce score et la définition de l’objectif du score.

![Détails sur le score prédictif du profil client](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## Surveillance des traitements de notation prédictive des prospects et des comptes {#monitoring-jobs}

Vous pouvez surveiller les mesures de base et le statut d’exécution quotidien des tâches via le tableau de bord. Les mesures incluent :

* Total des profils de compte/personne notés
* Tâche de notation suivante (date)
* Prochaine tâche de formation (date)

Pour plus d’informations, consultez la documentation sur la [surveillance des tâches pour la notation prédictive des prospects et des comptes](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
