---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Service de prise de décision
topic: overview
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '1592'
ht-degree: 0%

---


# Présentation du service de prise de décision

[!DNL Decisioning Service] permet de créer des expériences personnalisées, optimisées et orchestrées dans des applications s’exécutant sur Adobe Experience Platform. Grâce à [!DNL Decisioning Service]elle, vous pouvez déterminer la meilleure *option* à partir d’un ensemble de choix disponibles. Ces options, également appelées alternatives, peuvent être des offres, des recommandations de produits, des composants de contenu pour une expérience Web, des scripts de conversation et des actions à entreprendre. Actuellement, le cas d’utilisation et le domaine de la prise de décision ** Offre sont pris en charge, où les options de décision sont modélisées spécifiquement comme des offres, avec la prise en charge de cas d’utilisation supplémentaires à venir.

Avec [!DNL Decisioning Service], les clients peuvent réutiliser la logique métier et partager un catalogue d’options entre canaux et applications. Au lieu de gérer les options de décision - et les stratégies de sélection - au sein même d’une application, elles peuvent désormais être exploitées indépendamment du moment, de la manière et du canal d’interaction de l’utilisateur final d’un client avec une entreprise ou une organisation.

Les stratégies de prise de décision peuvent prendre en compte les nombreuses interactions qu’un client a eues dans de nombreux canaux et applications. Par exemple, l’activité de l’application du centre d’appels peut activer ou supprimer un message marketing pendant un certain temps après une plainte, et ce message lui-même peut être basé sur les achats effectués et les révisions publiées par le client.

[!DNL Decisioning Service] facilite la personnalisation de l’expérience évoluée.

| Avant la prise de décision d’expérience | Après la prise de décision d’expérience |
| --- | --- |
| Personnalisez et optimisez l’expérience de l’utilisateur en un seul canal ou dans un petit ensemble de points de contact d’expérience. | Les expériences sont des réponses orchestrées entre les interactions. |
| Les optimisations sont centrées sur une phase unique et généralement courte du parcours de l’utilisateur final. | Les décisions sont basées sur l&#39;ensemble de l&#39;historique des interactions, depuis les comportements détectés dans le passé jusqu&#39;au contexte situationnel le plus récent. |
| En règle générale, les options et les stratégies de sélection des options à présenter lors de l’expérience d’un client sont codées de manière approfondie au sein d’une application. | Les stratégies de sélection de la meilleure option sont définies en dehors des applications spécifiques au canal et deviennent réutilisables. |
| Les expériences client sont personnalisées et optimisées selon un objectif simpliste, par exemple augmenter le nombre de passages en caisse réussis sur une page Web ou accepter une offre présentée dans une interaction avec un représentant. | Les expériences client sont optimisées en fonction d’une compréhension globale des besoins actuels du client et s’adaptent à toutes les expériences que l’utilisateur a eues, bonnes ou mauvaises. Par exemple, une campagne marketing peut ne pas convenir à un client qui a récemment déposé une plainte à propos d’un produit ou d’un service. |

[!DNL Decisioning Service] déplace les capacités de personnalisation de votre expérience du ciblage en un seul canal vers la détermination de l’étape globale du cycle de vie de l’engagement de vos clients auprès de votre marque indépendamment des canaux. Une étape de cycle de vie est beaucoup plus complexe qu&#39;une appartenance à un segment et repose presque toujours sur des flux de événements complexes, des règles de fonctionnement et des attributs prédits.

Autres termes utilisés par les produits et services visant à servir des cas d&#39;utilisation similaires :

- Gestion des interactions en temps réel (RTIM)
- Gestion du parcours
- Marketing et personnalisation par canal Omni
- Prise de décision en temps réel

## How does [!DNL Decisioning Service] work?

Les expériences peuvent être personnalisées [!DNL Decisioning Service] en temps réel, car votre client interagit avec votre marque via un canal entrant, tel que votre site ou votre application mobile. La prise de décision peut également être utilisée pour personnaliser les messages via un canal sortant, tel qu’un courriel ou une notification Push.

Les décisions peuvent être prises de plusieurs façons. Une méthode consiste à éliminer les options successivement jusqu&#39;à ce qu&#39;il ne reste plus qu&#39;une seule option ou que les options aient été éliminées et qu&#39;il reste un sous-ensemble ou qu&#39;un gagnant soit sélectionné de façon aléatoire dans l&#39;ensemble réduit. Une variante de cette approche pour sélectionner l’option gagnante selon une formule calculée. Le classement des options éligibles est effectué à l’aide d’une fonction. Pour la prise de décision par offre, cette fonction peut calculer le coût, la valeur de l&#39;offre pour l&#39;entreprise et utiliser une méthode préétablie pour déterminer la probabilité que l&#39;offre soit acceptée par l&#39;utilisateur final. Le score obtenu peut être utilisé pour classer les offres.

Par ailleurs, une stratégie peut être basée sur les résultats recueillis lors d’interactions antérieures avec des clients semblables qui ont été proposés à des options similaires. Dans cette stratégie, la fonction qui a calculé les valeurs de priorité est apprise. La valeur optimale des résultats est liée aux objectifs de l&#39;activité et l&#39;indicateur de rendement pour la prévision est la fréquence à laquelle le résultat a été atteint après la proposition de l&#39;option.

### Stratégie de décision

Les stratégies de décision sont configurées au moyen d’objets appelés _activités_. Chaque stratégie de décision est essentiellement un algorithme ou une fonction qui prend N options {o1, o2, ...oN} comme entrée et produit une liste ordonnée d&#39;options (o1, o2,...oK) par laquelle la première option de la liste est considérée comme la meilleure selon un critère d&#39;optimisation, la deuxième option de la liste de résultats est alors considérée comme la deuxième meilleure option et ainsi de suite.

A tout moment au cours du voyage d’un client, la meilleure option pour une activité donnée est réévaluée en fonction de l’ensemble le plus récent de variables contextuelles, de règles et de contraintes. Les variables contextuelles incluent les enregistrements stockés dans [!DNL Real Time Customer Profile]. Une entité d’enregistrement centrale est le profil d’un client, mais d’autres entités telles que les données opérationnelles sont également disponibles pour l’activité.

L’algorithme ou la fonction qui produit la liste des options top-K varie selon le cas d’utilisation. Les composants internes de cet algorithme sont différents selon les cas d’utilisation. Les composants sont définis dans un référentiel au moment de la conception et &quot;compilés&quot; dans des instructions pour la stratégie de décision spécifique au cas d&#39;utilisation.

![optimisation des décisions](./images/decisioning-optimization.png)

## Working with [!DNL Decisioning Service]

Comme les autres [!DNL Decisioning Service]services, [!DNL Platform] l’API adopte une philosophie de premier ordre. Cela signifie que l’API est l’interface principale dans laquelle toutes les fonctions, y compris les fonctions d’administration, sont rendues disponibles via les API. Cela signifie également que d’autres [!DNL Platform] services, solutions Adobe et intégrations tierces utilisent les mêmes API.

Vous pouvez l’utiliser [!DNL Decisioning Service] en mode d’interaction requête-réponse synchrone, facilité par une API REST HTTP simple. L’appel d’API renvoie la meilleure option actuellement pour un seul profil. La sélection de la &quot;meilleure option actuellement&quot; changera en fonction des règles et contraintes appliquées à toutes les options qui sont prises en compte par une activité donnée. L’API REST permet d’obtenir la prochaine meilleure option pour plusieurs activités à la fois. Cela permet d&#39;arbitrer les options entre les canaux. Lorsque des réponses pour plusieurs activités sont obtenues ensemble, des règles supplémentaires peuvent être appliquées.

![decisioning-API](./images/decisioning-API.png)

### Intégration à d&#39;autres [!DNL Platform] workflows

L&#39;utilisation de [!DNL Decisioning Service] est facultative et ne nécessite que quelques étapes en plus des étapes standard requises pour créer [!DNL Profile] des entités et les gérer.

>[!NOTE] Pour en tirer le meilleur parti, le [!DNL Real-time Customer Profile][!DNL Decisioning Service] magasin de profils s&#39;intègre directement au magasin de . Les appels d&#39;API doivent uniquement indiquer l&#39;une des identités d&#39;un profil donné.

La séquence type de débuts d’étapes avec création de profils :

- Authentifiez-vous à [!DNL Experience Platform].
- Définissez un schéma basé sur la classe de profil et éventuellement un schéma basé sur la classe de événement d’expérience.
- Configurez un jeu de données pour transférer des données d’enregistrement et de série chronologique vers [!DNL Customer Profile].
- Ajoutez les données au moyen du jeu de données configuré dans les données d’étape précédente ou d’instance de flux via Pipeline.
- Diffusez des événements d’expérience dans le [!DNL Platform] afin d’enrichir le profil avec des données comportementales.

En outre, pour l’utiliser [!DNL Decisioning Service], procédez comme suit :

- Définissez les composants de décision à l’aide des API Repository. Il s&#39;agit des entités logiques qui composent la stratégie de décision. Les composants de décision seront automatiquement compilés dans un format utilisé par la [!DNL Decision Service Runtime]société. Les API Repository sont illustrées à gauche dans le diagramme ci-dessous.
- Appelez l’API d’exécution pour obtenir la meilleure option, conformément à la logique métier définie à l’étape précédente. Les [!DNL Decision Service Runtime] API sont illustrées à droite dans le diagramme ci-dessous.

![decisioning-API1](./images/decisioning-API1.png)

L&#39;activation des entités logiques métier se produit automatiquement et en permanence. Dès qu&#39;une nouvelle option est enregistrée dans le référentiel et qu&#39;elle est marquée comme &quot;approuvée&quot;, elle sera candidate à l&#39;inclusion dans l&#39;ensemble des options disponibles. Dès qu’une règle de décision est mise à jour, le jeu de règles est réassemblé et préparé pour l’exécution. À cette étape d’activation automatique, toutes les contraintes définies par la logique métier qui ne dépendent pas du contexte d’exécution seront évaluées. Les résultats de cette étape d’activation sont envoyés dans un cache où ils sont disponibles pour l’ [!DNL Decisioning Service] exécution. Ceci est illustré dans le diagramme suivant.

![decisioning-API2](./images/decisioning-API2.png)

Une fois que les options définies, les jeux de règles et les contraintes sont activés et ont été poussées vers [!DNL Decisioning Service] les noeuds, une API simple est utilisée pour publier une demande de décision. L’API est généralement appelée par un service de diffusion qui utilise ensuite l’option proposée (par exemple, la prochaine meilleure action ou la prochaine meilleure offre) et qui regroupe l’expérience ou exécute l’action. Si la proposition est une offre, le contenu qui représente cette offre est recherché et inséré dans une expérience fournie à l’utilisateur final. Ceci est illustré dans le diagramme suivant.

![decisioning-API3](./images/decisioning-API3.png)

[!DNL Delivery Service] collecte les données pour la demande de décision. Il détermine l&#39;ID de l&#39;entité de profil pour laquelle la meilleure option est décidée. Il assemble également toutes les données contextuelles qui ne sont pas stockées dans [!DNL Customer Profile] mais qui sont potentiellement utilisées par la logique de décision.

La logique de décision est organisée par activités, chacune d’elles spécifiant un filtre pour le sous-ensemble d’options à prendre en compte pour cette activité, ainsi qu’une seule option de secours.

Chaque décision est prise en appliquant d&#39;abord des contraintes pour réduire le nombre d&#39;options, puis en classant les options restantes. Bien que la majeure partie de la logique soit évaluée à l&#39;intérieur [!DNL Decisioning Service], divers services auxiliaires sont utilisés pour aider à ces deux aspects. Par exemple, un service de plafonnement gère les limites supérieures de la fréquence d’utilisation d’une option dans une décision, et un autre service peut héberger un modèle d’apprentissage automatique utilisé pour calculer les scores pour un profil et une option.

Pour en savoir plus sur l&#39;utilisation des API Repository, consultez le didacticiel sur la [gestion des entités de prise de décision et des règles à l&#39;aide des API.](./tutorials/entities.md)

Pour en savoir plus sur l’utilisation de l’ [!DNL Decisioning Service] exécution, consultez le didacticiel [Utilisation de l’exécution du service de prise de décision à l’aide des API](./tutorials/runtime.md)