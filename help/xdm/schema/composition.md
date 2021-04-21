---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; enum ; mixin ; Mixin ; mixins ; mixins ; type de données ; types de données ; types de données ; type de données ; identité Principale ; identité Principale ; profil individuel XDM ; champs XDM ; type de données enum ; événement d'expérience XDM ; Expérience XDM ; événement d'expérience ; événement d'expérience ; événement d'expérience ; événement XDM événement;schéma conception;classe;classe;classes;classes;classes;classes;classes;type de données;type de données;type de données;type de données;schéma de données;Schéma ; Événements;carte d'identité;carte d'identité;carte d'identité;carte d'identité;carte d';carte d'; d'
solution: Experience Platform
title: Principes de base de la composition des Schémas
topic-legacy: overview
description: Ce document présente les schémas du modèle de données d’expérience (XDM) ainsi que les blocs de création, principes et bonnes pratiques de la composition de schémas à utiliser dans Adobe Experience Platform.
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '3501'
ht-degree: 41%

---

# Principes de base de la composition des schémas

Ce document présente les schémas [!DNL Experience Data Model] (XDM) ainsi que les éléments de base, les principes et les meilleures pratiques pour composer des schémas à utiliser dans Adobe Experience Platform. Pour obtenir des informations générales sur XDM et son utilisation dans [!DNL Platform], consultez la [Présentation du système XDM](../home.md).

## Compréhension des schémas

Un schéma est un jeu de règles qui représente et valide la structure et le format des données. À un niveau élevé, les schémas fournissent une définition abstraite d’un objet du monde réel (une personne, par exemple) et indiquent les données à inclure dans chaque instance de cet objet (comme le prénom, le nom, l’anniversaire, etc.).

Outre la description de la structure des données, les schémas appliquent des contraintes et des attentes aux données de manière à ce qu’elles puissent être validées lorsqu’elles sont déplacées d’un système à l’autre. Ces définitions standard permettent d’interpréter les données de manière cohérente, quelle que soit leur origine, et éliminent la nécessité d’une traduction entre les applications.

[!DNL Experience Platform] maintient cette normalisation sémantique en utilisant des schémas. Les schémas sont la manière standard de décrire les données dans [!DNL Experience Platform], ce qui permet à toutes les données conformes aux schémas d&#39;être réutilisées dans une organisation sans conflit, voire partagées entre plusieurs organisations.

Les schémas XDM sont idéaux pour stocker de grandes quantités de données complexes dans un format autonome. Pour plus d&#39;informations sur la façon dont XDM effectue cette opération, consultez les sections [objets incorporés](#embedded) et [big data](#big-data) dans l&#39;annexe du présent document.

### Workflows basés sur le schéma dans [!DNL Experience Platform]

La normalisation est un concept clé derrière [!DNL Experience Platform]. XDM, piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas standard pour la gestion de l’expérience client.

L&#39;infrastructure sur laquelle [!DNL Experience Platform] est construit, appelée [!DNL XDM System], facilite les workflows basés sur le schéma et inclut les [!DNL Schema Registry], [!DNL Schema Editor], les métadonnées de schéma et les schémas de consommation de services. Pour plus d’informations, consultez la [présentation du système XDM](../home.md).

Il y a plusieurs avantages clés à la construction et à l&#39;utilisation de schémas dans [!DNL Experience Platform]. Tout d&#39;abord, les schémas permettent une meilleure gouvernance des données et une meilleure minimisation des données, ce qui est particulièrement important avec la réglementation sur la protection des renseignements personnels. Deuxièmement, la création de schémas avec des composants standard de l&#39;Adobe permet d&#39;obtenir des informations prêtes à l&#39;emploi et d&#39;utiliser les services AI/ML avec un minimum de personnalisations. Enfin, les schémas fournissent une infrastructure pour le partage des données et une orchestration efficace.

## Planification de votre schéma

La première étape de la conception d’un schéma consiste à déterminer le concept ou l’objet dans le monde réel que vous essayez de capturer au sein du schéma. Une fois que vous avez identifié le concept que vous essayez de décrire, vous pouvez commencer à planifier votre schéma en réfléchissant à des éléments comme le type de données, les champs d’identité potentiels et la manière dont le schéma peut évoluer dans le futur.

### Comportements de données dans [!DNL Experience Platform]

Les données destinées à être utilisées dans [!DNL Experience Platform] sont regroupées en deux types de comportement :

* **Enregistrer les données** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **Données de série temporelle** : fournissent un instantané du système au moment où une action a été entreprise directement ou indirectement par un sujet enregistré.

Tous les schémas XDM décrivent des données pouvant être catégorisées en tant qu’enregistrement ou série temporelle. Le comportement des données d’un schéma est défini par la classe du schéma attribuée à celui-ci lorsqu’il est créé pour la première fois. Les classes XDM sont décrites en détail par la suite dans ce document.

Les schémas d’enregistrement et de série temporelle contiennent tous deux une carte des identités (`xdm:identityMap`). Ce champ contient la représentation de l’identité d’un sujet tiré des champs marqués comme « Identité » décrit à la section suivante.

### [!UICONTROL Identité] {#identity}

Les schémas sont utilisés pour importer des données dans [!DNL Experience Platform]. Ces données sont finalement utilisées par plusieurs services pour créer une vue unique et unifiée d’une entité individuelle. Par conséquent, il est important, lors de la réflexion sur les schémas, de penser aux identités des clients et de déterminer les champs qui peuvent être utilisés pour identifier un sujet, quel que soit l&#39;endroit d&#39;où proviennent les données.

Pour faciliter ce processus, les champs clés de vos schémas peuvent être marqués comme identités. Lors de l’assimilation des données, les données contenues dans ces champs sont insérées dans le &quot;[!UICONTROL graphique d’identité]&quot; de cette personne. Les données graphiques peuvent ensuite être consultées par [[!DNL Real-time Customer Profile]](../../profile/home.md) et d&#39;autres services [!DNL Experience Platform] afin de fournir une vue groupée de chaque client.

Les champs généralement marqués comme &quot;[!UICONTROL Identité]&quot; sont les suivants : adresse électronique, numéro de téléphone, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), ID de gestion de la relation client ou autres champs d’ID uniques. Vous devez également tenir compte de tous les identifiants uniques propres à votre organisation, car ils peuvent également être de bons champs &quot;[!UICONTROL Identité]&quot;.

Il est important de réfléchir à l&#39;identité des clients au cours de la phase de planification du schéma afin de veiller à ce que les données soient rassemblées pour créer le profil le plus robuste possible. Consultez la présentation du [Service d&#39;identité de Adobe Experience Platform](../../identity-service/home.md) pour en savoir plus sur la manière dont les informations d&#39;identité peuvent vous aider à fournir des expériences numériques à vos clients.

#### `xdm:identityMap` {#identityMap}

`xdm:identityMap` est un champ de type carte qui décrit les différentes valeurs d’identité d’un individu, ainsi que les espaces de nommage qui lui sont associés. Ce champ peut être utilisé pour fournir des informations d&#39;identité à vos schémas, au lieu de définir des valeurs d&#39;identité dans la structure du schéma lui-même.

Voici un exemple de carte d’identité simple :

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": false
    }
  ],
  "ECID": [
    {
      "id": "87098882279810196101440938110216748923",
      "primary": false
    },
    {
      "id": "55019962992006103186215643814973128178",
      "primary": false
    }
  ],
  "loyaltyId": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": true
    }
  ]
}
```

Comme l&#39;exemple ci-dessus le montre, chaque clé de l&#39;objet `identityMap` représente un espace de nommage d&#39;identité. La valeur de chaque clé est un tableau d&#39;objets représentant les valeurs d&#39;identité (`id`) de l&#39;espace de nommage respectif. Consultez la documentation [!DNL Identity Service] pour obtenir une [liste d&#39;espaces de nommage d&#39;identité standard](../../identity-service/troubleshooting-guide.md#standard-namespaces) reconnus par les applications d&#39;Adobe.

>[!NOTE]
>
>Une valeur booléenne indique si la valeur est une identité Principale (`primary`) peut également être fournie pour chaque valeur d&#39;identité. Les identités Principal doivent uniquement être définies pour les schémas destinés à être utilisés dans [!DNL Real-time Customer Profile]. Pour plus d&#39;informations, consultez la section [schémas d&#39;union](#union).

### Principes d’évolution des schémas {#evolution}

Étant donné que la nature des expériences numériques continue à évoluer, les schémas utilisés pour les représenter le doivent aussi. Un schéma bien conçu est donc capable de s’adapter et d’évoluer si nécessaire sans provoquer des modifications destructives aux versions précédentes du schéma.

Étant donné que le maintien de la compatibilité ascendante est essentiel pour l&#39;évolution du schéma, [!DNL Experience Platform] applique un principe de versioning purement additif pour s&#39;assurer que toute révision du schéma n&#39;entraîne que des mises à jour et des modifications non destructives. En d’autres termes, **les modifications entraînant des ruptures ne sont pas prises en charge.**

| Modifications prises en charge | Modifications entraînant une rupture (non prises en charge) |
|------------------------------------|---------------------------------|
| <ul><li>Ajouter des nouveaux champs à un schéma existant</li><li>Rendre un champ obligatoire facultatif</li></ul> | <ul><li>Supprimer des champs définis précédemment</li><li>Introduire de nouveaux champs obligatoires</li><li>Renommer ou redéfinir des champs existants</li><li>Supprimer ou limiter des valeurs de champ précédemment prises en charge</li><li>Déplacer des attributs vers un autre emplacement de l’arborescence</li></ul> |

>[!NOTE]
>
>Si un schéma n&#39;a pas encore été utilisé pour importer des données dans [!DNL Experience Platform], vous pouvez introduire une modification de rupture à ce schéma. Cependant, une fois que le schéma a été utilisé dans [!DNL Platform], il doit respecter la politique de versioning additive.

### Schémas et ingestion de données

Pour importer des données dans [!DNL Experience Platform], un jeu de données doit d&#39;abord être créé. Les jeux de données sont les blocs de construction pour la transformation des données et le suivi de [[!DNL Catalog Service]](../../catalog/home.md) et représentent généralement les tables ou les fichiers qui contiennent des données imbriquées. Tous les jeux de données sont basés sur des schémas XDM existants qui fournissent des contraintes sur ce que les données ingérées doivent contenir et sur la manière dont elles doivent être structurées. Pour plus d’informations, consultez la présentation d’[Adobe Experience Platform Data Ingestion](../../ingestion/home.md).

## Blocs de création d’un schéma

[!DNL Experience Platform] utilise une approche de composition dans laquelle des blocs de création standard sont associés pour créer des schémas. Cette approche favorise la réutilisation de composants existants et conditionne la normalisation dans le secteur pour soutenir les schémas et les composants fournisseurs dans [!DNL Platform].

Les schémas sont composés à l’aide de la formule suivante :

**Classe + Mixin&amp;ast; = Schéma XDM**

&amp;ast;Un schéma est composé d’une classe et de zéro, un ou plusieurs mixins. Cela signifie que vous pouvez composer un schéma du jeu de données sans utiliser de mixins.

### Classe {#class}

La composition d’un schéma commence par l’attribution d’une classe. Les classes définissent les aspects comportementaux des données que le schéma contiendra (enregistrements ou séries temporelles). En outre, les classes décrivent le plus petit de nombres de propriétés communes que tous les schémas basés sur cette classe doivent inclure et fournir une manière de fusionner plusieurs jeux de données compatibles.

Une classe de schéma détermine quels mixins seront admissibles à l&#39;utilisation dans ce schéma. Cette question est traitée plus en détail dans la section [suivante](#mixin).

Adobe fournit plusieurs classes XDM standard (&quot;core&quot;). Deux de ces classes, [!DNL XDM Individual Profile] et [!DNL XDM ExperienceEvent], sont requises pour presque tous les processus de plateforme en aval. Outre ces classes de base, vous pouvez également créer vos propres classes personnalisées afin de décrire des cas d’utilisation plus spécifiques pour votre entreprise. Les classes personnalisées sont définies par une organisation lorsqu&#39;il n&#39;existe aucune classe de base définie par Adobe disponible pour décrire un cas d&#39;utilisation unique.

La capture d’écran suivante montre comment les classes sont représentées dans l’interface utilisateur de la plate-forme. Comme l&#39;exemple de schéma illustré ne contient aucun mixin, tous les champs affichés sont fournis par la classe de schéma ([!UICONTROL Profil individuel XDM]).

![](../images/schema-composition/class.png)

Pour obtenir la liste la plus récente des classes XDM standard disponibles, consultez le [référentiel XDM officiel](https://github.com/adobe/xdm/tree/master/components/classes). Vous pouvez également vous reporter au guide sur [l&#39;exploration des composants XDM](../ui/explore.md) si vous préférez vue des ressources dans l&#39;interface utilisateur.

### Mixin {#mixin}

Un mixin est un composant réutilisable qui définit un ou plusieurs champs qui mettent en œuvre certaines fonctionnalités comme les détails personnels, les préférences d’hôtel ou les adresses. Les mixins sont destinés à être inclus dans le cadre d’un schéma qui met en œuvre une classe compatible.

Les mixins définissent la ou les classes avec lesquelles ils sont compatibles en fonction du comportement des données qu’ils représentent (enregistrement ou série temporelle). Cela signifie que tous les mixins ne peuvent pas être utilisés pour toutes les classes.

[!DNL Experience Platform] inclut de nombreux mixins d’Adobe standard tout en permettant aux fournisseurs de définir des mixins pour leurs utilisateurs et aux utilisateurs individuels de définir des mixins pour leurs propres concepts spécifiques.

Par exemple, pour capturer des détails tels que &quot;[!UICONTROL Prénom]&quot; et &quot;[!UICONTROL Adresse du domicile]&quot; pour votre schéma &quot;[!UICONTROL Membres de fidélité]&quot;, vous pouvez utiliser des mixins standard qui définissent ces concepts communs. Cependant, les concepts spécifiques à des cas d’utilisation moins courants (tels que &quot;[!UICONTROL Niveau de Programme de fidélité]&quot;) n’ont souvent pas de mixin prédéfini. Dans ce cas, vous devez définir vos propres mixins pour capturer ces informations.

N’oubliez pas que les schémas sont composés de « zéro, un ou plusieurs » mixins, ce qui signifie que vous pouvez composer un schéma valide sans utiliser de mixins du tout.

La capture d’écran suivante montre comment les mixins sont représentés dans l’interface utilisateur de la plate-forme. Un mixin unique ([!UICONTROL Détails démographiques]) est ajouté à un schéma dans cet exemple, qui fournit un regroupement de champs à la structure du schéma.

![](../images/schema-composition/mixin.png)

Pour obtenir la liste la plus récente des mixins XDM standard disponibles, consultez le [référentiel XDM officiel](https://github.com/adobe/xdm/tree/master/components/mixins). Vous pouvez également vous reporter au guide sur [l&#39;exploration des composants XDM](../ui/explore.md) si vous préférez vue des ressources dans l&#39;interface utilisateur.

### Type de données {#data-type}

Les types de données sont utilisés comme types de champ de référence dans des classes ou des schémas de la même manière que des champs littéraux de base. La principale différence réside dans le fait que les types de données peuvent définir plusieurs sous-champs. Tout comme un mixin, un type de données permet l’utilisation cohérente d’une structure à champs multiples, mais avec plus de flexibilité qu’un mixin, car un type de données peut être inclus n’importe où dans un schéma en l’ajoutant comme « type de données » d’un champ.

[!DNL Experience Platform] fournit un certain nombre de types de données courants dans le  [!DNL Schema Registry] cadre de la prise en charge de l’utilisation de modèles standard pour décrire des structures de données communes. Vous trouverez des informations plus détaillées à ce sujet dans les didacticiels [!DNL Schema Registry], qui s&#39;affichent plus clairement lorsque vous parcourez les étapes de définition des types de données.

La capture d’écran suivante montre comment les types de données sont représentés dans l’interface utilisateur de la plate-forme. L&#39;un des champs fournis par le mixin [!UICONTROL Détails démographiques] utilise le type de données &quot;[!UICONTROL Nom de personne]&quot;, comme indiqué par le texte qui suit le caractère de barre verticale (`|`) en regard du nom du champ. Ce type de données fournit plusieurs sous-champs relatifs au nom d&#39;une personne, concept qui peut être réutilisé pour d&#39;autres champs où le nom d&#39;une personne doit être capturé.

![](../images/schema-composition/data-type.png)

Pour obtenir la liste la plus récente des types de données XDM standard disponibles, consultez le [référentiel XDM officiel](https://github.com/adobe/xdm/tree/master/components/datatypes). Vous pouvez également vous reporter au guide sur [l&#39;exploration des composants XDM](../ui/explore.md) si vous préférez vue des ressources dans l&#39;interface utilisateur.

### Champ

Un champ est le bloc de création le plus basique d’un schéma. Les champs apportent des contraintes concernant le type de données qu’ils peuvent contenir en définissant un type de données spécifique. Ces types de données de base définissent un champ unique, tandis que les [types de données](#data-type) mentionnés précédemment vous permettent de définir plusieurs sous-champs et de réutiliser la même structure à champs multiples sur plusieurs schémas. Ainsi, en plus de définir le &quot;type de données&quot; d&#39;un champ comme l&#39;un des types de données définis dans le Registre, [!DNL Experience Platform] prend en charge les types scalaires de base tels que :

* Chaîne
* Entier
* Double
* Booléen
* Tableau
* Objet

>[!TIP]
>
>Voir l&#39;[annexe](#objects-v-freeform) pour plus d&#39;informations sur les avantages et les inconvénients de l&#39;utilisation de champs de forme libre par rapport aux champs de type d&#39;objet.

Les plages valides de ces types scalaires peuvent être limitées davantage à certains motifs, formats, minimums/maximums ou valeurs prédéfinies. Grâce à ces contraintes, il est possible de représenter une large plage de types de champ spécifiques, notamment :

* Enum
* Long
* Short
* Byte
* Date
* Date-time
* Map

>[!NOTE]
>
>Le type de champ « map » permet des données de paires clé-valeur, y compris plusieurs valeurs pour une clé unique. Les cartes ne peuvent être définies qu’au niveau du système, ce qui signifie que vous pouvez rencontrer une carte dans un schéma de secteur ou de fournisseur, mais celle-ci ne peut pas être utilisée dans les champs que vous définissez. Le [guide de développement de l’API Schema Registry](../api/getting-started.md) contient plus d’informations sur la définition des types de champ.

Certaines opérations de données utilisées par des services et des applications en aval imposent des contraintes sur certains types de champs. Les services concernés incluent, sans s’y limiter :

* [[!DNL Real-time Customer Profile]](../../profile/home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Segmentation]](../../segmentation/home.md)
* [[!DNL Query Service]](../../query-service/home.md)
* [[!DNL Data Science Workspace]](../../data-science-workspace/home.md)

Avant de créer un schéma à utiliser dans les services en aval, veuillez consulter la documentation appropriée de ces services afin de mieux comprendre les exigences et les contraintes de champ pour les opérations de données auxquelles le schéma est destiné.

### Champs XDM

Outre les champs de base et la possibilité de définir vos propres types de données, XDM fournit un ensemble standard de champs et de types de données qui sont implicitement compris par les services [!DNL Experience Platform] et offrent une plus grande cohérence lorsqu&#39;ils sont utilisés dans les composants [!DNL Platform].

Ces champs, tels que &quot;Prénom&quot; et &quot;Adresse électronique&quot;, contiennent des connotations supplémentaires au-delà des types de champs scalaires de base, indiquant à [!DNL Platform] que tout champ partageant le même type de données XDM se comporte de la même manière. Ce comportement peut être considéré comme cohérent, quel que soit l&#39;endroit d&#39;où proviennent les données ou le service [!DNL Platform] dans lequel les données sont utilisées.

Consultez le [dictionnaire des champs XDM](field-dictionary.md) pour obtenir une liste complète des champs XDM disponibles. Nous vous recommandons d’utiliser les champs XDM et les types de données dès que possible pour aider à la cohérence et à la standardisation dans [!DNL Experience Platform].

## Exemple de composition

Les schémas représentent le format et la structure des données qui seront ingérées dans [!DNL Platform] et qui sont créées à l&#39;aide d&#39;un modèle de composition. Comme mentionné précédemment, ces schémas se composent d’une classe et de zéro, un ou plusieurs mixins compatibles avec cette classe.

Par exemple, un schéma décrivant les achats effectués dans un magasin de détail peut être appelé &quot;[!UICONTROL Transactions de stockage]&quot;. Le schéma implémente la classe [!DNL XDM ExperienceEvent] associée au mixin standard [!UICONTROL Commerce] et à un mixin [!UICONTROL Product Info] défini par l&#39;utilisateur.

Un autre schéma qui suit le trafic du site Web peut être appelé &quot;[!UICONTROL Visites Web]&quot;. Il implémente également la classe [!DNL XDM ExperienceEvent], mais cette fois combine le mixin standard [!UICONTROL Web].

Le graphique ci-dessous montre ces schémas et les champs fournis pour chaque mixin. Il contient également deux schémas basés sur la classe [!DNL XDM Individual Profile], y compris le schéma &quot;[!UICONTROL Membres de fidélité]&quot; mentionné précédemment dans ce guide.

![](../images/schema-composition/composition.png)

### Union {#union}

Bien que [!DNL Experience Platform] vous permette de composer des schémas pour des cas d&#39;utilisation particuliers, il vous permet également de voir une &quot;union&quot; de schémas pour un type de classe spécifique. Le diagramme précédent présente deux schémas basés sur la classe XDM ExperienceEvent et deux schémas basés sur la classe [!DNL XDM Individual Profile]. L’union, illustrée ci-dessous, agrégat les champs de tous les schémas qui partagent la même classe ([!DNL XDM ExperienceEvent] et [!DNL XDM Individual Profile], respectivement).

![](../images/schema-composition/union.png)

En activant un schéma à utiliser avec [!DNL Real-time Customer Profile], il sera inclus dans l&#39;union pour ce type de classe. [!DNL Profile] fournit des profils robustes et centralisés d&#39;attributs du client ainsi qu&#39;un compte horodaté de chaque événement que le client a eu dans tout système intégré à  [!DNL Platform]. [!DNL Profile] utilise la vue d’union pour représenter ces données et fournir une vue holistique de chaque client.

Pour plus d&#39;informations sur l&#39;utilisation de [!DNL Profile], consultez la [Présentation du Profil client en temps réel](../../profile/home.md).

## Mappage des fichiers de données à des schémas XDM

Tous les fichiers de données assimilés à [!DNL Experience Platform] doivent être conformes à la structure d&#39;un schéma XDM. Pour plus d’informations sur la manière de formater les fichiers de données pour se conformer aux hiérarchies XDM (ainsi que des fichiers d’exemple), consultez le document sur les [exemples de transformations ETL](../../etl/transformations.md). Pour obtenir des informations générales sur l&#39;assimilation de fichiers de données dans [!DNL Experience Platform], consultez la [présentation de l&#39;assimilation par lot](../../ingestion/batch-ingestion/overview.md).

## Schémas pour les segments externes

Si vous amenez des segments à partir de systèmes externes dans la plate-forme, vous devez utiliser les composants suivants pour les capturer dans vos schémas :

* [[!UICONTROL Classe]  de ](../classes/segment-definition.md)définition de segment: Utilisez cette classe standard pour capturer les attributs clés d&#39;une définition de segment externe.
* [[!UICONTROL Segmenter le ] mixin](../mixins/profile/segmentation.md) des détails de l&#39;adhésion : Ajoutez ce mixin à votre  [!UICONTROL schéma de profil individuel ] XDM afin d’associer des profils clients à des segments spécifiques.

## Étapes suivantes

Maintenant que vous comprenez les bases de la composition des schémas, vous êtes prêt à commencer à explorer et à construire des schémas à l&#39;aide du [!DNL Schema Registry].

Pour examiner la structure des deux classes XDM de base et de leurs mixins compatibles couramment utilisés, consultez la documentation de référence suivante :

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

[!DNL Schema Registry] est utilisé pour accéder à [!DNL Schema Library] dans Adobe Experience Platform et fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les ressources de bibliothèque disponibles sont accessibles. [!DNL Schema Library] contient les ressources du secteur définies par l&#39;Adobe, les ressources du fournisseur définies par les partenaires [!DNL Experience Platform], ainsi que les classes, mixins, types de données et schémas qui ont été composés par des membres de votre organisation.

Pour commencer à composer un schéma à l’aide de l’interface utilisateur, suivez le [tutoriel de l’éditeur de schémas](../tutorials/create-schema-ui.md) pour créer le schéma « Loyalty Members » mentionné tout au long de ce document.

Pour commencer à utiliser l&#39;API [!DNL Schema Registry], début en lisant le [guide du développeur de l&#39;API de registre de Schémas](../api/getting-started.md). Après avoir lu le guide de développement, suivez les étapes décrites dans le tutoriel [Création d’un schéma à l’aide de l’API Schema Registry](../tutorials/create-schema-api.md).

## Annexe

Les sections suivantes contiennent des informations complémentaires sur les principes de la composition des schémas.

### Tableaux relationnels et objets intégrés {#embedded}

Lorsque vous travaillez avec des bases de données relationnelles, les bonnes pratiques consistent à normaliser les données ou à prendre une entité et à la diviser en éléments individuels qui sont ensuite affichés sur plusieurs tableaux. Pour pouvoir lire les données dans leur ensemble ou mettre à jour l’entité, des opérations de lecture et d’écriture doivent être effectuées sur plusieurs tableaux individuels à l’aide de la fonction REJOINDRE.

Grâce aux objets incorporés, les schémas XDM peuvent représenter directement des données complexes et les stocker dans des documents autonomes avec une structure hiérarchique. L’un des principaux avantages de cette structure est qu’elle vous permet d’effectuer des requêtes sur des données sans avoir à reconstruire l’entité par des liaisons onéreuses sur plusieurs tableaux dénormalisés. Il n&#39;existe aucune restriction stricte quant au nombre de niveaux de hiérarchie de votre schéma.

### Schémas et Big Data {#big-data}

Les systèmes numériques modernes génèrent une grande quantité de signaux comportementaux (données de transaction, journaux web, Internet des objets, affichage, etc.). Le Big Data offre des opportunités extraordinaires d’optimiser des expériences, mais les utiliser représente un véritable défi en raison de leur échelle et de la diversité des données. Pour tirer parti des données, vous devez normaliser leur structure, leur format et leurs définitions afin de les traiter de manière cohérente et efficace.

Les schémas permettent de résoudre ce problème en permettant l’intégration des données à partir de diverses sources, l’uniformisation au moyen de structures et de définitions communes et le partage entre les solutions. Cela permet aux processus et aux services suivants de répondre à tout type de questions posées sur les données, en s’éloignant de l’approche traditionnelle de la modélisation des données dans laquelle toutes les questions posées sur les données sont connues à l’avance et les données sont modélisées pour être conformes à ces attentes.

### Objets versus champs de forme libre {#objects-v-freeform}

Lors de la conception de vos schémas, certains facteurs clés doivent être pris en compte lors du choix des objets par rapport aux champs de forme libre :

| Objets | Champs de formulaire libre |
| --- | --- |
| Augmente l’imbrication | Imbrication moindre ou aucune |
| Crée des regroupements de champs logiques | Les champs sont placés dans des emplacements ad hoc. |

#### Objets

Les avantages et les inconvénients de l’utilisation d’objets par rapport aux champs de formulaire libre sont répertoriés ci-dessous.

**Avantages** :

* Il est préférable d’utiliser des objets lorsque vous souhaitez créer un regroupement logique de certains champs.
* Les objets organisent le schéma de manière plus structurée.
* Les objets aident indirectement à créer une bonne structure de menus dans l’interface utilisateur du créateur de segments. Les champs regroupés dans le schéma sont directement reflétés dans la structure de dossiers fournie dans l’interface utilisateur du créateur de segments.

**Contre** :

* Les champs deviennent plus imbriqués.
* Lorsque vous utilisez [Adobe Experience Platform Requête Service](../../query-service/home.md), des chaînes de référence plus longues doivent être fournies aux champs de requête imbriqués dans des objets.

#### Champs de formulaire libre

Les avantages et les inconvénients de l’utilisation de champs de forme libre sur des objets sont répertoriés ci-dessous.

**Avantages** :

* Les champs de forme libre sont créés directement sous l’objet racine du schéma (`_tenantId`), ce qui augmente la visibilité.
* Les chaînes de référence pour les champs de formulaire libre tendent à être plus courtes lors de l’utilisation de Requête Service.

**Contre** :

* L’emplacement des champs de forme libre dans le schéma est ad hoc, ce qui signifie qu’ils apparaissent dans l’ordre alphabétique dans l’éditeur de Schéma. Cela peut rendre les schémas moins structurés et des champs de forme libre similaires peuvent se retrouver très séparés selon leurs noms.
