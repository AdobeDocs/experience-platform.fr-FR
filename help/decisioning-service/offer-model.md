---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' modèle de domaine de prise de décision '
topic: overview
translation-type: tm+mt
source-git-commit: fdaef24a23c1c1da064ca33e8bed522e506fead5

---


# Présentation du modèle de domaine de prise de décision

 prise de décision  est un cas d’utilisation du service de prise de décision dans lequel vous formalisez et gérez de manière centralisée les règles et les prédictions utilisées pour engager les clients avec les  de.  prise de décision  est considérée comme un type de prise de décision _**sur le**_ contenu. Dans ce cas d&#39;utilisation, les options _**de**_ décision sont appelées _****_ et sont caractérisées comme telles par le contenu qui leur est joint. Pour une présentation du modèle d&#39;objet utilisé par le service de décision, reportez-vous au modèle [de domaine du service de](experience-model.md)décision.

L&#39;objectif est de présenter à l&#39;utilisateur final un &quot;meilleur  &quot; dans tout, quel que soit le critère de ciblage, les contraintes de coût et de fréquence, ainsi que les interactions préalables entre les, y compris les recommandations de l&#39;ancien.

Comme pour tous les cas d’utilisation de la prise de décision, les options de décision ( ) sont gérées dans un rapport partagé par n’importe quel nombre d’applications.   de peut être créé par différents départements de votre organisation ou par des partenaires, et ces  de peuvent être ajoutés et supprimés quotidiennement.

 les  sont visuellement placés dans des expériences plus vastes par l’application qui diffuse l’expérience. _**Les emplacements**_, parfois appelés emplacements ou emplacements, sont des composants importants pour l’élaboration d’une stratégie. Concevoir une stratégie   est souvent en avec la définition de ces placements. Un   comporte généralement plusieurs représentations _**de**_ contenu, de sorte qu’il puisse être correctement intégré dans une variété d’expériences, où chacune a des contraintes dimensionnelles ou autres et requiert différents formats de médias.

 a souvent des liens avec des biens ou des services physiques et il y a un calcul des coûts. Une organisation doit être en mesure de limiter les ressources consommées par   et doit donc être en mesure de _**plafonner**_ le nombre total de fois qu&#39;un peut être proposé.

La valeur prévue d&#39;un  accepté  à l&#39;organisation est le critère d&#39;optimisation et va à l&#39;encontre du coût de réalisation d&#39;un . Le coût, la probabilité d&#39;acceptation et la valeur prévue sont utilisés pour classer le  . Le meilleur   est celui qui a le plus fort impact positif prédit sur les objectifs de votre de de .

 prise de décision  prend en compte les interactions qu’un utilisateur final a eu, _**dans de nombreux et applications, pour tirer parti des données de l’analyse de l’expérience et du**_ de l’utilisateur final. Par exemple, une application de centre d’appels peut utiliser  décision  pour activer ou supprimer un  en fonction des achats effectués et des révisions publiées par l’utilisateur final ; ou une application de gestion de courrier électronique peut compter sur  décision  pour sélectionner le prochain meilleur de  dans un bulletin d&#39;information hebdomadaire basé sur l&#39;historique de navigation d&#39;un site Web.

  ont d&#39;autres propriétés intéressantes. Souvent, il existe un _**calendrier**_ ou une plage de dates et d’heures défini lorsque le   est valide et lorsque le de la   doit être invalidé.

Enfin, l&#39;appel d&#39;un   se détériore avec la fréquence à laquelle il est présenté. Un   qui n&#39;est pas accepté après avoir été proposé à plusieurs reprises est une occasion perdue parce qu&#39;un autre de  aurait pu être présenté. C&#39;est pourquoi il faut gérer la _**fatigue**_ des utilisateurs finaux.

## Stratégie de décision en un coup d&#39;oeil

L’approche globale consiste à restreindre la sélection des  de  jusqu’à ce que toutes les contraintes soient satisfaites, puis à appliquer le modèle de classement aux options restantes, puis à optimiser sur plusieurs  de à l’aide des contraintes de plafonnement (déduplication et évitement des choix de secours).

| Composante stratégique | Réalisé en tant que |
| --- | --- |
|  de décision |    |
| Options de décision |  de  avec des représentations de contenu |
| Options de secours | de secours avec  de contenu |
| Ensemble fini d&#39;options de décision |  inventaire  (alias  bibliothèque ) |
|  de rubrique |  filtre  basé sur les balises et les identifiants de  |
| Résultats de la décision | Proposition d&#39;un   par , pour plusieurs à la fois |
| Résultats de la décision | d’expérience attendu en référence à la  de l’, p. ex. `eventType='opened'` |
| Algorithme de décision | Logique de service interne, paramétrée |
| Contraintes | Contraintes de positionnement, contraintes de calendrier, contraintes de plafonnement globales et par utilisateur, contraintes de déduplication |
| Règles de décision | Règles d’éligibilité |
| Modèle pour l&#39;utilitaire *attendu* |  rang ou priorité  |

Le nombre total de   dans l&#39;inventaire des options est généralement assez important (de l&#39;ordre de 10 000) et chaquede peut être axé sur les qui tombent dans un autre(sujet). La stratégie de décision   permet d&#39;associer un filtre de  à un dede. D&#39;autres contraintes seront évaluées au moment où la décision sera demandée.
Les sections suivantes expliquent en détail les composants du domaine de prise de décision  .

##  général 

 général , aussi appelé personnalisé, sont les options au centre du de décision de lade décision de la. Ils ont des attributs tels que le nom et le statut. L’attribut status indique si l’entité est prête à être incluse dans le  de la  de approuvée active.  général  aura plusieurs contraintes à leur ajouter. Pour en savoir plus, reportez-vous à la section Contraintes ‎ [ci-dessous](#offer-constraints).

## Contenu dans   de

###  emplacements 

Les emplacements définissent les contraintes de contenu et sont utilisés avec un   pour spécifier l’emplacement dans lequel la meilleure expérience sera diffusée. Cela réduit encore davantage le nombre d’options qui peuvent être prises en compte et constitue une autre contrainte imposée par le  . On parle alors de contrainte de placement. Seules les options dont le contenu répond à une contrainte d’emplacement, telles que  , seront prises en compte. Cette évaluation est effectuée aux premières étapes de la stratégie de décision. Lorsque les objets d’option modifient les contraintes de positionnement de chaque   sont réévalués et l’option peut être prise en considération ou en tirer pour un ou plusieurs .

Il n’est pas de la responsabilité du service de décision de formaliser les détails complexes des dépendances de contenu. Au lieu de cela, chaque client identifiera le des placements dans tous les  et attribuera à ces placements des identifiants et des noms uniques. En référençant un emplacement particulier, le concepteur affirme que le contenu donné s’adaptera à l’emplacement.

Lorsque le contenu est développé, le spécialiste du marketing   et le concepteur de contenu s’entendent simplement (doivent) sur un &quot;contrat implicite&quot; qui se trouve derrière le nom &quot;Image de héros&quot; ou &quot;Script d’ouverture d’appel de service&quot;. Le premier peut être convenu comme une image de 600 px de largeur et de 350 px de hauteur et le second peut restreindre le contenu au texte dans deux variantes de langue qui ne dépasse pas 50 mots en trois ou quatre phrases avec une structure sémantique. Placement pour ne pas stocker tout le sens du contrat caché.

### Offer Representations

Pour vous assurer qu&#39;un   puisse être présenté correctement dans les paramètres variables des emplacements dans votre, vous devez créer différentes représentations de ce. Le contenu joint à   de est regroupé par emplacements. Chaque   peut avoir une ou plusieurs représentations dans lesquelles chacune de ces représentations fait référence à l’un des emplacements définis. Chaque représentation dans un   doit utiliser un emplacement différent. Plus le nombre de représentations   a la possibilité d&#39;utiliser le de la  dans différentsde placement.

Un emplacement limite le type d’éléments de contenu qui peuvent être ajoutés à la représentation.

## des abandons  

Les  de secours sont des options de décision qui ne comportent pas de contraintes supplémentaires, à l’exception des règles de placement. Les de secours  ont des représentations de contenu qui sont liées aux emplacements, tout comme n’importe quel autre  de.

Les de  de secours sont spécifiés dans  de données afin d’indiquer une expérience de contenu viable à utiliser lorsque les contraintes combinées excluent toutes les options réduites. Etant donné qu’elle ne dépend pas du contexte d’exécution ou de la  du, la contrainte de placement peut être vérifiée à l’avance lorsque le  du est assemblé. En utilisant le de secours  , il y a toujours une réponse à la question : Quel est actuellement le meilleur   ?

##  contraintes 

### Contraintes de calendrier

Dans le domaine de prise de décision  du , le  a une période de validité. Cela signifie que la   ne peut pas être proposée avant que la date et l&#39;heure de sa  ne soient dépassées et ne peut plus l&#39;être après la date et l&#39;heure de fin de la. L&#39;entité   a une structure simple qui définit ces contraintes de calendrier.

Périodiquement, les   expirés seront supprimés de l&#39;des options considérées. Mais le filtre de calendrier est appliqué correctement au moment où la décision est demandée, de sorte que les contraintes soient appliquées avec précision.

### Contraintes de plafonnement

  peut avoir une contrainte de recouvrement facultative. Il se compose de deux valeurs :

- La valeur de limite globale limite la fréquence à laquelle un   peut être proposé dans l’ensemble du jeu de  de (ciblés).

- Le plafond par  et détermine la fréquence à laquelle  peut être proposé au même.

### Contraintes de duplication

Lorsqu&#39;une décision est demandée, le client peut demander des propositions pour plusieurs   simultanément. Il s’agit d’un scénario typique de la prise de décision du contenu. Chaque  de  fournit une ou plusieurs options de contenu à l’expérience globale. En raison de l’aspect de la composition, les décisions doivent être arbitrées entre   pour éviter les doubles emplois - à moins que le du  ne choisisse un sous-ensemble disjoint de l’inventaire global des options. Une option de haut rang sera probablement au sommet de tous les   et ce serait une mauvaise expérience si tous les  proposaient la même option. D&#39;un autre côté, si un système de  veut savoir ce qu&#39;est la prochaine meilleure conversion pour tous les et qu&#39;il n&#39;y a pas de contrainte de plafonnement, il peut être correct de proposer la même option pour les différentsde la .

Les contraintes de duplication ne sont actuellement pas écrites dans le référentiel des objets métier. Au lieu de cela, la déduplication est la stratégie par défaut au moment de l’exécution. Un paramètre de requête peut remplacer le comportement par défaut pour supprimer l’étape de déduplication.

### Contraintes  - 

Jusqu&#39;à présent, les contraintes dont il a été question ont été applicables indépendamment de la personne pour laquelle la  de  est choisie. La prise de décision d’expérience prend également en charge un cas d’utilisation dans lequel les propositions de personnalisation reposent sur les  d’enregistrement et de séries chronologiques d’un client. Les règles sont évaluées par , afin de déterminer si un  est admissible ou doit être supprimé pour cet utilisateur. Pour ce faire, un  peut être associé à chaque  de. Outre le  et le d&#39;expérience d&#39;un utilisateur final, le prendra en compte les données contextuelles en temps réel. Ces données sont fournies par le service  et peuvent prendre la forme de données qui ne sont pas liées à un, comme les niveaux d&#39;inventaire, les conditions météorologiques, les horaires de vol.

Il est important de faire la distinction entre les règles de ciblage et de segmentation, et entre les règles d’éligibilité et les règles de priorité pour la prise de décision. Pour le ciblage d&#39;un ensemble de  est la sortie ( sélection de ) pour l&#39;éligibilité un ensemble d&#39;options (autorisé) est la sortie de l&#39;évaluation.

##  collections 

L&#39;inventaire est le groupe global d&#39;options qui sont prises en compte pour la prise de décision. L&#39;inventaire peut être divisé en  ou en collections. Une collection d’options est représentée par une balise commune que ces options possèdent. Les  de sont utilisées pour tester si  appartiennent à un certain, ou plus précisément, partagent la ou les mêmes balises.

### Balises

Les balises permettent d’exprimer qu’un groupe d’options appartient à un .

Une option peut comporter plusieurs balises et peut donc être simultanément dans plusieurs . Les  de peuvent également se chevaucher ou en contenir une autre. Lorsqu’un &quot;S&quot; est défini par  ayant la balise &quot;A&quot; et que le &quot;R&quot; est défini par des options avec les balises &quot;A&quot; et &quot;B&quot;, &quot;S&quot; devient un sur-ensemble de &quot;R&quot;.

### Filtres

Les  de sont utilisées pour définir les critères d’un ensemble d’options appartenant à un  de. On peut considérer les  comme des  de par rapport à l&#39;inventaire de l&#39;ensemble de l&#39;. Il existe deux méthodes de base pour former un filtre : en indiquant qu’un   a une ou plusieurs balises et en sélectionnant explicitement l’ensemble de  de  de données. L’ancienne méthode peut être configurée pour indiquer qu’un   dans cette collection doit avoir toutes les balises spécifiées ou qu’une option est admissible lorsqu’elle comporte au moins une des balises spécifiées.

Lorsque des options sont explicitement placées dans une collection, leur jeu de balises est ignoré pour cette collection.

##   

  configurer et contrôler le processus de prise de décision. Actuellement, la stratégie de décision est principalement prédéfinie, mais les futures itérations du modèle de domaine de décision   permettront la sélection de modèles, de règles et de contraintes supplémentaires.

Une expérience peut être assemblée à l’aide de nombreux   simultanément. Actuellement, jusqu’à 30   peuvent être traitées dans une seule demande de décision. Si plus de 30  ou emplacements  dans une expérience doivent être remplis avec du contenu, plusieurs demandes peuvent être effectuées pour le même . Toutefois, lorsque   sont inclus dans la même demande de décision, la déduplication des sera effectuée parmi ces.

Si   de sont définis d’une manière qu’ils choisissent parmi des ensembles de de  disjoints, cela fait peu de différence que lessoient combinés dans la même requête ou divisés en requêtes distinctes. Mais les contraintes de temps réseau et de temps de réponse peuvent nécessiter la combinaison de   dans la même requête. Comme différentes requêtes peuvent être acheminées vers différents noeuds de service, les mêmes données de  de peuvent devoir être récupérées dans différents noeuds. Cela réduit la bande passante E/S disponible pour les autres requêtes.

  sont utilisés pour insérer du contenu dans une expérience. Pour faciliter (et non pour s’assurer) que les éléments de contenu &quot;s’adaptent&quot; correctement, un   fait référence à un emplacement unique. Notez qu&#39;un emplacement n&#39;est pas toujours un emplacement/emplacement concret, mais plutôt une abstraction de ces emplacements/emplacements. Par exemple, dans une page Web avec une grille de mosaïques, chaque mosaïque peut être gouvernée par le même emplacement, en supposant qu’elle ait toutes la même forme et la même taille et qu’elle puisse contenir le même contenu. Cependant, une mosaïque individuelle est généralement fournie par son propre .

La figure suivante illustre la manière dont les entités commerciales sont liées les unes aux autres :

![](./images/figure-10.png)

Lorsque les clients créent et lient le graphique d’objets pour les décisions, il y a généralement trois flux de travail différents. Ces sont les suivants :

- Configuration des entités de prise en charge telles que les balises et les emplacements. Ces entités sont utilisées pour structurer, filtrer et regrouper d&#39;autres entités. Ils sont également utilisés pour assurer une certaine coordination entre le deuxième et le troisième flux de travaux. Ce flux de travail constitue un travail initial, mais à tout moment, des améliorations peuvent être apportées à la configuration. Bien que les balises soient relativement simples, les placements exigent une planification plus poussée. Au minimum, une entreprise doit dresser un inventaire de tous les lieux où une décision est présentée.

- Création de   avec les différentes représentations et règles de fonctionnement (contraintes). Ce flux de travail centralisé fournit les options parmi lesquelles nous devons sélectionner les meilleures. Les balises du premier flux de travail sont utilisées pour classer   et les emplacements sont utilisés pour indiquer les options qui peuvent être présentées et l’emplacement.

   - Ce flux de travail définit également des contraintes absolues pour le  . Ils sont absolus parce qu’ils seront toujours appliqués et n’affectent pas seulement le classement parmi un ensemble de  . Par exemple, lorsqu’une contrainte de calendrier est définie, il est appliqué que le  de  ne sera jamais sélectionné avant la date et l’heure de son et jamais après sa date et son heure de fin. Les contraintes qui seront définies dans ce flux de travail sont les contraintes [de](#calendar-constraints)calendrier, les contraintes [de](#capping-constraints) plafonnement et les contraintes [d’](#profile-constraints---eligibility-rules)éligibilité. Un sous-processus ici est la définition de règles supplémentaires qui déterminent qui peut recevoir un   donné.

      - Au même moment que des contraintes sont créées pour un  , ses représentations sont sélectionnées. Ce processus suppose que le contenu est déjà créé quelque part et qu’il est simplement téléchargé vers le référentiel de contenu et sélectionné à partir de celui-ci. C&#39;est ici que les emplacements du premier flux de travail entrent en jeu. Un  peut sélectionner des emplacements et associer le contenu sous ce [placement](#offer-placements).

      - La création d’un de secours  est la dernière étape de ce flux de travaux. Un de secours  est très proche d&#39;un de  général sans contraintes.

- Le dernier flux de travail concerne la création de   de. Toutefois, cette étape ne se produit pas nécessairement de manière séquentielle après le flux de travail pour créer  . Les deux processus sont en cours et simultanés.   sont utilisés pour restreindre la portée des options par sujet et par lieu de présentation des décisions. Un  fait référence à une [collection](#offer-collections) et à un emplacement. Il doit également spécifier un de [secours ](#fallback-offers) utilisé dans les cas où un de  admissible ne peut pas être déterminé.

