---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Service de prise de décision
topic: overview
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Présentation du service de prise de décision

Le service de prise de décision permet de créer des expériences personnalisées, optimisées et orchestrées dans des applications s’exécutant sur Adobe Experience Platform. Le service de prise de décision vous permet de déterminer la meilleure *option* à partir d’un ensemble de choix disponibles. Ces options, également appelées alternatives, peuvent être  , recommandations de produits, composants de contenu pour une expérience Web, scripts de conversation et actions à entreprendre. Actuellement, le cas d’utilisation et le domaine de la prise *de décision* des sont pris en charge, où les options de décision sont modélisées spécifiquement en tant que de , avec la prise en charge d’un plus grand nombre de cas d’utilisation à venir.

Avec le service de prise de décision, les clients peuvent réutiliser la logique métier et partager un catalogue d’options entre les  et les applications. Au lieu de gérer les options de décision - et les stratégies de sélection - au sein même d’une application, il est désormais possible de les exploiter quel que soit le moment, la manière et le dans lesquels l’utilisateur final d’un client  interagit avec une entreprise ou une organisation.

Les stratégies de prise de décision peuvent prendre en compte les nombreuses interactions qu’un client a eues dans de nombreux  et applications. Par exemple, l’application de centre d’appels  le peut activer ou supprimer un message marketing pendant un certain temps après une plainte, et ce message lui-même peut être basé sur les achats effectués et les révisions publiées par le client.

Le service de prise de décision facilite la personnalisation de l’expérience évoluée.

| Avant la prise de décision d’expérience | Après la prise de décision d’expérience |
| --- | --- |
| Personnalisez et optimisez les expériences de leurs utilisateurs au sein d’un seul  de ou dans un petit ensemble de points de contact d’expérience. | Les expériences sont des réponses orchestrées entre les interactions. |
| Les optimisations sont ciblées sur une phase unique et généralement courte du parcours de l’utilisateur final. | Les décisions sont basées sur l’historique complet des interactions, depuis les comportements détectés dans le passé jusqu’au contexte situationnel le plus récent. |
| Les options et les stratégies de sélection des options à présenter lors de l’expérience d’un client sont généralement codées profondément au sein d’une application. | Les stratégies de sélection de la meilleure option sont définies en dehors du  des applications spécifiques et deviennent réutilisables. |
| Les expériences des clients sont personnalisées et optimisées selon un objectif simpliste, par exemple augmenter le nombre de passages en caisse réussis sur une page Web ou accepter une   présentée dans une interaction avec un représentant. | Les expériences client sont optimisées en fonction d’une compréhension globale des besoins actuels du client et s’adaptent à toutes les expériences que l’utilisateur a eues, bonnes ou mauvaises. Par exemple, une campagne marketing peut ne pas convenir à un client qui a récemment déposé une plainte à propos d’un produit ou d’un service. |

Le service de prise de décision déplace les capacités de personnalisation de votre expérience du ciblage dans un seul  à la détermination de l’étape globale du cycle de vie de l’engagement de vos clients avec votre marque, indépendamment des  de votre. Une étape de cycle de vie est beaucoup plus complexe qu’une appartenance à un segment et repose presque toujours sur des flux de  complexes, des règles de fonctionnement et des attributs prédits.

Autres termes utilisés par les produits et services visant à servir des cas d&#39;utilisation similaires:

- Gestion des interactions en temps réel (RTIM)
- Gestion du voyage
- Marketing et personnalisation des  Omni
- Prise de décision en temps réel

## Comment fonctionne le service de prise de décision ?

Les expériences peuvent être personnalisées à l’aide du service de prise de décision en temps réel, car votre client interagit avec votre marque via un  d’entrée, tel que votre site ou votre application mobile. La prise de décision peut également être utilisée pour personnaliser les messages via des  sortants, comme un courriel ou une notification Push.

Les décisions peuvent être prises de plusieurs façons. L’une des approches consiste à éliminer les options successivement jusqu’à ce qu’il ne reste plus qu’une seule option ou que les options aient été éliminées et qu’il reste un sous-ensemble ou qu’un gagnant soit sélectionné de manière aléatoire dans l’ensemble réduit. Une variante de cette approche pour sélectionner l’option gagnante selon une formule calculée. Le classement des options admissibles est effectué à l’aide d’une fonction. Pour  prise de décision , cette fonction pourrait calculer le coût, la valeur du de la  à l&#39;entreprise et utiliser un prédéterminé de la probabilité que leest accepté par l&#39;utilisateur final. Le score obtenu peut être utilisé pour classer le  .

Une stratégie peut aussi être basée sur les résultats recueillis lors d’interactions antérieures avec des clients similaires qui ont été proposés comme options similaires. Dans cette stratégie, la fonction qui a calculé les valeurs de priorité est apprise. La valeur optimale des résultats est liée aux objectifs de la   et l&#39;indicateur de rendement de la prévision est la fréquence à laquelle le résultat a été atteint après la proposition de l&#39;option.

### Stratégie de décision

Les stratégies de décision sont configurées au moyen d’objets appelés __. Chaque stratégie de décision est essentiellement un algorithme ou une fonction qui prend N options {o1, o2, ...oN} comme entrée et produit un ordonné d’options (o1, o2,...oK) par lequel la première option du est considérée comme la meilleure selon un critère d’optimisation, la deuxième option du résultat est alors considérée comme la deuxième meilleure option dujeu, etc.

A tout moment au cours du voyage d’un client, la meilleure option pour un   donné est réévaluée en fonction de l’ensemble le plus récent de variables, de règles et de contraintes contextuelles. Les variables contextuelles incluent les enregistrements stockés dans le  Client en temps réel. Une entité d’enregistrement centrale est le  d’un client, mais d’autres entités, comme les données d’exploitation, sont également disponibles pour l’ de l’.

L’algorithme ou la fonction qui produit le  des options top-K varie selon le cas d’utilisation. Les composants internes de cet algorithme sont différents selon les cas d’utilisation. Les composants sont définis dans un référentiel au moment de la conception et &quot;compilés&quot; dans des instructions pour la stratégie de décision spécifique au cas d&#39;utilisation.

![optimisation des décisions](./images/decisioning-optimization.png)

## Utilisation du service de prise de décision

Le service de prise de décision, comme les autres services de plateforme, adopte une philosophie d’API en premier. Cela signifie que l’API est l’interface principale dans laquelle toutes les fonctions, y compris les fonctions d’administration, sont rendues disponibles via les API. Cela signifie également que les autres services de plateforme, les solutions Adobe et les intégrations tierces utilisent les mêmes API.

Vous pouvez utiliser le service de prise de décision en mode synchrone d’interaction requête-réponse, facilité par une API REST HTTP simple. L’appel d’API renvoie la meilleure option pour un seul  de. La sélection de la &quot;meilleure option actuellement&quot; changera en fonction des règles et des contraintes appliquées à toutes les options qui sont prises en compte par un  donné . L’API REST permet d’obtenir la prochaine meilleure option pour plusieurs   à la fois. Cela permet d&#39;arbitrer les options entre les . Lorsque des réponses pour plusieurs   sont obtenues ensemble, des règles supplémentaires peuvent être appliquées.

![decisioning-API](./images/decisioning-API.png)

### Intégration à d’autres  de plateformes

L&#39;utilisation du service de prise de décision est facultative et ne nécessite que quelques étapes en plus des étapes standard requises pour créer des entités  et les gérer.

>[!NOTE] Pour tirer le meilleur parti du  Client en temps réel, le Service de prise de décision s’intègre directement au magasin de  de. Les appels d’API doivent uniquement indiquer l’une des identités d’un  donné.

La séquence typique des étapes  avec la création de  de :

- Authentifiez-vous sur la plateforme Experience.
- Définissez un  basé sur la classe  et, éventuellement, définissez un  basé sur la classe de l’d’expérience.
- Configurez un jeu de données pour transférer des données d’enregistrement et de série chronologique vers le du client.
- Ajouter des données via le jeu de données configuré dans les données de l’étape précédente ou de l’instance de flux via Pipeline.
-  d’expérience de diffusion en continu dans la plateforme pour enrichir le  de données comportementales.

En outre, pour utiliser le service de prise de décision, procédez comme suit :

- Définissez les composants de décision à l’aide des API Repository. Ce sont les entités logiques qui constituent la stratégie de décision. Les composants de décision seront automatiquement compilés dans un format utilisé par le moteur d’exécution de Decision Service. Les API Repository sont illustrées sur le côté gauche du diagramme ci-dessous.
- Appelez l’API d’exécution pour obtenir la meilleure option selon la logique métier définie à l’étape précédente. Les API d’exécution du service de décision sont illustrées sur le côté droit du diagramme ci-dessous.

![decisioning-API1](./images/decisioning-API1.png)

Le  des entités de logique métier se produit automatiquement et en permanence. Dès qu’une nouvelle option est enregistrée dans le référentiel et qu’elle est marquée comme &quot;approuvée&quot;, elle sera candidate pour inclusion dans l’ensemble des options disponibles. Dès qu’une règle de décision est mise à jour, le jeu de règles est réassemblé et préparé pour l’exécution à l’exécution. À cette étape automatique de  , toutes les contraintes définies par la logique métier qui ne dépendent pas du contexte d’exécution seront évaluées. Les résultats de cette   d&#39;étape sont envoyés dans un cache où ils sont disponibles pour le moteur d&#39;exécution du service de prise de décision. Ceci est illustré dans le diagramme suivant.

![decisioning-API2](./images/decisioning-API2.png)

Une fois que les options définies, les jeux de règles et les contraintes sont activés et ont été transférées aux noeuds du service de prise de décision, une API simple est utilisée pour publier une demande de décision. L’API est généralement appelée par un service de  qui effectue ensuite l’option proposée (par exemple, la prochaine meilleure action ou la prochaine meilleure  de) et assemble l’expérience ou exécute l’action. Si la proposition est un  , alors le contenu qui représente le  est recherché et inséré dans une expérience fournie à l’utilisateur final. Ceci est illustré dans le diagramme suivant.

![decisioning-API3](./images/decisioning-API3.png)

Le service  collecte les données pour la demande de décision. Il détermine l&#39;ID de l&#39;entité  pour laquelle la meilleure option est décidée. Il assemble également toutes les données contextuelles qui ne sont pas stockées dans les  du client, mais qui sont potentiellement utilisées par la logique de décision.

La logique de décision est organisée par  , chacun d’eux spécifiant un filtre pour le sous-ensemble d’options qui doit être pris en compte pour ce , ainsi qu’une seule option de secours.

Chaque décision est prise en appliquant d’abord des contraintes pour réduire le nombre d’options, puis en classant les options restantes. Bien que la majeure partie de la logique soit évaluée au sein du service de prise de décision, divers services auxiliaires sont utilisés pour aider à ces deux aspects. Par exemple, un service de plafonnement gère les limites supérieures de la fréquence à laquelle une option peut être utilisée dans une décision, et un autre service peut héberger un modèle d’apprentissage automatique utilisé pour calculer les scores pour un  et une option.

Pour en savoir plus sur l’utilisation des API Repository, consultez le didacticiel sur la [gestion des entités de prise de décision et des règles à l’aide des API.](./tutorials/entities.md)

Pour en savoir plus sur l’utilisation du runtime du service de prise de décision, voir le didacticiel [Utilisation du runtime du service de prise de décision à l’aide des API](./tutorials/runtime.md)