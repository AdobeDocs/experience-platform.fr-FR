---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;énumération;identité Principale;identité Principale;profil individuel XDM;événement d’expérience;événement d’expérience XDM;événement d’expérience XDM;événement d’expérience;événement d’expérience;événement d’expérience;événement d’expérience XDM;conception de schéma;bonnes pratiques
solution: Experience Platform
title: Bonnes Pratiques Pour La Modélisation Des Données
description: Ce document présente les schémas du modèle de données d’expérience (XDM) ainsi que les blocs de création, principes et bonnes pratiques de la composition de schémas à utiliser dans Adobe Experience Platform.
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '2699'
ht-degree: 3%

---

# Bonnes pratiques de modélisation des données

[!DNL Experience Data Model] (XDM) est le cadre de base qui normalise les données d’expérience client en fournissant des structures et des définitions communes à utiliser dans les services Adobe Experience Platform en aval. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées à une représentation commune qui vous permet d’obtenir des informations précieuses à partir des actions des clients, de définir des audiences de clients par le biais de segments et d’exprimer les attributs du client à des fins de personnalisation.

XDM étant extrêmement polyvalent et personnalisable par sa conception, il est donc important de suivre les bonnes pratiques de modélisation des données lors de la conception de vos schémas. Ce document couvre les principales décisions et considérations à prendre lors du mappage de vos données d’expérience client à XDM.

## Prise en main

Avant de lire ce guide, veuillez consulter la section [Présentation du système XDM](../home.md) pour une présentation de haut niveau de XDM et de son rôle dans Experience Platform.

En outre, ce guide se concentre exclusivement sur les considérations clés concernant la conception de schéma. Il est donc vivement recommandé de vous référer au [principes de base de la composition des schémas](./composition.md) pour des explications détaillées des éléments de schéma individuels mentionnés tout au long de ce guide.

## Résumé des bonnes pratiques

L’approche recommandée pour concevoir votre modèle de données à utiliser dans Experience Platform peut être résumée comme suit :

1. Présentation des cas d’utilisation professionnels pour vos données.
1. Identifier les sources de données Principales qui doivent être introduites dans [!DNL Platform] pour répondre à ces cas d’utilisation.
1. Identifiez toutes les sources de données secondaires susceptibles d’intéresser l’utilisateur. Par exemple, si actuellement une seule unité opérationnelle de votre entreprise souhaite transférer ses données vers [!DNL Platform], une unité opérationnelle similaire pourrait également souhaiter exporter des données similaires à l’avenir. En prenant en compte ces sources secondaires, vous pouvez normaliser le modèle de données dans l’ensemble de votre entreprise.
1. Créez un diagramme de relation d’entité de haut niveau (ERD) pour les sources de données qui ont été identifiées.
1. Convertir l’ERD de haut niveau en [!DNL Platform]ERD centré sur les utilisateurs (y compris les profils, les événements d’expérience et les entités de recherche).

Les étapes relatives à l’identification des sources de données applicables requises pour exécuter vos cas d’utilisation métier varient d’une organisation à l’autre. Bien que le reste des sections de ce document se concentre sur les dernières étapes d’organisation et de construction d’un ERD une fois les sources de données identifiées, les explications des différents composants du diagramme peuvent vous éclairer sur les décisions à prendre concernant les sources de données vers lesquelles vous devez migrer. [!DNL Platform].

## Création d’un ERD de haut niveau

Une fois que vous avez déterminé les sources de données que vous souhaitez importer [!DNL Platform], créez un ERD de haut niveau pour vous aider à orienter le processus de mappage de vos données aux schémas XDM.

L’exemple ci-dessous représente un ERD simplifié pour une entreprise qui souhaite importer des données dans [!DNL Platform]. Le diagramme présente les entités essentielles qui doivent être triées en classes XDM, notamment les comptes clients, les hôtels, les adresses et plusieurs événements de commerce électronique courants.

![](../images/best-practices/erd.png)

## Trier les entités en catégories de profil, de recherche et d’événement

Une fois que vous avez créé un ERD pour identifier les entités essentielles que vous souhaitez intégrer [!DNL Platform], ces entités doivent être triées en catégories de profil, de recherche et d’événement :

| Catégorie | Description |
| --- | --- |
| Entités de profil | Les entités de profil représentent les attributs relatifs à une personne, généralement un client. Les entités appartenant à cette catégorie doivent être représentées par des schémas basés sur la variable **[!DNL XDM Individual Profile]class**. |
| Entités de recherche | Les entités de recherche représentent des concepts qui peuvent être associés à une personne, mais qui ne peuvent pas être directement utilisés pour identifier la personne. Les entités appartenant à cette catégorie doivent être représentées par des schémas basés sur **classes personnalisées**. |
| Entités d’événement | Les entités d’événement représentent des concepts liés aux actions qu’un client peut entreprendre, aux événements système ou à tout autre concept dans lequel vous souhaitez peut-être suivre les modifications au fil du temps. Les entités appartenant à cette catégorie doivent être représentées par des schémas basés sur la variable **[!DNL XDM ExperienceEvent]class**. |

{style=&quot;table-layout:auto&quot;}

### Considérations pour le tri des entités

Les sections ci-dessous fournissent des conseils supplémentaires sur la manière de classer vos entités dans les catégories ci-dessus.

#### Données mutables et immuables

Une Principale méthode de tri entre les catégories d’entités consiste à déterminer si les données capturées sont modifiables ou non.

Les attributs appartenant aux profils ou aux entités de recherche sont généralement modifiables. Par exemple, les préférences d’un client peuvent changer au fil du temps et les paramètres d’un plan d’abonnement peuvent être mis à jour en fonction des tendances du marché.

En revanche, les données d’événement sont généralement immuables. Puisque les événements sont associés à un horodatage spécifique, l’&quot;instantané système&quot; fourni par un événement ne change pas. Par exemple, un événement peut capturer les préférences d’un client lorsqu’il passe en caisse un panier et ne change pas même si les préférences du client finissent par changer ultérieurement. Les données d’événement ne peuvent pas être modifiées après leur enregistrement.

En résumé, les profils et les entités de recherche contiennent des attributs modifiables et représentent les informations les plus récentes sur les sujets qu’ils capturent, tandis que les événements sont des enregistrements non modifiables du système à un moment spécifique.

#### Attributs du client

Si une entité contient des attributs liés à un client individuel, il s’agit probablement d’une entité de profil. Voici quelques exemples d’attributs du client :

* Informations personnelles telles que le nom, la date de naissance, le sexe et le ou les identifiants de compte.
* Informations de localisation telles que les adresses et les informations GPS.
* Coordonnées telles que numéros de téléphone et adresses électroniques.

#### Suivi des données au fil du temps

Si vous souhaitez analyser la manière dont certains attributs au sein d’une entité changent au fil du temps, il s’agit probablement d’une entité d’événement. Par exemple, l’ajout d’éléments de produit à un panier peut être suivi en tant qu’événements de panier à ajouter dans [!DNL Platform]:

| Identifiant client | Type | ID de produit | Quantité | Horodatage |
| --- | --- | --- | --- | --- |
| 1234567 | Addition | 275098 | 2 | 1er octobre à 10h32 |
| 1234567 | À supprimer | 275098 | 1 | 1er octobre à 10h33 |
| 1234567 | Addition | 486502 | 1 | 1er octobre 10:41 |
| 1234567 | Addition | 910482 | 5 | 3 octobre, 14 h 15 |

{style=&quot;table-layout:auto&quot;}

#### Cas d’utilisation de la segmentation

Lors de la catégorisation de vos entités, il est important de réfléchir aux segments d’audience que vous souhaitez peut-être créer pour répondre à vos cas d’utilisation professionnels particuliers.

Par exemple, une entreprise souhaite connaître tous les membres &quot;Gold&quot; ou &quot;Platinum&quot; de son programme de fidélité qui ont effectué plus de cinq achats l’année dernière. Sur la base de cette logique de segment, vous pouvez tirer les conclusions suivantes concernant la manière dont les entités pertinentes doivent être représentées :

* &quot;Gold&quot; et &quot;Platine&quot; représentent les états de fidélité applicables à un client individuel. Puisque la logique de segment ne concerne que l’état de fidélité actuel des clients, ces données peuvent être modélisées dans le cadre d’un schéma de profil. Si vous souhaitez suivre les modifications de l’état de fidélité au fil du temps, vous pouvez également créer un schéma d’événement supplémentaire pour les modifications de l’état de fidélité.
* Les achats sont des événements qui se produisent à un moment donné et la logique de segment concerne les événements d’achat dans une fenêtre temporelle spécifiée. Ces données doivent donc être modélisées en tant que schéma d’événement.

#### Cas d’utilisation de l’activation

Outre les considérations relatives aux cas d’utilisation de la segmentation, vous devez également examiner les cas d’utilisation de l’activation pour ces segments afin d’identifier d’autres attributs pertinents.

Par exemple, une entreprise a créé un segment d’audience basé sur la règle qui `country = US`. Ensuite, lors de l’activation de ce segment vers certaines cibles en aval, l’entreprise souhaite filtrer tous les profils exportés en fonction de l’état d’origine. Par conséquent, une `state` doit également être capturé dans l’entité de profil applicable.

#### Valeurs agrégées

En fonction du cas d’utilisation et de la granularité de vos données, vous devez décider si certaines valeurs doivent être pré-agrégées avant d’être incluses dans un profil ou une entité d’événement.

Par exemple, une entreprise souhaite créer un segment en fonction du nombre d’achats de panier. Vous pouvez choisir d’incorporer ces données avec la granularité la plus faible en incluant chaque événement d’achat horodaté comme entité propre. Cependant, cela peut parfois augmenter le nombre d’événements enregistrés de manière exponentielle. Pour réduire le nombre d’événements ingérés, vous pouvez choisir de créer une valeur agrégée. `numberOfPurchases` sur une période d’une semaine ou d’un mois. D’autres fonctions d’agrégat telles que MIN et MAX peuvent également s’appliquer à ces situations.

>[!CAUTION]
>
>Experience Platform n’effectue actuellement pas d’agrégation automatique de valeurs, bien que cela soit prévu pour les prochaines versions. Si vous choisissez d’utiliser des valeurs agrégées, vous devez effectuer les calculs en externe avant d’envoyer les données à [!DNL Platform].

#### Cardinalité

Les cardinalités établies dans votre ERD peuvent également fournir des indices sur la manière de classer vos entités. S’il existe une relation de type &quot;un à plusieurs&quot; entre deux entités, l’entité qui représente le &quot;nombre&quot; sera probablement une entité d’événement. Cependant, il existe également des cas où le &quot;nombre&quot; est un ensemble d’entités de recherche fournies sous forme de tableau dans une entité de profil.

>[!NOTE]
>
>Comme il n’existe pas d’approche universelle pour tous les cas d’utilisation, il est important de tenir compte des avantages et des inconvénients de chaque situation lors de la classification des entités en fonction de leur cardinalité. Voir [section suivante](#pros-and-cons) pour plus d’informations.

Le tableau suivant décrit certaines relations d’entité courantes et les catégories qui peuvent en découler :

| Relation | Cardinalité | Catégories d’entités |
| --- | --- | --- |
| Clients et Passages en caisse | Un à plusieurs | Un seul client peut avoir de nombreux passages en caisse, c’est-à-dire des événements qui peuvent être suivis au fil du temps. Les clients seraient donc une entité de profil, tandis que les Passages en caisse seraient une entité d’événement. |
| Clients et comptes de fidélité | Un à un | Un seul client ne peut avoir qu’un seul compte de fidélité, et vice versa. Comme la relation est individuelle, les clients et les comptes de fidélité représentent tous deux des entités de profil. |
| Clients et abonnements | Un à plusieurs | Un seul client peut avoir de nombreux abonnements. Puisque la société ne s’intéresse qu’aux abonnements actuels d’un client, les clients sont une entité de profil, tandis que les abonnements sont une entité de recherche. |

{style=&quot;table-layout:auto&quot;}

### Avantages et inconvénients de différentes classes d’entités {#pros-and-cons}

Bien que la section précédente ait fourni quelques instructions générales pour décider comment classer vos entités, il est important de comprendre qu’il peut souvent y avoir des avantages et des inconvénients à choisir une catégorie d’entités plutôt qu’une autre. L’étude de cas suivante a pour but d’illustrer la manière dont vous pouvez envisager vos options dans ces situations.

Une entreprise effectue le suivi des principaux abonnements de ses clients, où un client peut avoir de nombreux abonnements. L’entreprise souhaite également inclure des abonnements pour les cas pratiques de segmentation, comme la recherche de tous les utilisateurs avec des abonnements principaux.

Dans ce scénario, la société dispose de deux options potentielles pour représenter les abonnements d’un client dans son modèle de données :

1. [Utilisation des attributs de profil](#profile-approach)
1. [Utilisation des entités d’événement](#event-approach)

#### Approche 1 : Utilisation des attributs de profil {#profile-approach}

La première approche consiste à inclure un tableau d’abonnements en tant qu’attributs au sein de l’entité de profil pour les clients. Les objets de ce tableau contiendront des champs pour `category`, `status`, `planName`, `startDate`, et `endDate`.

<img src="../images/best-practices/profile-schema.png" width="800"><br>

**Avantages**

* La segmentation est possible dans le cas d’utilisation prévu.
* Le schéma ne conserve que les derniers enregistrements d’abonnement pour un client.

**Inconvénients**

* Le tableau entier doit être redémarré chaque fois que des modifications sont apportées à un champ du tableau.
* Si différentes sources de données ou unités opérationnelles alimentent des données dans le tableau, il sera difficile de conserver le dernier tableau mis à jour synchronisé sur tous les canaux.

#### Approche 2 : Utilisation des entités d’événement {#event-approach}

La seconde approche consiste à utiliser des schémas d’événement pour représenter les abonnements. Cela implique l’ingestion des mêmes champs d’abonnement que la première approche, avec un ID d’abonnement, un ID client et un horodatage du moment où l’événement d’abonnement s’est produit.

<img src="../images/best-practices/event-schema.png" width="800"><br>

**Avantages**

* Les règles de segmentation peuvent être plus flexibles (par exemple, trouver tous les clients qui ont modifié leurs abonnements au cours des 30 derniers jours).
* Lorsque l’état d’abonnement d’un client change, vous n’avez plus à mettre à jour un tableau long et potentiellement complexe dans les attributs de profil du client. Cela s’avère particulièrement utile si des modifications simultanées de la liste d’abonnements du client proviennent de plusieurs sources.

**Inconvénients**

* La segmentation devient plus complexe pour le cas d’utilisation prévu d’origine (identification de l’état des inscriptions les plus récentes des clients). Le segment a désormais besoin d’une logique supplémentaire pour marquer le dernier événement d’abonnement pour un client afin de vérifier son état.
* Les événements risquent plus d’expirer automatiquement et d’être purgés de la banque de profils. Consultez le guide sur la [Expiration des événements d’expérience](../../profile/event-expirations.md) pour plus d’informations.

## Créer des schémas en fonction de vos entités catégorisées

Une fois que vous avez trié vos entités en catégories de profil, de recherche et d’événement, vous pouvez commencer à convertir votre modèle de données en schémas XDM. À des fins de démonstration, l’exemple de modèle de données illustré précédemment a été trié en catégories appropriées dans le diagramme suivant :

<img src="../images/best-practices/erd-sorted.png" width="800"><br>

La catégorie sous laquelle une entité a été triée doit déterminer la classe XDM sur laquelle vous basez son schéma. Réitération :

* Les entités de profil doivent utiliser la variable [!DNL XDM Individual Profile] classe .
* Les entités d’événement doivent utiliser la variable [!DNL XDM ExperienceEvent] classe .
* Les entités de recherche doivent utiliser des classes XDM personnalisées définies par votre organisation.

>[!NOTE]
>
>Bien que les entités d’événement soient presque toujours représentées par des schémas distincts, les entités des catégories de profil ou de recherche peuvent être combinées dans un seul schéma XDM, selon leur cardinalité.
>
>Par exemple, comme l’entité Clients entretient une relation de type &quot;un à un&quot; avec l’entité LoyaltyAccounts, le schéma de l’entité Clients peut également inclure une `LoyaltyAccount` pour contenir les champs de fidélité appropriés pour chaque client. Cependant, si la relation est de un à plusieurs, l’entité qui représente le &quot;plusieurs&quot; peut être représentée par un schéma distinct ou un tableau d’attributs de profil, selon sa complexité.

Les sections ci-dessous fournissent des conseils généraux sur la création de schémas basés sur votre ERD.

### Adopter une approche de modélisation itérative

Le [règles d’évolution des schémas](./composition.md#evolution) Vous devez indiquer que seules les modifications non destructives peuvent être apportées aux schémas une fois qu’ils ont été implémentés. En d’autres termes, une fois que vous avez ajouté un champ à un schéma et que les données ont été ingérées par rapport à ce champ, le champ ne peut plus être supprimé. Il est donc essentiel d’adopter une approche de modélisation itérative lorsque vous créez vos schémas pour la première fois, en commençant par une mise en oeuvre simplifiée qui gagne progressivement en complexité au fil du temps.

Si vous ne savez pas si un champ particulier est nécessaire pour l’inclure dans un schéma, la bonne pratique consiste à l’exclure. S’il est déterminé par la suite que le champ est nécessaire, il peut toujours être ajouté à la prochaine itération du schéma.

### Champs d’identité

Dans Experience Platform, les champs XDM marqués comme identités sont utilisés pour rassembler des informations sur les clients individuels provenant de plusieurs sources de données. Bien qu’un schéma puisse comporter plusieurs champs marqués comme identités, une seule identité Principale doit être définie pour que le schéma puisse être utilisé dans [!DNL Real-Time Customer Profile]. Voir la section sur [champs d’identité](./composition.md#identity) dans les principes de base de la composition des schémas pour plus d’informations sur le cas d’utilisation de ces champs.

Lors de la conception de vos schémas, toute clé Principale dans vos tableaux de base de données relationnelle sera probablement candidate à des identités Principales. Les autres exemples de champs d’identité applicables sont les adresses électroniques du client, les numéros de téléphone, les ID de compte et les [ECID](../../identity-service/ecid.md).

### Adobe de groupes de champs de schéma d’application

Experience Platform fournit plusieurs groupes de champs de schéma XDM prêts à l’emploi pour la capture de données liées aux applications d’Adobe suivantes :

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Par exemple, la variable [[!UICONTROL Modèle ExperienceEvent Adobe Analytics] groupe de champs](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) vous permet de mapper [!DNL Analytics]Champs spécifiques à vos schémas XDM. Selon les applications d’Adobe que vous utilisez, vous devez utiliser ces groupes de champs fournis par Adobe dans vos schémas.

<img src="../images/best-practices/analytics-field-group.png" width="700"><br>

Adobe des groupes de champs d’application attribuent automatiquement une identité Principale par défaut grâce à l’utilisation de la variable `identityMap` champ, qui est un objet généré par le système et en lecture seule qui mappe les valeurs d’identité standard pour un client individuel.

Pour Adobe Analytics, ECID est l’identité Principale par défaut. Si une valeur ECID n’est pas fournie par un client, l’identité Principale est définie par défaut sur AAID.

>[!IMPORTANT]
>
>Lors de l’utilisation de groupes de champs d’application Adobe, aucun autre champ ne doit être marqué comme identité Principale. Si d’autres propriétés doivent être marquées comme identités, ces champs doivent être attribués en tant qu’identités secondaires à la place.

## Étapes suivantes

Ce document couvrait les directives générales et les bonnes pratiques pour la conception de votre modèle de données pour Experience Platform. Pour résumer :

* Utilisez une approche descendante en triant vos tableaux de données en catégories de profil, de recherche et d’événement avant de créer vos schémas.
* Il existe souvent plusieurs approches et options lorsqu’il s’agit de concevoir des schémas à des fins différentes.
* Votre modèle de données doit prendre en charge vos cas d’utilisation métier, tels que la segmentation ou l’analyse de parcours client.
* Rendez vos schémas aussi simples que possible et ajoutez uniquement de nouveaux champs lorsque cela est absolument nécessaire.

Une fois que vous êtes prêt, consultez le tutoriel sur [création d’un schéma dans l’interface utilisateur](../tutorials/create-schema-ui.md) pour obtenir des instructions détaillées sur la création d’un schéma, affectez la classe appropriée à l’entité et ajoutez des champs auxquels mapper vos données.
