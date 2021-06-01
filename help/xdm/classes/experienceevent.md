---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;identityMap;carte d’identité;carte d’identité;conception de schéma;carte;carte;modélisation d’événement;modélisation d’événement;bonnes pratiques;événement;événements;
solution: Experience Platform
title: Classe XDM ExperienceEvent
topic-legacy: overview
description: Ce document présente la classe XDM ExperienceEvent et les bonnes pratiques en matière de modélisation des données d’événement.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: c5b15cf23801457c3846499185d7dfd61cfa5291
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 4%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] est une classe XDM (Experience Data Model) standard qui vous permet de créer un instantané horodaté du système lorsqu’un événement spécifique se produit ou qu’un certain ensemble de conditions a été atteint.

Un événement d’expérience est un enregistrement factuel de ce qui s’est produit, y compris le moment et l’identité de la personne impliquée. Les événements peuvent être explicites (actions humaines directement observables) ou implicites (générés sans action humaine directe) et sont enregistrés sans agrégation ni interprétation. Pour plus d’informations de haut niveau sur l’utilisation de cette classe dans l’écosystème Platform, reportez-vous à la [présentation XDM](../home.md#data-behaviors).

La classe [!DNL XDM ExperienceEvent] elle-même fournit plusieurs champs de série temporelle à un schéma. Les valeurs de certains de ces champs sont automatiquement renseignées lors de l’ingestion des données :

![](../images/classes/experienceevent/structure.png)

| Propriété | Description |
| --- | --- |
| `_id` | Identifiant de chaîne unique pour l’événement. Ce champ permet de suivre l’unicité d’un événement individuel, d’éviter la duplication des données et de rechercher cet événement dans les services en aval. Dans certains cas, `_id` peut être un [identifiant unique universel (UUID)](https://tools.ietf.org/html/rfc4122) ou [identifiant unique global (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Si vous diffusez des données depuis une connexion source ou que vous ingérez directement à partir d’un fichier Parquet, vous devez générer cette valeur en concaténant une certaine combinaison de champs qui rend l’événement unique, comme un identifiant Principal, un horodatage, un type d’événement, etc. La valeur concaténée doit être une chaîne formatée `uri-reference`, ce qui signifie que tout caractère deux-points doit être supprimé. Par la suite, la valeur concaténée doit être hachée à l’aide de SHA-256 ou d’un autre algorithme de votre choix.<br><br>Il est important de distinguer que  **ce champ ne représente pas une identité liée à une personne** individuelle, mais plutôt l’enregistrement des données lui-même. Les données d’identité relatives à une personne doivent être reléguées aux [champs d’identité](../schema/composition.md#identity) fournis par des groupes de champs compatibles à la place. |
| `eventMergeId` | Si vous utilisez le [SDK Web de Adobe Experience Platform](../../edge/home.md) pour ingérer des données, cela représente l’identifiant du lot ingéré qui a provoqué la création de l’enregistrement. Ce champ est automatiquement renseigné par le système lors de l’ingestion des données. L’utilisation de ce champ en dehors du contexte d’une mise en oeuvre de SDK Web n’est pas prise en charge. |
| `eventType` | Chaîne indiquant le type ou la catégorie de l’événement. Ce champ peut être utilisé si vous souhaitez distinguer différents types d’événements au sein du même schéma et du même jeu de données, par exemple en distinguant un événement de consultation de produit d’un événement de &quot;add-to-shopping-panier&quot; pour une société de vente au détail.<br><br>Les valeurs standard de cette propriété sont fournies dans la  [section](#eventType) de l’annexe, y compris des descriptions de leur cas d’utilisation prévu. Ce champ est une énumération extensible, ce qui signifie que vous pouvez également utiliser vos propres chaînes de type d’événement pour classer les événements dont vous effectuez le suivi.<br><br>`eventType` vous limite à l’utilisation d’un seul événement par accès sur votre application. Par conséquent, vous devez utiliser des champs calculés pour indiquer au système quel événement est le plus important. Pour plus d’informations, voir la section [Bonnes pratiques pour les champs calculés](#calculated). |
| `producedBy` | Une valeur string qui décrit le producteur ou l’origine de l’événement. Ce champ peut être utilisé pour filtrer certains producteurs d’événements si nécessaire à des fins de segmentation.<br><br>Certaines valeurs suggérées pour cette propriété sont fournies dans la  [section](#producedBy) de l’annexe. Ce champ est une énumération extensible, ce qui signifie que vous pouvez également utiliser vos propres chaînes pour représenter différents producteurs d’événements. |
| `identityMap` | Champ de mappage contenant un ensemble d’identités d’espace de noms pour l’individu auquel s’applique l’événement. Ce champ est automatiquement mis à jour par le système lors de l’ingestion des données d’identité. Pour utiliser correctement ce champ pour [Real-time Customer Profile](../../profile/home.md), ne tentez pas de mettre à jour manuellement le contenu du champ dans vos opérations de données.<br /><br />Pour plus d’informations sur leur cas d’utilisation, reportez-vous à la section sur les mappages d’identité dans les  [principes de base de la ](../schema/composition.md#identityMap) composition de schémas. |
| `timestamp` | Horodatage ISO 8601 du moment où l’événement s’est produit, formaté selon [RFC 3339 Section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Cet horodatage doit avoir lieu dans le passé. Consultez la section ci-dessous sur [horodatages](#timestamps) pour connaître les bonnes pratiques d’utilisation de ce champ. |

{style=&quot;table-layout:auto&quot;}

## Bonnes pratiques relatives à la modélisation des événements

Les sections suivantes présentent les bonnes pratiques relatives à la conception de vos schémas de modèle de données d’expérience (XDM) basés sur un événement dans Adobe Experience Platform.

### Horodatages {#timestamps}

Le champ racine `timestamp` d’un schéma d’événement peut **uniquement** représenter l’observation de l’événement lui-même et doit se produire dans le passé. Si vos cas d’utilisation de segmentation nécessitent l’utilisation d’horodatages qui peuvent se produire ultérieurement, ces valeurs doivent être contraintes ailleurs dans votre schéma d’événement d’expérience.

Par exemple, si une entreprise du secteur du voyage et de l’hôtellerie modélise un événement de réservation de vol, le champ `timestamp` de niveau classe représente le moment où l’événement de réservation a été observé. D’autres horodatages liés à l’événement, tels que la date de début de la réservation de voyage, doivent être capturés dans des champs distincts fournis par des groupes de champs standard ou personnalisés.

![](../images/classes/experienceevent/timestamps.png)

En séparant l’horodatage au niveau de la classe des autres valeurs datetime associées dans vos schémas d’événement, vous pouvez mettre en oeuvre des cas d’utilisation de segmentation flexibles tout en conservant un compte horodaté des parcours client dans votre application d’expérience.

### Utilisation des champs calculés {#calculated}

Certaines interactions dans vos applications d’expérience peuvent entraîner plusieurs événements associés partageant techniquement le même horodatage d’événement et pouvant donc être représentés comme un seul enregistrement d’événement. Si, par exemple, un client consulte un produit sur votre site web, un enregistrement d’événement peut avoir deux valeurs `eventType` potentielles : un événement &quot;product view&quot; (`commerce.productViews`) ou un événement &quot;page vue&quot; générique (`web.webpagedetails.pageViews`). Dans ce cas, vous pouvez utiliser des champs calculés pour capturer les attributs les plus importants lorsque plusieurs événements sont capturés dans un seul accès.

[Adobe Experience Platform Data ](../../data-prep/home.md) Preppermet de mapper, de transformer et de valider des données vers et depuis XDM. En utilisant les [fonctions de mappage](../../data-prep/functions.md) disponibles fournies par le service, vous pouvez appeler des opérateurs logiques pour prioriser, transformer et/ou consolider des données à partir d’enregistrements multi-événements lors de leur ingestion dans Experience Platform. Dans l’exemple ci-dessus, vous pouvez désigner `eventType` comme champ calculé qui donne la priorité à une &quot;consultation de produit&quot; par rapport à une &quot;page vue&quot; chaque fois qu’elles se produisent.

Si vous ingérez manuellement des données dans Platform via l’interface utilisateur, consultez le guide sur le [mappage d’un fichier CSV à XDM](../../ingestion/tutorials/map-a-csv-file.md) pour obtenir des instructions spécifiques sur la création de champs calculés.

Si vous diffusez des données en continu vers Platform à l’aide d’une connexion source, vous pouvez configurer la source pour qu’elle utilise à la place des champs calculés. Reportez-vous à la [documentation de votre source particulière](../../sources/home.md) pour obtenir des instructions sur la mise en oeuvre des champs calculés lors de la configuration de la connexion.

## Groupes de champs de schéma compatibles {#field-groups}

>[!NOTE]
>
>Les noms de plusieurs groupes de champs ont changé. Pour plus d’informations, consultez le document [mises à jour des noms de groupe de champs](../field-groups/name-updates.md) .

Adobe fournit plusieurs groupes de champs standard à utiliser avec la classe [!DNL XDM ExperienceEvent]. Voici une liste de certains groupes de champs couramment utilisés pour la classe :

* [[!UICONTROL Détails de l’ID d’utilisateur final]](../field-groups/event/enduserids.md)
* [[!UICONTROL Détails de l’environnement]](../field-groups/event/environment-details.md)

## Annexe

La section suivante contient des informations supplémentaires sur la classe [!UICONTROL XDM ExperienceEvent].

### Valeurs acceptées pour `eventType` {#eventType}

Le tableau suivant décrit les valeurs acceptées pour `eventType`, ainsi que leurs définitions :

| Valeur | Définition |
| --- | --- |
| `advertising.completes` | Une ressource multimédia minutée a été visionnée jusqu’à la fin. Cela ne signifie pas nécessairement que l’utilisateur a visionné l’ensemble de la vidéo, car l’utilisateur aurait pu sauter devant. |
| `advertising.timePlayed` | Décrit le temps passé par un utilisateur sur une ressource multimédia minutée spécifique. |
| `advertising.federated` | Indique si un événement d’expérience a été créé par le biais d’une fédération de données (partage de données entre clients). |
| `advertising.clicks` | Cliquez sur la ou les actions sur une publicité. |
| `advertising.conversions` | Actions prédéfinies exécutées par un client qui déclenche un événement pour l’évaluation des performances. |
| `advertising.firstQuartiles` | Une publicité vidéo numérique a été lue pendant 25 % de sa durée à une vitesse normale. |
| `advertising.impressions` | Impressions d’une publicité destinée à un client ayant le potentiel d’être visualisé. |
| `advertising.midpoints` | Une publicité vidéo numérique a été lue pendant 50% de sa durée à une vitesse normale. |
| `advertising.starts` | Une publicité vidéo numérique a commencé à être lue. |
| `advertising.thirdQuartiles` | Une publicité vidéo numérique a été lue pendant 75 % de sa durée à une vitesse normale. |
| `web.webpagedetails.pageViews` | Une page web a reçu une ou plusieurs vues. |
| `web.webinteraction.linkClicks` | Un lien a été sélectionné une ou plusieurs fois. |
| `commerce.checkouts` | Un événement de passage en caisse s’est produit pour une liste de produits. Il peut y avoir plusieurs événements de passage en caisse s’il existe plusieurs étapes dans un processus de passage en caisse. S’il existe plusieurs étapes, l’horodatage et la page/expérience référencée pour chaque événement sont utilisés pour identifier chaque événement (étape) individuel, représenté dans l’ordre. |
| `commerce.productListAdds` | Un produit a été ajouté à la liste de produits ou au panier. |
| `commerce.productListOpens` | Une nouvelle liste de produits (panier) a été initialisée ou créée. |
| `commerce.productListRemovals` | Une ou plusieurs entrées de produit ont été supprimées d’une liste de produits ou d’un panier. |
| `commerce.productListReopens` | Une liste de produits (panier) qui n’était plus accessible (abandonnée) a été réactivée par un client, par exemple via une activité de remarketing. |
| `commerce.productListViews` | Une liste de produits ou un panier a reçu une ou plusieurs consultations. |
| `commerce.productViews` | Un produit a reçu une ou plusieurs consultations. |
| `commerce.purchases` | Une commande a été acceptée. Il s’agit de la seule action requise dans une conversion de commerce. Une liste de produits doit être référencée pour un événement d’achat. |
| `commerce.saveForLaters` | Une liste de produits a été enregistrée en vue d’une utilisation ultérieure, par exemple une liste de souhaits de produits. |
| `delivery.feedback` | Événements de retour pour une diffusion, par exemple une diffusion par email. |
| `message.feedback` | Événements de retour comme envoyé/rebond/erreur pour les messages envoyés à un client. |
| `message.tracking` | Suivi des événements tels que les actions d’ouverture/de clic/personnalisées sur les messages envoyés à un client. |

{style=&quot;table-layout:auto&quot;}

### Valeurs suggérées pour `producedBy` {#producedBy}

Le tableau suivant décrit certaines valeurs acceptées pour `producedBy` :

| Valeur | Définition |
| --- | --- |
| `self` | Auto |
| `system` | Système |
| `salesRef` | représentant commercial |
| `customerRep` | Représentant client |
