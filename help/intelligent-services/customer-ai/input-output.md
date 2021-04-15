---
keywords: Experience Platform ; prise en main ; assistance client ; rubriques populaires ; entrée d’assistance client ; sortie d’assistance client
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Entrée et sortie dans l’API client
topic: Prise en main
description: En savoir plus sur les événements, les intrants et les extrants requis utilisés par l’API client.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
translation-type: tm+mt
source-git-commit: 2ef2a6431865e8ffdc2abd6cf527249e8b5ca4d0
workflow-type: tm+mt
source-wordcount: '2878'
ht-degree: 17%

---

# Entrée et sortie dans l’API client

Le document suivant décrit les différents événements, intrants et extrants requis utilisés dans l’IA du client.

## Prise en main

L’API du client analyse l’un des jeux de données suivants pour prédire les scores de propension de conversion ou de déclenchement :

- Jeu de données du Événement d’expérience de consommation (CEE)
- Données Adobe Analytics à l’aide du [connecteur source Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Données Adobe Audience Manager à l’aide du [connecteur de source d’Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)

>[!IMPORTANT]
>
>Les connecteurs source mettent jusqu’à quatre semaines pour renvoyer les données. Si vous avez récemment configuré un connecteur, vous devez vérifier que le jeu de données contient la longueur minimale de données requise pour l’IA du client. Consultez la section [données historiques](#data-requirements) pour vérifier que vous disposez de suffisamment de données pour atteindre votre objectif de prévision.

Ce document exige une compréhension de base du schéma CEE. Veuillez consulter la documentation [Préparation des données des services intelligents](../data-preparation.md) avant de continuer.

Le tableau ci-dessous présente la terminologie commune utilisée dans ce document :

| Terme | Définition |
| --- | --- |
| [Modèle de données d’expérience (XDM)](../../xdm/home.md) | XDM est le cadre fondateur qui permet à Adobe Experience Cloud, soutenu par Adobe Experience Platform, de transmettre le bon message à la bonne personne, sur le bon canal, exactement au bon moment. La méthodologie sur laquelle Experience Platform repose, à savoir le système XDM, rend les schémas de modèles de données d’expérience opérationnels pour qu’ils soient utilisés par les services de Platform. |
| Schéma XDM | Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit. Avant que les données puissent être ingérées dans la plate-forme, un schéma doit être composé pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenu dans chaque champ. Les schémas se composent d&#39;une classe XDM de base et de mixins nuls ou plus. |
| Classe XDM | Tous les schémas XDM décrivent des données pouvant être catégorisées en tant qu’enregistrement ou série temporelle. Le comportement des données d’un schéma est défini par la classe du schéma, qui est affectée à un schéma lors de sa création. Les classes XDM décrivent le plus petit nombre de propriétés qu’un schéma doit contenir pour représenter un comportement de données spécifique. |
| [Mixins](../../xdm/schema/composition.md) | Composant qui définit un ou plusieurs champs d’un schéma. Les mixins appliquent la manière dont leurs champs apparaissent dans la hiérarchie de l’schéma et présentent donc la même structure dans chaque schéma dans lequel ils sont inclus. Les mixins ne sont compatibles qu’avec des classes spécifiques, identifiées par leur attribut `meta:intendedToExtend`. |
| [Type de données](../../xdm/schema/composition.md) | Composant pouvant également fournir un ou plusieurs champs pour un schéma. Toutefois, contrairement aux mixins, les types de données ne sont pas limités à une classe particulière. Ainsi, les types de données constituent une option plus souple pour décrire des structures de données communes réutilisables sur plusieurs schémas avec des classes potentiellement différentes. Les types de données décrits dans le présent document sont pris en charge par les schémas CEE et Adobe Analytics. |
| Churn | Mesure du pourcentage de comptes qui annulent ou choisissent de ne pas renouveler leurs abonnements. Un taux de rendement élevé peut avoir une incidence négative sur les recettes périodiques mensuelles (RMR) et peut également indiquer un mécontentement à l’égard d’un produit ou d’un service. |
| [Real-time Customer Profile](../../profile/home.md) | Real-time Customer Profile fournit un profil de consommateur centralisé pour une gestion d’expérience ciblée et personnalisée. Chaque profil contient des données agrégées sur tous les systèmes ainsi que des comptes horodatés exploitables d’événements impliquant les personnes concernées par l’un des systèmes que vous utilisez avec Experience Platform. |

## Données d’entrée d’API client

>[!TIP]
>
> L’IA du client détermine automatiquement quels événements sont utiles pour les prédictions et déclenche un avertissement si les données disponibles ne sont pas suffisantes pour générer des prédictions de qualité.

L’IA du client prend en charge les données CEE, Adobe Analytics et Adobe Audience Manager. Le schéma CEE exige que vous ajoutiez des mixins pendant le processus de création du schéma. Si vous utilisez des jeux de données Adobe Analytics ou Adobe Audience Manager, le connecteur source mappe directement les événements standard (Commerce, Détails de la page Web, Application et Recherche) répertoriés ci-dessous pendant le processus de connexion.

Pour plus d’informations sur le mappage des données Adobe Analytics ou des données d’Audience Manager, consultez le guide [Mappages de champs Analytics](../../sources/connectors/adobe-applications/analytics.md) ou [Mappages de champs d’Audience Manager](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

### Événements standard utilisés par l’API client {#standard-events}

Les Événements d’expérience XDM sont utilisés pour déterminer divers comportements de client. Selon la structure de vos données, les types d&#39;événement répertoriés ci-dessous peuvent ne pas englober tous les comportements de vos clients. Il vous appartient de déterminer quels champs disposent des données nécessaires pour identifier clairement et sans ambiguïté l’activité des utilisateurs Web. En fonction de l’objectif de prédiction, les champs nécessaires peuvent changer.

L’IA du client repose sur différents types d&#39;événement pour la création de fonctionnalités de modèle. Ces types d&#39;événement sont automatiquement ajoutés à votre schéma à l’aide de plusieurs mixins XDM.

>[!NOTE]
>
>Si vous utilisez des données Adobe Analytics ou Adobe Audience Manager, le schéma est automatiquement créé avec les événements standard requis pour capturer vos données. Si vous créez votre propre schéma CEE personnalisé pour capturer des données, vous devez tenir compte des mixins nécessaires pour capturer vos données.

Il n&#39;est pas nécessaire de disposer de données pour chacun des événements standard énumérés ci-dessous, mais certains événements sont requis pour certains scénarios. Si vous disposez de l’une des données de événement standard, il est recommandé de l’inclure dans votre schéma. Par exemple, si vous souhaitez créer une application d’API client pour prédire les événements d’achat, il serait utile d’avoir des données des types de données `Commerce` et `Web page details`.

Pour vue d’un mixin dans l’interface utilisateur de la plateforme, sélectionnez l’onglet **[!UICONTROL Schémas]** dans le rail de gauche, puis sélectionnez l’onglet **[!UICONTROL Mixins]**.


| Mixin | Type d&#39;événement | Chemin du champ XDM |
| --- | --- | --- |
| [!UICONTROL Détails du commerce] | order | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | checkouts | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | purchases | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemovals | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListOpens | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Détails Web] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL Détails de l’application] | applicationCloses | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrashes | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsages | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL Détails de la recherche] | rechercher | search.keywords |

En outre, l’API du client peut utiliser les données d’abonnement pour créer de meilleurs modèles de fonctionnement. Des données d’Abonnement sont nécessaires pour chaque profil à l’aide du format de type de données [[!UICONTROL Abonnement]](../../xdm/data-types/subscription.md). La plupart des champs sont facultatifs, cependant, pour un modèle d’exécution optimal, il est fortement recommandé de fournir des données pour autant de champs que possible, par exemple, `startDate`, `endDate` et tout autre détail pertinent.

### Données historiques {#data-requirements}

L’IA du client requiert des données historiques pour la formation au modèle, mais la quantité de données requise est basée sur deux éléments clés : fenêtre de résultats et population admissible.

Par défaut, l’API du client recherche un utilisateur qui a eu activité au cours des 120 derniers jours si aucune définition de population éligible n’est fournie lors de la configuration de l’application. En outre, l’IA du client requiert au moins 500 événements qualifiants et 500  non qualifiés (1 000 au total) de données historiques basées sur une définition d’objectif prévue.

Les exemples suivants fournis utilisent une formule simple pour vous aider à déterminer la quantité minimale de données requise. Si vous avez plus que les exigences minimales, votre modèle est susceptible de fournir des résultats plus précis. Si vous disposez de moins de la quantité minimale requise, le modèle échoue car il n&#39;y a pas une quantité suffisante de données pour la formation au modèle.

**Formule**:

Longueur minimale des données requises = population admissible + fenêtre de résultat

>[!NOTE]
>
> 30 est le nombre minimum de jours requis pour la population admissible. Si ce n’est pas le cas, la valeur par défaut est de 120 jours.

Exemples :

- Vous souhaitez prédire si un client est susceptible d’acheter une montre dans les 30 prochains jours. Vous souhaitez également noter les utilisateurs qui ont une certaine activité Web au cours des 60 derniers jours. Dans ce cas, la longueur minimale des données est de 60 jours + 30 jours. La population éligible est de 60 jours et la fenêtre de résultats est de 30 jours pour un total de 90 jours.

- Vous souhaitez prédire si l’utilisateur est susceptible d’acheter une montre dans les 7 prochains jours. Dans ce cas, la longueur minimale des données est de 120 jours + 7 jours. La population éligible est définie par défaut sur 120 jours et la fenêtre de résultats est de 7 jours pour un total de 127 jours.

- Vous souhaitez prédire si le client est susceptible d’acheter une montre dans les 7 prochains jours. Vous souhaitez également noter les utilisateurs qui ont une certaine activité Web au cours des 7 derniers jours. Dans ce cas, la longueur minimale des données est de 30 jours + 7 jours. La population admissible a besoin d&#39;un minimum de 30 jours et la fenêtre de résultats est de 7 jours pour un total de 37 jours.

Outre les données minimales requises, l’API du client fonctionne également mieux avec les données récentes. Dans ce cas d’utilisation, l’API du client effectue une prévision pour l’avenir en fonction des données comportementales récentes d’un utilisateur. En d&#39;autres termes, des données plus récentes sont susceptibles de produire une prévision plus précise.

### Exemples de scénarios

Dans cette section, différents scénarios pour les instances d’API client sont décrits ainsi que les types d&#39;événement requis et recommandés. Pour plus d&#39;informations sur le mixin et son chemin de champ, consultez le [tableau de événements standard](#standard-events) ci-dessus.

>[!NOTE]
>
> Les types d&#39;événement requis sont utilisés pour identifier clairement et sans ambiguïté l’activité des utilisateurs du Web. Le nombre de types d&#39;événement requis changera en fonction de l’objectif de prédiction et de la structure de votre schéma. Si vous n’êtes pas certain qu’un type d&#39;événement particulier est nécessaire, il est recommandé d’inclure ce type d&#39;événement lors de la création de votre schéma CEE. Si vous utilisez des données Adobe Analytics ou Adobe Audience Manager, les événements standard requis doivent être disponibles en fonction des données en flux continu.

### Scénario 1 : Conversion d’achats sur un site Web de vente au détail d’e-commerce

**Objectif de la prévision :** Prévoyez la propension de conversion des profils admissibles à acheter un certain article d’habillement sur un site Web.

**Types d&#39;événement standard requis :**

Les types d&#39;événement répertoriés ci-dessous sont requis pour une sortie optimale de l’IA du client avec cet objectif de prédiction particulier. Il est possible d’exclure un événement requis en fonction de votre objectif de prédiction, mais l’exclusion de plusieurs événements peut entraîner des résultats médiocres.

- order
- passages en caisse
- achats
- webVisit
- rechercher

**Types d&#39;événement standard recommandés supplémentaires :**

Tout des [types d&#39;événement](#standard-events) restants peut être requis en fonction de la complexité de votre objectif et de la population éligible lors de la configuration de votre instance d’API client. Si les données sont disponibles pour un type de données particulier, il est recommandé de les inclure dans votre schéma.

### Scénario 2 : Conversion d’Abonnement sur un site Web de service de diffusion en continu de médias

**Objectif de la prévision :** Prévoyez la propension de conversion des abonnements pour les profils admissibles à s&#39;engager à un certain niveau d&#39;abonnement, tel qu&#39;un régime standard ou un régime de primes.

**Types d&#39;événement standard requis :**

Les types d&#39;événement répertoriés ci-dessous sont requis pour une sortie optimale de l’IA du client avec cet objectif de prédiction particulier. Il est possible d’exclure un événement requis en fonction de votre objectif de prédiction, mais l’exclusion de plusieurs événements peut entraîner des résultats médiocres.

- order
- passages en caisse
- achats
- webVisit
- rechercher

Dans cet exemple, `order`, `checkouts` et `purchases` sont utilisés pour indiquer qu&#39;un abonnement a été acheté et son type.

De plus, pour un modèle précis, il est conseillé d&#39;utiliser certaines des propriétés disponibles dans le type de données d&#39;abonnement [](../../xdm/data-types/subscription.md).

**Types d&#39;événement standard recommandés supplémentaires :**

Tout des [types d&#39;événement](#standard-events) restants peut être requis en fonction de la complexité de votre objectif et de la population éligible lors de la configuration de votre instance d’API client. Si les données sont disponibles pour un type de données particulier, il est recommandé de les inclure dans votre schéma.

### Scénario 3 : Consulté sur un site Web de vente au détail d&#39;e-commerce

**Objectif de prévision :** prévoir la probabilité qu’un événement d’achat ne se produise pas.

**Types d&#39;événement standard requis :**

Les types d&#39;événement répertoriés ci-dessous sont requis pour une sortie optimale de l’IA du client avec cet objectif de prédiction particulier. Il est possible d’exclure un événement requis en fonction de votre objectif de prédiction, mais l’exclusion de plusieurs événements peut entraîner des résultats médiocres.

- order
- passages en caisse
- achats
- webVisit
- rechercher

**Types d&#39;événement standard recommandés supplémentaires :**

Tout des [types d&#39;événement](#standard-events) restants peut être requis en fonction de la complexité de votre objectif et de la population éligible lors de la configuration de votre instance d’API client. Si les données sont disponibles pour un type de données particulier, il est recommandé de les inclure dans votre schéma.

### Scénario 4 : Mettre à niveau la conversion sur un site Web de vente au détail

**Objectif de prédiction :** Prévoyez la propension à acheter de la population qui a acheté un produit spécifique pour acheter un nouveau produit associé.

**Types d&#39;événement standard requis :**

Les types d&#39;événement répertoriés ci-dessous sont requis pour une sortie optimale de l’IA du client avec cet objectif de prédiction particulier. Il est possible d’exclure un événement requis en fonction de votre objectif de prédiction, mais l’exclusion de plusieurs événements peut entraîner des résultats médiocres.

- order
- passages en caisse
- achats
- webVisit
- rechercher

**Types d&#39;événement standard recommandés supplémentaires :**

Tout des [types d&#39;événement](#standard-events) restants peut être requis en fonction de la complexité de votre objectif et de la population éligible lors de la configuration de votre instance d’API client. Si les données sont disponibles pour un type de données particulier, il est recommandé de les inclure dans votre schéma.

### Scénario 5 : Désabonnez-vous (brutal) sur un site d&#39;information en ligne

**Objectif de prédiction :** Prévoyez la propension de la population admissible à se désabonner d’un service le mois prochain.

**Types d&#39;événement standard requis :**

Les types d&#39;événement répertoriés ci-dessous sont requis pour une sortie optimale de l’IA du client avec cet objectif de prédiction particulier. Il est possible d’exclure un événement requis en fonction de votre objectif de prédiction, mais l’exclusion de plusieurs événements peut entraîner des résultats médiocres.

- webVisit
- rechercher

De plus, pour un modèle précis, il est conseillé d&#39;utiliser certaines des propriétés disponibles dans le type de données d&#39;abonnement [](../../xdm/data-types/subscription.md).

**Types d&#39;événement standard recommandés supplémentaires :**

Tout des [types d&#39;événement](#standard-events) restants peut être requis en fonction de la complexité de votre objectif et de la population éligible lors de la configuration de votre instance d’API client. Si les données sont disponibles pour un type de données particulier, il est recommandé de les inclure dans votre schéma.

### Scénario 6 : Lancement de l’application mobile

**Objectif de prévision :** Prévoyez la propension des profils admissibles à lancer une application mobile payante au cours des X prochains jours. Cela est similaire à la prévision de l’indicateur de performance clé (IPC) des &quot;utilisateurs Principaux mensuels&quot;.

**Types d&#39;événement standard requis :**

Les types d&#39;événement répertoriés ci-dessous sont requis pour une sortie optimale de l’IA du client avec cet objectif de prédiction particulier. Il est possible d’exclure un événement requis en fonction de votre objectif de prédiction, mais l’exclusion de plusieurs événements peut entraîner des résultats médiocres.

- order
- passages en caisse
- achats
- webVisit
- applicationCloses
- applicationCrashes
- applicationFeatureUsages
- applicationFirstLaunches
- applicationInstalls
- applicationLaunches
- applicationUpgrades

Dans cet exemple, `order`, `checkouts` et `purchases` sont utilisés lorsqu&#39;une application mobile doit être achetée.

**Types d&#39;événement standard recommandés supplémentaires :**

Tout des [types d&#39;événement](#standard-events) restants peut être requis en fonction de la complexité de votre objectif et de la population éligible lors de la configuration de votre instance d’API client. Si les données sont disponibles pour un type de données particulier, il est recommandé de les inclure dans votre schéma.

### Scénario 7 : Caractéristiques réalisées (Adobe Audience Manager)

**Objectif de la prédiction :** Prévoyez la propension à réaliser certains traits.

**Types d&#39;événement standard requis :**

Pour utiliser les caractéristiques de Adobe Audience Manager, vous devez créer une connexion source à l&#39;aide du [connecteur source d&#39;Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). Le connecteur source crée automatiquement le schéma avec les mixins appropriés. Il n’est pas nécessaire d’ajouter manuellement des types d&#39;événement supplémentaires pour que le schéma fonctionne avec l’IA du client.

Lorsque vous configurez une nouvelle instance d’IA client, `audienceName` et `audienceID` peuvent être utilisés pour sélectionner une caractéristique particulière à évaluer lors de la définition de votre objectif.

## Données de sortie de Customer AI

Customer AI génère plusieurs attributs pour les profils individuels supposés éligibles. Il existe deux façons de consommer le score (sortie) en fonction de ce que vous avez configuré. Si vous disposez d’un jeu de données compatible Profil client en temps réel, vous pouvez utiliser des informations issues du Profil client en temps réel dans le [créateur de segments](../../segmentation/ui/segment-builder.md). Si vous ne disposez pas d’un jeu de données compatible avec les Profils, vous pouvez [télécharger le fichier de sortie d’IA du client](./user-guide/download-scores.md) disponible sur le lac de données.

>[!NOTE]
>
> Les valeurs de sortie sont utilisées par le Profil client en temps réel qui peut être utilisé pour créer et définir des segments.

Le tableau ci-dessous décrit les différents attributs trouvés dans les sorties de Customer AI :

| Attribut | Description |
| ----- | ----------- |
| Score | La probabilité relative qu’un client atteigne l’objectif prévu au cours de la période définie. Cette valeur ne doit pas être considérée comme un pourcentage de probabilité, mais plutôt comme la probabilité d’un individu par rapport à la population totale. Ce score est compris entre 0 et 100. |
| Probabilité | Cet attribut est la probabilité réelle qu’un profil atteigne l’objectif prévu au cours de la période définie. Si vous comparez les sorties en fonction d’objectifs différents, nous vous recommandons de prendre en compte le percentile ou le score de probabilité. Vous devez toujours utiliser la probabilité lorsque vous essayez de déterminer la probabilité moyenne sur la population éligible, car la probabilité a tendance à être basse pour les événements qui ne se produisent pas fréquemment. Les valeurs des probabilités sont comprises entre 0 et 1. |
| Percentile | Cette valeur fournit des informations concernant la performance d’un profil par rapport à d’autres profils aux notes similaires. Par exemple, un profil dont le rang de percentile est de 99 pour l’attrition indique qu’il y a une forte chance d’attrition par rapport à 99 % des autres profils évalués. Les percentiles sont compris entre 1 et 100. |
| Type de propension | Le type de propension sélectionné. |
| Date de la note | Date à laquelle la notation a eu lieu. |
| Facteurs d’influence | Raisons prévues de la probabilité de conversion ou d’attrition d’un profil. Les facteurs se composent des attributs suivants :<ul><li>Code : le profil ou l’attribut comportemental qui influencent positivement le score prévu d’un profil. </li><li>Valeur : la valeur du profil ou de l’attribut comportemental.</li><li>Importance : indique le poids que le profil ou l’attribut comportemental a sur le score prévu (faible, moyen, élevé)</li></ul> |

## Étapes suivantes {#next-steps}

Une fois vos données préparées et vos informations d’identification et schémas en place, début en suivant le guide [Configurer une instance d’API client](./user-guide/configure.md). Ce guide vous guide tout au long de la création d’une instance pour l’IA du client.
