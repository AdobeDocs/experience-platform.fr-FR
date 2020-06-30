---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Modèle de domaine de prise de décision d’expérience
topic: overview
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 0%

---


# Modèle de domaine d’expérience [!DNL Decisioning]

Dans cette section, les composants de [!DNL Decisioning Service] sont expliqués et la manière dont ces composants interagissent est détaillée. Les concepts et leurs relations forment le *Domaine* du problème de prise de décision. Ces composants fondamentaux entrent en jeu, quelle que soit votre utilisation [!DNL Decisioning Service].

## Options de décision

Une option *de* décision d’expérience est une expérience potentielle qui peut être présentée à un client spécifique. Une option est également appelée choix ou alternative. Lorsque vous choisissez la meilleure option pour un client, [!DNL Decisioning Service] considère les options ***d<sub>1</sub>***à***<sub>dN</sub>*** parmi un ensemble fini d’options **`D`**.

Les décisions sont prises en identifiant la meilleure option parmi un ensemble d&#39;options disponibles. Une approche consiste à éliminer successivement les options *de* décision ***<sub>di</sub>***du jeu*** D ***jusqu’à ce qu’il ne reste plus qu’une seule option, puis à choisir un &quot;gagnant&quot; de manière aléatoire parmi les autres. Une autre forme de prise de décision consiste à classer les options de décision restantes (admissibles) en fonction de leur résultat attendu.

### Ensemble fini d&#39;options de décision

Dans le domaine de la prise de décision d’expérience, les options à partir desquelles une ou plusieurs options sont sélectionnées existent a priori et le calcul d’une décision ne crée pas de nouvelles options à la volée. Nous disons que le domaine des options est fini au moment où les décisions sont prises. Cela peut sembler une limitation, mais un ensemble fini d&#39;options donne la possibilité d&#39;utiliser des algorithmes d&#39;apprentissage automatique et des techniques similaires pour déterminer laquelle des options est &quot;la meilleure&quot;. De nombreux algorithmes d’apprentissage ne seraient pas en mesure de produire la meilleure option parmi un ensemble d’alternatives infinies qui ne peuvent pas être comparées les unes aux autres et pour lesquelles il n’existe aucune donnée d’exemple.

## Résultats des décisions

Il est important de faire la distinction entre le résultat de la décision `d` et le résultat `o`, c&#39;est-à-dire les résultats escomptés qui ont été fixés par la décision. Souvent, une décision ne peut pas produire directement un résultat. La décision ne consiste qu&#39;à sélectionner (ou à proposer) l&#39;option avec le meilleur résultat attendu. Entre propositions et résultats, de nombreux événements et interactions se produisent, souvent retardés de jours ou de semaines. En termes plus formels, le résultat est fonction de la décision `o = f(d)`.

Pour trouver la décision optimale, chaque résultat se voit attribuer une valeur ***d&#39;*** utilitaire `U(o) = U(f(d))`.
Pour le cas d’utilisation de la prise de décision d’Offre, cette fonction calculerait le coût de réalisation de l’offre et la valeur gagnée par l’entreprise lorsque l’offre est acceptée par le client. Le résultat serait utilisé pour trouver la décision optimale (offre) en maximisant la valeur d&#39;utilité sur toutes les options (offres).

Il n&#39;est généralement pas possible de prédire avec certitude quel sera le résultat d&#39;une décision particulière et, par conséquent, une approche probabiliste est nécessaire. La valeur ***de l&#39;*** utilitaire `U(o)` devient la valeur ***attendue de l&#39;utilitaire d&#39;une option de décision.*** `EU(d)`

## Propositions de décision

Une proposition *de* décision est un choix d&#39;option de décision qui a été fait en réponse à une demande de décision réelle. Comme nous l&#39;avons indiqué plus haut, les résultats d&#39;une décision peuvent se produire beaucoup plus tard et les résultats ne peuvent pas être atteints en une seule étape non plus. Il est donc important de suivre les propositions au moyen de divers événements *d&#39;* expérience afin qu&#39;elles puissent être réattribuées aux options de décision. Cette boucle de rétroaction est utilisée pour améliorer la précision de la prédiction pour `EU(d)`.

Une proposition est conservée en tant qu’entité et possède donc un identifiant. L&#39;entité détient des références aux options sélectionnées et peut enregistrer les données contextuelles utilisées pour prendre la décision. Avoir un identifiant permet également à d&#39;autres entités de le référencer. L&#39;une de ces entités est le événement ** de décision. Il conserve l&#39;horodatage, qui marque le moment où sa décision (proposition) a été prise. Un événement de décision est un événement enregistré de l&#39;action d&#39;exécution de la décision. D&#39;autres événements qui font référence à l&#39;entité proposée sont des événements d&#39;expérience. Chaque événement d&#39;expérience peut être étendu pour faire référence à une proposition de décision. L&#39;interprétation est que le événement d&#39;expérience peut être attribué entièrement ou partiellement à la proposition de la décision.

## Stratégie de décision - Algorithme

Avec un ensemble fini d&#39;options à choisir, chaque stratégie *de* décision est essentiellement un algorithme - ou une fonction - qui prend des options de **`N`** décision *{d<sub>1</sub>, d<sub>2, ...dN}liste en entrée et produit une  classée d&#39;options de décision (dr1, dr2,..)drk  où la première option de décision dans la liste est considérée comme optimale en fonction d&#39;un utilitaire attendu, la deuxième option dans la liste de résultats est alors considérée comme la deuxième meilleure option, etc.</sub><sub></sub>**<sub></sub><sub></sub><sub></sub>* En règle générale, la visionneuse aura une cardinalité plus élevée que la liste de classement résultante, car l’algorithme de décision élimine les options qui ne sont pas éligibles et un algorithme peut être configuré pour renvoyer uniquement les options principales, s’arrêtant après avoir trouvé suffisamment d’options. **`K`** 
Le cadre de décision général est présenté dans le diagramme suivant.

![Figure 1](./images/decisioning-optimization.png)

## Activités de décision

*Les activités* de décision configurent l’algorithme et fournissent les paramètres pour une stratégie de décision spécifique. Les paramètres de stratégie incluent les contraintes appliquées aux options et la fonction de classement. Toutes les décisions sont prises dans le cadre d&#39;une activité. [!DNL Decisioning Service] héberge de nombreuses activités et les activités peuvent être réutilisées sur plusieurs canaux. À tout moment, la meilleure option est évaluée en fonction de l’ensemble de contraintes, de règles et de modèles le plus récent.

Une activité de décision définit la collecte des options de décision à envisager. Il filtres le sous-ensemble de toutes les options qui intéressent cette activité. Cela permet [!DNL Decisioning service] à la gestion des catégories thématiques dans le catalogue de toutes les options.

Une activité de décision spécifie une option *de* secours si les contraintes combinées disqualifient toutes les autres options. Cela signifie qu&#39;il y a toujours une réponse à la question : Quelle est actuellement la &quot;meilleure&quot; option ?

Les activités de décision peuvent spécifier le lieu de diffusion de l’expérience. Cela réduit davantage le nombre d&#39;options de décision qui peuvent être envisagées et constitue une autre contrainte imposée par l&#39;activité de décision. Il s&#39;agit de la contrainte *de* placement. Seules les options de décision dont le contenu respecte cette contrainte de placement seront prises en compte. Cette évaluation est effectuée dans les premières étapes de la stratégie de décision. Lorsque les définitions changent, les contraintes de placement de chaque activité de décision sont réévaluées et l&#39;option de décision peut être prise en considération ou ne pas l&#39;être pour une ou plusieurs activités de décision.

## Contexte de décision

Jusqu&#39;à présent, seule la *logique* commerciale qui affecte la décision a été décrite. Mais les *données* d&#39;entrée de la décision ont encore plus d&#39;impact sur la production. Ces données sont appelées contexte *de* décision et sont différentes pour chaque utilisateur et chaque fois qu’une décision est prise, par opposition aux contraintes, règles et modèles qui sont identiques pour des utilisateurs différents pour la même activité. Les règles, les contraintes et les modèles changent également moins fréquemment. Pour la prise de décision en temps réel, le contexte de la décision devra également être déterminé en temps réel.

Les données contextuelles de décision peuvent être divisées en données liées au profil d’utilisateur, en données métier et en données collectées en interne.

- *Les entités* de Profil sont utilisées pour représenter les données de l&#39;utilisateur final, mais toutes les entités de profil ne représentent pas un individu. Il peut s&#39;agir d&#39;un foyer, d&#39;un groupe social ou de toute autre matière. Les événements d’expérience sont des enregistrements de données de série chronologique joints à un profil. S’il existe une expérience, ces données constituent le *sujet* de cette expérience.
- De l&#39;autre côté, il y a les entités ** commerciales. Ils peuvent être considérés comme les *objets* des interactions. Ces entités sont souvent référencées dans les événements d&#39;expérience des entités de profil. Les sites Web et les pages, les magasins, les détails des produits, le contenu numérique, les données d&#39;inventaire des produits, etc. sont des exemples d&#39;entités commerciales.
- La dernière catégorie de données dans le contexte de la décision est celle des données qui ont été créées pendant le fonctionnement de la [!DNL Decisioning Service]. Chaque événement de décision entre dans cette catégorie, ainsi que les réponses des clients, les données de proposition forment un ensemble de données internes appelé l&#39;historique ** proposition-réponse.

Il existe trois façons dont les données peuvent faire partie du contexte de décision. Les données d’enregistrement et de série chronologique peuvent être téléchargées via des fichiers de jeux de données. Ce chemin est principalement destiné à la synchronisation en masse avec des systèmes externes. Les données d’enregistrement et de série chronologique peuvent également être diffusées en continu [!DNL Platform] où les données sont indexées et jointes aux entités de formulaire. Par le troisième chemin, les données contextuelles peuvent être transmises en tant que paramètres à la demande de décision. Cette forme de données est de nature éphémère et n&#39;est pertinente que pour la décision demandée. Il n’est pas conservé en tant qu’entité et n’est pas disponible pour d’autres requêtes.
