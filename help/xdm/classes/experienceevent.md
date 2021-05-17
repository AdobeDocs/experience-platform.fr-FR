---
keywords: Experience Platform ; accueil ; sujets populaires ; schéma ; Schéma ; XDM ; profil individuel ; champs ; schémas ; Schémas ; IdentityMap ; IdentityMap ; IdentityMap ; IdentityMap ; IdentityMap ; IdentityMap ; Schéma design ; map ; Map ; union schéma ; union
solution: Experience Platform
title: XDM ExperienceEvent, classe
topic-legacy: overview
description: Ce document fournit un aperçu de la classe XDM ExperienceEvent.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 9fbb40a401250496761dcce63a3f033a8746ae7e
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 4%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] est une classe standard de modèle de données d’expérience (XDM) qui vous permet de créer un instantané horodaté du système lorsqu’un événement spécifique se produit ou qu’un certain ensemble de conditions a été atteint.

Un Événement d’expérience est un enregistrement factuel de ce qui s’est produit, y compris le moment et l’identité de la personne concernée. Les événements peuvent être explicites (actions humaines directement observables) ou implicites (soulevées sans action humaine directe) et sont enregistrés sans agrégation ni interprétation. Pour plus d&#39;informations de haut niveau sur l&#39;utilisation de cette classe dans l&#39;écosystème de la plate-forme, consultez la [présentation de XDM](../home.md#data-behaviors).

La classe [!DNL XDM ExperienceEvent] fournit elle-même plusieurs champs relatifs aux séries chronologiques à un schéma. Les valeurs de certains de ces champs sont automatiquement renseignées lors de l’assimilation des données :

![](../images/classes/experienceevent/structure.png)

| Propriété | Description |
| --- | --- |
| `_id` | Identifiant de chaîne unique pour le événement. Ce champ permet de suivre l’unicité d’un événement individuel, d’éviter la duplication des données et de rechercher ce événement dans les services en aval.<br><br>Dans certains cas,  `_id` il peut s’agir d’un identifiant  [unique universel (UUID)](https://tools.ietf.org/html/rfc4122) ou d’un identifiant unique  [mondial (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0). Dans Adobe Experience Platform Data Prep, cette valeur peut être générée à l’aide des fonctions de mappage [`uuid` ou `guid` ](../../data-prep/functions.md#special-operations).<br><br>Si vous diffusez en continu des données à partir d’une connexion source ou que vous ingérez directement à partir d’un fichier Parquet, vous devez générer cette valeur en concaténant un certain nombre de champs combinés qui rendent l’événement unique, tels qu’un identifiant Principal, un horodatage, un type d&#39;événement, etc.<br><br>Il est important de distinguer que  **ce champ ne représente pas une identité liée à une personne**, mais plutôt l&#39;enregistrement des données proprement dites. Les données d&#39;identité relatives à une personne doivent être reléguées aux [champs d&#39;identité](../schema/composition.md#identity) fournis par des mixins compatibles. |
| `eventMergeId` | Si vous utilisez [Adobe Experience Platform Web SDK](../../edge/home.md) pour assimiler des données, cela représente l&#39;identifiant du lot assimilé qui a provoqué la création de l&#39;enregistrement. Ce champ est automatiquement renseigné par le système lors de l’assimilation des données. L’utilisation de ce champ en dehors du contexte d’une implémentation du SDK Web n’est pas prise en charge. |
| `eventType` | Chaîne indiquant le type ou la catégorie du événement. Ce champ peut être utilisé si vous souhaitez distinguer différents types d&#39;événement au sein d’un même schéma et d’un même jeu de données, par exemple en distinguant un événement de vue de produits d’un événement de panier d’achat supplémentaire pour une société de vente au détail.<br><br>Les valeurs standard de cette propriété sont fournies dans la section [ de l’](#eventType)annexe, y compris la description de leur utilisation prévue. Ce champ est un enum extensible, ce qui signifie que vous pouvez également utiliser vos propres chaînes de type d&#39;événement pour classer les événements suivis par catégorie. |
| `producedBy` | Valeur de chaîne qui décrit le producteur ou l’origine du événement. Ce champ peut être utilisé pour filtrer certains producteurs de événement si nécessaire à des fins de segmentation.<br><br>Certaines valeurs suggérées pour cette propriété sont fournies dans la section [ de l’](#producedBy)annexe. Ce champ est un enum extensible, ce qui signifie que vous pouvez également utiliser vos propres chaînes pour représenter différents producteurs de événement. |
| `identityMap` | Champ de mappage contenant un ensemble d’identités d’espacement de noms pour la personne à laquelle le événement s’applique. Ce champ est automatiquement mis à jour par le système lorsque des données d&#39;identité sont saisies. Afin d’utiliser correctement ce champ pour [Profil client en temps réel](../../profile/home.md), n’essayez pas de mettre à jour manuellement le contenu du champ dans vos opérations de données.<br /><br />Consultez la section sur les cartes d&#39;identité dans les  [bases de la ](../schema/composition.md#identityMap) composition de schémas pour plus d&#39;informations sur leur cas d&#39;utilisation. |
| `timestamp` | Horodatage ISO 8601 indiquant le moment où le événement s’est produit, formaté selon la section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) du [RFC 339. Cet horodatage doit se produire dans le passé. Consultez la section suivante sur [horodatages](#timestamps) pour connaître les meilleures pratiques d&#39;utilisation de ce champ. |

## Meilleures pratiques pour la modélisation des événements

Les sections suivantes décrivent les meilleures pratiques de conception de vos schémas de modèle de données d’expérience (XDM) basés sur un événement dans Adobe Experience Platform.

### Horodatages {#timestamps}

Le champ racine `timestamp` d&#39;un schéma de événement peut **uniquement** représenter l&#39;observation du événement lui-même et doit se produire dans le passé. Si les cas d’utilisation de la segmentation nécessitent l’utilisation d’horodatages qui peuvent se produire dans le futur, ces valeurs doivent être restreintes ailleurs dans votre schéma de Événement d’expérience.

Par exemple, si une entreprise de l&#39;industrie du voyage et de l&#39;accueil modélise un événement de réservation de vol, le champ classe `timestamp` représente le moment où le événement de réservation a été observé. Les autres horodatages liés au événement, tels que la date de début de la réservation de voyage, doivent être saisis dans des champs distincts fournis par des mixins standard ou personnalisés.

![](../images/classes/experienceevent/timestamps.png)

En séparant l’horodatage au niveau de la classe des autres valeurs datetime associées dans vos schémas de événement, vous pouvez mettre en oeuvre des cas d’utilisation de la segmentation flexible tout en conservant un compte horodaté des parcours de client dans votre application d’expérience.

### Utilisation des champs calculés

Certaines interactions dans vos applications d’expérience peuvent entraîner plusieurs événements liés qui partagent techniquement le même horodatage de événement et peuvent donc être représentés sous la forme d’un enregistrement de événement unique. Par exemple, si un client vue un produit sur votre site Web, cela peut entraîner un enregistrement de événement contenant à la fois des attributs de &quot;vue de produit&quot; et certains attributs de &quot;vue de page&quot; génériques qui se chevauchent. Dans ces cas, vous pouvez utiliser des champs calculés pour capturer les attributs les plus importants lorsque plusieurs événements sont capturés dans un enregistrement.

[Adobe Experience Platform Data ](../../data-prep/home.md) Preppermet de mapper, de transformer et de valider des données vers et depuis XDM. A l&#39;aide des fonctions de mappage [disponibles](../../data-prep/functions.md) fournies par le service, vous pouvez appeler des opérateurs logiques pour établir des priorités, transformer et/ou consolider des données à partir d&#39;enregistrements à plusieurs événements lors de leur assimilation à un Experience Platform.

Si vous importez manuellement des données dans la plate-forme via l’interface utilisateur, consultez le guide [mappage d’un fichier CSV à XDM](../../ingestion/tutorials/map-a-csv-file.md) pour obtenir des instructions spécifiques sur la création de champs calculés.

Si vous diffusez des données sur la plate-forme à l’aide d’une connexion source, vous pouvez configurer la source pour qu’elle utilise à la place les champs calculés. Consultez la [documentation de votre source particulière](../../sources/home.md) pour savoir comment implémenter des champs calculés lors de la configuration de la connexion.

## Groupes de champs de schéma compatibles {#field-groups}

>[!NOTE]
>
>Les noms de plusieurs groupes de champs ont changé. Pour plus d’informations, consultez le document [mise à jour du nom du groupe de champs](../field-groups/name-updates.md).

Adobe fournit plusieurs groupes de champs standard à utiliser avec la classe [!DNL XDM ExperienceEvent]. Voici une liste de certains groupes de champs couramment utilisés pour la classe :

* [[!UICONTROL Détails de l’ID d’utilisateur final]](../field-groups/event/enduserids.md)
* [[!UICONTROL Détails de l&#39;Environnement]](../field-groups/event/environment-details.md)

## Annexe

La section suivante contient des informations supplémentaires sur la classe [!UICONTROL XDM ExperienceEvent].

### Valeurs acceptées pour `eventType` {#eventType}

Le tableau suivant présente les valeurs acceptées pour `eventType`, ainsi que leurs définitions :

| Valeur | Définition |
| --- | --- |
| `advertising.completes` | Un fichier multimédia chronométré a été visionné jusqu’à la fin. Cela ne signifie pas nécessairement que le spectateur a visionné la vidéo dans son intégralité, car il aurait pu sauter devant. |
| `advertising.timePlayed` | Décrit le temps passé par un utilisateur sur une ressource multimédia minutée spécifique. |
| `advertising.federated` | Indique si un Événement d’expérience a été créé par le biais d’une fédération de données (partage de données entre clients). |
| `advertising.clicks` | Cliquez sur une ou plusieurs actions sur une publicité. |
| `advertising.conversions` | Action(s) prédéfinie(s) exécutée(s) par un client qui déclenche un événement pour l&#39;évaluation des performances. |
| `advertising.firstQuartiles` | Une publicité vidéo numérique a été lue pendant 25 % de sa durée à une vitesse normale. |
| `advertising.impressions` | Impression d’une publicité destinée à un client susceptible d’être consultée. |
| `advertising.midpoints` | Une publicité vidéo numérique a été lue pendant 50% de sa durée à une vitesse normale. |
| `advertising.starts` | La lecture d&#39;une publicité vidéo numérique a commencé. |
| `advertising.thirdQuartiles` | Une publicité vidéo numérique a été lue pendant 75 % de sa durée à une vitesse normale. |
| `web.webpagedetails.pageViews` | Une page Web a reçu une ou plusieurs vues. |
| `web.webinteraction.linkClicks` | Un lien a été sélectionné une ou plusieurs fois. |
| `commerce.checkouts` | Un événement de passage en caisse s&#39;est produit pour une liste de produits. Il peut y avoir plusieurs événements de passage en caisse s&#39;il y a plusieurs étapes dans un processus de passage en caisse. S’il existe plusieurs étapes, l’horodatage et la page/expérience référencée pour chaque événement sont utilisés pour identifier chaque événement (étape) individuel, représenté dans l’ordre. |
| `commerce.productListAdds` | Un produit a été ajouté à la liste de produits ou au panier. |
| `commerce.productListOpens` | Une nouvelle liste de produits (panier) a été initialisée ou créée. |
| `commerce.productListRemovals` | Une ou plusieurs entrées de produits ont été supprimées d’une liste de produits ou d’un panier. |
| `commerce.productListReopens` | Une liste de produit (panier) qui n’était plus accessible (abandonnée) a été réactivée par un client, par exemple par le biais d’une activité de marketing de relance. |
| `commerce.productListViews` | Une liste de produit ou un panier d’achat a reçu une ou plusieurs vues. |
| `commerce.productViews` | Un produit a reçu une ou plusieurs vues. |
| `commerce.purchases` | Une commande a été acceptée. Il s’agit de la seule action requise dans une conversion commerciale. Une liste de produit doit être référencée pour un événement d’achat. |
| `commerce.saveForLaters` | Une liste de produit a été enregistrée pour une utilisation ultérieure, telle une liste de souhaits de produit. |
| `delivery.feedback` | Événements de commentaires pour une diffusion, telle qu’une diffusion de courriel. |
| `message.feedback` | Événements de commentaires tels que envoyé/rebond/erreur pour les messages envoyés à un client. |
| `message.tracking` | Suivi de événements tels que des actions d’ouverture/clic/personnalisation sur les messages envoyés à un client. |

### Valeurs suggérées pour `producedBy` {#producedBy}

Le tableau suivant présente quelques valeurs acceptées pour `producedBy` :

| Valeur | Définition |
| --- | --- |
| `self` | Auto |
| `system` | Système |
| `salesRef` | Représentant commercial |
| `customerRep` | Représentant du client |
