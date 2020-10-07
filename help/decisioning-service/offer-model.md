---
keywords: Experience Platform;home;popular topics;offer management;Offer Management
solution: Experience Platform
title: Modèle de domaine de prise de décision relative aux offres
topic: overview
description: La prise de décision relative aux offres est un cas d’utilisation du service de prise de décision dans lequel vous formalisez et gérez de manière centralisée les règles et les prédictions utilisées pour impliquer les clients vis-à-vis des offres.
translation-type: tm+mt
source-git-commit: a362b67cec1e760687abb0c22dc8c46f47e766b7
workflow-type: tm+mt
source-wordcount: '2640'
ht-degree: 96%

---


# Présentation du modèle de domaine de prise de décision relative aux offres

Offer decisioning is a use case of [!DNL Decisioning Service] within which you formalize and centrally manage the rules and predictions used for engaging customers with offers. La prise de décision relative aux offres est considérée comme un type de prise de décision relative au contenu. Dans ce cas d’utilisation, les options de décision sont appelées des offres, et sont caractérisées en tant que telles par le contenu qui y est associé. For an introduction of the object model used by the [!DNL Decisioning Service], please refer to [Decisioning Service Domain Model](experience-model.md).

L’objectif est de présenter à l’utilisateur final une « meilleure offre » sur n’importe quel canal en fonction de critères de ciblage, de contraintes de coût et de fréquence, ainsi que d’interactions préalables entre les canaux, y compris les offres antérieures proposées.

Comme pour tous les cas d’utilisation de la prise de décision, les options de décision (offres) sont gérées dans un référentiel partagé par n’importe quel nombre d’applications. Les offres peuvent être créées par différents services de votre organisation ou par des partenaires, et celles-ci peuvent être ajoutées et supprimées quotidiennement.

Les offres sont placées visuellement dans des expériences plus importantes par l’application qui les propose. Les emplacements, parfois appelés zones ou places, sont des éléments importants pour l’élaboration d’une stratégie. La conception d’une stratégie d’offre commence souvent par la définition de ces emplacements. Une offre a généralement de multiples représentations de contenu afin de pouvoir être correctement intégrée dans diverses expériences, où chacune présente des contraintes dimensionnelles ou autres et nécessite différents formats de médias.

Les offres sont souvent associées à des biens ou des services physiques et font l’objet d’un calcul de coût. Une organisation doit être capable de limiter les ressources utilisées par les offres et doit donc pouvoir plafonner le nombre total de fois où une offre peut être proposée.

La valeur prédite d’une offre acceptée pour l’organisation est le critère d’optimisation et s’oppose au coût de la présentation d’une offre. Le coût, la probabilité d’acceptation et la valeur prédite sont utilisés pour classer les offres. La meilleure offre est celle qui a le plus grand impact positif prédit sur les objectifs de vos activités d’offre.

La prise de décision relative aux offres tient compte des interactions qu’un utilisateur final a eues via de nombreux canaux et applications. Elle s’appuie sur le profil de l’utilisateur final et sur les données d’événement d’expérience. Par exemple, une application de centre d’appel peut utiliser la prise de décision relative aux offres pour activer ou supprimer une offre basée sur les achats effectués et les commentaires émis par l’utilisateur final ; ou une application de gestion des e-mails peut s’appuyer sur la prise de décision relative aux offres pour sélectionner la meilleure offre disponible dans une newsletter hebdomadaire en fonction de l’historique de navigation sur un site web.

Les offres ont d’autres propriétés intéressantes. Souvent, il existe un planning ou une plage de dates et d’heures définis lorsque l’offre est valide et au moment où elle doit être invalidée.

Enfin, l’attrait d’une offre se détériore proportionnellement à la fréquence de sa présentation. Une offre qui n’est pas acceptée après avoir été proposée à plusieurs reprises est une occasion manquée car une autre offre aurait pu être présentée. C’est pourquoi il faut gérer la fatigue de l’utilisateur final.

## Principales caractéristiques de la stratégie de décision relative aux offres

L’approche globale consiste à restreindre la sélection des offres jusqu’à ce que toutes les contraintes soient respectées, puis à appliquer le modèle de classement aux options restantes, et enfin à optimiser les activités multiples en utilisant les contraintes de limitation (déduplication et contournement des choix de secours).

| Composante de la stratégie | Réalisée à titre de |
| --- | --- |
| Activités de décision | Activités d’offre |
| Options de décision | Offre avec représentations de contenu |
| Options de secours | Offre de secours avec représentations de contenu |
| Ensemble fini d’options de décision | Inventaire des offres (aussi appelé bibliothèque des offres) |
| Catégories de thèmes | Filtre d’offres basé sur des balises et des identificateurs d’offres |
| Propositions de décision | Proposition d’une offre par activité, pour plusieurs activités à la fois |
| Résultats des décisions | Événement d’expérience attendu en référence à l’offre, par exemple `eventType='opened'` |
| Algorithme de décision | Logique de service interne, paramétrée |
| Contraintes | Contraintes d’emplacement, contraintes calendaires, contraintes de limitation globales et par utilisateur, contraintes de déduplication |
| Règles de décision | Règles d’éligibilité |
| Modèle pour l’*utilité attendue* | Classement ou priorité de l’offre |

Le nombre total d’offres dans l’inventaire des options est généralement assez important (de l’ordre de 10 000) et chaque activité d’offre peut porter sur des offres qui relèvent d’une catégorie (thème) différente. La stratégie de décision relative aux offres permet de joindre un filtre d’offre à une activité d’offre. Les contraintes supplémentaires seront évaluées au moment où la décision sera requise.
Les sections suivantes expliquent en détail les composantes du domaine de la prise de décision relative aux offres.

## Offres générales

Les offres générales, également appelées offres personnalisées, sont les options au centre des activités de décision relatives aux offres. Elles comportent des attributs comme le nom et l’état. L’attribut État indique si l’entité est prête à être incluse dans la liste des offres actives approuvées. Les offres générales sont soumises à plusieurs contraintes. Pour en savoir plus, consultez la section ‎Contraintes [ci-dessous](#offer-constraints).

## Contenu des offres

### Emplacements d’offre

Les emplacements définissent les contraintes de contenu et sont utilisés avec une activité pour spécifier où la meilleure expérience disponible est proposée. Cela réduit davantage le nombre d’options pouvant être envisagées, et constitue une contrainte supplémentaire imposée par l’activité. Cette contrainte s’intitule contrainte d’emplacement. Seules les options dont le contenu répond à une contrainte d’emplacement, telles que les offres, seront prises en considération. Cette évaluation est effectuée dans les premières étapes de la stratégie de décision. Lorsque les objets d’option changent, les contraintes d’emplacement de chaque activité sont réévaluées, et l’option peut être prise en considération ou non pour une ou plusieurs activités.

It is not the responsibility of the [!DNL Decisioning Service] to formalize the complex details of content dependencies. Au lieu de cela, chaque client identifiera la liste des emplacements sur tous les canaux et attribuera à ces emplacements des identifiants et des noms uniques. En référençant un emplacement particulier, le concepteur affirme que le contenu donné s’y intégrera.

Lorsque le contenu est développé, le spécialiste du marketing des offres et le concepteur du contenu (doivent se mettre) se mettent simplement d’accord sur un « contrat implicite » sous-jacent au nom « Bannière de la page d’accueil » ou « Scénario d’ouverture d’un appel de service ». Le premier peut se présenter sous la forme d’une image de 600 pixels de largeur et 350 pixels de hauteur et le second peut se limiter à un texte en deux variantes linguistiques qui ne dépasse pas 50 mots sur trois ou quatre phrases avec une structure sémantique. L’emplacement permet de ne pas retenir toute la signification du contrat caché.

### Représentations d’offre

Pour qu’une offre puisse être présentée correctement dans les différents paramètres des emplacements de vos canaux, il faut créer différentes représentations de cette offre. Les contenus associés aux offres sont regroupés par emplacement. Chaque offre peut avoir une ou plusieurs représentations, et chacune de ces représentations fait référence à l’un des emplacements définis. Chaque représentation dans une offre doit utiliser un emplacement différent. Plus une offre a de représentations, plus il est possible de l’utiliser dans différents contextes d’emplacement.

Un emplacement limite le type d’éléments de contenu pouvant être ajoutés à la représentation.

## Offres de secours

Les offres de secours sont des options de décision qui n’ont pas de contraintes supplémentaires, à l’exception des règles d’emplacement. Les offres de secours ont des représentations de contenu liées aux emplacements, tout comme n’importe quelle autre offre.

Les offres de secours sont spécifiées dans les activités pour indiquer une expérience de contenu viable à utiliser lorsque des contraintes combinées rendent caduques toutes les options restreintes. Ne dépendant pas du contexte d’exécution ni du profil, il est possible de vérifier à l’avance la contrainte d’emplacement lors de la mise en place de l’activité. Grâce aux offres de secours, il existe toujours une réponse à la question : quelle est actuellement la meilleure offre ?

## Contraintes d’offre

### Contraintes calendaires

Dans le domaine de la prise de décision relative aux offres, les offres ont une période de validité. Cela signifie que l’offre ne peut pas être proposée avant que sa date et son heure de début ne soient passées, et ne peut plus être proposée après que sa date et son heure de fin soient écoulées. L’entité de l’offre a une structure simple qui définit ces contraintes calendaires.

Régulièrement, les offres expirées sont retirées de la liste des options envisagées. Cependant, le filtre calendaire est appliqué au moment même où la décision est requise afin que les contraintes soient appliquées avec précision.

### Contraintes de limitation

Les offres peuvent avoir une contrainte de limitation facultative. Elle se compose de deux valeurs :

- La valeur de la limite globale restreint la fréquence à laquelle une offre peut être proposée sur l’ensemble du profil (audience ciblée).

- La limite par profil détermine la fréquence à laquelle cette offre peut être proposée au même profil.

### Contraintes de duplication

Lorsqu’une décision est requise, le client peut demander des propositions pour plusieurs activités à la fois. C’est un scénario typique de la prise de décision en matière de contenu. Chaque activité apporte une ou plusieurs options de contenu à l’expérience globale. En raison de l’aspect de la composition, les décisions doivent être arbitrées entre les activités pour éviter la duplication, à moins que celles-ci ne choisissent chacune un sous-ensemble disjoint de l’inventaire global des options. Une option de haut rang est susceptible de se retrouver en haut de la liste de toutes les activités. Si toutes les activités proposaient la même option, l’expérience serait médiocre. D’autre part, si un système de diffusion souhaite savoir quelle est la meilleure conversion disponible sur tous les canaux et qu’il n’y a pas de contrainte de limitation, il est possible de proposer la même option pour différentes activités.

Les contraintes de duplication ne sont actuellement pas écrites dans le référentiel d’objets métier. En revanche, la déduplication est la stratégie par défaut au moment de l’exécution. Un paramètre de requête peut remplacer le comportement par défaut pour supprimer l’étape de déduplication.

### [!DNL Profile] contraintes - Règles d&#39;éligibilité

Jusqu’à présent, les contraintes évoquées ont été applicables quelle que soit la personne pour laquelle l’offre est sélectionnée. La prise de décision d’expérience prend également en charge un cas d’utilisation dans lequel les propositions de personnalisation reposent sur les événements d’enregistrement et de série temporelle d’un client. Les règles sont évaluées par profil, afin de décider si une offre est admissible ou doit être supprimée pour cet utilisateur. Pour ce faire, une règle d’éligibilité peut être associée à chaque offre. Outre les événements liés au profil et à l’expérience d’un utilisateur final, la règle d’éligibilité tiendra compte des données contextuelles en temps réel. Ces données sont fournies par le service de diffusion et peuvent prendre la forme de données non liées à un profil, comme les niveaux d’inventaire, les conditions météorologiques, et les horaires de vol.

Il est important de faire la distinction entre les règles de ciblage et de segmentation, et entre les règles d’éligibilité et de priorité pour la prise de décision. Pour le ciblage, un ensemble de profils est le résultat (sélection de l’audience). Pour l’éligibilité, un ensemble d’options (offres autorisées) est le résultat de l’évaluation.

## Collections d’offres

L’inventaire est l’ensemble des options envisagées pour la prise de décision. L’inventaire peut être subdivisé en catégories ou en collections. Une collection d’options est représentée par une balise commune attribuée à ces options. Les filtres sont utilisés pour vérifier si les offres appartiennent à une certaine catégorie ou, plus précisément, si elles partagent la ou les mêmes balises.

### Balises

Les balises permettent d’indiquer qu’un groupe d’options appartient à une catégorie.

Une option peut comporter plusieurs balises et, par conséquent, se trouver simultanément dans plusieurs catégories. Les catégories peuvent également se chevaucher ou en contenir une autre. Lorsqu’une catégorie « S » est définie par des offres ayant la balise « A » et que la catégorie « R » est définie par des options ayant à la fois les balises « A » et « B », alors « S » devient un sur-ensemble de « R ».

### Filtres

Les filtres sont utilisés pour définir les critères d’un ensemble d’options appartenant à une catégorie. Les filtres peuvent être considérés comme des requêtes par rapport à l’inventaire des offres générales. Il existe deux méthodes de base pour former un filtre : en indiquant qu’une offre possède une ou plusieurs balises et en sélectionnant explicitement l’ensemble des offres. La première méthode peut être configurée pour indiquer qu’une offre dans cette collection doit avoir toutes les balises spécifiées ou qu’une option est admissible lorsqu’elle comporte au moins une des balises spécifiées.

Lorsque des options sont explicitement placées dans une collection, leur jeu de balises est ignoré pour cette collection.

## Activités d’offre

Les activités configurent et contrôlent le processus de prise de décision. Actuellement, la stratégie de décision est principalement prédéterminée, mais de futures itérations du modèle de domaine de prise de décision relative aux offres permettront de sélectionner des modèles, des règles et des contraintes supplémentaires.

Une expérience peut être constituée en utilisant plusieurs activités simultanément. Actuellement, il est possible de traiter jusqu’à 30 activités dans une seule requête de prise de décision. Si plus de 30 activités ou places dans une expérience doivent être complétées par du contenu, plusieurs requêtes peuvent être effectuées pour le même profil. Toutefois, lorsque des activités sont incluses dans une même requête de décision, la déduplication des propositions d’offre est effectuée parmi ces activités.

Si les activités sont définies de manière à être sélectionnées parmi des ensembles d’offres disjoints, alors cela importe peu que les activités soient combinées dans une même requête ou séparées dans des requêtes distinctes. Cependant, les contraintes liées au réseau et au temps de réponse peuvent nécessiter le regroupement des activités dans une même requête. Comme différentes requêtes peuvent être acheminées vers différents nœuds de service, il est possible que les mêmes données de profil doivent être récupérées dans différents nœuds. Cela réduit la bande passante effective des E/S disponible pour les autres requêtes.

Les activités sont utilisées pour ajouter du contenu à une expérience. Pour faciliter (et non garantir) la bonne « adéquation » des éléments de contenu, une activité fait référence à un seul emplacement. Notez qu’un emplacement n’est pas toujours un endroit/une place concrète, mais plutôt une abstraction de ces endroits/places. Par exemple, dans une page web avec une grille de mosaïques, chaque mosaïque pourrait être régie par le même emplacement, à condition qu’elles aient toutes une forme et une taille similaires et qu’elles puissent contenir un même contenu. Toutefois, une mosaïque individuelle est généralement fournie par sa propre activité.

La figure ci-dessous illustre les relations entre les entités commerciales :

![](./images/figure-10.png)

Généralement, lorsque les clients créent et relient le graphique d’objets pour les décisions, trois axes de travail différents se distinguent. En voici la liste :

- Mise en place des entités de prise en charge telles que les balises et les emplacements. Ces entités sont utilisées pour structurer, filtrer et regrouper d’autres entités. Elles assurent également une certaine coordination entre le deuxième et le troisième workflow. Ce workflow constitue un travail préparatoire, mais à tout moment, des améliorations peuvent être apportées à la mise en place. Bien que les balises soient relativement simples, les emplacements nécessitent une planification plus poussée. Une entreprise doit au minimum dresser un inventaire de tous les emplacements où une décision est présentée.

- Création d’offres avec les différentes représentations et règles commerciales (contraintes). Ce workflow central fournit les options parmi lesquelles il nous faut sélectionner les meilleures. Les balises du premier workflow sont utilisées pour classer les offres et les emplacements permettent d’indiquer quelles options peuvent être présentées, et où.

   - Ce workflow définit également des contraintes absolues pour les offres. Elles sont absolues car elles seront toujours appliquées et n’affectent pas seulement le classement parmi un ensemble d’offres. Par exemple, lorsqu’une contrainte calendaire est définie, l’offre n’est jamais sélectionnée avant sa date/heure de début et après sa date/heure de fin. Les contraintes qui seront définies dans ce workflow sont les [contraintes calendaires](#calendar-constraints), les [contraintes de limitation](#capping-constraints) et les [contraintes d’éligibilité](#profile-constraints---eligibility-rules). Un workflow secondaire est ici la définition de règles supplémentaires déterminant qui est éligible pour recevoir une offre donnée.

      - Pendant que des contraintes sont créées pour une offre, ses représentations sont sélectionnées. Ce workflow suppose que le contenu est déjà créé quelque part et qu’il est simplement chargé et sélectionné dans le référentiel de contenu. C’est là que les emplacements du premier workflow entrent en jeu. Une offre peut sélectionner des emplacements et associer le contenu à cet [emplacement](#offer-placements).

      - La création d’offres de secours adaptées est la dernière étape de ce workflow. Une offre de secours ressemble beaucoup à une offre générale sans contraintes.

- Le dernier workflow concerne la création d’activités. Toutefois, cette étape ne se déroule pas nécessairement de manière séquentielle après le workflow de création des offres. Les deux processus sont en cours et simultanés. Les activités sont utilisées pour réduire la portée des options par thème et par emplacement de présentation des décisions. Une activité fait référence à une [collection](#offer-collections) et à un emplacement. Elle doit également spécifier une [offre de secours](#fallback-offers) à utiliser dans les cas où une offre admissible ne peut être déterminée.

