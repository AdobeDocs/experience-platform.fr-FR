---
keywords: Experience Platform ; accueil ; sujets populaires ; schéma ; Schéma ; enum ; Principale identity ; Principale identité ; profil individuel XDM ; événement d’expérience ; Événement d’expérience XDM ; XDM ExperienceEvent ; experienceEvent ; experienceEvent ; événement d’expérience ; XDM Experienceevenet;schéma conception de  ; meilleures pratiques
solution: Experience Platform
title: Bonnes Pratiques Pour La Modélisation Des Données
topic-legacy: overview
description: Ce document présente les schémas du modèle de données d’expérience (XDM) ainsi que les blocs de création, principes et bonnes pratiques de la composition de schémas à utiliser dans Adobe Experience Platform.
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '2515'
ht-degree: 2%

---

# Meilleures pratiques pour la modélisation des données

[!DNL Experience Data Model] (XDM) est le cadre de base qui normalise les données d’expérience client en fournissant des structures et des définitions communes à utiliser dans les services Adobe Experience Platform en aval. En respectant les normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune qui vous permet d’obtenir des informations précieuses sur les actions client, de définir les audiences client par le biais de segments et d’exprimer les attributs client à des fins de personnalisation.

Comme XDM est extrêmement polyvalent et personnalisable par conception, il est donc important de suivre les meilleures pratiques de modélisation des données lors de la conception de vos schémas. Ce document décrit les principales décisions et considérations à prendre en compte lors de la mise en correspondance des données d’expérience client avec XDM.

## Prise en main

Avant de lire ce guide, veuillez consulter l&#39;[Présentation du système XDM](../home.md) pour une présentation de haut niveau de XDM et de son rôle dans l&#39;Experience Platform.

En outre, ce guide porte exclusivement sur les considérations clés concernant la conception de schéma. Il est donc fortement recommandé de se reporter aux [bases de la composition des schémas](./composition.md) pour obtenir des explications détaillées sur les différents éléments de schéma mentionnés dans ce guide.

## Résumé des bonnes pratiques

L’approche recommandée pour la conception de votre modèle de données à utiliser dans l’Experience Platform peut être résumée comme suit :

1. Identifiez les cas d’utilisation commerciale de vos données.
1. Identifier les sources de données Principales qui doivent être intégrées à [!DNL Platform] pour traiter ces cas d&#39;utilisation.
1. Identifiez toutes les sources de données secondaires qui pourraient également présenter un intérêt. Par exemple, si, pour l&#39;instant, une seule unité opérationnelle de votre organisation souhaite transférer ses données à [!DNL Platform], une unité opérationnelle similaire pourrait également souhaiter transférer des données similaires à l&#39;avenir. La prise en compte de ces sources secondaires permet de normaliser le modèle de données dans l’ensemble de votre organisation.
1. Créez un diagramme de relations d’entité de haut niveau (ERD) pour les sources de données qui ont été identifiées.
1. Convertissez l’ERD de haut niveau en ERD centré [!DNL Platform] (y compris les profils, les Événements d’expérience et les entités de recherche).

Les étapes relatives à l&#39;identification des sources de données applicables nécessaires à l&#39;exécution de vos dossiers d&#39;utilisation commerciale varieront d&#39;une organisation à l&#39;autre. Bien que le reste des sections de ce document se concentre sur les dernières étapes d&#39;organisation et de construction d&#39;un ERD après l&#39;identification des sources de données, les explications des différents composants du diagramme peuvent vous éclairer sur les choix de vos sources de données à migrer vers [!DNL Platform].

## Créer un ERD de haut niveau

Une fois que vous avez déterminé les sources de données que vous souhaitez importer dans [!DNL Platform], créez un ERD de haut niveau pour vous aider à orienter le processus de mappage de vos données aux schémas XDM.

L&#39;exemple ci-dessous représente une ERD simplifiée pour une société qui souhaite importer des données dans [!DNL Platform]. Le diagramme met en évidence les entités essentielles qui doivent être triées en classes XDM, y compris les comptes clients, les hôtels, les adresses et plusieurs événements de commerce électronique courants.

![](../images/best-practices/erd.png)

## Tri des entités en catégories de profil, de recherche et de événement

Une fois que vous avez créé un ERD pour identifier les entités essentielles que vous souhaitez importer dans [!DNL Platform], ces entités doivent être triées en catégories de profil, de recherche et de événement :

| Catégorie | Description |
| --- | --- |
| Entités de profil | Les entités de profil représentent des attributs relatifs à une personne, généralement un client. Les entités qui relèvent de cette catégorie doivent être représentées par des schémas basés sur la classe **[!DNL XDM Individual Profile]**. |
| Entités de recherche | Les entités de recherche représentent des concepts qui peuvent se rapporter à une personne, mais qui ne peuvent pas être directement utilisés pour identifier la personne. Les entités qui relèvent de cette catégorie doivent être représentées par des schémas basés sur **classes personnalisées**. |
| Entités de événement | Les entités de événement représentent des concepts liés aux actions qu&#39;un client peut entreprendre, aux événements système ou à tout autre concept dans lequel vous pouvez suivre les modifications au fil du temps. Les entités qui relèvent de cette catégorie doivent être représentées par des schémas basés sur la classe **[!DNL XDM ExperienceEvent]**. |

### Considérations relatives au tri des entités

Les sections ci-dessous fournissent d&#39;autres conseils sur la manière de trier vos entités en fonction des catégories ci-dessus.

#### Attributs du client

Si une entité contient des attributs liés à un client individuel, il s’agit probablement d’une entité de profil. Voici quelques exemples d’attributs du client :

* Des informations personnelles telles que le nom, la date de naissance, le sexe et le ou les ID de compte.
* Informations sur l’emplacement, telles que les adresses et les informations GPS.
* Coordonnées, telles que numéros de téléphone et adresses électroniques.

#### Suivi des données au fil du temps

Si vous souhaitez analyser la manière dont certains attributs d&#39;une entité changent au fil du temps, il s&#39;agit probablement d&#39;une entité événement. Par exemple, l’ajout d’éléments de produit à un panier peut être suivi en tant que événements de panier à ajouts dans [!DNL Platform] :

| Customer ID | Type | ID de produit | Quantité | Horodatage |
| --- | --- | --- | --- | --- |
| 1234567 | Addition | 275098 | 2 | 1er octobre, 10h32 |
| 1234567 | Supprimer | 275098 | 1 | 1er octobre, 10h33 |
| 1234567 | Addition | 486502 | 1 | 1er octobre, 10:41 |
| 1234567 | Addition | 910482 | 5 | 3 octobre, 14:15 |

#### Cas d’utilisation de la segmentation

Lors de la catégorisation de vos entités, il est important de réfléchir aux segments d&#39;audience que vous souhaitez peut-être créer pour répondre à vos cas particuliers d&#39;utilisation commerciale.

Par exemple, une société veut connaître tous les membres &quot;Or&quot; ou &quot;Platine&quot; de son programme de fidélité qui ont fait plus de cinq achats l&#39;année dernière. Sur la base de cette logique de segmentation, on peut tirer les conclusions suivantes concernant la manière dont les entités concernées devraient être représentées :

* &quot;Or&quot; et &quot;Platine&quot; représentent les états de fidélité applicables à un client individuel. Puisque la logique de segment ne concerne que l’état actuel de fidélité des clients, ces données peuvent être modélisées dans le cadre d’un schéma de profil. Si vous souhaitez suivre les modifications de l’état de fidélité au fil du temps, vous pouvez également créer un schéma de événement supplémentaire pour les modifications de l’état de fidélité.
* Les achats sont des événements qui se produisent à un moment donné et la logique de segment concerne les événements d&#39;achat dans une période spécifiée. Ces données doivent donc être modélisées en tant que schéma de événement.

#### Cas d’utilisation des Activations

Outre les considérations relatives aux cas d’utilisation de la segmentation, vous devez également examiner les cas d’utilisation des activations pour ces segments afin d’identifier d’autres attributs pertinents.

Par exemple, une société a créé un segment d’audience basé sur la règle `country = US`. Ensuite, lorsque ce segment est activé sur certaines cibles en aval, la société souhaite filtrer tous les profils exportés en fonction de l’état d’accueil. Par conséquent, un attribut `state` doit également être capturé dans l&#39;entité de profil applicable.

#### Valeurs agrégées

En fonction du cas d’utilisation et de la granularité de vos données, vous devez déterminer si certaines valeurs doivent être préagrégées avant d’être incluses dans une entité de profil ou de événement.

Par exemple, une société souhaite créer un segment en fonction du nombre d’achats de paniers. Vous pouvez choisir d’incorporer ces données à la granularité la plus faible en incluant chaque événement d’achat horodaté en tant qu’entité propre. Cependant, cela peut parfois augmenter le nombre de événements enregistrés de manière exponentielle. Pour réduire le nombre de événements ingérés, vous pouvez choisir de créer une valeur d’agrégat `numberOfPurchases` sur une période d’une semaine ou d’un mois. D&#39;autres fonctions d&#39;agrégat comme MIN et MAX peuvent également s&#39;appliquer à ces situations.

>[!CAUTION]
>
>L’Experience Platform n’effectue pas actuellement d’agrégation automatique des valeurs, bien que cette opération soit prévue pour les versions ultérieures. Si vous choisissez d’utiliser des valeurs agrégées, vous devez effectuer les calculs en externe avant d’envoyer les données à [!DNL Platform].

#### Cardinalité

Les cardinalités établies dans votre DRE peuvent également fournir des indices sur la manière de classer vos entités. S&#39;il existe une relation de type &quot;un à plusieurs&quot; entre deux entités, l&#39;entité qui représente le &quot;plusieurs&quot; sera probablement une entité événement. Cependant, il existe également des cas où &quot;plusieurs&quot; est un ensemble d&#39;entités de recherche fournies sous forme de tableau dans une entité de profil.

>[!NOTE]
>
>Étant donné qu&#39;il n&#39;existe pas d&#39;approche universelle pour tous les cas d&#39;utilisation, il est important de tenir compte des avantages et des inconvénients de chaque situation lorsqu&#39;on classe les entités en fonction de leur cardinalité. Voir la section [suivante](#pros-and-cons) pour plus d&#39;informations.

Le tableau suivant présente quelques relations d&#39;entité communes et les catégories qui peuvent en découler :

| Relation | Cardinalité | Catégories d’entité |
| --- | --- | --- |
| Clients et passages en caisse | Un à plusieurs | Un client unique peut avoir plusieurs passages en caisse, c&#39;est-à-dire des événements qui peuvent être suivis au fil du temps. Les clients seraient donc une entité de profil, tandis que les passages en caisse seraient une entité de événement. |
| Clients et comptes de fidélité | Un à un | Un client unique ne peut avoir qu’un seul compte de fidélité, et vice versa. Dans la mesure où la relation est personnalisée, les clients et les comptes de fidélité représentent tous deux des entités de profil. |
| Clients et Abonnements | Un à plusieurs | Un client unique peut avoir plusieurs abonnements. Puisque la société ne concerne que les abonnements actuels d’un client, Clients est une entité de profil, tandis que les Abonnements sont une entité de recherche. |

### Avantages et inconvénients de différentes classes d&#39;entités {#pros-and-cons}

Bien que la section précédente fournisse quelques lignes directrices générales pour décider comment classer vos entités, il est important de comprendre qu&#39;il peut y avoir souvent des avantages et des inconvénients pour choisir une catégorie d&#39;entité plutôt qu&#39;une autre. L&#39;étude de cas ci-après a pour but d&#39;illustrer comment vous pourriez envisager vos options dans ces situations.

Une société effectue le suivi des abonnements principaux pour ses clients, où un client peut avoir plusieurs abonnements. La société souhaite également inclure des abonnements pour les cas d’utilisation de la segmentation, comme la recherche de tous les utilisateurs ayant des abonnements principaux.

Dans ce scénario, la société dispose de deux options potentielles pour représenter les abonnements d’un client dans son modèle de données :

1. [Utiliser des attributs de profil](#profile-approach)
1. [Utiliser des entités de événement](#event-approach)

#### Approche 1 : Utiliser les attributs de profil {#profile-approach}

La première approche consisterait à inclure un tableau d&#39;abonnements en tant qu&#39;attributs dans l&#39;entité de profil pour les clients. Les objets de ce tableau contiendront des champs pour `category`, `status`, `planName`, `startDate` et `endDate`.

<img src="../images/best-practices/profile-schema.png" width="800"><br>

**Avantages**

* La segmentation est possible pour le cas d’utilisation prévu.
* Le schéma ne conserve que les derniers enregistrements d&#39;abonnement pour un client.

**Cons**

* La baie entière doit être redémarrée chaque fois que des modifications sont apportées à un champ de la baie.
* Si différentes sources de données ou unités opérationnelles alimentent des données dans la baie, il sera difficile de synchroniser la baie la plus récente sur tous les canaux.

#### Approche 2 : Utiliser des entités de événement {#event-approach}

La deuxième approche consisterait à utiliser des schémas de événement pour représenter les abonnements. Cela implique l’importation des mêmes champs d’abonnement que la première approche, avec l’ajout d’un ID d’abonnement, d’un ID de client et d’un horodatage indiquant le moment où le événement d’abonnement s’est produit.

<img src="../images/best-practices/event-schema.png" width="800"><br>

**Avantages**

* Les règles de segmentation peuvent être plus flexibles (par exemple, trouver tous les clients qui ont modifié leurs abonnements au cours des 30 derniers jours).
* Lorsque le statut d&#39;abonnement d&#39;un client change, vous n&#39;avez plus à mettre à jour une baie longue et potentiellement complexe dans les attributs de profil du client. Cela s’avère particulièrement utile si des modifications simultanées de la liste d’abonnement du client proviennent de plusieurs sources.

**Cons**

* La segmentation devient plus complexe pour le cas d’utilisation prévu d’origine (identifiant l’état des abonnements les plus récents des clients). Le segment a désormais besoin d’une logique supplémentaire pour marquer le dernier événement d’abonnement d’un client afin de vérifier son état.

## Créer des schémas en fonction de vos entités catégorisées

Une fois que vous avez trié vos entités en catégories de profil, de recherche et de événement, vous pouvez début convertir votre modèle de données en schémas XDM. À des fins de démonstration, l’exemple de modèle de données présenté précédemment a été trié en catégories appropriées dans le diagramme suivant :

<img src="../images/best-practices/erd-sorted.png" width="800"><br>

La catégorie sous laquelle une entité a été triée doit déterminer la classe XDM sur laquelle vous basez son schéma. Pour répéter :

* Les entités de profil doivent utiliser la classe [!DNL XDM Individual Profile].
* Les entités de événement doivent utiliser la classe [!DNL XDM ExperienceEvent].
* Les entités de recherche doivent utiliser des classes XDM personnalisées définies par votre organisation.

>[!NOTE]
>
>Bien que les entités de événement soient presque toujours représentées par des schémas distincts, les entités du profil ou des catégories de recherche peuvent être combinées dans un seul schéma XDM, selon leur cardinalité.
>
>Par exemple, puisque l&#39;entité Clients entretient une relation personnalisée avec l&#39;entité LoyaltyComptes, le schéma de l&#39;entité Clients peut également inclure un objet `LoyaltyAccount` contenant les champs de fidélité appropriés pour chaque client. Cependant, si la relation est de un à plusieurs, l&#39;entité qui représente le &quot;nombre&quot; peut être représentée par un schéma distinct ou un ensemble d&#39;attributs de profil, selon sa complexité.

Les sections ci-dessous fournissent des conseils généraux sur la construction de schémas en fonction de votre DRE.

### Adopter une approche de modélisation itérative

Les [règles de l&#39;évolution des schémas](./composition.md#evolution) dictent que seuls des changements non destructifs peuvent être apportés aux schémas une fois qu&#39;ils ont été mis en oeuvre. En d’autres termes, une fois que vous avez ajouté un champ à un schéma et que des données ont été ingérées sur ce champ, le champ ne peut plus être supprimé. Il est donc essentiel d&#39;adopter une approche de modélisation itérative lors de la création initiale de vos schémas, en commençant par une mise en oeuvre simplifiée qui gagne progressivement en complexité au fil du temps.

Si vous ne savez pas si un champ particulier est nécessaire pour être inclus dans un schéma, la meilleure pratique consiste à l’exclure. S’il est déterminé par la suite que le champ est nécessaire, il peut toujours être ajouté à la prochaine itération du schéma.

### Champs d’identité

Dans l’Experience Platform, les champs XDM marqués comme identités sont utilisés pour rassembler les informations sur les clients individuels provenant de plusieurs sources de données. Bien qu&#39;un schéma puisse comporter plusieurs champs marqués comme identités, une seule identité Principale doit être définie pour que le schéma puisse être activé pour une utilisation dans [!DNL Real-time Customer Profile]. Consultez la section [champs d&#39;identité](./composition.md#identity) dans les bases de la composition des schémas pour plus d&#39;informations sur le cas d&#39;utilisation de ces champs.

Lors de la conception de vos schémas, toute clé Principale dans vos tables de base de données relationnelles sera probablement candidate pour des identités Principales. Les autres exemples de champs d&#39;identité applicables sont les adresses électroniques des clients, les numéros de téléphone, les ID de compte et [ECID](../../identity-service/ecid.md).

### Groupes de champs de schéma d&#39;application d&#39;Adobe

Experience Platform fournit plusieurs groupes de champs de schéma XDM prêts à l’emploi pour la capture de données liées aux applications d’Adobe suivantes :

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Par exemple, le groupe de champs [[!UICONTROL Modèle Adobe Analytics ExperienceEvent]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) vous permet de mapper des champs [!DNL Analytics] spécifiques à vos schémas XDM. Selon les applications d’Adobe que vous utilisez, vous devez utiliser ces groupes de champs fournis par Adobe dans vos schémas.

<img src="../images/best-practices/analytics-field-group.png" width="700"><br>

Les groupes de champs d&#39;application d&#39;Adobe attribuent automatiquement une identité Principale par défaut à l&#39;aide du champ `identityMap`, qui est un objet généré par le système et en lecture seule qui mappe les valeurs d&#39;identité standard d&#39;un client individuel.

Pour Adobe Analytics, l’ECID est l’identité Principale par défaut. Si une valeur ECID n&#39;est pas fournie par un client, l&#39;identité Principale devient AAID par défaut.

>[!IMPORTANT]
>
>Lors de l’utilisation de groupes de champs d’application d’Adobe, aucun autre champ ne doit être marqué comme identité Principale. S’il existe d’autres propriétés qui doivent être marquées comme identités, ces champs doivent être attribués en tant qu’identités secondaires à la place.

## Étapes suivantes

Ce document décrit les instructions générales et les meilleures pratiques relatives à la conception de votre modèle de données pour Experience Platform. Pour résumer :

* Utilisez une approche descendante en triant vos tableaux de données en catégories de profil, de recherche et de événement avant de construire vos schémas.
* Il existe souvent de multiples approches et options lorsqu&#39;il s&#39;agit de concevoir des schémas à des fins différentes.
* Votre modèle de données doit prendre en charge les cas d’utilisation de votre entreprise, tels que la segmentation ou l’analyse du parcours client.
* Rendez vos schémas aussi simples que possible et ajoutez uniquement de nouveaux champs quand cela est absolument nécessaire.

Une fois que vous êtes prêt, consultez le didacticiel [Création d&#39;un schéma dans l&#39;interface utilisateur](../tutorials/create-schema-ui.md) pour obtenir des instructions détaillées sur la création d&#39;un schéma, affectez la classe appropriée pour l&#39;entité et ajoutez des champs à lesquels mapper vos données.
