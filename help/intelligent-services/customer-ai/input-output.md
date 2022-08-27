---
keywords: Experience Platform;prise en main;service clientèle;rubriques les plus consultées;entrée de l’assistance client;sortie de l’assistance client
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Entrée et sortie dans Customer AI
topic-legacy: Getting started
description: En savoir plus sur les événements, les entrées et les sorties requis utilisés par Customer AI.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: e0e96a52e30f5c34e0695c3e291bed9b6c085e00
workflow-type: tm+mt
source-wordcount: '3195'
ht-degree: 15%

---

# Entrée et sortie dans Customer AI

Le document suivant décrit les différents événements, entrées et sorties requis utilisés dans Customer AI.

## Prise en main

Customer AI analyse l’un des jeux de données suivants pour prédire les scores de propension à l’attrition ou à la conversion :

- les données Adobe Analytics à l’aide de la variable [Connecteur source Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Données Adobe Audience Manager utilisant la variable [Connecteur source d’Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- Jeu de données d’événement d’expérience (EE)
- Jeu de données d’événements d’expérience client (CEE)

Vous pouvez ajouter plusieurs jeux de données provenant de sources différentes si chacun des jeux de données partage le même type d’identité (espace de noms), tel qu’un ECID. Pour plus d’informations sur l’ajout de plusieurs jeux de données, consultez la section [Guide d’utilisation de Customer AI](./user-guide/configure.md#select-data)

>[!IMPORTANT]
>
>Les connecteurs source prennent jusqu’à quatre semaines pour renvoyer les données. Si vous avez récemment configuré un connecteur, vous devez vérifier que le jeu de données contient la longueur minimale de données requise pour Customer AI. Veuillez consulter la section [données historiques](#data-requirements) pour vérifier que vous disposez de suffisamment de données pour votre objectif de prédiction.

Ce document nécessite une compréhension de base du schéma CEE. Veuillez consulter la section [Préparation des données des services intelligents](../data-preparation.md) avant de continuer.

Le tableau suivant présente la terminologie courante utilisée dans ce document :

| Terme | Définition |
| --- | --- |
| [Modèle de données d’expérience (XDM)](../../xdm/home.md) | XDM est le cadre de base qui permet à Adobe Experience Cloud, optimisé par Adobe Experience Platform, de diffuser le message approprié à la bonne personne, sur le bon canal, exactement au bon moment. La méthodologie sur laquelle Experience Platform repose, à savoir le système XDM, rend les schémas de modèles de données d’expérience opérationnels pour qu’ils soient utilisés par les services de Platform. |
| Schéma XDM | Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit. Avant que les données puissent être ingérées dans Platform, un schéma doit être composé pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenues dans chaque champ. Les schémas se composent d’une classe XDM de base et de zéro ou plusieurs groupes de champs de schéma. |
| Classe XDM | Tous les schémas XDM décrivent des données pouvant être catégorisées en tant qu’enregistrement ou série temporelle. Le comportement des données d’un schéma est défini par la classe du schéma, qui est affectée à un schéma lors de sa création initiale. Les classes XDM décrivent le plus petit nombre de propriétés qu’un schéma doit contenir pour représenter un comportement de données spécifique. |
| [Groupes de champs](../../xdm/schema/composition.md) | Composant qui définit un ou plusieurs champs d’un schéma. Les groupes de champs imposent la manière dont leurs champs apparaissent dans la hiérarchie du schéma et présentent donc la même structure dans chaque schéma dans lequel ils sont inclus. Les groupes de champs ne sont compatibles qu’avec des classes spécifiques, identifiées par leurs `meta:intendedToExtend` attribut. |
| [Type de données](../../xdm/schema/composition.md) | Composant pouvant également fournir un ou plusieurs champs pour un schéma. Cependant, contrairement aux groupes de champs, les types de données ne sont pas limités à une classe particulière. Ainsi, les types de données constituent une option plus souple pour décrire des structures de données communes réutilisables sur plusieurs schémas avec des classes potentiellement différentes. Les types de données décrits dans ce document sont pris en charge par les schémas CEE et Adobe Analytics. |
| Churn | Mesure du pourcentage des comptes qui annulent ou choisissent de ne pas renouveler leurs abonnements. Un taux de perte de clientèle élevé peut avoir une incidence négative sur les recettes mensuelles récurrentes et peut également indiquer un mécontentement à l’égard d’un produit ou d’un service. |
| [Real-time Customer Profile](../../profile/home.md) | Real-time Customer Profile fournit un profil de consommateur centralisé pour une gestion d’expérience ciblée et personnalisée. Chaque profil contient des données agrégées sur tous les systèmes ainsi que des comptes horodatés exploitables d’événements impliquant les personnes concernées par l’un des systèmes que vous utilisez avec Experience Platform. |

## Données d’entrée de Customer AI

>[!TIP]
>
> Customer AI détermine automatiquement les événements qui sont utiles pour les prédictions et génère un avertissement si les données disponibles ne sont pas suffisantes pour générer des prédictions de qualité.

Customer AI prend en charge les jeux de données Adobe Analytics, Adobe Audience Manager, Experience Event (EE) et Consumer Experience Event (CEE). Le schéma CEE nécessite l’ajout de groupes de champs lors du processus de création du schéma. Si vous utilisez des jeux de données Adobe Analytics ou Adobe Audience Manager, le connecteur source mappe directement les événements standard (Commerce, Détails de la page web, Application et Recherche) répertoriés ci-dessous pendant le processus de connexion. Vous pouvez ajouter plusieurs jeux de données provenant de sources différentes si chacun des jeux de données partage le même type d’identité (espace de noms), tel qu’un ECID.

Pour plus d’informations sur le mappage des données Adobe Analytics ou des données d’Audience Manager, consultez la section [Mappages des champs Analytics](../../sources/connectors/adobe-applications/analytics.md) ou [Mappages des champs d’Audience Manager](../../sources/connectors/adobe-applications/mapping/audience-manager.md) guide.

### Événements standard utilisés par Customer AI {#standard-events}

Les événements d’expérience XDM sont utilisés pour déterminer différents comportements de client. Selon la structure de vos données, les types d’événements répertoriés ci-dessous peuvent ne pas englober tous les comportements de votre client. C’est à vous de déterminer les champs qui contiennent les données nécessaires pour identifier clairement et sans ambiguïté l’activité des utilisateurs web. Selon l’objectif de prédiction, les champs requis peuvent changer.

Customer AI repose sur différents types d’événements pour la création de fonctionnalités de modèle. Ces types d’événement sont automatiquement ajoutés à votre schéma à l’aide de plusieurs groupes de champs XDM.

>[!NOTE]
>
>Si vous utilisez des données Adobe Analytics ou Adobe Audience Manager, le schéma est automatiquement créé avec les événements standard requis pour capturer vos données. Si vous créez votre propre schéma CEE personnalisé pour capturer des données, vous devez tenir compte des groupes de champs nécessaires pour capturer vos données.

Il n’est pas nécessaire de disposer de données pour chacun des événements standard répertoriés ci-dessous, mais certains événements sont obligatoires pour certains scénarios. Si vous disposez de l’une des données d’événement standard, il est recommandé de l’inclure dans votre schéma. Par exemple, si vous souhaitez créer une application Customer AI pour prédire les événements d’achat, il serait utile d’avoir des données provenant de la variable `Commerce` et `Web page details` types de données.

Pour afficher un groupe de champs dans l’interface utilisateur de Platform, sélectionnez le **[!UICONTROL Schémas]** dans le rail de gauche, puis sélectionnez l’option **[!UICONTROL Groupes de champs]** .

| Groupe de champs | Type d’événement | Chemin du champ XDM |
| --- | --- | --- |
| [!UICONTROL Informations commerciales] | ordre | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | checkouts | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | purchases | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemovals | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListOpens | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Détails web] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL Détails de l’application] | applicationCloses | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrashes | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsages | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL Détails de la recherche] | recherche | search.keywords |

En outre, Customer AI peut utiliser les données d’abonnement pour créer de meilleurs modèles d’attrition. Les données d’abonnement sont nécessaires pour chaque profil à l’aide de la variable [[!UICONTROL Abonnement]](../../xdm/data-types/subscription.md) format de type de données. La plupart des champs sont facultatifs, cependant, pour un modèle d’attrition optimal, il est vivement recommandé de fournir des données pour autant de champs que possible, par exemple : `startDate`, `endDate`, ainsi que tout autre détail pertinent.

### Ajout d’événements personnalisés et d’attributs de profil

Si vous disposez d’informations que vous souhaitez inclure en plus de la variable [champs d’événement standard](#standard-events) utilisé par Customer AI, une option d’événement personnalisé et d’attribut de profil personnalisé est fournie pendant votre [configuration de l&#39;instance](./user-guide/configure.md#custom-events).

Si le jeu de données que vous avez sélectionné inclut des événements personnalisés ou des attributs de profil tels qu’une &quot;réservation d’hôtel&quot; ou un &quot;employé d’une société X&quot; définis dans votre schéma, vous pouvez les ajouter à votre instance. Ces autres événements personnalisés et attributs de profil sont utilisés par Customer AI pour améliorer la qualité de votre modèle et fournir des résultats plus précis.

### Données historiques {#data-requirements}

Customer AI nécessite des données historiques pour la formation des modèles, mais la quantité de données requise est basée sur deux éléments clés : la fenêtre des résultats et la population éligible.

Par défaut, Customer AI recherche un utilisateur qui a eu une activité au cours des 120 derniers jours si aucune définition de population éligible n’est fournie pendant la configuration de l’application. En outre, Customer AI nécessite au moins 500 événements admissibles et 500 événements non admissibles (1 000 au total) de données historiques en fonction d’une définition d’objectif prédite.

Les exemples suivants fournis utilisent une formule simple pour vous aider à déterminer la quantité minimale de données requise. Si vous avez plus que la configuration minimale requise, votre modèle est susceptible de fournir des résultats plus précis. Si vous disposez de moins de la quantité minimale requise, le modèle échoue, car il n’y a pas une quantité suffisante de données pour la formation du modèle.

**Formule**:

Longueur minimale des données requises = population éligible + fenêtre de résultat

>[!NOTE]
>
> 30 est le nombre minimum de jours requis pour la population éligible. Si ce paramètre n’est pas fourni, la valeur par défaut est de 120 jours.

Exemples :

- Vous souhaitez prédire si un client est susceptible d’acheter une montre dans les 30 prochains jours. Vous souhaitez également noter les utilisateurs qui ont une activité web au cours des 60 derniers jours. Dans ce cas, la durée minimale de données requise = 60 jours + 30 jours. La population éligible est de 60 jours et la fenêtre de résultat est de 30 jours au total de 90 jours.

- Vous souhaitez prédire si l’utilisateur est susceptible d’acheter une montre dans les 7 prochains jours. Dans ce cas, la durée minimale de données requise = 120 jours + 7 jours. La population éligible est définie par défaut sur 120 jours et la fenêtre de résultat est de 7 jours au total sur 127 jours.

- Vous souhaitez prédire si le client est susceptible d’acheter une montre dans les 7 prochains jours. Vous souhaitez également noter les utilisateurs qui ont une activité web au cours des 7 derniers jours. Dans ce cas, la durée minimale de données requise = 30 jours + 7 jours. La population éligible nécessite un minimum de 30 jours et la fenêtre de résultat est de 7 jours totalisant 37 jours.

Outre les données minimales requises, Customer AI fonctionne également mieux avec les données récentes. Dans ce cas d’utilisation, Customer AI effectue une prévision pour l’avenir en fonction des données comportementales récentes d’un utilisateur. En d’autres termes, des données plus récentes sont susceptibles de générer une prédiction plus précise.

### Exemples de scénarios

Dans cette section, différents scénarios pour les instances de Customer AI sont décrits ainsi que les types d’événements requis et recommandés. Reportez-vous à la section [table des événements standard](#standard-events) ci-dessus pour plus d’informations sur le groupe de champs et son chemin d’accès.

>[!NOTE]
>
> Les types d’événements requis sont utilisés pour identifier clairement et sans ambiguïté l’activité des utilisateurs web. Le nombre de types d’événement requis change en fonction de l’objectif de prédiction et de la structure de votre schéma. Si vous ne savez pas si un type d’événement particulier est nécessaire, il est recommandé d’inclure ce type d’événement lors de la création de votre schéma CEE. Si vous utilisez des données Adobe Analytics ou Adobe Audience Manager, les événements standard requis doivent être disponibles en fonction des données que vous diffusez en continu.

### Scénario 1 : Conversion d’achat sur un site web de vente au détail d’e-commerce

**Objectif de prédiction :** prévoir la propension de conversion des profils éligibles pour l’achat d’un certain article de vêtements sur un site web ;

**Types d’événement standard requis :**

Les types d’événements répertoriés ci-dessous sont requis pour une sortie optimale de Customer AI avec cet objectif de prédiction particulier. Il est possible d’exclure un événement obligatoire en fonction de votre objectif de prédiction. Toutefois, l’exclusion de plusieurs événements peut entraîner des résultats médiocres.

- ordre
- checkouts
- achats
- webVisit
- recherche

**Types d’événements standard recommandés supplémentaires :**

L’un des éléments restants [types d’événement](#standard-events) peut être nécessaire en fonction de la complexité de votre objectif et de la population éligible lors de la configuration de votre instance Customer AI. Si les données sont disponibles pour un type de données particulier, il est recommandé de les inclure dans votre schéma.

### Scénario 2 : Conversion des abonnements sur un site web de service de diffusion en continu de médias

**Objectif de prédiction :** Prédire la propension de conversion des abonnements pour les profils éligibles à s’engager à un certain niveau d’abonnement, tel qu’un forfait standard ou Premium.

**Types d’événement standard requis :**

Les types d’événements répertoriés ci-dessous sont requis pour une sortie optimale de Customer AI avec cet objectif de prédiction particulier. Il est possible d’exclure un événement obligatoire en fonction de votre objectif de prédiction. Toutefois, l’exclusion de plusieurs événements peut entraîner des résultats médiocres.

- ordre
- checkouts
- achats
- webVisit
- recherche

Dans cet exemple, `order`, `checkouts`, et `purchases` sont utilisés pour indiquer qu’un abonnement a été acheté et son type.

En outre, pour un modèle précis, il est conseillé d’utiliser certaines des propriétés disponibles dans la variable [type de données d&#39;abonnement](../../xdm/data-types/subscription.md).

**Types d’événements standard recommandés supplémentaires :**

L’un des éléments restants [types d’événement](#standard-events) peut être nécessaire en fonction de la complexité de votre objectif et de la population éligible lors de la configuration de votre instance Customer AI. Si les données sont disponibles pour un type de données particulier, il est recommandé de les inclure dans votre schéma.

### Scénario 3 : Visite sur un site web de vente en ligne

**Objectif de prédiction :** prévoir la probabilité qu’un événement d’achat ne se produise pas ;

**Types d’événement standard requis :**

Les types d’événements répertoriés ci-dessous sont requis pour une sortie optimale de Customer AI avec cet objectif de prédiction particulier. Il est possible d’exclure un événement obligatoire en fonction de votre objectif de prédiction. Toutefois, l’exclusion de plusieurs événements peut entraîner des résultats médiocres.

- ordre
- checkouts
- achats
- webVisit
- recherche

**Types d’événements standard recommandés supplémentaires :**

L’un des éléments restants [types d’événement](#standard-events) peut être nécessaire en fonction de la complexité de votre objectif et de la population éligible lors de la configuration de votre instance Customer AI. Si les données sont disponibles pour un type de données particulier, il est recommandé de les inclure dans votre schéma.

### Scénario 4 : Conversion de vente incitative sur un site web de vente au détail d’e-commerce

**Objectif de prédiction :** Prédire la propension à l’achat de la population qui a acheté un produit spécifique pour acheter un nouveau produit associé.

**Types d’événement standard requis :**

Les types d’événements répertoriés ci-dessous sont requis pour une sortie optimale de Customer AI avec cet objectif de prédiction particulier. Il est possible d’exclure un événement obligatoire en fonction de votre objectif de prédiction. Toutefois, l’exclusion de plusieurs événements peut entraîner des résultats médiocres.

- ordre
- checkouts
- achats
- webVisit
- recherche

**Types d’événements standard recommandés supplémentaires :**

L’un des éléments restants [types d’événement](#standard-events) peut être nécessaire en fonction de la complexité de votre objectif et de la population éligible lors de la configuration de votre instance Customer AI. Si les données sont disponibles pour un type de données particulier, il est recommandé de les inclure dans votre schéma.

### Scénario 5 : Désabonner (attrition) sur un site d&#39;information en ligne

**Objectif de prédiction :** prévoir la propension de la population éligible à se désabonner d’un service le mois prochain ;

**Types d’événement standard requis :**

Les types d’événements répertoriés ci-dessous sont requis pour une sortie optimale de Customer AI avec cet objectif de prédiction particulier. Il est possible d’exclure un événement obligatoire en fonction de votre objectif de prédiction. Toutefois, l’exclusion de plusieurs événements peut entraîner des résultats médiocres.

- webVisit
- recherche

En outre, pour un modèle précis, il est conseillé d’utiliser certaines des propriétés disponibles dans la variable [type de données d&#39;abonnement](../../xdm/data-types/subscription.md).

**Types d’événements standard recommandés supplémentaires :**

L’un des éléments restants [types d’événement](#standard-events) peut être nécessaire en fonction de la complexité de votre objectif et de la population éligible lors de la configuration de votre instance Customer AI. Si les données sont disponibles pour un type de données particulier, il est recommandé de les inclure dans votre schéma.

### Scénario 6 : Lancement d’une application mobile

**Objectif de prédiction :** Prévoyez la propension des profils éligibles à lancer une application mobile payante dans les X prochains jours. Cela revient à prédire l’indicateur de performance clé (IPC) des &quot;utilisateurs Principaux par mois&quot;.

**Types d’événement standard requis :**

Les types d’événements répertoriés ci-dessous sont requis pour une sortie optimale de Customer AI avec cet objectif de prédiction particulier. Il est possible d’exclure un événement obligatoire en fonction de votre objectif de prédiction. Toutefois, l’exclusion de plusieurs événements peut entraîner des résultats médiocres.

- ordre
- checkouts
- achats
- webVisit
- applicationCloses
- applicationCrashes
- applicationFeatureUsages
- applicationFirstLaunches
- applicationInstalls
- applicationLaunches
- applicationUpgrades

Dans cet exemple, `order`, `checkouts`, et `purchases` sont utilisées lorsqu’une application mobile doit être achetée.

**Types d’événements standard recommandés supplémentaires :**

L’un des éléments restants [types d’événement](#standard-events) peut être nécessaire en fonction de la complexité de votre objectif et de la population éligible lors de la configuration de votre instance Customer AI. Si les données sont disponibles pour un type de données particulier, il est recommandé de les inclure dans votre schéma.

### Scénario 7 : Caractéristiques réalisées (Adobe Audience Manager)

**Objectif de prédiction :** prévoir la propension de certaines caractéristiques à réaliser ;

**Types d’événement standard requis :**

Pour utiliser les caractéristiques de Adobe Audience Manager, vous devez créer une connexion source à l’aide du [Connecteur source d’Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). Le connecteur source crée automatiquement le schéma avec le ou les groupes de champs appropriés. Vous n’avez pas besoin d’ajouter manuellement des types d’événements supplémentaires pour que le schéma fonctionne avec Customer AI.

Lorsque vous configurez une nouvelle instance d’IA dédiée aux clients, `audienceName` et `audienceID` peut être utilisé pour sélectionner une caractéristique spécifique pour la notation lors de la définition de votre objectif.

## Données de sortie de Customer AI

Customer AI génère plusieurs attributs pour les profils individuels supposés éligibles. Il existe deux façons d’utiliser le score (sortie) en fonction de ce que vous avez mis en service. Si vous disposez d’un jeu de données activé pour Real-time Customer Profile, vous pouvez utiliser les informations de Real-time Customer Profile dans la variable [Créateur de segments](../../segmentation/ui/segment-builder.md). Si vous ne disposez pas d’un jeu de données activé pour Profile, vous pouvez [Téléchargez la sortie de Customer AI](./user-guide/download-scores.md) jeu de données disponible sur le lac de données.

Vous trouverez le jeu de données de sortie sous **Jeux de données** dans Platform. Tous les jeux de données de sortie de Customer AI commencent par le nom . **Scores Customer AI - Name_of_app**. De même, tous les schémas de sortie de Customer AI commencent par le nom . **Schéma Customer AI - Name_of_app**.

![cai-schema-name-of-app](./images/user-guide/cai-schema-name-of-app.png)

>[!NOTE]
>
> Les valeurs de sortie sont consommées par Real-time Customer Profile qui peut être utilisé pour créer et définir des segments.

Le tableau ci-dessous décrit les différents attributs trouvés dans les sorties de Customer AI :

| Attribut | Description |
| ----- | ----------- |
| Score | La probabilité relative qu’un client atteigne l’objectif prévu au cours de la période définie. Cette valeur ne doit pas être considérée comme un pourcentage de probabilité, mais plutôt comme la probabilité d’un individu par rapport à la population totale. Ce score est compris entre 0 et 100. |
| Probabilité | Cet attribut est la probabilité réelle qu’un profil atteigne l’objectif prévu au cours de la période définie. Si vous comparez les sorties en fonction d’objectifs différents, nous vous recommandons de prendre en compte le percentile ou le score de probabilité. Vous devez toujours utiliser la probabilité lorsque vous essayez de déterminer la probabilité moyenne sur la population éligible, car la probabilité a tendance à être basse pour les événements qui ne se produisent pas fréquemment. Les valeurs des probabilités sont comprises entre 0 et 1. |
| Percentile | Cette valeur fournit des informations concernant la performance d’un profil par rapport à d’autres profils aux notes similaires. Par exemple, un profil dont le rang de percentile est de 99 pour l’attrition indique qu’il y a une forte chance d’attrition par rapport à 99 % des autres profils évalués. Les percentiles sont compris entre 1 et 100. |
| Type de propension | Le type de propension sélectionné. |
| Date de la note | Date à laquelle la notation a eu lieu. |
| Facteurs d’influence | Raisons prévues de la probabilité de conversion ou d’attrition d’un profil. Les facteurs se composent des attributs suivants :<ul><li>Code : le profil ou l’attribut comportemental qui influencent positivement le score prévu d’un profil. </li><li>Valeur : la valeur du profil ou de l’attribut comportemental.</li><li>Importance : indique le poids que le profil ou l’attribut comportemental a sur le score prévu (faible, moyen, élevé)</li></ul> |

>[!NOTE]
>
> - Customer AI utilise uniquement des données mises à jour pour suivre une formation et une notation plus poussées. De même, lorsque vous demandez la suppression de données, Customer AI s’abstient d’utiliser les données supprimées.
> - Customer AI exploite des jeux de données Platform. Pour prendre en charge les demandes de droits des consommateurs qu’une marque peut recevoir, les marques doivent utiliser le Privacy Service Platform pour soumettre les demandes d’accès et de suppression des clients afin de supprimer leurs données dans le lac de données, Identity Service et Real-time Customer Profile.
> - Tous les jeux de données que nous utilisons pour l’entrée/la sortie des modèles suivront les directives de Platform. Le chiffrement des données de plateforme s’applique aux données au repos et en transit. Consultez la documentation pour en savoir plus sur [cryptage des données](../../../help/landing/governance-privacy-security/encryption.md)


## Étapes suivantes {#next-steps}

Une fois vos données préparées et vos informations d’identification et schémas en place, commencez par suivre la [Configuration d’une instance Customer AI](./user-guide/configure.md) guide. Ce guide vous guide tout au long des étapes nécessaires à la création d’une instance pour Customer AI.




