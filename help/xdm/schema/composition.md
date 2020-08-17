---
keywords: Experience Platform;home;popular topics;schema;Schema;enum;mixin;Mixin;Mixins;mixins;data type;data types;Data types;Data type;primary identity;primary idenity;XDM individual profile;XDM fields;enum datatype;Experience event;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM Experienceevenet;schema design
solution: Experience Platform
title: Principes de base de la composition des schémas
topic: overview
description: Ce document présente les schémas du modèle de données d’expérience (XDM) ainsi que les blocs de création, principes et bonnes pratiques de la composition de schémas à utiliser dans Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 04efbf63741ef39bbf0b22795be74087f1f7c595
workflow-type: tm+mt
source-wordcount: '2811'
ht-degree: 59%

---


# Principes de base de la composition des schémas

This document provides an introduction to [!DNL Experience Data Model] (XDM) schemas and the building blocks, principles, and best practices for composing schemas to be used in Adobe Experience Platform. For general information on XDM and how it is used within [!DNL Platform], see the [XDM System overview](../home.md).

## Compréhension des schémas

Un schéma est un jeu de règles qui représente et valide la structure et le format des données. À un niveau élevé, les schémas fournissent une définition abstraite d’un objet du monde réel (une personne, par exemple) et indiquent les données à inclure dans chaque instance de cet objet (comme le prénom, le nom, l’anniversaire, etc.).

Outre la description de la structure des données, les schémas appliquent des contraintes et des attentes aux données de manière à ce qu’elles puissent être validées lorsqu’elles sont déplacées d’un système à l’autre. Ces définitions standard permettent d’interpréter les données de manière cohérente, quelle que soit leur origine, et éliminent la nécessité d’une traduction entre les applications.

[!DNL Experience Platform] maintient cette normalisation sémantique grâce à l’utilisation de schémas. Schemas are the standard way of describing data in [!DNL Experience Platform], allowing all data that conforms to schemas to be reusable without conflicts across an organization and even to be sharable between multiple organizations.

### Tableaux relationnels et objets intégrés

Lorsque vous travaillez avec des bases de données relationnelles, les bonnes pratiques consistent à normaliser les données ou à prendre une entité et à la diviser en éléments individuels qui sont ensuite affichés sur plusieurs tableaux. Pour pouvoir lire les données dans leur ensemble ou mettre à jour l’entité, des opérations de lecture et d’écriture doivent être effectuées sur plusieurs tableaux individuels à l’aide de la fonction REJOINDRE.

Grâce aux objets intégrés, les schémas XDM peuvent représenter des données complexes directement et les conserver dans des documents autonomes possédant une structure hiérarchique. L’un des principaux avantages de cette structure est qu’elle vous permet d’effectuer des requêtes sur des données sans avoir à reconstruire l’entité par des liaisons onéreuses sur plusieurs tableaux dénormalisés.

### Schémas et Big Data

Les systèmes numériques modernes génèrent une grande quantité de signaux comportementaux (données de transaction, journaux web, Internet des objets, affichage, etc.). Le Big Data offre des opportunités extraordinaires d’optimiser des expériences, mais les utiliser représente un véritable défi en raison de leur échelle et de la diversité des données. Pour tirer parti des données, vous devez normaliser leur structure, leur format et leurs définitions afin de les traiter de manière cohérente et efficace.

Les schémas permettent de résoudre ce problème en permettant l’intégration des données à partir de diverses sources, l’uniformisation au moyen de structures et de définitions communes et le partage entre les solutions. Cela permet aux processus et aux services suivants de répondre à tout type de questions posées sur les données, en s’éloignant de l’approche traditionnelle de la modélisation des données dans laquelle toutes les questions posées sur les données sont connues à l’avance et les données sont modélisées pour être conformes à ces attentes.

### Schema-based workflows in [!DNL Experience Platform]

La normalisation est un concept clé derrière [!DNL Experience Platform]. XDM, piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas standard pour la gestion de l’expérience client.

L’infrastructure sur laquelle [!DNL Experience Platform] est construite, appelée [!DNL XDM System]&quot;infrastructure&quot;, facilite les workflows basés sur le schéma et inclut les [!DNL Schema Registry][!DNL Schema Editor]métadonnées de schéma et les schémas de consommation de services. Pour plus d’informations, consultez la [présentation du système XDM](../home.md).

## Planification de votre schéma

La première étape de la conception d’un schéma consiste à déterminer le concept ou l’objet dans le monde réel que vous essayez de capturer au sein du schéma. Une fois que vous avez identifié le concept que vous essayez de décrire, vous pouvez commencer à planifier votre schéma en réfléchissant à des éléments comme le type de données, les champs d’identité potentiels et la manière dont le schéma peut évoluer dans le futur.

### Data behaviors in [!DNL Experience Platform]

Data intended for use in [!DNL Experience Platform] is grouped into two behavior types:

* **Enregistrer les données** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **Données de série temporelle** : fournissent un instantané du système au moment où une action a été entreprise directement ou indirectement par un sujet enregistré.

Tous les schémas XDM décrivent des données pouvant être catégorisées en tant qu’enregistrement ou série temporelle. Le comportement des données d’un schéma est défini par la **classe** du schéma attribuée à celui-ci lorsqu’il est créé pour la première fois. Les classes XDM sont décrites en détail par la suite dans ce document.

Les schémas d’enregistrement et de série temporelle contiennent tous deux une carte des identités (`xdm:identityMap`). Ce champ contient la représentation de l’identité d’un sujet tiré des champs marqués comme « Identité » décrit à la section suivante.

### [!UICONTROL Identité]

Schemas are used for ingesting data into [!DNL Experience Platform]. Ces données sont finalement utilisées par plusieurs services pour créer une vue unique et unifiée d’une entité individuelle. Par conséquent, il est important, lors de la réflexion sur les schémas, de penser aux identités des clients et de déterminer les champs qui peuvent être utilisés pour identifier un sujet, quel que soit l&#39;endroit d&#39;où proviennent les données.

Pour faciliter ce processus, les champs clés de vos schémas peuvent être marqués comme identités. Upon data ingestion, the data in those fields is inserted into the &quot;[!UICONTROL Identity Graph]&quot; for that individual. The graph data can then be accessed by [!DNL Real-time Customer Profile](../../profile/home.md) and other [!DNL Experience Platform] services to provide a stitched-together view of each individual customer.

Fields that are commonly marked as &quot;[!UICONTROL Identity]&quot; include: email address, phone number, [!DNL Experience Cloud ID (ECID)](https://docs.adobe.com/content/help/fr-FR/id-service/using/home.html), CRM ID, or other unique ID fields. You should also consider any unique identifiers specific to your organization, as they may be good &quot;[!UICONTROL Identity]&quot; fields as well.

Il est important de réfléchir aux identités client au cours de la phase de planification des schémas afin de vous assurer que les données sont rassemblées pour créer le profil le plus complet possible. See the overview on [Adobe Experience Platform Identity Service](../../identity-service/home.md) to learn more about how identity information can help you deliver digital experiences to your customers.

#### xdm:identityMap

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

Comme l&#39;exemple ci-dessus le montre, chaque clé de l&#39; `identityMap` objet représente un espace de nommage d&#39;identité. La valeur de chaque clé est un tableau d&#39;objets représentant les valeurs d&#39;identité (`id`) de l&#39;espace de nommage respectif. Consultez la [!DNL Identity Service] documentation pour obtenir une [liste d&#39;espaces de nommage](../../identity-service/troubleshooting-guide.md#standard-namespaces) d&#39;identité standard reconnus par les applications d&#39;Adobe.

>[!NOTE]
>
>Une valeur booléenne indique si la valeur est ou non une Principale identité (`primary`) peut également être fournie pour chaque valeur d&#39;identité. Les identités Principal ne doivent être définies que pour les schémas destinés à être utilisés dans [!DNL Real-time Customer Profile]. See the section on [union schemas](#union) for more information.

### Principes d’évolution des schémas {#evolution}

Étant donné que la nature des expériences numériques continue à évoluer, les schémas utilisés pour les représenter le doivent aussi. Un schéma bien conçu est donc capable de s’adapter et d’évoluer si nécessaire sans provoquer des modifications destructives aux versions précédentes du schéma.

Since maintaining backwards compatibility is crucial for schema evolution, [!DNL Experience Platform] enforces a purely additive versioning principle to ensure that any revisions to the schema only result in non-destructive updates and changes. En d’autres termes, **les modifications entraînant des ruptures ne sont pas prises en charge.**

| Modifications prises en charge | Modifications entraînant une rupture (non prises en charge) |
|------------------------------------|---------------------------------|
| <ul><li>Ajouter des nouveaux champs à un schéma existant</li><li>Rendre un champ obligatoire facultatif</li></ul> | <ul><li>Supprimer des champs définis précédemment</li><li>Introduire de nouveaux champs obligatoires</li><li>Renommer ou redéfinir des champs existants</li><li>Supprimer ou limiter des valeurs de champ précédemment prises en charge</li><li>Déplacer des attributs vers un autre emplacement de l’arborescence</li></ul> |

>[!NOTE]
>
>If a schema has not yet been used to ingest data into [!DNL Experience Platform], you may introduce a breaking change to that schema. However, once the schema has been used in [!DNL Platform], it must adhere to the additive versioning policy.

### Schémas et ingestion de données

In order to ingest data into [!DNL Experience Platform], a dataset must first be created. Datasets are the building blocks for data transformation and tracking for [!DNL Catalog Service](../../catalog/home.md), and generally represent tables or files that contain ingested data. Tous les jeux de données sont basés sur des schémas XDM existants qui fournissent des contraintes sur ce que les données ingérées doivent contenir et sur la manière dont elles doivent être structurées. Pour plus d’informations, consultez la présentation d’[Adobe Experience Platform Data Ingestion](../../ingestion/home.md).

## Blocs de création d’un schéma

[!DNL Experience Platform] utilise une approche de composition dans laquelle des blocs de création standard sont associés pour créer des schémas. Cette approche favorise la réutilisation de composants existants et conditionne la normalisation dans le secteur pour soutenir les schémas et les composants fournisseurs dans [!DNL Platform].

Les schémas sont composés à l’aide de la formule suivante :

**Classe + Mixin&amp;ast; = Schéma XDM**

&amp;ast;Un schéma est composé d’une classe et de _zéro, un ou plusieurs_ mixins. Cela signifie que vous pouvez composer un schéma du jeu de données sans utiliser de mixins.

### Classe

La composition d’un schéma commence par l’attribution d’une classe. Les classes définissent les aspects comportementaux des données que le schéma contiendra (enregistrements ou séries temporelles). En outre, les classes décrivent le plus petit de nombres de propriétés communes que tous les schémas basés sur cette classe doivent inclure et fournir une manière de fusionner plusieurs jeux de données compatibles.

Une classe détermine également les mixins éligibles à utiliser dans le schéma. Ce sujet est discuté plus en détail dans la section suivante consacrée aux [mixins](#mixin).

There are standard classes provided with every integration of [!DNL Experience Platform], known as &quot;Industry&quot; classes. Les classes de secteur sont généralement des normes acceptées par le secteur qui s’appliquent à un grand nombre de cas d’utilisation. Examples of Industry classes include the [!DNL XDM Individual Profile] and [!DNL XDM ExperienceEvent] classes provided by Adobe.

[!DNL Experience Platform][!DNL Experience Platform] autorise également les classes « Fournisseur » qui sont des classes définies par les partenaires et rendues disponibles pour tous les clients qui utilisent ce service fournisseur ou l’application dans [!DNL Platform].

There are also classes used to describe more specific use cases for individual organizations within [!DNL Platform], called &quot;Customer&quot; classes. Les classes de client sont définies par une organisation lorsqu’il n’y a pas de classes de secteur ou de fournisseur disponibles pour décrire un cas d’utilisation unique.

For example, a schema representing members of a Loyalty program describes record data about an individual and therefore can be based on the [!DNL XDM Individual Profile] class, a standard Industry class defined by Adobe.

### Mixin {#mixin}

Un mixin est un composant réutilisable qui définit un ou plusieurs champs qui mettent en œuvre certaines fonctionnalités comme les détails personnels, les préférences d’hôtel ou les adresses. Les mixins sont destinés à être inclus dans le cadre d’un schéma qui met en œuvre une classe compatible.

Les mixins définissent la ou les classes avec lesquelles ils sont compatibles en fonction du comportement des données qu’ils représentent (enregistrement ou série temporelle). Cela signifie que tous les mixins ne peuvent pas être utilisés pour toutes les classes.

Les mixins ont la même portée et la même définition que les classes : il existe des mixins de secteur, de fournisseur et de client définis par les organisations individuelles utilisant [!DNL Platform]. [!DNL Experience Platform] inclut de nombreux mixins standard de secteur tout en permettant également aux fournisseurs de définir des mixins pour leurs utilisateurs et aux utilisateurs individuels de définir des mixins pour leurs propres concepts spécifiques.

For example, to capture details such as &quot;[!UICONTROL First Name]&quot; and &quot;[!UICONTROL Home Address]&quot; for your &quot;[!UICONTROL Loyalty Members]&quot; schema, you would be able to use standard mixins that define those common concepts. However, concepts that are specific to less-common use cases (such as &quot;[!UICONTROL Loyalty Program Level]&quot;) often do not have a pre-defined mixin. Dans ce cas, vous devez définir vos propres mixins pour capturer ces informations.

N’oubliez pas que les schémas sont composés de « zéro, un ou plusieurs » mixins, ce qui signifie que vous pouvez composer un schéma valide sans utiliser de mixins du tout.

### Type de données {#data-type}

Les types de données sont utilisés comme types de champ de référence dans des classes ou des schémas de la même manière que des champs littéraux de base. La principale différence réside dans le fait que les types de données peuvent définir plusieurs sous-champs. Tout comme un mixin, un type de données permet l’utilisation cohérente d’une structure à champs multiples, mais avec plus de flexibilité qu’un mixin, car un type de données peut être inclus n’importe où dans un schéma en l’ajoutant comme « type de données » d’un champ.

[!DNL Experience Platform] fournit un certain nombre de types de données courants dans le [!DNL Schema Registry] cadre de la prise en charge de l’utilisation de modèles standard pour décrire des structures de données communes. This is explained in more detail in the [!DNL Schema Registry] tutorials, where it will become more clear as you walk through the steps to define data types.

### Champ

Un champ est le bloc de création le plus basique d’un schéma. Les champs apportent des contraintes concernant le type de données qu’ils peuvent contenir en définissant un type de données spécifique. Ces types de données de base définissent un champ unique, tandis que les [types de données](#data-type) mentionnés précédemment vous permettent de définir plusieurs sous-champs et de réutiliser la même structure à champs multiples sur plusieurs schémas. So, in addition to defining a field&#39;s &quot;data type&quot; as one of the data types defined in the registry, [!DNL Experience Platform] supports basic scalar types such as:

* Chaîne
* Entier
* Nombre
* Booléen
* Tableau
* Objet

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

* [!DNL Real-time Customer Profile](../../profile/home.md)
* [!DNL Identity Service](../../identity-service/home.md)
* [!DNL Segmentation](../../segmentation/home.md)
* [!DNL Query Service](../../query-service/home.md)
* [!DNL Data Science Workspace](../../data-science-workspace/home.md)

Avant de créer un schéma à utiliser dans les services en aval, veuillez consulter la documentation appropriée de ces services afin de mieux comprendre les exigences et les contraintes de champ pour les opérations de données auxquelles le schéma est destiné.

### Champs XDM

In addition to basic fields and the ability to define your own data types, XDM provides a standard set of fields and data types that are implicitly understood by [!DNL Experience Platform] services and provide greater consistency when used across [!DNL Platform] components.

These fields, such as &quot;First Name&quot; and &quot;Email Address&quot; contain added connotations beyond basic scalar field types, telling [!DNL Platform] that any fields sharing the same XDM data type will behave in the same way. This behavior can be trusted to be consistent regardless of where the data is coming from, or in which [!DNL Platform] service the data is being used.

Consultez le [dictionnaire des champs XDM](field-dictionary.md) pour obtenir une liste complète des champs XDM disponibles. Nous vous recommandons d’utiliser les champs XDM et les types de données dès que possible pour aider à la cohérence et à la standardisation dans [!DNL Experience Platform].

## Exemple de composition

Schemas represent the format and structure of data that will be ingested into [!DNL Platform], and are built using a composition model. Comme mentionné précédemment, ces schémas se composent d’une classe et de zéro, un ou plusieurs mixins compatibles avec cette classe.

For example, a schema describing purchases made at a retail store might be called &quot;[!UICONTROL Store Transactions]&quot;. The schema implements the [!DNL XDM ExperienceEvent] class combined with the standard [!UICONTROL Commerce] mixin and a user-defined [!UICONTROL Product Info] mixin.

Another schema which tracks website traffic might be called &quot;[!UICONTROL Web Visits]&quot;. It also implements the [!DNL XDM ExperienceEvent] class, but this time combines the standard [!UICONTROL Web] mixin.

Le graphique ci-dessous montre ces schémas et les champs fournis pour chaque mixin. It also contains two schemas based on the [!DNL XDM Individual Profile] class, including the &quot;[!UICONTROL Loyalty Members]&quot; schema mentioned previously in this guide.

![](../images/schema-composition/composition.png)

### Union {#union}

While [!DNL Experience Platform] allows you to compose schemas for particular use cases, it also allows you to see a &quot;union&quot; of schemas for a specific class type. The previous diagram shows two schemas based on the XDM ExperienceEvent class and two schemas based on [!DNL XDM Individual Profile] class. The union, shown below, aggregates the fields of all schemas that share the same class ([!DNL XDM ExperienceEvent] and [!DNL XDM Individual Profile], respectively).

![](../images/schema-composition/union.png)

By enabling a schema for use with [!DNL Real-time Customer Profile], it will be included in the union for that class type. [!DNL Profile] fournit des profils robustes et centralisés d&#39;attributs du client ainsi qu&#39;un compte horodaté de chaque événement que le client a eu dans tout système intégré à [!DNL Platform]. [!DNL Profile] utilise la vue d’union pour représenter ces données et fournir une vue holistique de chaque client.

For more information on working with [!DNL Profile], see the [Real-time Customer Profile overview](../../profile/home.md).

## Mappage des fichiers de données à des schémas XDM

All datafiles that are ingested into [!DNL Experience Platform] must conform to the structure of an XDM schema. Pour plus d’informations sur la manière de formater les fichiers de données pour se conformer aux hiérarchies XDM (ainsi que des fichiers d’exemple), consultez le document sur les [exemples de transformations ETL](../../etl/transformations.md). For general information about ingesting datafiles into [!DNL Experience Platform], see the [batch ingestion overview](../../ingestion/batch-ingestion/overview.md).

## Étapes suivantes

Now that you understand the basics of schema composition, you are ready to begin building schemas using the [!DNL Schema Registry].

The [!DNL Schema Registry] is used to access the [!DNL Schema Library] within Adobe Experience Platform, and provides a user interface and RESTful API from which all available library resources are accessible. The [!DNL Schema Library] contains Industry resources defined by Adobe, Vendor resources defined by [!DNL Experience Platform] partners, and classes, mixins, data types, and schemas that have been composed by members of your organization.

Pour commencer à composer un schéma à l’aide de l’interface utilisateur, suivez le [tutoriel de l’éditeur de schémas](../tutorials/create-schema-ui.md) pour créer le schéma « Loyalty Members » mentionné tout au long de ce document.

To begin using the [!DNL Schema Registry] API, start by reading the [Schema Registry API developer guide](../api/getting-started.md). Après avoir lu le guide de développement, suivez les étapes décrites dans le tutoriel [Création d’un schéma à l’aide de l’API Schema Registry](../tutorials/create-schema-api.md).