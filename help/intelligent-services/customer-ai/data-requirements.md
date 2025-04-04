---
keywords: Experience Platform ; prise en main ; IA dédiée aux clientes et clients ; rubriques les plus consultées ; entrée d’IA dédiée aux clientes et clients ; sortie d’IA dédiée aux clientes et clients ; exigences de données
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Exigences des données dans l’IA dédiée aux clientes et clients
topic-legacy: Getting started
description: Apprenez-en plus sur les événements, les entrées et les sorties requis utilisés par l’IA dédiée aux clientes et clients.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2551'
ht-degree: 92%

---


# Entrée et sortie dans l’IA dédiée aux clientes et clients

Le document suivant décrit les différents événements, entrées et sorties requis utilisés par l’IA dédiée aux clientes et clients.

## Prise en main {#getting-started}

Voici les étapes pour créer des modèles de propension et identifier les audiences cibles pour le marketing personnalisé dans l’IA dédiée aux clientes et clients :

1. Cas pratiques généraux : comment les modèles de propension aideraient-ils à identifier les audiences cibles pour le marketing personnalisé ? Quels sont mes objectifs commerciaux et les tactiques correspondantes pour atteindre l’objectif ? Où la modélisation de propension peut-elle s’adapter à ce processus ?

2. Cas d’utilisation prioritaires : quelles sont les priorités les plus élevées pour l’entreprise ?

3. Créer des modèles dans l’IA dédiée aux clientes et clients : regardez ce [tutoriel rapide](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html?lang=fr) et reportez-vous à notre [guide de l’interface utilisateur](../customer-ai/user-guide/configure.md) pour un processus étape par étape de création d’un modèle.

4. [Créer des segments](../customer-ai/user-guide/create-segment.md) en utiisant des résultats du modèle.

5. Prenez des actions commerciales ciblées en fonction de ces segments. Surveillez les résultats et effectuez une itération sur les actions à améliorer.

Voici des exemples de configurations pour votre premier modèle.  L’exemple de modèle, élaboré dans ce document, utilise un modèle de l’IA dédiée aux clientes et clients pour prédire qui est susceptible de convertir une activité de vente au détail au cours des 30 prochains jours. Le jeu de données d’entrée est un jeu de données d’Adobe Analytics.

| Étape | Définition | Exemple |
| ---- | ------ | ------- |
| Configuration | Spécifiez des informations de base sur le modèle. | **Nom** : Modèle de propension à l’achat de crayon <br> **Type de modèle** : conversion |
| Sélectionner les données | Spécifiez les jeux de données utilisés pour créer le modèle. | **Jeu de données** : jeu de données d’Adobe Analytics <br> **Identité** : assurez-vous que la colonne d’identité de chaque jeu de données est définie comme identité commune. |
| Définir l’objectif | Définissez l’objectif, la population éligible, les événements personnalisés et les attributs de profil. | **Objectif de prédiction** : sélectionnez la valeur `commerce.purchases.value` égale à crayon <br> **Fenêtre de résultat** : 30 jours. |
| Définir les options | Configurer le planning de l’actualisation du modèle et activer les scores pour Profil | **Planification** : hebdomadaire <br> **Activer pour le profil** : cela doit être activé pour que la sortie du modèle soit utilisée dans la segmentation. |

## Présentation des données {#data-overview}

Les sections suivantes décrivent les différents événements, entrées et sorties requis utilisés par l’IA dédiée aux clientes et clients.

L’IA dédiée aux clients et clients analyse les jeux de données suivants pour prédire l’attrition (lorsqu’un client ou une cliente est susceptible d’arrêter d’utiliser le produit) ou la conversion (lorsqu’un client ou une cliente est susceptible d’effectuer un achat) des scores de propension.

- Données d’Adobe Analytics à l’aide du [connecteur source d’Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Données d’Adobe Audience Manager à l’aide du [connecteur source d’Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [Jeu de données d’événement d’expérience](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html?lang=fr)
- [Jeu de données d’événement d’expérience client](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html#cee-schema?lang=fr)

Vous pouvez ajouter plusieurs jeux de données provenant de sources différentes si chacun des jeux de données partage le même type d’identité (espace de noms), tel qu’un ECID. Pour plus d’informations sur l’ajout de plusieurs jeux de données, consultez le [guide d’utilisation de l’IA dédiée aux clientes et clients](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>Les connecteurs source prennent jusqu’à quatre semaines pour renvoyer les données. Si vous avez récemment configuré un connecteur, vous devez vérifier que le jeu de données contient la longueur minimale de données requise pour l’IA dédiée aux clientes et clients. Veuillez consulter la section [données historiques](#data-requirements) pour vérifier que vous disposez de suffisamment de données pour votre objectif de prédiction.

Le tableau suivant présente la terminologie courante utilisée dans ce document :

| Terme | Définition |
| --- | --- |
| [Modèle de données d’expérience (XDM)](../../xdm/home.md) | XDM est le cadre de base qui permet à Adobe Experience Cloud, optimisé par Experience Platform, de transmettre le message approprié à la bonne personne, sur le bon canal et exactement au bon moment. Experience Platform utilise le système XDM pour organiser les données d’une manière qui facilite leur utilisation pour les services Experience Platform. |
| [Schéma XDM](../../xdm/schema/composition.md) | Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit. Avant que les données puissent être ingérées dans Experience Platform, un schéma doit être créé pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenu dans chaque champ. Les schémas se composent d’une classe XDM de base et de zéro ou plusieurs groupes de champs. |
| [Classe XDM](../../xdm/schema/field-constraints.md) | Tous les schémas XDM décrivent des données qui peuvent être catégorisées comme `Experience Event`. Le comportement des données d’un schéma est défini par la classe du schéma attribuée à celui-ci lorsqu’il est créé pour la première fois. Les classes XDM décrivent le plus petit nombre de propriétés qu’un schéma doit contenir pour représenter un comportement de données spécifique. |
| [Groupes de champs](../../xdm/schema/composition.md) | Un composant qui définit un ou plusieurs champs d’un schéma. Les groupes de champs imposent la manière dont leurs champs apparaissent dans la hiérarchie du schéma, et présentent donc la même structure dans chaque schéma dans lequel ils sont inclus. Les groupes de champs ne sont compatibles qu’avec des classes spécifiques, identifiées par leur attribut `meta:intendedToExtend`. |
| [Type de données](../../xdm/schema/composition.md) | Un composant qui peut également fournir un ou plusieurs champs pour un schéma. Toutefois, contrairement aux groupes de champs, les types de données ne sont pas limités à une classe particulière. Ainsi, les types de données constituent une option plus souple pour décrire des structures de données communes réutilisables sur plusieurs schémas avec des classes potentiellement différentes. Les types de données décrits dans ce document sont pris en charge par les schémas CEE et Adobe Analytics. |
| [Real-time Customer Profile](../../profile/home.md) | Le profil client en temps réel fournit un profil de consommateur centralisé pour une gestion d’expérience ciblée et personnalisée. Chaque profil contient des données agrégées sur tous les systèmes ainsi que des comptes horodatés exploitables d’événements impliquant les personnes concernées par l’un des systèmes que vous utilisez avec Experience Platform. |

## Données de sortie de l’IA dédiée aux clientes et clients {#customer-ai-input-data}

Pour les jeux de données d’entrée, tels qu’Adobe Analytics et Adobe Audience Manager, les connecteurs sources respectifs mappent directement les événements dans ces groupes de champs standards (Commerce, Web, Application et Recherche) par défaut pendant le processus de connexion. Le tableau ci-dessous présente les champs d’événement dans les groupes de champs standards par défaut pour l’IA dédiée aux clientes et clients.

Pour plus d’informations sur le mappage des données d’Adobe Analytics ou des données d’Audience Manager, consultez le [guide de mappages de champs](../../sources/connectors/adobe-applications/mapping/audience-manager.md) d’Analytics ou d’Audience Manager.

Vous pouvez utiliser des schémas XDM d’événement d’expérience ou d’événement d’expérience client pour les jeux de données d’entrée qui ne sont pas renseignés via l’un des connecteurs ci-dessus. D’autres groupes de champs XDM peuvent être ajoutés pendant le processus de création de schéma. Les groupes de champs peuvent être fournis par Adobe, comme les groupes de champs standard ou un groupe de champs personnalisé, qui correspond à la représentation des données dans Experience Platform.

>[!IMPORTANT]
>
>Vous devez vous assurer que les données sont renseignées dans ces jeux de données d’entrée. Si aucun événement des groupes de champs standards n’est trouvé dans les jeux de données d’entrée, vous devez ajouter des événements personnalisés pendant le processus de configuration. Consultez les détails sur les événements personnalisés.

### Groupes de champs standards utilisés par l’IA dédiée aux clientes et clients {#standard-events}

Les événements d’expérience sont utilisés pour déterminer divers comportements de clientèle. Selon la structure de vos données, les types d’événements répertoriés ci-dessous peuvent ne pas englober tous les comportements de votre clientèle. C’est à vous de déterminer quels champs contiennent les données nécessaires pour identifier clairement et sans ambiguïté l’activité de l’utilisateur ou de l’utilisatrice sur le web ou sur un autre canal. Selon l’objectif de prédiction, les champs requis peuvent changer.

>[!NOTE]
>
>Si vous utilisez des données d’Adobe Analytics ou d’Adobe Audience Manager, le schéma est automatiquement créé avec les événements standards requis pour capturer vos données. Si vous créez votre propre schéma EE personnalisé pour capturer des données, vous devez tenir compte des groupes de champs nécessaires pour capturer vos données.

L’IA dédiée aux clientes et clients utilise par défaut les événements de ces quatre groupes de champs standards : Commerce, Web, Application et Recherche. Il n’est pas nécessaire d’avoir des données pour chaque événement dans les groupes de champs standards répertoriés ci-dessous, mais certains événements sont requis pour certains scénarios. Si des événements sont disponibles dans les groupes de champs standards, il est recommandé de les inclure dans votre schéma. Par exemple, si vous souhaitez créer un modèle d’IA dédiée aux clientes et clients pour prédire les événements d’achat, il est utile de disposer de données provenant des groupes de champs des détails des pages Commerce et Web.

Pour afficher un groupe de champs dans l’interface utilisateur d’Experience Platform, sélectionnez l’onglet **[!UICONTROL Schémas]** dans le rail de gauche, puis sélectionnez l’onglet **[!UICONTROL Groupes de champs]**.

| Groupe de champs | Type d’événement | Chemin d’accès au champ XDM |
| --- | --- | --- |
| [!UICONTROL Détails Commerce] | order | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListViews | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | checkouts | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | purchases | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemovals | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | productListOpens | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | productViews | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL Détails Web] | webVisit | `web.webPageDetails.name` |
|  | webInteraction | `web.webInteraction.linkClicks.value` |
| [!UICONTROL Détails Application] | applicationCloses | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | applicationCrashes | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | applicationFeatureUsages | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | applicationFirstLaunches | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> `application.name` </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> `application.name` </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL Détails Recherche] | search | `search.keywords` |

En outre, l’IA dédiée aux clientes et clients peut utiliser les données d’abonnement pour créer de meilleurs modèles d’attrition. Les données d’abonnement sont nécessaires pour chaque profil utilisant le format de type de données [[!UICONTROL Abonnement]](../../xdm/data-types/subscription.md). La plupart des champs sont facultatifs, cependant, pour un modèle d’attrition optimal, il est vivement recommandé de fournir des données pour autant de champs que possible, par exemple, `startDate`, `endDate`, ainsi que tout autre détail pertinent. Contactez l’équipe de votre compte pour obtenir une prise en charge supplémentaire de cette fonctionnalité.

### Ajouter des événements personnalisés et des attributs de profil {#add-custom-events}

Si vous disposez d’informations que vous souhaitez inclure en plus des [champs d’événement standards](#standard-events) par défaut utilisés par l’IA dédiée aux clientes et clients, vous pouvez utiliser la [configuration d’événement personnalisé](./user-guide/configure.md#custom-events) pour améliorer les données utilisées par le modèle.

#### Quand utiliser des événements personnalisés ?

Les événements personnalisés sont nécessaires lorsque les jeux de données sélectionnés à l’étape de sélection de jeu de données ne contiennent *aucun* des champs d’événement par défaut utilisés par l’IA dédiée aux clientes et clients. L’IA dédiée aux clientes et clients a besoin d’informations sur au moins un événement de comportement d’utilisateur ou d’utilisatrice autre que le résultat.

Les événements personnalisés s’avèrent utiles pour :

- Intégrer les connaissances du domaine ou l’expertise préalable dans le modèle.

- Améliorer la qualité du modèle prédictif.

- Obtenir des informations et des interprétations supplémentaires.

Les meilleurs éléments pour les événements personnalisés sont les données qui contiennent des connaissances de domaine qui peuvent être prédictives du résultat. Voici quelques exemples généraux d’événements personnalisés :

- Enregistrer un compte

- S’abonner à la newsletter

- Appeler le service clientèle

Vous trouverez ci-dessous une sélection d’exemples d’événements personnalisés spécifiques au secteur :

| Secteur industriel | Événements personnalisés |
| --- | --- |
| Vente au détail | Transaction en magasin <br> Inscription à la carte de club <br> Bon mobile. |
| Divertissement | Achat d’un abonnement de saison <br> Streaming de vidéos. |
| Hôtellerie | Réservation d’un restaurant <br> Achat de points de fidélité. |
| Voyage | Ajout d’informations sur les voyageurs et voyageuses connus Acheter des miles. |
| Communications | Mise à niveau/rétrogradation/annulation de l’abonnement. |

Pour être sélectionnés, les événements personnalisés doivent représenter des actions initiées par l’utilisateur ou l’utilisatrice. Par exemple, « Envoi d’e-mail » est une action lancée par une personne spécialiste du marketing et non par l’utilisateur ou l’utilisatrice. Cette action ne doit donc pas être utilisée comme événement personnalisé.

### Données historiques

L’IA dédiée aux clientes et clients nécessite des données historiques pour la formation des modèles. La durée nécessaire à l’existence des données dans le système est déterminée par deux éléments clés : la fenêtre de résultat et la population éligible.

Par défaut, l’IA dédiée aux clientes et clients recherche un utilisateur ou une utilisatrice qui a eu une activité au cours des 45 derniers jours si aucune définition de population éligible n’est fournie pendant la configuration de l’application. En outre, l’IA dédiée aux clientes et clients nécessite au moins 500 événements admissibles et 500 événements non admissibles (1 000 au total) à partir de données historiques en fonction d’une définition d’objectif prédite.

Les exemples suivants montrent l’utilisation d’une formule simple qui vous aide à déterminer la quantité minimale de données requise. Si vous disposez de données plus volumineuses que le minimum requis, votre modèle est susceptible de fournir des résultats plus précis. Si vous disposez de moins que la quantité minimale requise, le modèle échoue, car il n’y a pas suffisamment de données pour la formation du modèle.

L’IA dédiée aux clientes et clients utilise un modèle de survie pour estimer la probabilité qu’un événement se produise à un moment donné et identifier les facteurs d’influence, parallèlement à un apprentissage supervisé qui définit les populations positives et négatives, et à des arbres de décision tels que `lightgbm` pour générer un score de probabilité.

**Formule** :

Pour décider de la durée minimale requise des données du système :

- La durée minimale de création des fonctionnalités est de 30 jours. Comparez la fenêtre de recherche en amont d’éligibilité avec 30 jours :

   - Si la fenêtre de recherche en amont d’éligibilité est supérieure à 30 jours, l’exigence de données = fenêtre de recherche en amont d’éligibilité + fenêtre de résultat.

   - Dans le cas contraire, les exigences de données = 30 jours + fenêtre de résultat.

** S’il existe plusieurs conditions pour définir la population éligible, la fenêtre de recherche en amont d’éligibilité est la plus longue.

>[!NOTE]
>
>30 est le nombre minimum de jours requis pour la population éligible. Si ce paramètre n’est pas fourni, la valeur par défaut est de 45 jours.

**Exemples** :

- Vous souhaitez prédire si un client ou une cliente est susceptible d’acheter une montre dans les 30 prochains jours pour ceux qui ont une activité web au cours des 60 derniers jours.

   - Fenêtre de recherche en amont d’éligibilité = 60 jours

   - Fenêtre de résultat = 30 jours

   - Données requises = 60 jours + 30 jours = 90 jours

- Vous souhaitez prédire si l’utilisateur ou l’utilisatrice est susceptible d’acheter une montre au cours des 7 prochains jours **sans** fournir une population éligible explicite. Dans ce cas, la population éligible est définie par défaut sur « personnes qui ont eu une activité au cours des 45 derniers jours » et la fenêtre de résultat est de 7 jours.

   - Fenêtre de recherche en amont d’éligibilité = 45 jours

   - Fenêtre de résultat = 7 jours

   - Données requises = 45 jours + 7 jours = 52 jours

- Vous souhaitez prédire si le client ou la cliente est susceptible d’acheter une montre dans les 7 prochains jours pour ceux qui ont une activité web au cours des 7 derniers jours.

   - Fenêtre de recherche en amont d’éligibilité = 7 jours

   - Données minimales requises pour créer des fonctionnalités = 30 jours

   - Fenêtre de résultat = 7 jours

   - Données requises = 30 jours + 7 jours = 37 jours

Bien que l’IA dédiée aux clientes et clients exige un temps minimal pour que les données existent dans le système, elle fonctionne également mieux avec les données récentes. En utilisant des données comportementales plus récentes, l’IA dédiée aux clientes et clients est susceptible de générer une prédiction plus précise du comportement futur d’un utilisateur ou d’une utilisatrice.

## Données de sortie de Customer AI {#customer-ai-output-data}

Customer AI génère plusieurs attributs pour les profils individuels supposés éligibles. Il y a deux façons de consommer le score (sortie) en fonction de ce que vous avez provisionné. Si vous disposez d’un jeu de données activé pour Real-time Customer Profile, vous pouvez utiliser les informations de Real-time Customer Profile dans le [Créateur de segments](../../segmentation/ui/segment-builder.md). Si vous ne disposez pas d’un jeu de données activé pour le profil, vous pouvez [télécharger l’ensemble de données de la sortie de l’IA dédiée aux clientes et clients](./user-guide/download-scores.md) disponible sur le lac de données.

Le jeu de données de sortie se trouve dans l’espace de travail Experience Platform **Jeux de données**. Tous les jeux de données de sortie de l’IA dédiée aux clientes et clients commencent par le nom **Customer AI Scores - NAME_OF_APP**. De même, tous les schémas de sortie de Customer AI commencent par le nom **Customer AI Schema - Name_of_app**.

![Nom des jeux de données de sortie dans Customer AI](./images/user-guide/cai-schema-name-of-app.png)

Le tableau ci-dessous décrit les différents attributs trouvés dans les sorties de Customer AI :

| Attribut | Description |
| ----- | ----------- |
| [!UICONTROL Score] | La probabilité relative qu’un client atteigne l’objectif prévu au cours de la période définie. Cette valeur ne doit pas être considérée comme un pourcentage de probabilité, mais plutôt comme la probabilité d’un individu par rapport à la population totale. Ce score est compris entre 0 et 100. |
| Probabilité | Cet attribut est la probabilité réelle qu’un profil atteigne l’objectif prévu au cours de la période définie. Si vous comparez les sorties en fonction d’objectifs différents, nous vous recommandons de prendre en compte la probabilité plutôt que le centile ou le score. Vous devez toujours utiliser la probabilité lorsque vous essayez de déterminer la probabilité moyenne sur la population éligible, car la probabilité a tendance à être basse pour les événements qui ne se produisent pas fréquemment. Les valeurs des probabilités sont comprises entre 0 et 1. |
| Percentile | Cette valeur fournit des informations concernant la performance d’un profil par rapport à d’autres profils aux notes similaires. Par exemple, un profil dont le rang de percentile est de 99 pour l’attrition indique qu’il y a une forte chance d’attrition par rapport à 99 % des autres profils évalués. Les centiles sont compris entre 1 et 100. |
| Type de propension | Le type de propension sélectionné. |
| Date de la note | Date à laquelle la notation a eu lieu. |
| Facteurs d’influence | Il s’agit des raisons prédites pour lesquelles un profil est susceptible de procéder à la conversion ou à l’attrition. Ces facteurs se composent des attributs suivants :<ul><li>Code : le profil ou l’attribut comportemental qui influencent positivement le score prévu d’un profil. </li><li>Valeur : la valeur du profil ou de l’attribut comportemental.</li><li>Importance : indique le poids que le profil ou l’attribut comportemental a sur le score prévu (faible, moyen, élevé)</li></ul> |

## Étapes suivantes {#next-steps}

Une fois que vous avez préparé vos données et que l’ensemble de vos informations d’identification et schémas sont en place, reportez-vous au guide de [Configuration d’une instance Customer AI](./user-guide/configure.md) qui vous guide tout au long d’un tutoriel détaillé sur la création d’une instance Customer AI.