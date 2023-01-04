---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;identityMap;mappage dʼidentités;Mappage dʼidentités;Conception du schéma;mappage;Mappage;modélisation des événements;modélisation d’événements;bonnes pratiques;événement;événements;
solution: Experience Platform
title: Classe XDM ExperienceEvent
topic-legacy: overview
description: Ce document présente la classe XDM ExperienceEvent et décrit les bonnes pratiques pour la modélisation des données d’événement.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1830'
ht-degree: 95%

---

# Classe [!DNL XDM ExperienceEvent]

[!DNL XDM ExperienceEvent] est une classe XDM (modèle de données d’expérience) standard, qui vous permet de créer un instantané horodaté du système lorsqu’un événement spécifique se produit ou qu’un certain ensemble de conditions a été atteint.

Un événement dʼexpérience est un enregistrement factuel de ce qui s’est passé, y compris le moment et l’identité de la personne impliquée. Les événements peuvent être explicites (actions humaines directement observables) ou implicites (obtenus sans action humaine directe) et sont enregistrés sans agrégation ni interprétation. Pour plus d’informations détaillées sur l’utilisation de cette classe dans l’écosystème Platform, consultez la section [Présentation du système XDM](../home.md#data-behaviors).

La classe [!DNL XDM ExperienceEvent] elle-même fournit plusieurs champs temporels à un schéma. Deux de ces champs (`_id` et `timestamp`) sont **required** pour tous les schémas basés sur la classe , tandis que les autres sont facultatifs. Les valeurs de certains champs sont automatiquement renseignées lors de l’ingestion des données.

![Structure de XDM ExperienceEvent telle qu’elle apparaît dans l’interface utilisateur de Platform](../images/classes/experienceevent/structure.png)

| Propriété | Description |
| --- | --- |
| `_id`<br>**(Obligatoire)** | Identifiant de chaîne unique pour lʼévénement. Ce champ permet de déterminer l’unicité d’un événement individuel, d’éviter la duplication des données et de rechercher cet événement dans les services en aval. Dans certains cas, `_id` peut être un [Identifiant universel unique (UUID)](https://tools.ietf.org/html/rfc4122) ou un [Identifiant global unique (GUID)](https://docs.microsoft.com/fr-fr/dotnet/api/system.guid?view=net-5.0).<br><br>Si vous diffusez des données en continu à partir dʼune connexion source ou si vous ingérez directement à partir d’un fichier parquet, vous devez générer cette valeur en concaténant une certaine combinaison de champs qui rendent l’événement unique, comme un identifiant principal, un horodatage, un type d’événement, etc. La valeur concaténée doit être une chaîne formatée `uri-reference`, ce qui signifie que tout caractère deux-points doit être supprimé. La valeur concaténée doit ensuite être hachée à l’aide de lʼalgorithme SHA-256 ou d’un autre de votre choix.<br><br>Il est important de distinguer que **ce champ ne représente pas une identité liée à une personne individuelle**, mais plutôt lʼenregistrement de données lui-même. Les données d’identité relatives à une personne doivent plutôt être reléguées dans des [champs d’identité](../schema/composition.md#identity) fournis par des groupes de champs compatibles. |
| `eventMergeId` | Si vous utilisez le [SDK web Adobe Experience Platform](../../edge/home.md) pour lʼingestion des données, cela représente l’identifiant du lot ingéré à l’origine de la création de l’enregistrement. Ce champ est automatiquement renseigné par le système lors de l’ingestion des données. L’utilisation de ce champ en dehors du cadre d’une implémentation du SDK web n’est pas prise en charge. |
| `eventType` | Chaîne indiquant le type ou la catégorie de l’événement. Ce champ peut être utilisé pour distinguer différents types d’événements au sein dʼun même schéma et dʼun même jeu de données. Par exemple, pour une société active dans la vente au détail, vous pouvez souhaiter distinguer un événement de consultation de produit d’un événement dʼajout au panier.<br><br>Les valeurs standard de cette propriété sont fournies dans la [section annexe](#eventType), y compris des descriptions de leur cas d’utilisation prévu. Ce champ est une énumération extensible, ce qui signifie que vous pouvez également utiliser vos propres chaînes de type d’événement pour classer les événements dont vous effectuez le suivi.La propriété <br><br>`eventType` vous limite à l’utilisation d’un seul événement par accès sur votre application. Par conséquent, vous devez utiliser des champs calculés pour indiquer au système quel événement est le plus important. Pour plus d’informations, consultez la section dédiée aux [bonnes pratiques relatives aux champs calculés](#calculated). |
| `producedBy` | Valeur de chaîne qui décrit le déclencheur ou l’origine de l’événement. Ce champ peut être utilisé, si nécessaire, pour filtrer certains déclencheurs d’événements à des fins de segmentation.<br><br>Certaines valeurs suggérées pour cette propriété sont indiquées dans la [section annexe](#producedBy). Ce champ est une énumération extensible, ce qui signifie que vous pouvez également utiliser vos propres chaînes pour représenter différents déclencheurs d’événements. |
| `identityMap` | Champ de mappage contenant un jeu d’identités d’espace de noms pour l’individu auquel l’événement s’applique. Ce champ est automatiquement mis à jour par le système lors de l’ingestion des données d’identité. Pour utiliser correctement ce champ pour [Profil client en temps réel](../../profile/home.md), ne tentez pas de mettre à jour manuellement le contenu du champ dans vos opérations de données.<br /><br />Pour plus d’informations sur les cas d’utilisation des mappages dʼidentités, consultez la section correspondante sur la page consacrée aux [principes de base de la composition des schémas](../schema/composition.md#identityMap). |
| `timestamp`<br>**(Obligatoire)** | Horodatage ISO 8601 du moment où l’événement s’est produit, formaté selon la norme [RFC 3339 (section 5.6)](https://tools.ietf.org/html/rfc3339#section-5.6). Cet horodatage doit se produire dans le passé. Pour connaître les bonnes pratiques relatives à l’utilisation de ce champ, consultez la section ci-dessous relative aux [horodatages](#timestamps). |

{style=&quot;table-layout:auto&quot;}

## Bonnes pratiques relatives à la modélisation des événements

Les sections suivantes décrivent les bonnes pratiques pour la conception de vos schémas XDM (Modèle de données d’expérience) basés sur des événements dans Adobe Experience Platform.

### Horodatages {#timestamps}

Le champ racine `timestamp` d’un schéma d’événement peut **uniquement** représenter l’observation de l’événement lui-même et doit se produire dans le passé. Si vos cas d’utilisation de segmentation nécessitent l’utilisation d’horodatages qui peuvent se produire dans le futur, ces valeurs doivent être inscrites ailleurs dans votre schéma d’événement d’expérience.

Par exemple, si une entreprise active dans le secteur du voyage et de l’hôtellerie modélise un événement de réservation de vol, le champ `timestamp` au niveau de la classe représente lʼheure à laquelle l’événement de réservation a été observé. D’autres horodatages liés à l’événement, tels que la date de début de la réservation de voyage, doivent être capturés dans des champs distincts fournis par des groupes de champs standard ou personnalisés.

![](../images/classes/experienceevent/timestamps.png)

En séparant l’horodatage au niveau de la classe des autres valeurs datetime associées dans vos schémas d’événement, vous pouvez implémenter des cas d’utilisation de segmentation flexibles tout en conservant un compte horodaté des parcours client dans votre application d’expérience.

### Utiliser des champs calculés {#calculated}

Certaines interactions dans vos applications d’expérience peuvent entraîner plusieurs événements associés partageant techniquement le même horodatage d’événement et pouvant donc être représentés comme un seul enregistrement d’événement. Si, par exemple, un client consulte un produit sur votre site web, un enregistrement d’événement comportant deux valeurs `eventType` potentielles peut être généré : un événement « vue du produit » (`commerce.productViews`) ou un événement générique « page vue » (`web.webpagedetails.pageViews`). Dans ces cas, vous pouvez utiliser des champs calculés pour capturer les attributs les plus importants lors d’une capture de plusieurs événements dans un seul accès.

La [Préparation de données Adobe Experience Platform](../../data-prep/home.md) vous permet de mapper, de transformer et de valider des données vers et depuis XDM. En utilisant les [fonctions de mappage](../../data-prep/functions.md) fournies par le service, vous pouvez appeler des opérateurs logiques pour prioriser, transformer et/ou consolider des données provenant d’enregistrements multi-événements lors de leur ingestion dans Experience Platform. Dans l’exemple ci-dessus, vous pouvez désigner `eventType` comme champ calculé qui donne la priorité à une « vue du produit » plutôt qu’à une « vue de page » lorsquʼelles se produisent toutes les deux.

Si vous ingérez manuellement des données dans Platform via l’interface utilisateur, consultez le guide sur les [champs calculés](../../data-prep/ui/mapping.md#calculated-fields) pour obtenir des instructions spécifiques sur la création de champs calculés.

Si vous diffusez des données en continu vers Platform à l’aide d’une connexion source, vous pouvez configurer la source pour qu’elle utilise à la place des champs calculés. Consultez la [documentation de votre source spécifique](../../sources/home.md) pour obtenir des instructions sur lʼimplémentation de champs calculés lors de la configuration de la connexion.

## Groupes de champs de schéma compatibles {#field-groups}

>[!NOTE]
>
>Les noms de plusieurs groupes de champs ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../field-groups/name-updates.md).

Adobe fournit plusieurs groupes de champs standard à utiliser avec la classe [!DNL XDM ExperienceEvent]. Voici une liste de groupes de champs couramment utilisés pour la classe :

* [[!UICONTROL Extension complète Adobe Analytics ExperienceEvent]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Transferts de solde]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL Détails de la campagne marketing]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Actions de carte]](../field-groups/event/card-actions.md)
* [[!UICONTROL Informations sur le canal]](../field-groups/event/channel-details.md)
* [[!UICONTROL Informations commerciales]](../field-groups/event/commerce-details.md)
* [[!UICONTROL Détails du dépôt]](../field-groups/event/deposit-details.md)
* [[!UICONTROL Informations sur la reprise des appareils]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL Réservation de restaurant]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL Informations sur l’identifiant de l’utilisateur final]](../field-groups/event/enduserids.md)
* [[!UICONTROL Détails de l’environnement]](../field-groups/event/environment-details.md)
* [[!UICONTROL Réservation de vol]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL Consentement IAB TCF 2.0]](../field-groups/event/iab.md)
* [[!UICONTROL Réservation de logement]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL Détails de la demande de devis]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Détails de la réservation]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Détails web]](../field-groups/event/web-details.md)

## Annexe

La section suivante contient des informations supplémentaires sur la classe [!UICONTROL XDM ExperienceEvent].

### Valeurs acceptées pour `eventType` {#eventType}

Le tableau suivant décrit les valeurs acceptées pour `eventType`, ainsi que leurs définitions :

| Valeur | Définition |
| --- | --- |
| `advertising.clicks` | Action(s) de clic sur une publicité. |
| `advertising.completes` | Une ressource multimédia minutée a été visionnée jusqu’à la fin. Cela ne signifie pas nécessairement que l’utilisateur a visionné l’ensemble de la vidéo, car il a pu avancer dans celle-ci. |
| `advertising.conversions` | Action(s) prédéfinie(s) exécutée(s) par un client qui déclenche(nt) un événement pour l’évaluation des performances. |
| `advertising.federated` | Indique si un événement d’expérience a été créé par le biais d’une fédération de données (partage de données entre clients). |
| `advertising.firstQuartiles` | Une publicité vidéo numérique a été lue pendant 25 % de sa durée à une vitesse normale. |
| `advertising.impressions` | Impression(s) d’une publicité destinée à un client ayant le potentiel d’être visualisée. |
| `advertising.midpoints` | Une publicité vidéo numérique a été lue pendant 50 % de sa durée à une vitesse normale. |
| `advertising.starts` | Une publicité vidéo numérique a commencé à être lue. |
| `advertising.thirdQuartiles` | Une publicité vidéo numérique a été lue pendant 75 % de sa durée à une vitesse normale. |
| `advertising.timePlayed` | Décrit le temps passé par un utilisateur sur un fichier multimédia minuté spécifique. |
| `application.close` | Une application a été fermée ou réduite en arrière-plan. |
| `application.launch` | Une application a été lancée ou mise en premier plan. |
| `commerce.checkouts` | Un événement de passage en caisse s’est produit pour une liste de produits. Il peut y avoir plusieurs événements de passage en caisse s’il existe plusieurs étapes dans un processus de passage en caisse. S’il y a plusieurs étapes, l’horodatage et la page/expérience référencée pour chaque événement sont utilisés pour identifier chaque événement individuel (étape), représenté dans l’ordre. |
| `commerce.productListAdds` | Un produit a été ajouté à la liste de produits ou au panier. |
| `commerce.productListOpens` | Une nouvelle liste de produits (panier) a été initialisée ou créée. |
| `commerce.productListRemovals` | Une ou plusieurs entrées de produits ont été supprimées d’une liste de produits ou d’un panier. |
| `commerce.productListReopens` | Une liste de produits (panier) qui n’était plus accessible (abandonnée) a été réactivée par un client, par exemple via une activité de remarketing. |
| `commerce.productListViews` | Une liste de produits ou un panier a été consulté une ou plusieurs fois. |
| `commerce.productViews` | Un produit a été consulté une ou plusieurs fois. |
| `commerce.purchases` | Une commande a été acceptée. Il s’agit de la seule action requise lors dʼune conversion commerciale. Un événement d’achat doit avoir une liste de produits référencée. |
| `commerce.saveForLaters` | Une liste de produits a été enregistrée pour une utilisation ultérieure. Par exemple, une liste de souhaits. |
| `decisioning.propositionDisplay` | Une proposition de prise de décision a été présentée à une personne. |
| `decisioning.propositionInteract` | Une personne a interagi avec une proposition de prise de décision. |
| `delivery.feedback` | Événements de retour pour une diffusion, telle qu’une diffusion par e-mail. |
| `directMarketing.emailBounced` | Un e-mail adressé à une personne a été retourné. |
| `directMarketing.emailBouncedSoft` | Un e-mail adressé à une personne nʼa pas été remis. |
| `directMarketing.emailClicked` | Une personne a cliqué sur un lien dans un e-mail marketing. |
| `directMarketing.emailDelivered` | Un e-mail a été correctement envoyé au service de messagerie de la personne. |
| `directMarketing.emailOpened` | Une personne a ouvert un e-mail marketing. |
| `directMarketing.emailUnsubscribed` | Une personne a annulé son abonnement à un e-mail marketing. |
| `inappmessageTracking.dismiss` | Un message in-app a été ignoré. |
| `inappmessageTracking.display` | Un message in-app a été affiché. |
| `inappmessageTracking.interact` | Un message in-app a fait l’objet d’une interaction. |
| `leadOperation.callWebhook` | un webhook a été appelé en réponse à un prospect. |
| `leadOperation.convertLead` | Un prospect a été converti. |
| `leadOperation.interestingMoment` | Un moment intéressant a été enregistré pour une personne. |
| `leadOperation.newLead` | Un prospect a été créé. |
| `leadOperation.scoreChanged` | La valeur de l’attribut de notation du prospect modifiée. |
| `leadOperation.statusInCampaignProgressionChanged` | Le statut d’un prospect dans une campagne a changé. |
| `listOperation.addToList` | Une personne a été ajoutée à une liste marketing. |
| `listOperation.removeFromList` | Une personne a été supprimée d’une liste marketing. |
| `message.feedback` | Événements de retour comme envoyé/bounce/erreur pour les messages envoyés à un client. |
| `message.tracking` | Événements de tracking tels que lʼouverture, le clic et les actions personnalisées sur les messages envoyés à un client. |
| `opportunityEvent.addToOpportunity` | Une personne a été ajoutée à une opportunité. |
| `opportunityEvent.opportunityUpdated` | Une opportunité a été mise à jour. |
| `opportunityEvent.removeFromOpportunity` | Une personne a été retirée d’une opportunité. |
| `pushTracking.applicationOpened` | Une personne a ouvert une application à partir d’une notification push. |
| `pushTracking.customAction` | Une personne a cliqué sur une action personnalisée dans une notification push. |
| `web.formFilledOut` | Une personne a rempli un formulaire sur une page web. |
| `web.webinteraction.linkClicks` | Un lien a été sélectionné une ou plusieurs fois. |
| `web.webpagedetails.pageViews` | Une page web a été consultée une ou plusieurs fois. |

{style=&quot;table-layout:auto&quot;}

### Valeurs suggérées pour `producedBy` {#producedBy}

Le tableau suivant présente quelques-unes des valeurs acceptées pour `producedBy` :

| Valeur | Définition |
| --- | --- |
| `self` | Self |
| `system` | Système |
| `salesRef` | Représentant commercial |
| `customerRep` | Représentant du client |
