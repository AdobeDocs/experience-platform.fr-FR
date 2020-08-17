---
keywords: Experience Platform;home;popular topics;offer management;Offer Management;Journey;customer journey;journey;decision events;decision event;Decision events
solution: Experience Platform
title: Service de prise de décision
topic: overview
description: Le service de prise de décision vous offre la possibilité de créer des expériences personnalisées, optimisées et orchestrées dans des applications s’exécutant sur Adobe Experience Platform. À l’aide du service de prise de décision, vous pouvez déterminer la meilleure option depuis un ensemble de choix disponibles. Ces options, également appelées alternatives, peuvent être des offres, des recommandations de produits, des composants de contenu pour une expérience web, des scripts de conversation et des actions à prendre.
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 78%

---


# Présentation du service de prise de décision

[!DNL Decisioning Service] permet de créer des expériences personnalisées, optimisées et orchestrées dans des applications s’exécutant sur Adobe Experience Platform. Using [!DNL Decisioning Service], you can determine the best *option* from a set of available choices. Ces options, également appelées alternatives, peuvent être des offres, des recommandations de produits, des composants de contenu pour une expérience web, des scripts de conversation et des actions à prendre. Actuellement, le cas d’utilisation et le domaine de la *prise de décision relative aux offres* sont pris en charge. Les options de décision y sont conçues spécifiquement comme des offres, avec une prise en charge pour d’autres cas d’utilisation à venir.

With [!DNL Decisioning Service], customers can reuse business logic as well as share a catalog of options across channels and applications. Au lieu de gérer les options de décision, et les stratégies pour les sélectionner, au sein même d’une application, il est désormais possible de les mettre à profit quels que soient le moment, le mode et le canal d’interaction entre l’utilisateur final d’un client et une entreprise ou une organisation.

Les stratégies de prise de décision peuvent prendre en compte les nombreuses interactions qu’un client a eues via de nombreux canaux et applications. Par exemple, l’activité d’une application de centre d’appel pourrait consister à activer ou à supprimer un message marketing pendant un certain temps à la suite d’une plainte, et ce message lui-même pourrait découler des achats effectués et des commentaires émis par le client.

[!DNL Decisioning Service] facilite la personnalisation de l’expérience évoluée.

| Avant la prise de décision basée sur l’expérience | Après la prise de décision basée sur l’expérience |
| --- | --- |
| Personnalisation et optimisation des expériences de l’utilisateur sur un seul canal ou sur un petit ensemble de points de contact d’expérience. | Les expériences sont des réponses orchestrées entre les interactions. |
| Les optimisations sont axées sur une seule phase, généralement courte, du parcours de l’utilisateur final. | Les décisions reposent sur l’historique complet des interactions, depuis les comportements détectés antérieurement jusqu’au contexte situationnel le plus récent. |
| Les options et les stratégies de sélection des éléments à présenter lors de l’expérience d’un client sont généralement codées minutieusement au sein d’une application. | Les stratégies de sélection de la meilleure option sont définies en dehors des applications spécifiques au canal et deviennent réutilisables. |
| Les expériences client sont personnalisées et optimisées selon un objectif simpliste, comme l’augmentation du nombre de passages en caisse réussis sur une page web ou l’acceptation d’une offre présentée lors d’une interaction avec un représentant. | Les expériences client sont optimisées par une compréhension globale des besoins actuels du client et s’adaptent à toutes les expériences que l’utilisateur a eues, bonnes ou mauvaises. Par exemple, une campagne marketing peut ne pas convenir à un client qui a récemment déposé une plainte concernant un produit ou un service. |

[!DNL Decisioning Service] déplace les capacités de personnalisation de votre expérience du ciblage en un seul canal vers la détermination de l’étape globale du cycle de vie de l’engagement de vos clients auprès de votre marque indépendamment des canaux. Une étape du cycle de vie est beaucoup plus complexe qu’une appartenance à un segment, et repose presque toujours sur des flux d’événements complexes, des règles commerciales et des attributs prédéfinis.

Autres termes employés par les produits et services visant à être utilisés dans des cas d’utilisation similaires :

- Gestion des interactions en temps réel (RTIM)
- Gestion des parcours
- Personnalisation et marketing omnicanal
- Prise de décision en temps réel

## How does [!DNL Decisioning Service] work?

Experiences can be customized using [!DNL Decisioning Service] in real time, as your customer engages with your brand via an inbound channel, such as your site or mobile app. Vous pouvez également utiliser la prise de décision pour personnaliser les messages via un canal sortant, comme un e-mail ou une notification push.

Les décisions peuvent être prises de plusieurs façons. Une des approches consiste à éliminer successivement les options jusqu’à ce qu’il n’en reste plus qu’une ou que les options aient été réduites et qu’il reste un sous-ensemble ou qu’un gagnant soit choisi au hasard dans l’ensemble réduit. Une variante de cette approche consiste à choisir l’option gagnante selon une formule calculée. Le classement des options admissibles s’effectue à l’aide d’une fonction. Pour la prise de décision relative aux offres, cette fonction pourrait calculer le coût, la valeur de l’offre pour l’entreprise et se baser sur une probabilité prédéterminée que l’offre soit acceptée par l’utilisateur final. Le résultat obtenu peut être utilisé pour commander les offres.

Alternativement ou en complément, une stratégie peut reposer sur les résultats recueillis lors d’interactions antérieures avec des clients similaires auxquels des options semblables ont été proposées. Dans cette stratégie, il est question d’apprendre à connaître la fonction qui a calculé les valeurs de priorité. La valeur optimale du résultat est liée aux objectifs de l’activité et l’indicateur de performance pour la prédiction est la fréquence à laquelle le résultat a été atteint après que l’option a été proposée.

### Stratégie de décision

Les stratégies de décision sont configurées au moyen d’objets appelés _activités_. Chaque stratégie de décision est essentiellement un algorithme ou une fonction qui prend N options {o1, o2, …oN} comme entrée et produit une liste ordonnée d’options (o1, o2,…oK) où la première est considérée comme la meilleure selon un critère d’optimisation, la deuxième option de la liste de résultats est ensuite considérée comme la deuxième meilleure option, et ainsi de suite.

À tout moment pendant le parcours d’un client, la meilleure option pour une activité donnée est réévaluée en fonction de l’ensemble le plus récent de variables contextuelles, de règles et de contraintes. Context variables include the records stored in [!DNL Real Time Customer Profile]. Une entité d’enregistrement centrale est le profil d’un client, mais d’autres entités comme les données commerciales opérationnelles sont également disponibles pour l’activité.

L’algorithme ou la fonction qui produit la liste des options les plus fréquentes varie selon le cas d’utilisation. Les composants internes de cet algorithme sont différents selon les cas d’utilisation. Les composants sont définis dans un référentiel au moment de la conception et « compilés » en instructions pour la stratégie de décision spécifique au cas d’utilisation.

![décision-optimisation](./images/decisioning-optimization.png)

## Working with [!DNL Decisioning Service]

The [!DNL Decisioning Service], like other [!DNL Platform] services, adopts an API first philosophy. Cela signifie que l’API est la principale interface où toutes les fonctions, y compris les fonctions administratives, sont mises à disposition via les API. It also means that other [!DNL Platform] services, Adobe solutions, and 3rd party integrations use the same APIs.

You can use [!DNL Decisioning Service] in a synchronous request-response interaction mode facilitated by a simple HTTP REST API. L’appel API renvoie la meilleure option actuelle pour un profil unique. La sélection de la « meilleure option actuelle » changera en fonction des règles et des contraintes appliquées à toutes les options envisagées par une activité donnée. L’API REST permet d’obtenir la meilleure option suivante pour plusieurs activités à la fois. Cela permet l’arbitrage des options entre les différents canaux. Lorsque des réponses pour plusieurs activités sont obtenues simultanément, des règles supplémentaires peuvent s’appliquer.

![prise de décision-API](./images/decisioning-API.png)

### Integration with other [!DNL Platform] workflows

Use of [!DNL Decisioning Service] is optional and only requires a few steps in addition to the typical steps required to create [!DNL Profile] entities and manage them.

>[!NOTE]
>
>To make the most out of the [!DNL Real-time Customer Profile], the [!DNL Decisioning Service] directly integrates with the profile store. Les appels API n’ont besoin d’indiquer qu’une seule des identités pour un profil donné.

La séquence typique des étapes commence par l’établissement des profils :

- Authentifiez-vous à [!DNL Experience Platform].
- Définissez un schéma basé sur la classe de profil et, éventuellement, définissez un schéma basé sur la classe d’événement d’expérience.
- Configurez un jeu de données pour charger des données d’enregistrement et de série temporelle dans [!DNL Customer Profile].
- Ajoutez des données via le jeu de données configuré à l’étape précédente ou des données d’instance de flux via un pipeline.
- Stream experience events into the [!DNL Platform] to enrich the profile with behavioral data.

Additionally, to use [!DNL Decisioning Service], the following steps:

- Définissez les composants de décision à l’aide des API Repository. Ce sont les entités de la logique commerciale qui constituent la stratégie de décision. The decision components will be automatically compiled into a format used by the [!DNL Decision Service Runtime]. Les API Repository sont illustrées sur le côté gauche du diagramme ci-dessous.
- Appelez l’API Runtime pour obtenir la meilleure option selon la logique commerciale définie à l’étape précédente. The [!DNL Decision Service Runtime] APIs are illustrated on the right side in the diagram below.

![prise de décision-API1](./images/decisioning-API1.png)

L’activation des entités de la logique commerciale s’effectue automatiquement et en continu. Dès qu’une nouvelle option est enregistrée dans le référentiel et qu’elle est marquée comme « approuvée », elle sera susceptible d’être incluse dans l’ensemble des options disponibles. Dès qu’une règle de décision est mise à jour, le jeu de règles est reconstitué et préparé pour son exécution. Lors de cette étape d’activation automatique, toutes les contraintes définies par la logique commerciale qui ne dépendent pas du contexte d’exécution seront évaluées. The results of this activation step are sent to a cache where they are available to the [!DNL Decisioning Service] runtime. Ceci est illustré dans le diagramme suivant.

![prise de décision-API2](./images/decisioning-API2.png)

Once the option sets, rule sets and constraints are activated, and have been pushed to [!DNL Decisioning Service] nodes, a simple API is used to post a request for a decision. L’API est généralement appelée par un service de diffusion qui prend ensuite l’option proposée (par exemple, la prochaine meilleure action ou la prochaine meilleure offre) et recueille l’expérience ou exécute l’action. Si la proposition est une offre, alors le contenu qui représente cette offre est recherché et intégré dans une expérience proposée à l’utilisateur final. Ceci est illustré dans le diagramme suivant.

![prise de décision-API3](./images/decisioning-API3.png)

[!DNL Delivery Service] collecte les données pour la demande de décision. Il détermine l’identifiant de l’entité de profil pour laquelle la meilleure option est décidée. It also assembles any context data that is not stored in [!DNL Customer Profile] but is potentially used by the decision logic.

La logique de décision est organisée par activité, chacune d’entre elles spécifiant un filtre pour le sous-ensemble d’options à prendre en compte pour cette activité, ainsi qu’une seule option de secours.

Chaque décision est prise en appliquant d’abord des contraintes pour réduire le nombre d’options, puis en classant les options restantes. Although most of the logic is evaluated inside [!DNL Decisioning Service], various adjunct services are used to help with these two aspects. Par exemple, un service de plafonnement gère les limites supérieures de la fréquence à laquelle une option peut être utilisée dans toute décision, et un autre service peut héberger un modèle d’apprentissage automatique utilisé pour calculer les scores d’un profil et d’une option.

Pour en savoir plus sur l’utilisation des API Repository, consultez le tutoriel sur la [gestion des entités de prise de décision et des règles à l’aide des API](./tutorials/entities.md).

To learn more about using the [!DNL Decisioning Service] runtime, see the tutorial on [Working with the Decisioning Service runtime using APIs](./tutorials/runtime.md)