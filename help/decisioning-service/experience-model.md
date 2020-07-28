---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Modèle de domaine de prise de décision d’expérience
topic: overview
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 91%

---


# Experience [!DNL Decisioning] domain model

In this section, the components of [!DNL Decisioning Service] are explained and the ways in which those components interact are detailed. Les concepts et leurs relations forment le *Domaine* du problème de décision. These fundamental components come into play regardless of how you use [!DNL Decisioning Service].

## Options de décision

Une *option de décision* d’expérience est une expérience potentielle qui peut être présentée à un client spécifique. Une option peut également être appelée choix ou alternative. When deciding on the next best option for a customer, [!DNL Decisioning Service] considers options ***d<sub>1</sub>***to*** d<sub>N</sub>*** from amongst a finite set of options **`D`**.

Les décisions sont prises en identifiant la meilleure option parmi un ensemble d’options disponibles. L’une des approches consiste à éliminer successivement les *options de décision* ***d<sub>i</sub>*** du jeu *** D *** jusqu’à ce qu’il ne reste plus qu’une seule option, puis à choisir un « gagnant » de manière aléatoire dans le jeu restant. Une autre forme de prise de décision consiste à classer les autres options de décision (admissibles) en fonction de leur résultat attendu.

### Ensemble fini d’options de décision

Dans le domaine de prise de décision d’expérience, les options parmi lesquelles une ou plusieurs d’entre elles sont sélectionnées existent au préalable et le calcul d’une décision ne crée aucune nouvelle option à la volée. Le domaine des options est considéré comme fini au moment où les décisions sont prises. Cela peut passer pour une limitation, mais un ensemble fini d’options offre la possibilité d’utiliser des algorithmes d’apprentissage automatique et des techniques similaires pour déterminer laquelle des options est « la meilleure ». De nombreux algorithmes d’apprentissage ne seraient pas en mesure de produire la meilleure option parmi un ensemble d’alternatives infinies qui ne peuvent pas être comparées les unes aux autres et pour lesquelles il n’existe aucune donnée d’exemple.

## Résultats des décisions

Il est important de faire la distinction entre le résultat de la décision `d` et le résultat `o`, c’est-à-dire les résultats prévus par la décision. Une décision peut rarement produire un résultat direct. La décision consiste uniquement à sélectionner (ou à proposer) l’option avec le meilleur résultat attendu. Entre propositions et résultats, de nombreux événements et interactions se déroulent, souvent retardés pendant des jours ou des semaines. En termes plus formels, le résultat dépend de la décision `o = f(d)`.

Pour trouver la décision optimale, chaque résultat se voit attribuer une ***valeur d’utilité*** `U(o) = U(f(d))`.
Pour le cas d’utilisation de la prise de décision relative aux offres, cette fonction calculerait le coût de réalisation de l’offre ainsi que la valeur gagnée par l’entreprise lorsque le client accepte l’offre. Le résultat serait utilisé pour trouver la décision (l’offre) optimale en maximisant la valeur d’utilité par rapport à toutes les options (offres).

Il est généralement impossible de prédire avec certitude quel sera le résultat d’une décision spécifique. Il est donc nécessaire d’adopter une approche probabiliste. La ***valeur d’utilité*** `U(o)` devient la ***valeur d’utilité attendue d’une option de décision***. `EU(d)`

## Propositions de décision

Une *proposition de décision* est un choix d’option de décision réalisé en réponse à une réelle requête de décision. Comme mentionné plus haut, les résultats d’une décision peuvent se produire beaucoup plus tard et peuvent également ne pas être atteints en une seule étape. Il est donc important de suivre les propositions au moyen de divers *événements d’expérience* afin qu’elles puissent être réattribuées aux options de décision. Cette boucle de rétroaction permet d’améliorer la précision de prédiction pour `EU(d)`.

Une proposition est conservée en tant qu’entité et possède donc un identifiant. L’entité détient des références aux options sélectionnées et peut enregistrer les données contextuelles utilisées lors de la prise de décision. Disposer d’un identifiant permet également à d’autres entités de le référencer. L’une de ces entités est l’*événement de décision*. Il détient l’horodatage, qui marque le moment où sa décision (proposition) a été prise. Un événement de décision est une occurrence enregistrée de l’action d’exécuter la décision. Les autres événements faisant référence à l’entité de proposition sont des événements d’expérience. Chaque événement d’expérience peut être étendu pour faire référence à une proposition de décision. Ainsi, l’événement d’expérience peut être entièrement ou partiellement attribué à la proposition de la décision.

## Stratégie de décision - Algorithme

Avec un ensemble fini d’options parmi lesquelles choisir, chaque *stratégie de décision* constitue essentiellement un algorithme (ou une fonction) qui prend **`N`** options de décision *{d<sub>1</sub>, d<sub>2</sub>… d<sub>N</sub>}* comme entrée et produit une liste classée d’options de décision *(d<sub>r1</sub>, d<sub>r2</sub>… d<sub>rk</sub>)* selon laquelle la première option de décision de la liste est considérée comme optimale en fonction d’une utilité attendue, la deuxième option de la liste de résultats est quant à elle considérée comme la deuxième meilleure option, etc. En règle générale, la cardinalité de l’ensemble est supérieure à celle de la liste classée de résultats, car l’algorithme de décision élimine les options non admissibles et un algorithme peut être configuré pour renvoyer uniquement les meilleures options **`K`** et s’arrêter après avoir trouvé suffisamment d’options.
La structure de décision générale est illustrée dans le diagramme ci-dessous.

![Figure 1](./images/decisioning-optimization.png)

## Activités de décision

Les *activités de décision* configurent l’algorithme et fournissent des paramètres pour une stratégie de décision spécifique. Les paramètres de stratégie incluent les contraintes appliquées aux options ainsi que la fonction de classement. Toutes les décisions sont prises dans le cadre d’une activité. [!DNL Decisioning Service] héberge de nombreuses activités et les activités peuvent être réutilisées sur plusieurs canaux. À tout moment, la meilleure option est évaluée en fonction de l’ensemble de contraintes, de règles et de modèles le plus récent.

Une activité de décision définit la collecte des options de décision à prendre en considération. Elle filtre le sous-ensemble de toutes les options pertinentes pour cette activité. This allows the [!DNL Decisioning service] to manage topical categories within the catalog of all options.

Une activité de décision spécifie une *option de rechange* si les contraintes combinées disqualifient toutes les autres options. Cela signifie qu’il existe toujours une réponse à la question « quelle est actuellement la “meilleure” option ? »

Les activités de décision peuvent spécifier le lieu de distribution de l’expérience. Cela réduit davantage le nombre d’options de décision pouvant être envisagées, et constitue une contrainte supplémentaire imposée par l’activité de décision. Cette contrainte s’intitule *contrainte d’emplacement*. Seules les options de décision dont le contenu respecte cette contrainte d’emplacement seront prises en compte. Cette évaluation est effectuée dans les premières étapes de la stratégie de décision. Lorsque les définitions changent, les contraintes d’emplacement de chaque activité de décision sont réévaluées, et l’option de décision peut être prise en considération ou non pour une ou plusieurs activités de décision.

## Contexte de décision

Jusqu’à présent, seule la *logique* commerciale qui affecte la décision a été décrite. Toutefois, les *données* d’entrée de la décision ont encore plus d’impact sur la sortie. Ces données forment ce qui est appelé le *contexte de décision* et sont différentes pour chaque utilisateur et chaque fois qu’une décision est prise, par opposition aux contraintes, aux règles et aux modèles qui sont identiques pour différents utilisateurs pour la même activité. De la même manière, les règles, contraintes et modèles changent moins fréquemment. Pour la prise de décision en temps réel, le contexte de la décision devra également être déterminé en temps réel.

Les données contextuelles de décision peuvent se diviser en données de profil utilisateur, données d’entreprise et données collectées en interne.

- Les *entités de profil* sont utilisées pour représenter les données de l’utilisateur final, mais toutes les entités de profil ne représentent pas un individu. Il peut s’agir d’un foyer, d’un groupe social ou de tout autre sujet. Les événements d’expérience sont des enregistrements de données de série temporelle associés à un profil. S’il existe une expérience, ces données constituent alors le *sujet* de cette expérience.
- D’autre part existent les *entités commerciales*. Elles peuvent être considérées comme les *objets* des interactions. Ces entités sont souvent référencées dans les événements d’expérience des entités de profil. Les sites et les pages web, les magasins, les détails de produit, le contenu numérique, les données d’inventaire des produits sont autant d’exemples d’entités commerciales.
- The last category of data in the decision context is data that was created during operation of the [!DNL Decisioning Service]. Chaque événement de décision fait partie de cette catégorie. Les données de proposition forment avec les réponses des clients un jeu de données interne appelé l’historique de *proposition-réponse*.

Les données peuvent être intégrées au contexte de décision de trois façons. Les données d’enregistrement et de série temporelle peuvent être transférées au moyen de fichiers de jeu de données. Ce procédé est principalement destiné à une synchronisation en masse avec des systèmes externes. Record and time series data can also be streamed into [!DNL Platform] where the data is indexed and joined to form entities. Enfin, les données contextuelles peuvent être transmises en tant que paramètres à la requête de décision. Cette forme de données est de nature éphémère et n’est pertinente que pour la décision requise. Elle n’est pas conservée en tant qu’entité et n’est pas disponible pour d’autres requêtes.
