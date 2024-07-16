---
title: Score prédictif de piste et de compte dans Real-Time CDP B2B
type: Documentation
description: Présentation et informations supplémentaires sur la fonctionnalité de notation de compte et de piste prédictive dans la plateforme CDP B2B Experience Platform.
feature: Profiles, B2B
badgeB2B: label="Édition B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 11%

---

# Score prédictif de piste et de compte dans Real-Time CDP B2B

Les marketeurs B2B sont confrontés à de nombreux défis en haut de l’entonnoir marketing. Pour être efficaces, les spécialistes du marketing B2B doivent disposer d’un moyen automatisé de qualifier le grand nombre de personnes afin de pouvoir se concentrer sur les cibles à forte valeur ajoutée. La qualification doit être alignée sur le résultat commercial ultime, et pas seulement sur la conversion marketing.

Les comptes sont les entités ultimes qui achètent des produits et des services B2B. Afin de commercialiser et de vendre efficacement, les spécialistes du marketing B2B doivent connaître non seulement la probabilité d’achat de l’individu, mais aussi celle du compte.

Le marketing basé sur les comptes, en particulier, définit les comptes comme cibles marketing. Les scores de propension à acheter aident considérablement les spécialistes du marketing B2B à établir des priorités parmi les comptes afin d’optimiser leur retour sur investissement.

Le service de notation de compte et de piste prédictive répond aux défis ci-dessus en tirant parti des événements de conversion de l’étape d’opportunité et en les prédisant, et en agrégeant les activités de personne au niveau du compte afin de produire les scores du compte. Les scores sont facilement disponibles sous forme de champs personnalisés sur les profils de personne et de compte, et peuvent être facilement inclus comme critères de segment pour affiner votre audience. Les principaux facteurs d’influence sont également disponibles au niveau des agrégats et des unités afin d’aider les spécialistes du marketing B2B à mieux comprendre les éléments qui ont motivé les scores.

## Comprendre la notation prédictive des pistes et des comptes {#how-it-works}

>[!NOTE]
>
>La source de données [!DNL Marketo] est actuellement requise, car il s’agit de la seule source de données pouvant fournir les événements de conversion au niveau du profil de la personne.

La notation prédictive des pistes et des comptes utilise une méthode d’apprentissage automatique basée sur l’arborescence (boosting aléatoire de forêt/gradient) pour créer le modèle de notation prédictive des pistes.

Les administrateurs peuvent configurer plusieurs objectifs de notation de profil, également appelés modèles, un pour chaque événement de conversion configuré, ce qui permet de générer des scores distincts pour chaque objectif configuré.

La notation prédictive des pistes et des comptes prend en charge les types d’objectifs de conversion et les champs suivants :

| Type d’objectif | Champs |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>Exemple : `opportunityEvent.dataValueChanges.attributeName` est égal `Stage` et `opportunityEvent.dataValueChanges.newValue` est égal `Contract`</ul> |

L’algorithme prend en compte les attributs et données d’entrée suivants :

* Profil de personne

| Champ XDM | Obligatoire/Facultatif |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | Obligatoire |
| `workAddress.country` | Facultatif |
| `extSourceSystemAudit.createdDate` | Obligatoire |
| `extendedWorkDetails.jobTitle` | Facultatif |

>[!NOTE]
> 
>L’algorithme n’examine que le champ `sourceAccountKey.sourceKey` du groupe de champs Person:personComponents .

* Profil de compte

| Champ XDM | Obligatoire/Facultatif |
| --- | --- |
| `accountKey.sourceKey` | Obligatoire |
| `extSourceSystemAudit.createdDate` | Obligatoire |
| `accountOrganization.industry` | Facultatif |
| `accountOrganization.numberOfEmployees` | Facultatif |
| `accountOrganization.annualRevenue.amount` | Facultatif |

* Événement d’expérience

| Champ XDM | Obligatoire/Facultatif |
| --- | --- |
| `_id` | Obligatoire |
| `personKey.sourceKey` | Obligatoire |
| `timestamp` | Obligatoire |
| `eventType` | Obligatoire |

Plusieurs modèles sont pris en charge, avec les limites strictes suivantes définies :

* Chaque environnement de test de production a droit à cinq modèles.
* Chaque environnement de test de développement a droit à un modèle.

Les exigences de qualité des données sont les suivantes :

* Idéalement, il y a deux ans de données les plus récentes à des fins de formation.
* La durée minimale de données requise est de six mois plus la fenêtre de prédiction.
* Pour chaque objectif de prédiction, au moins 10 événements de conversion qualifiés sont requis.

Les tâches de notation sont exécutées tous les jours et les résultats sont enregistrés en tant qu’attributs de profil et attributs de compte, qui peuvent ensuite être utilisés dans les définitions de segment et la personnalisation. Des informations d’analyse d’usine sont également disponibles dans le tableau de bord de présentation du compte.

Consultez la documentation pour plus d’informations sur la façon de [gérer le service de piste prédictive et de notation de compte](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md).

## Affichage des résultats prédictifs de piste et de notation de compte {#how-to-view}

Après l’exécution de la tâche, les résultats sont enregistrés dans un nouveau jeu de données système pour chaque modèle sous le nom `LeadsAI.Scores` - ***nom du score***. Chaque groupe de champs de score peut se trouver à l’emplacement `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`.

| Attribut | Description |
| --- | --- |
| Score | La probabilité relative qu’un profil atteigne l’objectif prévu au cours de la période définie. Cette valeur ne doit pas être traitée comme un pourcentage de probabilité, mais plutôt comme la probabilité d’un profil par rapport à la population globale. Ce score est compris entre 0 et 100. |
| Percentile | Cette valeur fournit des informations concernant la performance d’un profil par rapport à d’autres profils aux notes similaires. Les percentiles sont compris entre 1 et 100. |
| Type de modèle | Le type de modèle sélectionné indique s’il s’agit d’un score de personne ou de compte. |
| Date de la note | Date à laquelle la notation a eu lieu. |
| Facteurs d’influence | Raisons prévues de la probabilité de conversion d’un profil. Les facteurs se composent des attributs suivants :<ul><li>Code : le profil ou l’attribut comportemental qui influencent positivement le score prévu d’un profil.</li><li>Valeur : la valeur du profil ou de l’attribut comportemental.</li><li>Importance : indique le poids que le profil ou l’attribut comportemental a sur le score prévu (faible, moyen, élevé).</li></ul> |

### Affichage des scores du profil client

Pour afficher les scores prédictifs d’un profil de personne, sélectionnez **[!UICONTROL Profils]** sous la section client dans le panneau de gauche, puis saisissez l’espace de noms d’identité et la valeur d’identité. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Afficher]**.

Sélectionnez ensuite le profil dans la liste.

![Profil client](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

La page **[!UICONTROL Detail]** inclut désormais les scores prédictifs. Cliquez sur l’icône de graphique en regard du score prédictif.

![Score prédictif de profil client](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

Une boîte de dialogue contextuelle affiche le score, la distribution globale du score, les principaux facteurs d’influence de ce score et la définition de l’objectif du score.

![Détails sur le score prédictif du profil client](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## Surveillance des tâches de notation de compte et de piste prédictives {#monitoring-jobs}

Le tableau de bord vous permet de surveiller les mesures de base et l’état d’exécution quotidien des tâches. Les mesures incluent :

* Nombre total de profils de personne/compte notés
* Tâche de notation suivante (date)
* Prochaine tâche de formation (date)

Pour plus d’informations, consultez la documentation sur la [surveillance des tâches pour la piste prédictive et la notation de compte](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
