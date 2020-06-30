---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Modèle de domaine de prise de décision d’Offre
topic: overview
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '2614'
ht-degree: 0%

---


# Offre Prise de décision Présentation du modèle de domaine

La prise de décision par Offre est un exemple d’utilisation dans lequel vous pouvez formaliser et gérer de manière centralisée les règles et prédictions utilisées pour attirer les clients avec des offres. [!DNL Decisioning Service] La décision d’Offre est considérée comme un type de décision _**de**_ contenu. Dans ce cas d&#39;utilisation, les options _**de**_ décision sont appelées _**offres**_ et se caractérisent par le contenu qui leur est joint. Pour une présentation du modèle d&#39;objet utilisé par le [!DNL Decisioning Service]service, veuillez vous reporter au modèle [de domaine du service de](experience-model.md)prise de décision.

L&#39;objectif est de présenter à l&#39;utilisateur final une &quot;meilleure Offre&quot; dans n&#39;importe quel canal en fonction des critères de ciblage, des contraintes de coût et de fréquence, ainsi que des interactions préalables entre canaux, y compris les Offres antérieures proposées.

Comme pour tous les cas d’utilisation de la prise de décision, les options de décision (offres) sont gérées dans un rapport partagé par n’importe quel nombre d’applications. Les Offres peuvent être créées par différents services de votre organisation ou par des partenaires, et ces offres peuvent être ajoutées et supprimées quotidiennement.

Les Offres sont visuellement placées dans des expériences plus vastes par l’application qui les diffuse. _**Les emplacements**_, parfois appelés emplacements ou emplacements, sont des composants importants pour l&#39;élaboration d&#39;une stratégie. La conception d&#39;une stratégie d&#39;offre début souvent avec la définition de ces placements. En règle générale, une offre comporte plusieurs représentations _**de**_ contenu afin de pouvoir être correctement intégrée dans une variété d’expériences, où chacune présente des contraintes dimensionnelles ou autres et requiert différents formats de médias.

Les Offres ont souvent une association avec des biens ou des services physiques et il y a un calcul des coûts. Une organisation doit être en mesure de limiter les ressources consommées par les offres et doit donc être en mesure de _**plafonner**_ le nombre total de fois où une offre peut être proposée.

La valeur prévue d&#39;une offre acceptée pour l&#39;organisation est le critère d&#39;optimisation et va à l&#39;encontre du coût de réalisation d&#39;une offre. Le coût, la probabilité d&#39;acceptation et la valeur prévue sont utilisés pour classer les offres. La Meilleure Offre est celle qui a le plus d&#39;impact positif prédit sur les objectifs de vos activités offres.

La prise de décision des Offres prend en compte les interactions qu’un utilisateur final a eu, _**dans de nombreux canaux**_ et applications, pour exploiter les données de événement d’profil et d’expérience d’un utilisateur final. Par exemple, une application de centre d’appels peut utiliser la prise de décision des Offres pour activer ou supprimer une offre en fonction des achats effectués et des révisions publiées par l’utilisateur final ; ou une application de gestion du courrier électronique peut s’appuyer sur la prise de décision des Offres pour sélectionner la prochaine meilleure Offre dans un bulletin d’information hebdomadaire en fonction de l’historique de navigation d’un site Web.

Les Offres ont d&#39;autres propriétés intéressantes. Il existe souvent un _**calendrier**_ ou une plage de dates et d&#39;heures défini lorsque l&#39;offre est valide et selon le moment où l&#39;offre doit être invalidée.

Enfin, l&#39;appel d&#39;une offre se détériore avec la fréquence à laquelle elle est présentée. Une Offre qui n&#39;est pas acceptée après avoir été proposée à plusieurs reprises est une occasion perdue parce qu&#39;une autre offre aurait pu être présentée. C&#39;est pourquoi il faut gérer la _**fatigue**_ des utilisateurs finaux.

## Offre Stratégie décisionnelle en un coup d&#39;oeil

L’approche globale consiste à restreindre la sélection des Offres jusqu’à ce que toutes les contraintes soient satisfaites, puis à appliquer le modèle de classement aux options restantes, puis à optimiser les  sur plusieurs activités à l’aide de contraintes de plafonnement (déduplication et évitement des choix de reprise).

| Composant de la stratégie | Réalisé comme |
| --- | --- |
| activités de décision | activités Offres |
| Options de décision | Offre avec les représentations de contenu |
| Options de secours | offre de secours avec représentations de contenu |
| Ensemble fini d&#39;options de décision | Inventaire des Offres (bibliothèque d&#39;offres, par exemple) |
| catégories thématiques | Filtre d’Offre basé sur les balises et les identifiants d’offre |
| Résultats de la décision | Proposition d&#39;une offre par activité, pour plusieurs activités à la fois |
| Résultats de la décision | événement d’expérience prévu par rapport à l’offre, p. ex. `eventType='opened'` |
| Algorithme de décision | Logique de service interne, paramétré |
| Contraintes | Contraintes de positionnement, contraintes de calendrier, contraintes de plafonnement globales et par utilisateur, contraintes de déduplication |
| Règles de décision | Règles d’éligibilité |
| Modèle pour l&#39;utilitaire *attendu* | Ordre de classement ou de priorité des Offres |

Le nombre total d&#39;offres dans l&#39;inventaire des options est généralement assez important (de l&#39;ordre de 10 000) et chaque activité d&#39;offre peut être axée sur les offres qui tombent dans une catégorie différente (sujet). La stratégie de décision d&#39;offre permet d&#39;associer un filtre d&#39;offre à une activité d&#39;offre. D&#39;autres contraintes seront évaluées au moment où la décision sera demandée.
Les sections suivantes décrivent en détail les composants du domaine de prise de décision des Offres.

## offres générales

Les offres générales, également appelées offres personnalisées, sont les options au centre des activités décisionnelles des offres. Ils ont des attributs tels que le nom et l’état. L&#39;attribut status indique si l&#39;entité est prête à être incluse dans la liste des offres approuvées actives. Plusieurs contraintes s&#39;ajouteront aux offres générales. Pour plus d&#39;informations à ce sujet, consultez la section Contraintes ‎ [ci-dessous](#offer-constraints).

## Contenu dans les Offres

### Positionnement des Offres

Les emplacements définissent les contraintes de contenu et sont utilisés avec une activité pour spécifier l’emplacement dans lequel la meilleure expérience suivante est livrée. Cela réduit davantage le nombre d&#39;options qui peuvent être envisagées et constitue une autre contrainte imposée par l&#39;activité. Il s&#39;agit de la contrainte de placement. Seules les options dont le contenu répond à une contrainte de placement, telles que les offres, seront prises en compte. Cette évaluation est effectuée dans les premières étapes de la stratégie de décision. Lorsque les objets d’option modifient les contraintes de placement de chaque activité sont réévalués et l’option peut être prise en compte ou en ressortir pour une ou plusieurs activités.

Il n&#39;est pas de la responsabilité du [!DNL Decisioning Service] gouvernement de formaliser les détails complexes des dépendances de contenu. Au lieu de cela, chaque client identifie la liste des placements sur tous les canaux et leur donne des identifiants et des noms uniques. En référençant un emplacement particulier, le concepteur affirme que le contenu donné s’adaptera à l’emplacement.

Lorsque le contenu est développé, le spécialiste du marketing d’offre et le concepteur de contenu s’entendent simplement (doivent) sur un &quot;contrat implicite&quot; qui se trouve derrière le nom &quot;Page d&#39;accueil Hero Image&quot; ou &quot;Script d’ouverture d’appel de service&quot;. Le premier peut être convenu comme une image de 600 px de largeur et de 350 px de hauteur et le second peut restreindre le contenu au texte dans deux variantes de langue qui n&#39;est pas plus de 50 mots en trois ou quatre phrases avec une structure sémantique. Placement pour ne pas stocker tout le sens du contrat caché.

### Rendus de l&#39;offre

Pour s&#39;assurer qu&#39;une offre peut être présentée correctement dans les différents paramètres des emplacements de vos canaux, différentes représentations de cette offre doivent être créées. Le contenu joint aux offres est regroupé par emplacements. Chaque offre peut avoir une ou plusieurs représentations dans lesquelles chacune de ces représentations fait référence à l&#39;un des emplacements définis. Chaque représentation dans une offre doit utiliser un emplacement différent. Plus une offre a de représentations, plus elle a de chances d&#39;utiliser l&#39;offre dans différents contextes de placement.

Un emplacement limite le type d’éléments de contenu qui peuvent être ajoutés à la représentation.

## offres de secours

Les offres de secours sont des options de décision qui ne comportent pas de contraintes supplémentaires, à l’exception des règles d’emplacements. Les offres de secours comportent des représentations de contenu liées à des emplacements, comme toute autre offre.

Les offres de secours sont spécifiées dans les activités pour indiquer une expérience de contenu viable à utiliser lorsque les contraintes combinées excluent toutes les options réduites. Etant donné qu’elle ne dépend pas du contexte d’exécution ou du profil, la contrainte de placement peut être vérifiée à l’avance lorsque l’activité est assemblée. Les offres de secours permettent toujours de répondre à la question suivante : Quelle est actuellement la meilleure offre ?

## Contraintes d&#39;Offre

### Contraintes de calendrier

Dans le domaine de la décision d’offre, les offres ont une période de validité. Cela signifie que l&#39;offre ne peut pas être proposée avant que sa date et son heure de début ne soient dépassées et ne peut plus être proposée après que sa date et son heure de fin sont dépassées. L&#39;entité offre a une structure simple qui définit ces contraintes de calendrier.

Régulièrement, les Offres expirées seront retirées de la liste des options considérées. Mais le filtre de calendrier est appliqué correctement au moment où la décision est demandée, de sorte que les contraintes soient appliquées avec précision.

### Contraintes de plafonnement

Les Offres peuvent avoir une contrainte de plafonnement facultative. Il se compose de deux valeurs :

- La valeur de plafond globale limite la fréquence à laquelle une offre peut être proposée dans l’ensemble du jeu de profils (audience ciblée).

- Le plafond par profil et détermine la fréquence à laquelle cette Offre peut être proposée au même profil.

### Contraintes de duplication

Lorsqu&#39;une décision est demandée, le client peut demander des propositions pour plusieurs activités à la fois. Il s’agit d’un scénario typique de la prise de décision du contenu. Chaque activité fournit une ou plusieurs options de contenu à l’expérience globale. En raison de l&#39;aspect de la composition, les décisions doivent être arbitrées entre les activités pour éviter les doubles emplois - à moins que les activités ne choisissent chacune un sous-ensemble disjoint de l&#39;inventaire global des options. Une option de haut rang est susceptible de se situer au sommet de toutes les activités et ce serait une mauvaise expérience si toutes les activités proposaient la même option. D&#39;un autre côté, si un système de diffusion veut savoir ce qu&#39;est la prochaine meilleure conversion sur tous les canaux et qu&#39;il n&#39;y a pas de contrainte de plafonnement, il peut être correct de proposer la même option sur différentes activités.

Les contraintes de duplication ne sont actuellement pas écrites dans le référentiel des objets métier. Au lieu de cela, la déduplication est la stratégie par défaut au moment de l’exécution. Un paramètre de requête peut remplacer le comportement par défaut pour supprimer l’étape de déduplication.

### [!DNL Profile] contraintes - Règles d&#39;éligibilité

Jusqu&#39;à présent, les contraintes dont il a été question ont été applicables indépendamment de la personne pour laquelle l&#39;offre a été choisie. La prise de décision d’expérience prend également en charge un cas d’utilisation dans lequel les propositions de personnalisation sont basées sur les événements d’enregistrement et de séries chronologiques d’un client. Les règles sont évaluées par profil, afin de déterminer si une offre est admissible ou doit être supprimée pour cet utilisateur. Pour ce faire, une règle d&#39;éligibilité peut être associée à chaque offre. Outre les événements d’profil et d’expérience d’un utilisateur final, la règle d&#39;éligibilité tiendra compte des données contextuelles en temps réel. Ces données sont fournies par le service de diffusion et peuvent prendre la forme de données qui ne sont pas liées à un profil, comme les niveaux d&#39;inventaire, les conditions météorologiques, les horaires de vol.

Il est important de faire la distinction entre les règles de ciblage et de segmentation, ainsi qu’entre les règles d’éligibilité et les règles de priorité pour la prise de décision. Pour le ciblage d’un ensemble de profils est la sortie (sélection d’audiences) pour l’éligibilité un ensemble d’options (offres autorisées) est le résultat de l’évaluation.

## Collections d’Offres

L&#39;inventaire est le groupe global d&#39;options qui sont prises en compte pour la prise de décision. L&#39;inventaire peut être divisé en catégories ou en collections. Un ensemble d’options est représenté par une balise commune que ces options possèdent. Les Filtres sont utilisés pour tester si les offres appartiennent à une certaine catégorie ou, plus précisément, partagent la ou les mêmes balises.

### Balises

Les balises permettent d’exprimer qu’un groupe d’options appartient à une catégorie.

Une option peut comporter plusieurs balises et peut donc se trouver simultanément dans plusieurs catégories. Les Catégories peuvent également se chevaucher ou en contenir une autre. Lorsqu’une catégorie &quot;S&quot; est définie par des offres ayant la balise &quot;A&quot; et que la catégorie &quot;R&quot; est définie par des options avec les balises &quot;A&quot; et &quot;B&quot;, &quot;S&quot; est alors un ensemble superset de &quot;R&quot;.

### Filtres

Les Filtres sont utilisés pour définir les critères d’un ensemble d’options appartenant à une catégorie. Les Filtres peuvent être considérés comme des requêtes par rapport à l&#39;inventaire des offres générales. Il existe deux méthodes de base pour former un filtre : en indiquant qu’une offre comporte une ou plusieurs balises et en sélectionnant explicitement l’ensemble d’offres. L’ancienne méthode peut être configurée pour indiquer qu’une offre de cette collection doit comporter toutes les balises spécifiées ou qu’une option est admissible lorsqu’elle comporte au moins une des balises spécifiées.

Lorsque des options sont explicitement placées dans une collection, leur jeu de balises est ignoré pour cette collection.

## Activités Offres

Les Activités configurent et contrôlent le processus de prise de décision. Actuellement, la stratégie de décision est principalement prédéfinie mais les futures itérations du modèle de domaine de prise de décision des Offres permettront la sélection de modèles, de règles supplémentaires et de contraintes.

Une expérience peut être assemblée à l’aide de nombreuses activités simultanément. Actuellement, jusqu’à 30 activités peuvent être traitées dans une seule demande de décision. Si plus de 30 activités ou emplacements d’une expérience doivent être remplis avec du contenu, plusieurs requêtes peuvent être effectuées pour le même profil. Toutefois, lorsque des activités sont incluses dans la même demande de décision, la déduplication des Propositions d&#39;offre sera effectuée entre ces activités.

Si les activités sont définies d&#39;une manière qu&#39;elles choisissent parmi des ensembles d&#39;offres disjoints, il n&#39;y a pas de différence entre les activités combinées dans la même requête ou fractionnées en requêtes distinctes. Mais les contraintes de temps de réseau et de réponse peuvent exiger la combinaison d&#39;activités dans la même demande. Comme différentes requêtes peuvent être acheminées vers différents noeuds de service, les mêmes données de profil peuvent devoir être extraites vers différents noeuds. Cela réduit la bande passante d&#39;E/S disponible pour les autres requêtes.

Les Activités sont utilisées pour insérer du contenu dans une expérience. Pour faciliter (et non pour s’assurer) que les éléments de contenu &quot;s’adaptent&quot; correctement, une activité fait référence à un emplacement unique. Notez qu&#39;un emplacement n&#39;est pas toujours un emplacement/emplacement concret mais plutôt une abstraction de ces emplacements/emplacements. Par exemple, dans une page Web avec une grille de mosaïques, chaque mosaïque peut être régie par le même emplacement, en supposant qu’elle ait toutes la même forme et la même taille et qu’elle puisse contenir le même contenu. Cependant, une mosaïque individuelle est généralement fournie par sa propre activité.

La figure suivante illustre comment les entités commerciales sont liées les unes aux autres :

![](./images/figure-10.png)

Lorsque les clients créent et lient le graphique d’objets pour les décisions, il y a généralement trois flux de travail différents. Ces sont les suivants :

- Configuration des entités de prise en charge telles que les balises et les emplacements. Ces entités sont utilisées pour structurer, filtrer et regrouper d&#39;autres entités. Ils servent également à assurer une certaine coordination entre le deuxième et le troisième processus. Ce flux de travail constitue un travail préalable mais à tout moment des améliorations peuvent être apportées à la configuration. Bien que les balises soient relativement simples, les placements nécessitent une planification un peu plus poussée. Au minimum, une entreprise doit dresser un inventaire de tous les lieux où une décision est présentée.

- Création d’offres avec les différentes représentations et règles de fonctionnement (contraintes). Ce flux de travail centralisé fournit les options parmi lesquelles nous devons sélectionner les meilleures. Les balises du premier flux de travail sont utilisées pour classer les offres et les emplacements sont utilisés pour indiquer les options qui peuvent être présentées et où.

   - Ce processus définit également les contraintes absolues pour les offres. Ils sont absolus parce qu’ils seront toujours appliqués et n’affectent pas seulement le classement d’un ensemble d’offres. Par exemple, lorsqu&#39;une contrainte de calendrier est définie, l&#39;offre ne sera jamais sélectionnée avant la date et l&#39;heure de début définies et jamais après la date et l&#39;heure de fin. Les contraintes qui seront définies dans ce flux de travail sont les contraintes [de](#calendar-constraints)calendrier, les contraintes [de](#capping-constraints) plafonnement et les contraintes [d&#39;](#profile-constraints---eligibility-rules)éligibilité. Un sous-processus est ici la définition de règles supplémentaires qui déterminent qui peut recevoir une offre donnée.

      - En même temps que des contraintes sont créées pour une offre, ses représentations sont sélectionnées. Ce processus suppose que le contenu est déjà créé quelque part et qu’il est simplement téléchargé vers le référentiel de contenu et sélectionné à partir de celui-ci. C&#39;est ici que les emplacements du premier flux de travail entrent en jeu. Une offre peut sélectionner des emplacements et associer le contenu sous cet [emplacement](#offer-placements).

      - La création d&#39;offres de secours appropriées est la dernière étape de ce flux de travaux. Une offre de secours ressemble beaucoup à une offre générale sans contraintes.

- Le dernier flux de travail concerne la création d’activités. Cependant, cette étape ne se produit pas nécessairement de manière séquentielle après le flux de travail pour créer des offres. Les deux processus sont en cours et simultanés. Les Activités sont utilisées pour restreindre la portée des options par sujet et par lieu de présentation des décisions. Une activité fait référence à une [collection](#offer-collections) et à un emplacement. Elle doit également spécifier une offre [de](#fallback-offers) secours utilisée dans les cas où une offre admissible ne peut pas être déterminée.

