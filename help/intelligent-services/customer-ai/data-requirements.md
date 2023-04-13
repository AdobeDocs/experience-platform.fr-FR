---
keywords: Experience Platform;prise en main;service clientèle;rubriques les plus consultées;entrée d’assistance client;sortie d’assistance client ; exigences de données
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Exigences de données dans Customer AI
topic-legacy: Getting started
description: En savoir plus sur les événements, les entrées et les sorties requis utilisés par Customer AI.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 5f7b602b68f5cbf4b1f4b08603757b0956e36408
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 17%

---


# Entrée et sortie dans Customer AI

Le document suivant décrit les différents événements, entrées et sorties requis utilisés dans Customer AI.

## Prise en main {#getting-started}

Voici les étapes pour créer des modèles de propension et identifier les audiences cibles pour le marketing personnalisé dans Customer AI :

1. Décrire les cas pratiques : Comment les modèles de propension aideraient-ils à identifier les audiences cibles pour le marketing personnalisé ? Quels sont mes objectifs commerciaux et les tactiques correspondantes pour atteindre l’objectif ? Où la modélisation de propension peut-elle s’adapter à ce processus ?

2. Définir des cas d’utilisation prioritaires : Quelles sont les priorités les plus élevées pour l’entreprise ?

3. Créez des modèles dans Customer AI : Regardez ceci : [tutoriel rapide](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html?lang=fr) et reportez-vous à notre [Guide de l’interface utilisateur](../customer-ai/user-guide/configure.md) pour un processus étape par étape afin de créer un modèle.

4. [Création de segments](../customer-ai/user-guide/create-segment.md) utilisation des résultats du modèle.

5. Prenez des actions commerciales ciblées en fonction de ces segments. Surveillez les résultats et effectuez une itération sur les actions à améliorer.

Voici des exemples de configurations pour votre premier modèle.  L’exemple de modèle, élaboré dans ce document, utilise un modèle Customer AI pour prédire qui est susceptible de convertir une activité de vente au détail au cours des 30 prochains jours. Le jeu de données d’entrée est un jeu de données Adobe Analytics.

| Étape  | Définition | Exemple |
| ---- | ------ | ------- |
| Configuration | Spécifiez des informations de base sur le modèle. | **Nom**: Modèle de propension à l’achat de crayon <br> **Type de modèle**: Conversion |
| Sélectionner les données | Spécifiez les jeux de données utilisés pour créer le modèle. | **Jeu de données**: Jeu de données Adobe Analytics <br> **Identité**: Assurez-vous que la colonne d’identité de chaque jeu de données est définie comme identité commune. |
| Définition de l’objectif | Définissez l’objectif, la population éligible, les événements personnalisés et les attributs de profil. | **Objectif de prédiction**: Sélectionner `commerce.purchases.value` égal à crayon <br> **Fenêtre de résultat**: 30 jours. |
| Options de définition | Configuration du planning de l’actualisation du modèle et activation des scores pour Profile | **Planification**: Hebdomadaire <br> **Activer pour le profil**: Cela doit être activé pour que la sortie du modèle soit utilisée dans la segmentation. |

## Présentation des données {#data-overview}

Les sections suivantes décrivent les différents événements, entrées et sorties requis utilisés dans Customer AI.

Customer AI analyse les jeux de données suivants pour prédire l’attrition (lorsqu’un client est susceptible d’arrêter d’utiliser le produit) ou la conversion (lorsqu’un client est susceptible d’effectuer un achat) des scores de propension :

- les données Adobe Analytics à l’aide de la variable [Connecteur source Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Données Adobe Audience Manager utilisant la variable [Connecteur source d’Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [Jeu de données Experience Event](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html)
- [Jeu de données Événement d’expérience client](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html#cee-schema)

Vous pouvez ajouter plusieurs jeux de données provenant de sources différentes si chacun des jeux de données partage le même type d’identité (espace de noms), tel qu’un ECID. Pour plus d’informations sur l’ajout de plusieurs jeux de données, consultez la section [Guide d’utilisation de Customer AI](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>Les connecteurs source prennent jusqu’à quatre semaines pour renvoyer les données. Si vous avez récemment configuré un connecteur, vous devez vérifier que le jeu de données contient la longueur minimale de données requise pour Customer AI. Veuillez consulter la section [données historiques](#data-requirements) pour vérifier que vous disposez de suffisamment de données pour votre objectif de prédiction.

Le tableau suivant présente la terminologie courante utilisée dans ce document :

| Terme | Définition |
| --- | --- |
| [Modèle de données d’expérience (XDM)](../../xdm/home.md) | XDM est le cadre de base qui permet à Adobe Experience Cloud, optimisé par Adobe Experience Platform, de diffuser le message approprié à la bonne personne, sur le bon canal, exactement au bon moment. Platform utilise le système XDM pour organiser les données d’une manière qui facilite leur utilisation pour les services Platform. |
| [Schéma XDM](../../xdm/schema/composition.md) | Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit. Avant que les données puissent être ingérées dans Platform, un schéma doit être composé pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenues dans chaque champ. Les schémas se composent d’une classe XDM de base et de zéro ou plusieurs groupes de champs de schéma. |
| [Classe XDM](../../xdm/schema/field-constraints.md) | Tous les schémas XDM décrivent des données qui peuvent être catégorisées comme `Experience Event`. Le comportement des données d’un schéma est défini par la classe du schéma, qui est affectée à un schéma lors de sa création initiale. Les classes XDM décrivent le plus petit nombre de propriétés qu’un schéma doit contenir pour représenter un comportement de données spécifique. |
| [Groupes de champs](../../xdm/schema/composition.md) | Composant qui définit un ou plusieurs champs d’un schéma. Les groupes de champs imposent la manière dont leurs champs apparaissent dans la hiérarchie du schéma et présentent donc la même structure dans chaque schéma dans lequel ils sont inclus. Les groupes de champs ne sont compatibles qu’avec des classes spécifiques, identifiées par leur attribut `meta:intendedToExtend`. |
| [Type de données](../../xdm/schema/composition.md) | Composant pouvant également fournir un ou plusieurs champs pour un schéma. Toutefois, contrairement aux groupes de champs, les types de données ne sont pas limités à une classe particulière. Ainsi, les types de données constituent une option plus souple pour décrire des structures de données communes réutilisables sur plusieurs schémas avec des classes potentiellement différentes. Les types de données décrits dans ce document sont pris en charge par les schémas CEE et Adobe Analytics. |
| [Real-time Customer Profile](../../profile/home.md) | Real-time Customer Profile fournit un profil de consommateur centralisé pour une gestion d’expérience ciblée et personnalisée. Chaque profil contient des données agrégées sur tous les systèmes ainsi que des comptes horodatés exploitables d’événements impliquant les personnes concernées par l’un des systèmes que vous utilisez avec Experience Platform. |

## Données d’entrée de Customer AI {#customer-ai-input-data}

Pour les jeux de données d’entrée, tels qu’Adobe Analytics et Adobe Audience Manager, les connecteurs sources respectifs mappent directement les événements dans ces groupes de champs standard (Commerce, Web, Application et Recherche) par défaut pendant le processus de connexion. Le tableau ci-dessous présente les champs d’événement dans les groupes de champs standard par défaut pour Customer AI.

Pour plus d’informations sur le mappage des données Adobe Analytics ou des données d’Audience Manager, consultez Mappages de champs Analytics ou Audience Manager . [guide des mappings de champ](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

Vous pouvez utiliser des schémas XDM d’événement d’expérience ou d’événement d’expérience client pour les jeux de données d’entrée qui ne sont pas renseignés via l’un des connecteurs ci-dessus. D’autres groupes de champs XDM peuvent être ajoutés pendant le processus de création de schéma. Les groupes de champs peuvent être fournis par Adobe, comme les groupes de champs standard ou un groupe de champs personnalisé, qui correspond à la représentation des données dans Platform.

>[!IMPORTANT]
>
>Vous devez vous assurer que les données sont renseignées dans ces jeux de données d’entrée. Si aucun événement des groupes de champs standard n’est trouvé dans les jeux de données d’entrée, vous devez ajouter des événements personnalisés pendant le workflow de configuration. Consultez les détails sur les événements personnalisés.

### Groupes de champs standard utilisés par Customer AI {#standard-events}

Les événements d’expérience sont utilisés pour déterminer divers comportements de client. Selon la structure de vos données, les types d’événements répertoriés ci-dessous peuvent ne pas englober tous les comportements de votre client. C’est à vous de déterminer les champs qui contiennent les données nécessaires pour identifier clairement et sans ambiguïté l’activité utilisateur web ou autre canal spécifique. Selon l’objectif de prédiction, les champs requis peuvent changer.

>[!NOTE]
>
>Si vous utilisez des données Adobe Analytics ou Adobe Audience Manager, le schéma est automatiquement créé avec les événements standard requis pour capturer vos données. Si vous créez votre propre schéma EE personnalisé pour capturer des données, vous devez tenir compte des groupes de champs nécessaires pour capturer vos données.

Customer AI utilise par défaut les événements de ces quatre groupes de champs standard : Commerce, Web, Application et recherche. Il n’est pas nécessaire d’avoir des données pour chaque événement dans les groupes de champs standard répertoriés ci-dessous, mais certains événements sont requis pour certains scénarios. Si des événements sont disponibles dans les groupes de champs standard, il est recommandé de les inclure dans votre schéma. Par exemple, si vous souhaitez créer un modèle Customer AI pour prédire les événements d’achat, il est utile de disposer de données provenant des groupes de champs Commerce et Détails de la page Web .

Pour afficher un groupe de champs dans l’interface utilisateur de Platform, sélectionnez le **[!UICONTROL Schémas]** dans le rail de gauche, puis sélectionnez l’option **[!UICONTROL Groupes de champs]** .

| Groupe de champs | Type d’événement | Chemin du champ XDM |
| --- | --- | --- |
| [!UICONTROL Informations commerciales] | commande | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListViews | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | checkouts | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | purchases | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemovals | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | productListOpens | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | productViews | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL Détails web] | webVisit | `web.webPageDetails.name` |
|  | webInteraction | `web.webInteraction.linkClicks.value` |
| [!UICONTROL Détails de l’application] | applicationCloses | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | applicationCrashes | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | applicationFeatureUsages | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | applicationFirstLaunches | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> `application.name` </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> `application.name` </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL Détails de la recherche] | recherche | `search.keywords` |

En outre, Customer AI peut utiliser les données d’abonnement pour créer de meilleurs modèles d’attrition. Les données d’abonnement sont nécessaires pour chaque profil à l’aide de la variable [[!UICONTROL Abonnement]](../../xdm/data-types/subscription.md) format de type de données. La plupart des champs sont facultatifs, cependant, pour un modèle d’attrition optimal, il est vivement recommandé de fournir des données pour autant de champs que possible, par exemple : `startDate`, `endDate`, ainsi que tout autre détail pertinent. Contactez l’équipe de votre compte pour obtenir une prise en charge supplémentaire de cette fonctionnalité.

### Ajout d’événements personnalisés et d’attributs de profil {#add-custom-events}

Si vous disposez d’informations que vous souhaitez inclure en plus de la valeur par défaut [champs d’événement standard](#standard-events) utilisé par Customer AI, vous pouvez utiliser la variable [configuration d’événement personnalisé](./user-guide/configure.md#custom-events) pour augmenter les données utilisées par le modèle.

#### Quand utiliser des événements personnalisés

Les événements personnalisés sont nécessaires lorsque les jeux de données sélectionnés à l’étape de sélection du jeu de données contiennent *none* des champs d’événement par défaut utilisés par Customer AI. Customer AI a besoin d’informations sur au moins un événement de comportement d’utilisateur autre que le résultat.

Les événements personnalisés s’avèrent utiles pour :

- Intégrer les connaissances du domaine ou l’expertise préalable dans le modèle.

- Amélioration de la qualité du modèle prédictif.

- Obtention d’informations et d’interprétations supplémentaires.

Les meilleurs candidats aux événements personnalisés sont les données qui contiennent des connaissances de domaine qui peuvent être prédictives du résultat. Voici quelques exemples généraux d’événements personnalisés :

- Inscrivez-vous au compte

- Abonner à la newsletter

- Effectuer un appel au service client

Vous trouverez ci-dessous une sélection d’exemples d’événements personnalisés spécifiques au secteur :

| Secteur industriel | Événements personnalisés |
| --- | --- |
| Vente au détail | Transaction en magasin<br>Inscrivez-vous à la carte de club<br>Clip bon mobile. |
| Divertissement | abonnement à la saison des achats <br> Diffusion vidéo en continu. |
| Hospitalité | Réservation au restaurant <br> Achat de points de fidélité. |
| Voyage | Ajoutez les informations connues sur le voyageur Achat miles. |
| Communications | Effectuez une mise à niveau/rétrogradation/annulez le plan. |

Pour être sélectionnés, les événements personnalisés doivent représenter des actions initiées par l’utilisateur. Par exemple, &quot;Envoi d’e-mail&quot; est une action lancée par un marketeur et non par l’utilisateur. Elle ne doit donc pas être utilisée comme événement personnalisé.

### Données historiques

Customer AI nécessite des données historiques pour la formation des modèles. La durée nécessaire à l’existence des données dans le système est déterminée par deux éléments clés : la fenêtre de résultat et la population éligible.

Par défaut, Customer AI recherche un utilisateur qui a eu une activité au cours des 45 derniers jours si aucune définition de population éligible n’est fournie pendant la configuration de l’application. En outre, Customer AI nécessite au moins 500 événements admissibles et 500 événements non admissibles (1 000 au total) à partir de données historiques en fonction d’une définition d’objectif prédite.

Les exemples suivants montrent l’utilisation d’une formule simple qui vous aide à déterminer la quantité minimale de données requise. Si vous disposez de données plus volumineuses que le minimum requis, votre modèle est susceptible de fournir des résultats plus précis. Si vous disposez de moins de la quantité minimale requise, le modèle échoue, car il n’y a pas suffisamment de données pour la formation du modèle.

**Formule**:

Pour décider de la durée minimale requise des données du système :

- La durée minimale de création des fonctionnalités est de 30 jours. Comparez l’intervalle de recherche en amont d’éligibilité avec 30 jours :

   - Si la période de recherche en amont d’éligibilité est supérieure à 30 jours, l’exigence de données = intervalle de recherche en amont d’éligibilité + intervalle de résultats.

   - Dans le cas contraire, les exigences de données = 30 jours + fenêtre de résultat.

** S’il existe plusieurs conditions pour définir la population éligible, le intervalle de recherche en amont d’éligibilité est le plus long.

>[!NOTE]
>
>30 est le nombre minimum de jours requis pour la population éligible. Si ce paramètre n’est pas fourni, la valeur par défaut est de 45 jours.

**Exemples**:

- Vous souhaitez prédire si un client est susceptible d’acheter une montre dans les 30 prochains jours pour ceux qui ont une activité web au cours des 60 derniers jours.

   - Intervalle de recherche en amont de l’éligibilité = 60 jours

   - Fenêtre de résultat = 30 jours

   - Données requises = 60 jours + 30 jours = 90 jours

- Vous souhaitez prédire si l’utilisateur est susceptible d’acheter une montre au cours des 7 prochains jours. **without** fournissant une population éligible explicite. Dans ce cas, la population éligible est définie par défaut sur &quot;ceux qui ont eu une activité au cours des 45 derniers jours&quot; et la fenêtre de résultat est de 7 jours.

   - Intervalle de recherche en amont de l’éligibilité = 45 jours

   - Fenêtre de résultat = 7 jours

   - Données requises = 45 jours + 7 jours = 52 jours

- Vous souhaitez prédire si le client est susceptible d’acheter une montre dans les 7 prochains jours pour ceux qui ont une activité web au cours des 7 derniers jours.

   - Intervalle de recherche en amont de l’éligibilité = 7 jours

   - Données minimales requises pour créer des fonctionnalités = 30 jours

   - Fenêtre de résultat = 7 jours

   - Données requises = 30 jours + 7 jours = 37 jours

Bien que l’IA dédiée aux clients exige un temps minimal pour que les données existent dans le système, elle fonctionne également mieux avec les données récentes. En utilisant des données comportementales plus récentes, Customer AI est susceptible de générer une prédiction plus précise du comportement futur d’un utilisateur.

## Données de sortie de Customer AI {#customer-ai-output-data}

Customer AI génère plusieurs attributs pour les profils individuels supposés éligibles. Il existe deux façons d’utiliser le score (sortie) en fonction de ce que vous avez mis en service. Si vous disposez d’un jeu de données activé pour Real-time Customer Profile, vous pouvez utiliser les informations de Real-time Customer Profile dans la variable [Créateur de segments](../../segmentation/ui/segment-builder.md). Si vous ne disposez pas d’un jeu de données activé pour Profile, vous pouvez [Téléchargez la sortie de Customer AI](./user-guide/download-scores.md) jeu de données disponible sur le lac de données.

Vous trouverez le jeu de données de sortie dans Platform. **Jeux de données** workspace. Tous les jeux de données de sortie de Customer AI commencent par le nom . **Scores Customer AI - NAME_OF_APP**. De même, tous les schémas de sortie de Customer AI commencent par le nom . **Schéma Customer AI - Name_of_app**.

![Nom des jeux de données de sortie dans Customer AI](./images/user-guide/cai-schema-name-of-app.png)

Le tableau ci-dessous décrit les différents attributs trouvés dans les sorties de Customer AI :

| Attribut | Description |
| ----- | ----------- |
| [!UICONTROL Score] | La probabilité relative qu’un client atteigne l’objectif prévu au cours de la période définie. Cette valeur ne doit pas être considérée comme un pourcentage de probabilité, mais plutôt comme la probabilité d’un individu par rapport à la population totale. Ce score est compris entre 0 et 100. |
| Probabilité | Cet attribut est la probabilité réelle qu’un profil atteigne l’objectif prévu au cours de la période définie. Lorsque vous comparez des sorties entre différents objectifs, il est recommandé de prendre en compte la probabilité par rapport au centile ou au score. Vous devez toujours utiliser la probabilité lorsque vous essayez de déterminer la probabilité moyenne sur la population éligible, car la probabilité a tendance à être basse pour les événements qui ne se produisent pas fréquemment. Les valeurs de la probabilité sont comprises entre 0 et 1. |
| Percentile | Cette valeur fournit des informations concernant la performance d’un profil par rapport à d’autres profils aux notes similaires. Par exemple, un profil dont le rang de percentile est de 99 pour l’attrition indique qu’il y a une forte chance d’attrition par rapport à 99 % des autres profils évalués. Les percentiles sont compris entre 1 et 100. |
| Type de propension | Le type de propension sélectionné. |
| Date de la note | Date à laquelle la notation a eu lieu. |
| Facteurs d’influence | Il s’agit des raisons prédites pour lesquelles un profil est susceptible de se convertir ou de se générer. Ces facteurs sont constitués des attributs suivants :<ul><li>Code : le profil ou l’attribut comportemental qui influencent positivement le score prévu d’un profil. </li><li>Valeur : la valeur du profil ou de l’attribut comportemental.</li><li>Importance : indique le poids que le profil ou l’attribut comportemental a sur le score prévu (faible, moyen, élevé)</li></ul> |

## Étapes suivantes {#next-steps}

Une fois que vous avez préparé vos données et que vous êtes certain que tous vos identifiants et schémas sont en place, reportez-vous à la section [Configuration d’une instance Customer AI](./user-guide/configure.md) Ce guide vous guide tout au long d’un tutoriel détaillé sur la création d’une instance Customer AI.