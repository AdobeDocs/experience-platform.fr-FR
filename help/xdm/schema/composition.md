---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Principes de base de la composition '
topic: overview
translation-type: tm+mt
source-git-commit: d0ccaa5511375253a2eca8f1235c2f953b734709

---


# Principes de base de la composition 

Ce présente le du modèle de données d’expérience (XDM) ainsi que les blocs de création, les principes et les bonnes pratiques pour la composition dela plate-forme de données d’expérience à utiliser dans Adobe Experience Platform. Pour plus d’informations sur XDM et son utilisation dans Platform, voir la présentation [du système](../home.md)XDM.

## Compréhension des 

Un est un ensemble de règles qui représentent et valident la structure et le format des données. A un niveau élevé, les  de fournissent une définition abstraite d’un objet du monde réel (une personne, par exemple) et indiquent les données à inclure dans chaque instance de cet objet (prénom, nom, anniversaire, etc.).

Outre la description de la structure des données, les  appliquent des contraintes et des attentes aux données afin qu’elles puissent être validées lorsqu’elles se déplacent d’un système à l’autre. Ces définitions standard permettent d’interpréter les données de manière cohérente, quel que soit le  , et éliminent la nécessité d’une traduction entre les applications.

Experience Platform maintient cette normalisation sémantique grâce à l’utilisation de . Les  de sont la manière standard de décrire les données dans la plateforme d’expérience, permettant à toutes les données conformes au d’être réutilisables sans conflit au sein d’une organisation et même d’être partagées entre plusieurs organisations.

### Tableaux relationnels par rapport aux objets incorporés

Lorsque vous travaillez avec des bases de données relationnelles, les meilleures pratiques consistent à normaliser les données ou à prendre une entité et à la diviser en éléments distincts qui sont ensuite affichés sur plusieurs tableaux. Afin de lire l&#39;ensemble des données ou de mettre à jour l&#39;entité, des opérations de lecture et d&#39;écriture doivent être effectuées sur de nombreux tableaux individuels à l&#39;aide de JOIN.

Grâce aux objets incorporés, les  XDM peuvent représenter directement des données complexes et les stocker dans des  autonomes avec une structure hiérarchique. L&#39;un des principaux avantages de cette structure est qu&#39;elle vous permet de  les données sans avoir à reconstruire l&#39;entité par des jointures coûteuses à plusieurs tableaux dénormalisés.

###  et Big Data

Les systèmes numériques modernes génèrent une grande quantité de signaux comportementaux (données de transaction, journaux Web, Internet des choses, affichage, etc.). Ces données volumineuses  des opportunités hors du commun d’optimiser les expériences, mais sont difficiles à utiliser en raison de l’échelle et de la variété des données. Pour tirer parti des données, il faut normaliser leur structure, leur format et leurs définitions afin qu&#39;elles puissent être traitées de manière cohérente et efficace.

Les  résoudre ce problème en permettant l&#39;intégration des données à partir de sources multiples, l&#39;uniformisation au moyen de structures et de définitions communes et le partage entre les solutions. Cela permet aux processus et aux services suivants de répondre à tout type de question posée sur les données, en s’éloignant de l’approche traditionnelle de la modélisation des données où toutes les questions qui seront posées sur les données sont connues à l’avance et les données sont modélisées pour être conformes à ces attentes.

### basé sur  dans la plateforme d’expérience

La normalisation est un concept clé derrière la plateforme d’expérience. XDM, piloté par Adobe, vise à normaliser les données d’expérience client et à définir des  standard pour la gestion de l’expérience client.

L’infrastructure sur laquelle est construite la plateforme d’expérience, connue sous le nom de système XDM, facilite les  de basées sur les et inclut le registre de l’, l’éditeur derapports, les métadonnées de l’et les modèles de consommation de service. See the [XDM System overview](../home.md) for more information.

## Planification de votre 

La première étape dans la construction d&#39;un  est de déterminer le concept, ou objet du monde réel, que vous essayez de capturer dans le . Une fois que vous avez identifié le concept que vous essayez de décrire, vous pouvez commencer à planifier votre  en pensant à des choses comme le type de données, les champs d&#39;identité potentiels et la façon dont le  de pourrait évoluer dans le futur.

### Comportements de données dans la plateforme d’expérience

Les données destinées à être utilisées dans la plate-forme d’expérience sont regroupées en deux types de comportement :

* **Enregistrer les données**: Fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **Données** de la série chronologique : Fournit un instantané du système au moment où une action a été effectuée directement ou indirectement par un sujet d&#39;enregistrement.

Tous les XDM décrivent des données pouvant être classées comme enregistrements ou séries chronologiques. Le comportement des données d’un  de est défini par la **classe** de  de, qui est affectée à un  lors de sa création. Les classes XDM sont décrites plus loin dans cette .

Les d&#39;enregistrements et de séries chronologiques  contiennent tous deux une carte des identités (`xdm:identityMap`). Ce champ contient la représentation de l’identité d’un sujet, à partir de champs marqués comme &quot;Identité&quot;, comme décrit dans la section suivante.

### Identité

Les  sont utilisées pour l’assimilation de données dans Experience Platform. Ces données peuvent être utilisées sur plusieurs services pour créer un unique et unifié d’une entité individuelle. Par conséquent, il est important, lorsque vous pensez aux, de penser à &quot;l&#39;identité&quot; et aux champs qui peuvent être utilisés pour identifier un sujet, quel que soit l&#39;endroit d&#39;où proviennent les données.

Pour faciliter ce processus, les champs clés peuvent être marqués comme &quot;Identité&quot;. Lors de l’assimilation des données, les données contenues dans ces champs seront insérées dans le &quot;graphique d’identité&quot; de cette personne. Les données du graphique peuvent ensuite être accessibles par l’utilisateur en temps [réel](../../profile/home.md) et d’autres services Experience Platform pour fournir un assemblé de chaque client.

Les champs généralement identifiés comme &quot;Identité&quot; sont les suivants : adresse électronique, numéro de téléphone, ID [Experience Cloud (ECID)](https://marketing.adobe.com/resources/help/en_US/mcvid/), ID CRM ou autres champs d’ID uniques. Vous devez également tenir compte de tous les identifiants uniques propres à votre organisation, car ils peuvent également être de bons champs &quot;Identité&quot;.

Il est important de réfléchir aux identités des clients pendant la phase de planification  des afin de s&#39;assurer que les données sont rassemblées pour créer le le plus robuste possible. Consultez la présentation [du service](../../identity-service/home.md) d’identité pour en savoir plus sur la manière dont les informations d’identité peuvent vous aider à fournir des expériences numériques à vos clients.

### Principes d&#39;évolution {#evolution}

Comme la nature des expériences numériques continue d’évoluer, les doivent également les représenter. Un bien conçu est donc en mesure de s&#39;adapter et d&#39;évoluer au besoin, sans provoquer de changements destructeurs aux versions précédentes du  de la.

Comme le maintien de la compatibilité ascendante est essentiel pour l’évolution des , la plateforme d’expérience applique un principe de gestion des versions purement additive afin de garantir que toute révision du  n’entraîne que des mises à jour et des modifications non destructives. En d’autres termes, les modifications **de rupture ne sont pas prises en charge.**

| Modifications prises en charge | Changements de rupture (non pris en charge) |
|------------------------------------|---------------------------------|
| <ul><li>Ajout de nouveaux champs à un existant </li><li>Rendre un champ obligatoire facultatif</li></ul> | <ul><li>Suppression de champs précédemment définis</li><li>Présentation de nouveaux champs obligatoires</li><li>Modification du nom ou de la définition de champs existants</li><li>Suppression ou restriction de valeurs de champ précédemment prises en charge</li><li>Déplacement d’attributs vers un autre emplacement de l’arborescence</li></ul> |

>[!NOTE] Si un  n’a pas encore été utilisé pour assimiler des données dans la plateforme d’expérience, vous pouvez introduire une modification de dernière minute dans ce  de. Cependant, une fois que le  a été utilisé dans Platform, il doit respecter la politique de contrôle de version additive.

###  et assimilation de données

Pour importer des données dans Experience Platform, un jeu de données doit d’abord être créé. Les jeux de données sont les blocs de construction de la transformation des données et du suivi pour le service [de](../../catalog/home.md)catalogue. Ils représentent généralement les tableaux ou les fichiers qui contiennent des données assimilées. Tous les jeux de données sont basés sur les  XDM existantes, qui fournissent des contraintes pour ce que les données assimilées doivent contenir et comment elles doivent être structurées. Pour plus d’informations, reportez-vous à la présentation sur l’administration [des données d’](../../ingestion/home.md) Adobe Experience Platform.

## Composants d’un 

Experience Platform utilise une approche de composition dans laquelle les blocs de création standard sont combinés pour créer des  de. Cette approche favorise la réutilisation des composants existants et favorise la normalisation dans l&#39;ensemble du secteur afin de prendre en charge les et les composants des fournisseurs dans Platform.

Les  sont composés selon la formule suivante :

**Classe + Mixin&amp;ast; =  de XDM**

&amp;ast;Un  de est composé d&#39;une classe et de _zéro ou plus_ de mixins. Cela signifie que vous pouvez composer un  de jeu de données sans utiliser de mixins.

### Classe

La composition d’un  commence par l’affectation d’une classe. Les classes définissent les aspects comportementaux des données que le contiendra (enregistrements ou séries chronologiques). En outre, les classes décrivent le plus petit nombre de propriétés communes que tous les basés sur cette classe doivent inclure et fournissent un moyen pour la fusion de plusieurs jeux de données compatibles.

Une classe détermine également les mixins qui pourront être utilisés dans le . Cette question est traitée plus en détail dans la section [mixin](#mixin) qui suit.

Il existe des classes standard fournies avec chaque intégration d’Experience Platform, appelées classes &quot;Industry&quot;. Les catégories de l&#39;industrie sont généralement des normes industrielles acceptées qui s&#39;appliquent à un large éventail de cas d&#39;utilisation. Parmi les exemples de classes d’industrie, citons les classes XDM Individuel  et XDM ExperienceEvent fournies par Adobe.

Experience Platform autorise également les classes &quot;Fournisseur&quot;, qui sont des classes définies par les partenaires d’Experience Platform et mises à la disposition de tous les clients qui utilisent ce service ou cette application fournisseur dans Platform.

Il existe également des classes utilisées pour décrire des cas d’utilisation plus spécifiques pour des organisations individuelles au sein de Platform, appelées classes &quot;Client&quot;. Les classes de clients sont définies par une organisation lorsqu’il n’existe aucune classe de secteur ou de fournisseur disponible pour décrire un cas d’utilisation unique.

Par exemple, un  représentant les membres d’un de fidélité  décrit les données d’enregistrement sur un individu et peut donc être basé sur la classe de  XDM Individuel, une classe industrielle standard définie par Adobe.

### Mixin {#mixin}

Un mixin est un composant réutilisable qui définit un ou plusieurs champs qui implémentent certaines fonctions telles que les détails personnels, les préférences de l’hôtel ou l’adresse. Les mixins sont destinés à être inclus dans une  de qui implémente une classe compatible.

Les mixins définissent la ou les classes avec lesquelles ils sont compatibles en fonction du comportement des données qu&#39;ils représentent (enregistrements ou séries chronologiques). Cela signifie que tous les mixins ne sont pas disponibles pour toutes les classes.

Les mixins ont la même portée et la même définition que les classes : il existe des mixins d’industrie, des mixins de fournisseurs et des mixins de clients définis par des organisations individuelles utilisant Platform. Experience Platform inclut de nombreux mixins standard du secteur, tout en permettant aux fournisseurs de définir des mixins pour leurs utilisateurs et aux utilisateurs individuels de définir des mixins pour leurs propres concepts spécifiques.

Par exemple, pour capturer des détails tels que &quot;Prénom&quot; et &quot;Adresse d’accueil&quot; pour vos  &quot;Membres fidélisés&quot;, vous pouvez utiliser des mixins standard qui définissent ces concepts communs. Toutefois, les concepts spécifiques à des cas d’utilisation moins courants (tels que &quot;Niveau de fidélité &quot;) ne comportent souvent pas de mixin prédéfini. Dans ce cas, vous devez définir votre propre mixin pour capturer ces informations.

Rappelez-vous que les  sont composées de mixins &quot;zéro ou plus&quot;, ce qui signifie que vous pouvez composer un valide  sans utiliser aucun mixin.

### Data type {#data-type}

Les types de données sont utilisés comme types de champs de référence dans les classes ou les  de de la même manière que les champs littéraux de base. La principale différence réside dans le fait que les types de données peuvent définir plusieurs sous-champs. Tout comme un mixin, un type de données permet l’utilisation cohérente d’une structure à champs multiples, mais offre une plus grande flexibilité qu’un mixin, car un type de données peut être inclus n’importe où dans un  en l’ajoutant comme &quot;type de données&quot; d’un champ.

Experience Platform fournit un certain nombre de types de données courants dans le cadre du Registre des  de afin de prendre en charge l’utilisation de modèles standard pour décrire des structures de données communes. Ceci est expliqué plus en détail dans les didacticiels du Registre des , où il devient plus clair lorsque vous passez en revue les étapes de définition des types de données.

### Champ

Un champ est le bloc de création le plus élémentaire d’un . Les champs fournissent des contraintes concernant le type de données qu’ils peuvent contenir en définissant un type de données spécifique. Ces types de données de base définissent un seul champ, alors que les types [de](#data-type) données susmentionnés vous permettent de définir plusieurs sous-champs et de réutiliser la même structure multi-champs dans divers  de. Ainsi, en plus de définir le &quot;type de données&quot; d’un champ comme l’un des types de données définis dans le Registre, la plate-forme d’expérience prend en charge les types scalaires de base tels que :

* Chaîne
* Entier
* Nombre
* Booléen
* Tableau
* Objet

Les plages valides de ces types scalaires peuvent être davantage restreintes à certains modèles, formats, minimums/maximums ou valeurs prédéfinies. Grâce à ces contraintes, un large éventail de types de champs plus spécifiques peuvent être représentés, notamment :

* Enum
* Long
* Court
* Octet
* Date
* Date-heure
* Carte

>[!NOTE] Le type de champ &quot;map&quot; permet d’obtenir des données de paires clé-valeur, y compris plusieurs valeurs pour une seule clé. Les cartes ne peuvent être définies qu’au niveau du système, ce qui signifie que vous pouvez rencontrer une carte dans un  défini par le secteur ou le fournisseur, mais qu’elle n’est pas disponible pour être utilisée dans les champs que vous définissez. Le guide [du développeur](../api/getting-started.md) d&#39;API de registre contient plus d&#39;informations sur la définition des types de champ.

Certaines opérations de données utilisées par les services et applications en aval imposent des contraintes à des types de champs spécifiques. Les services concernés comprennent, entre autres :

* [Profil client en temps réel](../../profile/home.md)
* [Service d’identité](../../identity-service/home.md)
* [Segmentation](../../segmentation/home.md)
* [Service](../../query-service/home.md)
* [Espace de travail Data Science](../../data-science-workspace/home.md)

Avant de créer un à utiliser dans les services en aval, veuillez consulter la documentation appropriée pour ces services afin de mieux comprendre les exigences et les contraintes sur le terrain pour les opérations de données auxquelles le est destiné.

### Champs XDM

Outre les champs de base et la possibilité de définir vos propres types de données, XDM fournit un ensemble standard de champs et de types de données qui sont implicitement compris par les services Experience Platform et offrent une plus grande cohérence lorsqu’ils sont utilisés entre les composants de la plateforme.

Ces champs, tels que &quot;Prénom&quot; et &quot;Adresse électronique&quot;, contiennent des connotations ajoutées au-delà des types de champs scalaires de base, indiquant à Platform que les champs partageant le même type de données XDM se comportent de la même manière. Ce comportement peut être considéré comme cohérent, quel que soit l’endroit d’où proviennent les données ou le service de plateforme dans lequel les données sont utilisées.

Consultez le dictionnaire [de champs](field-dictionary.md) XDM pour obtenir un complet des champs XDM disponibles. Il est recommandé d’utiliser les champs XDM et les types de données dans la mesure du possible afin de garantir la cohérence et la normalisation dans la plateforme d’expérience.

## Exemple de composition

Les  de représentent le format et la structure des données qui seront ingérées dans la plateforme et qui sont créées à l’aide d’un modèle de composition. Comme nous l&#39;avons déjà mentionné, ces  sont composées d&#39;une classe et de zéro ou plusieurs mixins compatibles avec cette classe.

Par exemple, un décrivant les achats effectués dans un magasin de détail peut être appelé &quot;Transactions de stockage&quot;. Le met en oeuvre la classe XDM ExperienceEvent associée au mixin Commerce standard et à un mixin Product Info défini par l’utilisateur.

Un autre qui suit le trafic du site Web peut être appelé &quot;Visites Web&quot;. Il implémente également la classe XDM ExperienceEvent, mais combine cette fois le mixin Web standard.

Le diagramme ci-dessous montre ces  et les champs fournis par chaque mixin. Il contient également deux  d’après la classe XDM Individuel , y compris lemodèle de &quot;Membres de la fidélité&quot; mentionné précédemment dans le présent guide.

![](../images/schema-composition/composition.png)

### Union {#union}

Tandis que la plateforme d’expérience vous permet de composer des  pour des cas d’utilisation particuliers, elle vous permet également de voir un &quot;&quot; de pour un type de classe spécifique. Le diagramme précédent montre deux  basés sur la classe XDM ExperienceEvent et deux  basés sur la classe XDM Individuelle . Le  , illustré ci-dessous,  les champs de tous lesqui partagent la même classe (XDM ExperienceEvent et XDM Individuel, respectivement).

![](../images/schema-composition/union.png)

En activant un  à utiliser avec le client en temps réel, il sera inclus dans lede la  pour ce type de classe.  offre un robuste et centralisé des attributs du client ainsi qu’un compte horodaté de chaque que le client a eu dans tout système intégré à Platform. utilise lede  pour représenter ces données et fournir un holistique de chaque client.

Pour plus d’informations sur l’utilisation des  de, reportez-vous à l’aperçu [du client en temps](../../profile/home.md)réel.

## Mappage de fichiers de données vers un XDM 

Tous les fichiers de données assimilés dans Experience Platform doivent être conformes à la structure d’un  XDM. Pour plus d’informations sur la manière de formater les fichiers de données pour se conformer aux hiérarchies XDM (y compris les fichiers d’exemple), voir le  sur les [exemples de transformations](../../etl/transformations.md)ETL. Pour plus d’informations sur l’assimilation de fichiers de données dans Experience Platform, voir la présentation [de l’assimilation par](../../ingestion/batch-ingestion/overview.md)lot.

## Étapes suivantes

Maintenant que vous comprenez les bases de la composition des , vous êtes prêt à commencer à créer des  de à l&#39;aide du registre de l&#39; de lasalle de rédaction.

Le Registre des  permet d’accéder à la bibliothèque de  dans Adobe Experience Platform. Il fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les ressources de bibliothèque disponibles sont accessibles. La bibliothèque de  contient les ressources du secteur industriel définies par Adobe, les ressources du fournisseur définies par les partenaires d’Experience Platform, ainsi que les classes, les mixins, les types de données et les  de qui ont été composés par des membres de votre organisation.

Pour commencer à composer un  à l’aide de l’interface utilisateur, suivez le didacticiel [de l’éditeur de  de](../tutorials/create-schema-ui.md) pour créer le &quot;Membres de la fidélité&quot; mentionné tout au long de ce.

Pour commencer à utiliser l&#39;API de Registre ,  en lisant le guide [du développeur de l&#39;API de Registre de l&#39;](../api/getting-started.md). Après avoir lu le guide du développeur, suivez les étapes décrites dans le didacticiel sur la [création d&#39;un  à l&#39;aide de l&#39;API](../tutorials/create-schema-api.md)de registre de .
