---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Principes de base de la composition des schémas
topic: overview
translation-type: tm+mt
source-git-commit: 14cd3d17c7d9ba602d02925abddec9e0b246a8c8

---


# Principes de base de la composition des schémas

Ce document présente les schémas du modèle de données d’expérience (XDM) ainsi que les éléments de base, les principes et les meilleures pratiques de composition de schémas à utiliser dans Adobe Experience Platform. Pour obtenir des informations générales sur XDM et son utilisation dans Platform, consultez la présentation [du système](../home.md)XDM.

## Présentation des schémas

Un schéma est un ensemble de règles qui représentent et valident la structure et le format des données. A un niveau élevé, les schémas fournissent une définition abstraite d’un objet du monde réel (tel qu’une personne) et indiquent les données à inclure dans chaque instance de cet objet (tel que le prénom, le nom, l’anniversaire, etc.).

Outre la description de la structure des données, les schémas appliquent des contraintes et des attentes aux données afin de pouvoir les valider lorsqu&#39;elles se déplacent entre les systèmes. Ces définitions standard permettent d’interpréter les données de manière cohérente, quelle que soit l’origine, et éliminent la nécessité de les traduire dans les applications.

Experience Platform maintient cette normalisation sémantique par l’utilisation de schémas. Les Schémas sont la manière standard de décrire les données dans la plateforme d’expérience, ce qui permet à toutes les données conformes aux schémas d’être réutilisables sans conflit au sein d’une organisation et même d’être partagées entre plusieurs organisations.

### Tableaux relationnels par rapport aux objets incorporés

Lorsque vous travaillez avec des bases de données relationnelles, les meilleures pratiques consistent à normaliser les données ou à prendre une entité et à la diviser en éléments distincts qui sont ensuite affichés sur plusieurs tables. Pour lire l&#39;ensemble des données ou mettre à jour l&#39;entité, des opérations de lecture et d&#39;écriture doivent être effectuées sur de nombreuses tables individuelles à l&#39;aide de JOIN.

Grâce aux objets incorporés, les schémas XDM peuvent représenter directement des données complexes et les stocker dans des documents autonomes avec une structure hiérarchique. L&#39;un des principaux avantages de cette structure est qu&#39;elle vous permet de requête des données sans avoir à reconstruire l&#39;entité par des jointures coûteuses à plusieurs tables dénormalisées.

### Schémas et données massives

Les systèmes numériques modernes génèrent de vastes quantités de signaux comportementaux (données de transaction, journaux Web, Internet des choses, affichage, etc.). Ce big data offre des opportunités extraordinaires d’optimisation des expériences, mais il est difficile de l’utiliser en raison de l’ampleur et de la variété des données. Afin de tirer profit des données, sa structure, son format et ses définitions doivent être normalisés de manière à pouvoir les traiter de manière cohérente et efficace.

Les Schémas résolvent ce problème en permettant l&#39;intégration des données à partir de sources multiples, l&#39;uniformisation au moyen de structures et de définitions communes et le partage entre les solutions. Cela permet aux processus et services suivants de répondre à tout type de question posée aux données, en s&#39;éloignant de l&#39;approche traditionnelle de la modélisation des données où toutes les questions qui seront posées aux données sont connues à l&#39;avance et les données sont modélisées pour se conformer à ces attentes.

### workflows basés sur des Schémas dans la plateforme d’expérience

La normalisation est un concept clé derrière la plateforme d’expérience. XDM, piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas standard pour la gestion de l’expérience client.

L’infrastructure sur laquelle est construite la plateforme d’expérience, appelée système XDM, facilite les workflows basés sur le schéma et inclut le registre des Schémas, l’éditeur de Schémas, les métadonnées de schéma et les schémas de consommation des services. See the [XDM System overview](../home.md) for more information.

## Planification de votre schéma

La première étape de la construction d&#39;un schéma est de déterminer le concept, ou objet du monde réel, que vous essayez de capturer dans le schéma. Une fois que vous avez identifié le concept que vous essayez de décrire, vous pouvez commencer à planifier votre schéma en pensant à des choses comme le type de données, les champs d&#39;identité potentiels et comment le schéma pourrait évoluer dans le futur.

### Comportements de données dans la plateforme d’expérience

Les données destinées à être utilisées dans la plate-forme d’expérience sont regroupées en deux types de comportement :

* **Enregistrer les données**: Fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **Données** de série chronologique : Fournit un instantané du système au moment où une action a été entreprise directement ou indirectement par un sujet d&#39;enregistrement.

Tous les schémas XDM décrivent des données pouvant être classées comme enregistrements ou séries chronologiques. Le comportement des données d&#39;un schéma est défini par la **classe** de schéma, qui est affectée à un schéma lors de sa création. Les classes XDM sont décrites plus en détail plus loin dans ce document.

Les schémas d&#39;enregistrements et de séries chronologiques contiennent tous deux une carte des identités (`xdm:identityMap`). Ce champ contient la représentation d&#39;identité d&#39;un sujet, à partir de champs marqués comme &quot;Identité&quot;, comme décrit dans la section suivante.

### Identité

Les Schémas sont utilisés pour ingérer des données dans la plateforme d’expérience. Ces données peuvent être utilisées sur plusieurs services pour créer une vue unique et unifiée d’une entité. Par conséquent, il est important, lorsque l&#39;on pense aux schémas, de penser à &quot;l&#39;identité&quot; et à quels champs peuvent être utilisés pour identifier un sujet, quel que soit l&#39;endroit d&#39;où proviennent les données.

Pour faciliter ce processus, les champs clés peuvent être marqués comme &quot;Identité&quot;. Lors de l&#39;assimilation des données, les données contenues dans ces champs seront insérées dans le &quot;diagramme d&#39;identité&quot; de cette personne. Les données graphiques peuvent ensuite être consultées par le Profil [client en temps](../../profile/home.md) réel et d’autres services de la plateforme d’expérience afin de fournir une vue groupée de chaque client.

Les champs généralement identifiés comme &quot;Identité&quot; sont les suivants : adresse électronique, numéro de téléphone, identifiant [Experience Cloud (ECID)](https://docs.adobe.com/content/help/fr-FR/id-service/using/home.html), identifiant CRM ou autres champs d’ID uniques. Vous devez également tenir compte de tous les identifiants uniques propres à votre organisation, car il peut s’agir également de bons champs &quot;Identité&quot;.

Il est important de réfléchir à l&#39;identité des clients au cours de la phase de planification du schéma afin de veiller à ce que les données soient rassemblées pour créer le profil le plus robuste possible. Consultez la présentation [du service](../../identity-service/home.md) d’identité pour en savoir plus sur la manière dont les informations d’identité peuvent vous aider à fournir des expériences numériques à vos clients.

### Principes d&#39;évolution du Schéma {#evolution}

À mesure que la nature des expériences numériques continue d&#39;évoluer, les schémas utilisés pour les représenter doivent également évoluer. Un schéma bien conçu est donc capable de s&#39;adapter et d&#39;évoluer au besoin, sans provoquer de changements destructeurs dans les versions précédentes du schéma.

Comme le maintien de la compatibilité ascendante est essentiel pour l’évolution des schémas, Experience Platform applique un principe de gestion des versions purement additif afin de garantir que toute révision du schéma n’entraîne que des mises à jour et des modifications non destructives. En d’autres termes, les modifications **de rupture ne sont pas prises en charge.**

| Modifications prises en charge | Changements de rupture (non pris en charge) |
|------------------------------------|---------------------------------|
| <ul><li>Ajout de nouveaux champs à un schéma existant</li><li>Rendre un champ obligatoire facultatif</li></ul> | <ul><li>Suppression de champs précédemment définis</li><li>Présentation de nouveaux champs obligatoires</li><li>Attribution d’un nouveau nom ou redéfinition aux champs existants</li><li>Suppression ou restriction de valeurs de champ précédemment prises en charge</li><li>Déplacement d’attributs vers un autre emplacement dans l’arborescence</li></ul> |

>[!NOTE] Si un schéma n’a pas encore été utilisé pour importer des données dans la plateforme d’expérience, vous pouvez introduire une modification de rupture dans ce schéma. Cependant, une fois que le schéma a été utilisé dans Platform, il doit se conformer à la politique de versioning additive.

### Schémas et assimilation de données

Pour importer des données dans la plate-forme d’expérience, un jeu de données doit d’abord être créé. Les jeux de données sont les blocs de construction pour la transformation des données et le suivi pour le service [de](../../catalog/home.md)catalogue et représentent généralement les tables ou les fichiers qui contiennent des données imbriquées. Tous les jeux de données sont basés sur des schémas XDM existants, qui fournissent des contraintes pour ce que les données assimilées doivent contenir et comment elles doivent être structurées. Pour plus d’informations, consultez la présentation sur l’administration [des données de la plateforme](../../ingestion/home.md) Adobe Experience Platform.

## Blocs de construction d&#39;un schéma

La plate-forme d’expérience utilise une approche de composition dans laquelle les blocs de construction standard sont combinés pour créer des schémas. Cette approche favorise la réutilisation des composants existants et favorise la normalisation dans l&#39;ensemble du secteur pour prendre en charge les schémas et composants des fournisseurs dans la plate-forme.

Les Schémas sont composés selon la formule suivante :

**Classe + Mixin&amp;amp ; ast ; = Schéma XDM**

&amp;ast ; Un schéma est composé d&#39;une classe et de _zéro ou plusieurs_ mixins. Cela signifie que vous pouvez composer un schéma de jeu de données sans utiliser de mixins.

### Classe

La composition d&#39;un schéma commence par l&#39;affectation d&#39;une classe. Les classes définissent les aspects comportementaux des données que le schéma contiendra (enregistrements ou séries chronologiques). En outre, les classes décrivent le plus petit nombre de propriétés communes que tous les schémas basés sur cette classe devraient inclure et fournir un moyen pour la fusion de plusieurs jeux de données compatibles.

Une classe détermine également les mixins qui seront admissibles à l&#39;utilisation dans le schéma. Cette question est traitée plus en détail dans la section [mixin](#mixin) qui suit.

Il existe des classes standard fournies avec chaque intégration d’Experience Platform, connues sous le nom de classes &quot;Industrie&quot;. Les catégories de l&#39;industrie sont généralement des normes industrielles acceptées qui s&#39;appliquent à un vaste ensemble de cas d&#39;utilisation. Les classes de Profil individuel XDM et XDM ExperienceEvent fournies par Adobe sont des exemples de classes du secteur.

Experience Platform permet également la création de classes &quot;Fournisseur&quot;, qui sont des classes définies par les partenaires Experience Platform et mises à la disposition de tous les clients qui utilisent ce service ou cette application fournisseur dans Platform.

Il existe également des classes utilisées pour décrire des cas d&#39;utilisation plus spécifiques pour des organisations individuelles au sein de la plate-forme, appelées classes &quot;client&quot;. Les classes de clients sont définies par une organisation lorsqu’il n’existe aucune classe de secteur ou de fournisseur disponible pour décrire un cas d’utilisation unique.

Par exemple, un schéma représentant les membres d’un programme de fidélité décrit les données d’enregistrement d’un individu et peut donc être basé sur la classe de Profil XDM Individuel, une classe industrielle standard définie par Adobe.

### Mixine {#mixin}

Un mixin est un composant réutilisable qui définit un ou plusieurs champs qui implémentent certaines fonctions telles que les détails personnels, les préférences de l&#39;hôtel ou l&#39;adresse. Les mixins sont destinés à être inclus dans un schéma qui implémente une classe compatible.

Les mixins définissent la ou les classes avec lesquelles ils sont compatibles en fonction du comportement des données qu&#39;ils représentent (enregistrements ou séries chronologiques). Cela signifie que tous les mixins ne sont pas disponibles pour toutes les classes.

Les mixins ont la même portée et définition que les classes : il existe des mixins d’industrie, des mixins de fournisseurs et des mixins de clients définis par des organisations individuelles utilisant la plate-forme. La plate-forme d’expérience comprend de nombreux mixins standard du secteur, tout en permettant aux fournisseurs de définir des mixins pour leurs utilisateurs et aux utilisateurs individuels de définir des mixins pour leurs propres concepts spécifiques.

Par exemple, pour capturer des détails tels que &quot;Prénom&quot; et &quot;Adresse d’accueil&quot; pour votre schéma &quot;Membres fidèles&quot;, vous pouvez utiliser des mixins standard qui définissent ces concepts communs. Cependant, les concepts spécifiques à des cas d’utilisation moins courants (tels que &quot;Niveau de Programme de fidélité&quot;) n’ont souvent pas de mixin prédéfini. Dans ce cas, vous devez définir votre propre mixin pour capturer ces informations.

Rappelez-vous que les schémas sont composés de mixins &quot;zéro ou plus&quot;, ce qui signifie que vous pouvez composer un schéma valide sans utiliser de mixins.

### Data type {#data-type}

Les types de données sont utilisés comme types de champs de référence dans les classes ou les schémas de la même manière que les champs littéraux de base. La principale différence réside dans le fait que les types de données peuvent définir plusieurs sous-champs. De la même manière qu’un mixin, un type de données permet l’utilisation cohérente d’une structure à champs multiples, mais offre davantage de flexibilité qu’un mixin, car un type de données peut être inclus n’importe où dans un schéma en l’ajoutant comme &quot;type de données&quot; d’un champ.

Experience Platform fournit un certain nombre de types de données courants dans le cadre du registre des Schémas afin de prendre en charge l’utilisation de modèles standard pour décrire des structures de données communes. Ceci est expliqué de manière plus détaillée dans les didacticiels du registre des Schémas, où il devient plus clair lorsque vous parcourez les étapes de définition des types de données.

### Champ

Un champ est le bloc de construction le plus élémentaire d’un schéma. Les champs fournissent des contraintes concernant le type de données qu’ils peuvent contenir en définissant un type de données spécifique. Ces types de données de base définissent un seul champ, tandis que les types [de](#data-type) données mentionnés précédemment vous permettent de définir plusieurs sous-champs et de réutiliser la même structure multichamps sur plusieurs schémas. Ainsi, en plus de définir le &quot;type de données&quot; d’un champ comme l’un des types de données définis dans le registre, Experience Platform prend en charge les types scalaires de base tels que :

* Chaîne
* Entier
* Nombre
* Booléen
* Tableau
* Objet

Les plages valides de ces types scalaires peuvent être davantage limitées à certains modèles, formats, minimums/maximums ou valeurs prédéfinies. Grâce à ces contraintes, un large éventail de types de champs plus spécifiques peuvent être représentés, notamment :

* Enum
* Long
* Court
* Octet
* Date
* Date-heure
* Carte

>[!NOTE] Le type de champ &quot;map&quot; permet d’obtenir des données de paires clé-valeur, y compris plusieurs valeurs pour une seule clé. Les cartes ne peuvent être définies qu’au niveau du système, ce qui signifie que vous pouvez rencontrer une carte dans un schéma défini par un fournisseur ou un secteur, mais qu’elle n’est pas disponible pour être utilisée dans les champs que vous définissez. Le guide [du développeur d&#39;API de registre de](../api/getting-started.md) Schéma contient plus d&#39;informations sur la définition des types de champs.

Certaines opérations de données utilisées par les services et applications en aval imposent des contraintes sur des types de champs spécifiques. Les services concernés comprennent, entre autres :

* [Profil client en temps réel](../../profile/home.md)
* [Service d’identité](../../identity-service/home.md)
* [Segmentation](../../segmentation/home.md)
* [Requête Service](../../query-service/home.md)
* [Espace de travail Data Science](../../data-science-workspace/home.md)

Avant de créer un schéma à utiliser dans les services en aval, veuillez consulter la documentation appropriée pour ces services afin de mieux comprendre les exigences et les contraintes sur le terrain pour les opérations de données auxquelles le schéma est destiné.

### Champs XDM

Outre les champs de base et la possibilité de définir vos propres types de données, XDM fournit un ensemble standard de champs et de types de données qui sont implicitement compris par les services Experience Platform et offrent une plus grande cohérence lorsqu’ils sont utilisés entre les composants de la plate-forme.

Ces champs, tels que &quot;Prénom&quot; et &quot;Adresse électronique&quot;, contiennent des connotations supplémentaires au-delà des types de champs scalaires de base, indiquant à Platform que les champs partageant le même type de données XDM se comportent de la même manière. Ce comportement peut être approuvé pour être cohérent, quel que soit l&#39;endroit d&#39;où proviennent les données ou le service Plateforme dans lequel les données sont utilisées.

Consultez le dictionnaire [de champs](field-dictionary.md) XDM pour obtenir une liste complète des champs XDM disponibles. Il est recommandé d’utiliser les champs XDM et les types de données chaque fois que cela est possible afin de garantir la cohérence et la normalisation entre les plateformes d’expérience.

## Exemple de composition

Les Schémas représentent le format et la structure des données qui seront assimilées à la plate-forme et qui sont créés à l’aide d’un modèle de composition. Comme nous l&#39;avons mentionné précédemment, ces schémas sont composés d&#39;une classe et de zéro ou plusieurs mixins compatibles avec cette classe.

Par exemple, un schéma décrivant les achats effectués dans un magasin de détail peut être appelé &quot;Transactions de stockage&quot;. Le schéma implémente la classe XDM ExperienceEvent associée au mixin Commerce standard et à un mixin Product Info défini par l’utilisateur.

Un autre schéma qui suit le trafic du site Web peut être appelé &quot;Visites Web&quot;. Il implémente également la classe XDM ExperienceEvent, mais combine cette fois le mixin Web standard.

Le diagramme ci-dessous montre ces schémas et les champs fournis par chaque mixin. Il contient également deux schémas basés sur la classe de Profils individuels XDM, y compris le schéma &quot;Membres loyaux&quot; mentionné précédemment dans le présent guide.

![](../images/schema-composition/composition.png)

### Union {#union}

Bien que la plate-forme d’expérience vous permette de composer des schémas pour des cas d’utilisation particuliers, elle vous permet également d’afficher une &quot;union&quot; de schémas pour un type de classe spécifique. Le diagramme précédent présente deux schémas basés sur la classe XDM ExperienceEvent et deux schémas basés sur la classe de Profil XDM Individuel. L’union, illustrée ci-dessous, agrégat les champs de tous les schémas qui partagent la même classe (XDM ExperienceEvent et XDM Individuel, respectivement).

![](../images/schema-composition/union.png)

En activant un schéma à utiliser avec le Profil client en temps réel, il sera inclus dans l’union pour ce type de classe. Profil fournit des profils robustes et centralisés d&#39;attributs du client ainsi qu&#39;un compte horodaté de chaque événement que le client a eu dans tout système intégré à Platform. Profil utilise la vue d’union pour représenter ces données et fournir une vue holistique de chaque client.

Pour plus d’informations sur l’utilisation du Profil, consultez la présentation [du Profil client en temps](../../profile/home.md)réel.

## Mappage des fichiers de données aux schémas XDM

Tous les fichiers de données qui sont incorporés dans Experience Platform doivent être conformes à la structure d’un schéma XDM. Pour plus d’informations sur la façon de formater les fichiers de données en fonction des hiérarchies XDM (y compris les fichiers d’exemple), voir le document sur les [exemples de transformations](../../etl/transformations.md)ETL. Pour obtenir des informations générales sur l’assimilation de fichiers de données dans Experience Platform, consultez la présentation [de l’assimilation par](../../ingestion/batch-ingestion/overview.md)lot.

## Étapes suivantes

Maintenant que vous connaissez les bases de la composition des schémas, vous êtes prêt à commencer à créer des schémas à l&#39;aide du registre des Schémas.

Le registre des Schémas permet d’accéder à la bibliothèque de Schémas dans Adobe Experience Platform et fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les ressources de bibliothèque disponibles sont accessibles. La bibliothèque de Schémas contient des ressources du secteur définies par Adobe, des ressources du fournisseur définies par les partenaires de la plateforme d’expérience, ainsi que des classes, mixins, types de données et schémas qui ont été composés par des membres de votre organisation.

Pour commencer à composer un schéma à l’aide de l’interface utilisateur, suivez le didacticiel [de l’éditeur de](../tutorials/create-schema-ui.md) Schémas pour créer le schéma &quot;Membres fidèles&quot; mentionné tout au long de ce document.

Pour commencer à utiliser l&#39;API Schéma Registry, début en lisant le guide [du développeur de l&#39;API](../api/getting-started.md)Schéma Registry. Après avoir lu le guide du développeur, suivez les étapes décrites dans le didacticiel sur la [création d&#39;un schéma à l&#39;aide de l&#39;API](../tutorials/create-schema-api.md)de registre de Schéma.
