---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Modèle de domaine de prise de décision d’expérience
topic: overview
translation-type: tm+mt
source-git-commit: 0f13ea667eecf936c69bcd98b0035a4355d73631

---


# Modèle de domaine de prise de décision d’expérience

Dans cette section, les composants du service de prise de décision sont expliqués et les modalités d&#39;interaction de ces composants sont détaillées. Les concepts et leurs relations forment le *Domaine* du problème de prise de décision. Ces composants fondamentaux entrent en jeu, quelle que soit la manière dont vous utilisez le service de prise de décision.

## Options de décision

Une option *de* décision d’expérience est une expérience potentielle qui peut être présentée à un client spécifique. Une option est également appelée choix ou alternative. Lorsque vous décidez de la meilleure option pour un client, le service de prise de décision considère les options ***d<sub>1</sub>***à***<sub>dN</sub>*** parmi un ensemble fini d&#39;options **`D`**.

Les décisions sont prises en identifiant la meilleure option parmi un ensemble d&#39;options disponibles. L’une des approches consiste à éliminer successivement les options *de* décision ***<sub>décidées</sub>***à partir du jeu*** D ***jusqu’à ce qu’il ne reste plus qu’une seule option, puis à choisir un &quot;gagnant&quot; de manière aléatoire dans le jeu restant. Une autre forme de prise de décision consiste à classer les autres options de décision (admissibles) en fonction de leur résultat attendu.

### Ensemble fini d&#39;options de décision

Dans le domaine de la prise de décision d’expérience, les options à partir desquelles une ou plusieurs options sont sélectionnées existent a priori et le calcul d’une décision ne crée pas de nouvelles options à la volée. Nous disons que le domaine des options est fini au moment où les décisions sont prises. Cela peut sembler une limitation, mais un ensemble fini d&#39;options donne la possibilité d&#39;utiliser des algorithmes d&#39;apprentissage automatique et des techniques similaires pour déterminer laquelle des options est &quot;la meilleure&quot;. De nombreux algorithmes d’apprentissage ne seraient pas en mesure de produire la meilleure option parmi un ensemble d’alternatives infinies qui ne peuvent être comparées les unes aux autres et pour lesquelles il n’existe aucune donnée d’exemple.

## Résultats des décisions

Il est important de faire la distinction entre le résultat de la décision `d` et le résultat `o`, c&#39;est-à-dire les résultats prévus par la décision. Une décision ne peut souvent pas produire de résultat directement. La décision consiste uniquement à sélectionner (ou à proposer) l’option avec le meilleur résultat attendu. Entre propositions et résultats, de nombreux  et interactions se produisent, souvent retardés par des jours ou des semaines. En termes plus formels, le résultat dépend de la décision `o = f(d)`.

Pour trouver la décision optimale, chaque résultat se voit attribuer une valeur ***d&#39;*** utilitaire `U(o) = U(f(d))`.
Pour le cas d’utilisation de la prise de décision  , cette fonction calculerait le coût de réalisation du , ainsi que la valeur gagnée par l’entreprise lorsque le est accepté par le client. Le résultat serait utilisé pour trouver la décision optimale ( ) en maximisant la valeur de l&#39;utilitaire par rapport à toutes les options ( ).

Il n&#39;est généralement pas possible de prédire avec certitude quel sera le résultat d&#39;une décision particulière et il est donc nécessaire d&#39;adopter une approche probabiliste. La valeur ***de l’*** utilitaire devient la valeur `U(o)` attendue de l’utilitaire d’une option ****** de décision. `EU(d)`

## Propositions de décision

Une proposition *de* décision est un choix d&#39;option de décision qui a été fait en réponse à une demande de décision réelle. Comme nous l&#39;avons mentionné plus haut, les résultats d&#39;une décision peuvent se produire beaucoup plus tard et les résultats peuvent ne pas être atteints en une seule étape non plus. Il est donc important de suivre les propositions au moyen d&#39;un *d&#39;* expériences variées afin qu&#39;elles puissent être attribuées aux options de décision. Cette boucle de rétroaction permet d’améliorer la précision de prédiction pour `EU(d)`.

Une proposition est conservée en tant qu’entité et possède donc un identifiant. L&#39;entité détient des références aux options sélectionnées et peut enregistrer les données contextuelles utilisées pour prendre la décision. Le fait d’avoir un identifiant permet également à d’autres entités de le référencer. L&#39;une de ces entités est la *de décision*. Il détient l&#39;horodatage, marquant le moment où sa décision (proposition) a été prise. Un de décision est un événement enregistré de l&#39;action d&#39;exécuter la décision. Les autres  qui font référence à l’entité de proposition sont des  d’expérience. Chaque  d’expérience peut être étendu pour faire référence à une proposition de décision. L&#39;interprétation est que l&#39; de l&#39;expérience peut être entièrement ou partiellement attribuée à la proposition de la décision.

## Stratégie de décision - Algorithme

Avec un ensemble fini d&#39;options à choisir, chaque stratégie *de* décision est essentiellement un algorithme - ou une fonction - qui prend les options de **`N`** décision *{d<sub>1</sub>, d<sub>2, ...dN}comme entrée et produit un classé d&#39;options de décision(dr1,dr2,.......)drk))Dans le cas où la première option de décision dans le est considérée comme optimale en fonction d&#39;un utilitaire attendu, la deuxième option dans lerésultat est alors considérée comme la deuxième meilleure option, etc.</sub><sub></sub>**<sub></sub><sub></sub><sub></sub>* En règle générale, la cardinalité du jeu est supérieure à celle du classé résultant, car l’algorithme de décision élimine les options non admissibles et un algorithme peut être configuré pour renvoyer uniquement les options principales, s’arrêtant après avoir trouvé suffisamment d’options. **`K`** 
Le cadre général de décision est présenté dans le diagramme suivant.

![Figure 1](./images/decisioning-optimization.png)

##  de décision

*de décision* configurer l’algorithme et fournir des paramètres pour une stratégie de décision spécifique. Les paramètres de stratégie incluent les contraintes appliquées aux options et la fonction de classement. Toutes les décisions sont prises dans le cadre d&#39;un  . Le service de prise de décision héberge de nombreux  , et les  peuvent être réutilisés dans l’ensemble du. A tout moment, la meilleure option est évaluée en fonction de l’ensemble de contraintes, de règles et de modèles le plus récent.

Une décision   définit la collecte des options de décision à prendre en considération. Il  le sous-ensemble de toutes les options qui intéressent ce . Cela permet au service de prise de décision de gérer les  d’actualité dans le catalogue de toutes les options.

Une décision   spécifie une option *de* secours si les contraintes combinées disqualifient toutes les autres options. Cela signifie qu&#39;il y a toujours une réponse à la question : Quelle est actuellement la &quot;meilleure&quot; option ?

 de décision  peut spécifier le lieu de diffusion de l’expérience. Cela réduit encore davantage le nombre d&#39;options de décision qui peuvent être envisagées et constitue une autre contrainte imposée par la décision  . On parle alors de contrainte *de* placement. Seules les options de décision dont le contenu respecte cette contrainte de placement seront prises en compte. Cette évaluation est effectuée aux premières étapes de la stratégie de décision. Lorsque les définitions changent les contraintes de placement de chaque décision  les  sont réévalués et l&#39;option de décision peut entrer ou ne pas être prise en considération pour une ou plusieurs décisions  le.

## Contexte de décision

Jusqu&#39;à présent, seule la *logique* commerciale qui affecte la décision a été décrite. Mais les *données* d&#39;entrée de la décision ont encore plus d&#39;impact sur la sortie. Ces données s’appellent le contexte *de* décision et sont différentes pour chaque utilisateur et chaque fois qu’une décision est prise, par opposition aux contraintes, règles et modèles qui sont les mêmes pour les utilisateurs différents pour le même  . Les règles, les contraintes et les modèles changent également moins fréquemment. Pour prendre une décision en temps réel, le contexte de la décision devra également être déterminé en temps réel.

Les données contextuelles de décision peuvent être divisées en données d’utilisateur, données d’entreprise et données collectées en interne.

- *Les entités*  sont utilisées pour représenter les données de l&#39;utilisateur final, mais toutes les entités  ne représentent pas une personne. Il peut s&#39;agir d&#39;un foyer, d&#39;un groupe social ou de tout autre sujet. Les  d’expérience sont des enregistrements de données de série chronologique associés à un  de. S’il existe une expérience, ces données sont alors l’ *objet* de cette expérience.
- De l&#39;autre côté, il y a les entités *commerciales*. Ils peuvent être considérés comme les *objets* des interactions. Ces entités sont souvent référencées dans le d&#39;expérience des entités . Les sites Web et les pages, les magasins, les détails des produits, le contenu numérique, les données d’inventaire des produits, etc., sont des exemples d’entités commerciales.
- Le dernier de données dans le contexte de la décision est celui des données qui ont été créées pendant l’exploitation du service de décision. Chaque de décision  dans ce, ainsi que les réponses des clients, les données de proposition forment un jeu de données interne appelé l&#39;historique ** proposition-réponse.

Il existe trois façons dont les données peuvent faire partie du contexte de décision. Les données d’enregistrement et de série chronologique peuvent être téléchargées via des fichiers de jeux de données. Ce chemin est principalement destiné à une synchronisation en masse avec des systèmes externes. Les données d’enregistrement et de série chronologique peuvent également être diffusées dans la plateforme où les données sont indexées et associées aux entités de formulaire. Par le troisième chemin, les données contextuelles peuvent être transmises en tant que paramètres à la demande de décision. Cette forme de données est de nature éphémère et n&#39;est pertinente que pour la décision demandée. Il n’est pas conservé en tant qu’entité et n’est pas disponible pour d’autres requêtes.
