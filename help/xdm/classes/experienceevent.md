---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;identityMap;mappage dʼidentités;Mappage dʼidentités;Conception du schéma;mappage;Mappage;modélisation des événements;modélisation d’événements;bonnes pratiques;événement;événements;
solution: Experience Platform
title: Classe XDM ExperienceEvent
description: Découvrez la classe XDM ExperienceEvent et les bonnes pratiques pour la modélisation des données d’événement.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 5537485206c1625ca661d6b33f7bba08538a0fa3
workflow-type: tm+mt
source-wordcount: '2761'
ht-degree: 38%

---

# Classe [!DNL XDM ExperienceEvent]

[!DNL XDM ExperienceEvent] est une classe XDM (Experience Data Model) standard. Utilisez cette classe pour créer un instantané horodaté du système lorsqu’un événement spécifique se produit ou qu’un certain ensemble de conditions a été atteint.

Un événement dʼexpérience est un enregistrement factuel de ce qui s’est passé, y compris le moment et l’identité de la personne impliquée. Les événements peuvent être explicites (actions humaines directement observables) ou implicites (obtenus sans action humaine directe) et sont enregistrés sans agrégation ni interprétation. Pour plus d’informations détaillées sur l’utilisation de cette classe dans l’écosystème Platform, consultez la section [Présentation du système XDM](../home.md#data-behaviors).

La classe [!DNL XDM ExperienceEvent] elle-même fournit plusieurs champs temporels à un schéma. Deux de ces champs (`_id` et `timestamp`) sont **obligatoires** pour tous les schémas basés sur cette classe, tandis que les autres sont facultatifs. Les valeurs de certains champs sont automatiquement renseignées lors de l’ingestion des données.

![Structure de XDM ExperienceEvent telle qu’elle apparaît dans l’interface utilisateur de Platform.](../images/classes/experienceevent/structure.png)

| Propriété | Description |
| --- | --- |
| `_id`<br>**(Obligatoire)** | Le champ Classe d’événements d’expérience `_id` identifie de manière unique les événements individuels ingérés dans Adobe Experience Platform. Ce champ permet de suivre l’unicité d’un événement individuel, d’éviter la duplication des données et de rechercher cet événement dans les services en aval.<br><br> Lorsque des événements en double sont détectés, les applications et services de Platform peuvent gérer la duplication différemment. Par exemple, les événements en double dans le service de profil sont ignorés si l’événement ayant le même `_id` existe déjà dans la banque de profils.<br><br>Dans certains cas, `_id` peut être un [identifiant unique universel (UUID)](https://datatracker.ietf.org/doc/html/rfc4122) ou un [identifiant unique global (GUID)](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Si vous diffusez des données depuis une connexion source ou que vous ingérez directement depuis un fichier Parquet, vous devez générer cette valeur en concaténant une certaine combinaison de champs qui rendent l’événement unique. Parmi les exemples d’événements pouvant être concaténés, citons l’ID principal, l’horodatage, le type d’événement, etc. La valeur concaténée doit être une chaîne formatée `uri-reference`, ce qui signifie que tout caractère deux-points doit être supprimé. La valeur concaténée doit ensuite être hachée à l’aide de lʼalgorithme SHA-256 ou d’un autre de votre choix.<br><br>Il est important de distinguer que **ce champ ne représente pas une identité liée à une personne individuelle**, mais plutôt lʼenregistrement de données lui-même. Les données d’identité relatives à une personne doivent plutôt être reléguées dans des [champs d’identité](../schema/composition.md#identity) fournis par des groupes de champs compatibles. |
| `eventMergeId` | Si vous utilisez le [SDK web Adobe Experience Platform](/help/web-sdk/home.md) pour lʼingestion des données, cela représente l’identifiant du lot ingéré à l’origine de la création de l’enregistrement. Ce champ est automatiquement renseigné par le système lors de l’ingestion des données. L’utilisation de ce champ en dehors du cadre d’une implémentation du SDK web n’est pas prise en charge. |
| `eventType` | Chaîne indiquant le type ou la catégorie de l’événement. Ce champ peut être utilisé pour distinguer différents types d’événements au sein dʼun même schéma et dʼun même jeu de données. Par exemple, pour une société active dans la vente au détail, vous pouvez souhaiter distinguer un événement de consultation de produit d’un événement dʼajout au panier.<br><br>Les valeurs standard de cette propriété sont fournies dans la [section annexe](#eventType), y compris des descriptions de leur cas d’utilisation prévu. Ce champ est une énumération extensible, ce qui signifie que vous pouvez également utiliser vos propres chaînes de type d’événement pour classer les événements dont vous effectuez le suivi.La propriété <br><br>`eventType` vous limite à l’utilisation d’un seul événement par accès sur votre application. Par conséquent, vous devez utiliser des champs calculés pour indiquer au système quel événement est le plus important. Pour plus d’informations, consultez la section dédiée aux [bonnes pratiques relatives aux champs calculés](#calculated). |
| `producedBy` | Valeur de chaîne qui décrit le déclencheur ou l’origine de l’événement. Ce champ peut être utilisé, si nécessaire, pour filtrer certains déclencheurs d’événements à des fins de segmentation.<br><br>Certaines valeurs suggérées pour cette propriété sont indiquées dans la [section annexe](#producedBy). Ce champ est une énumération extensible, ce qui signifie que vous pouvez également utiliser vos propres chaînes pour représenter différents déclencheurs d’événements. |
| `identityMap` | Champ de mappage contenant un jeu d’identités d’espace de noms pour l’individu auquel l’événement s’applique. Ce champ est automatiquement mis à jour par le système lors de l’ingestion des données d’identité. Pour utiliser correctement ce champ pour [Real-time Customer Profile](../../profile/home.md), ne tentez pas de mettre à jour manuellement le contenu du champ dans vos opérations de données.<br /><br />Pour plus d’informations sur les cas d’utilisation des mappages dʼidentités, consultez la section correspondante sur la page consacrée aux [principes de base de la composition des schémas](../schema/composition.md#identityMap). |
| `timestamp`<br>**(Obligatoire)** | Horodatage ISO 8601 du moment où l’événement s’est produit, formaté selon la norme [RFC 3339 (section 5.6)](https://datatracker.ietf.org/doc/html/rfc3339). Cet horodatage **must** se produit par le passé, mais **must** a lieu à partir de 1970. Pour connaître les bonnes pratiques relatives à l’utilisation de ce champ, consultez la section ci-dessous relative aux [horodatages](#timestamps). |

{style="table-layout:auto"}

## Bonnes pratiques relatives à la modélisation des événements

Les sections suivantes décrivent les bonnes pratiques pour la conception de vos schémas XDM (Modèle de données d’expérience) basés sur des événements dans Adobe Experience Platform.

### Horodatages {#timestamps}

Le champ racine `timestamp` d’un schéma d’événement peut **uniquement** représenter l’observation de l’événement lui-même et doit se produire dans le passé. Cependant, l&#39;événement **must** a lieu à partir de 1970. Si vos cas d’utilisation de segmentation nécessitent l’utilisation d’horodatages qui peuvent se produire dans le futur, ces valeurs doivent être inscrites ailleurs dans votre schéma d’événement d’expérience.

Par exemple, si une entreprise active dans le secteur du voyage et de l’hôtellerie modélise un événement de réservation de vol, le champ `timestamp` au niveau de la classe représente lʼheure à laquelle l’événement de réservation a été observé. D’autres horodatages liés à l’événement, tels que la date de début de la réservation de voyage, doivent être capturés dans des champs distincts fournis par des groupes de champs standard ou personnalisés.

![Exemple de schéma d&#39;événement d&#39;expérience avec réservation de vol et date de début en surbrillance.](../images/classes/experienceevent/timestamps.png)

En séparant l’horodatage au niveau de la classe des autres valeurs datetime associées dans vos schémas d’événement, vous pouvez implémenter des cas d’utilisation de segmentation flexibles tout en conservant un compte horodaté des parcours client dans votre application d’expérience.

### Utiliser des champs calculés {#calculated}

Certaines interactions dans vos applications d’expérience peuvent entraîner plusieurs événements associés partageant techniquement le même horodatage d’événement et pouvant donc être représentés comme un seul enregistrement d’événement. Si, par exemple, un client consulte un produit sur votre site web, un enregistrement d’événement comportant deux valeurs `eventType` potentielles peut être généré : un événement « vue du produit » (`commerce.productViews`) ou un événement générique « page vue » (`web.webpagedetails.pageViews`). Dans ces cas, vous pouvez utiliser des champs calculés pour capturer les attributs les plus importants lors d’une capture de plusieurs événements dans un seul accès.

Utilisez [Adobe Experience Platform Data Prep](../../data-prep/home.md) pour mapper, transformer et valider des données vers et depuis XDM. En utilisant les [fonctions de mappage](../../data-prep/functions.md) fournies par le service, vous pouvez appeler des opérateurs logiques pour prioriser, transformer et/ou consolider des données provenant d’enregistrements multi-événements lors de leur ingestion dans Experience Platform. Dans l’exemple ci-dessus, vous pouvez désigner `eventType` comme champ calculé qui donne la priorité à une « vue du produit » plutôt qu’à une « vue de page » lorsquʼelles se produisent toutes les deux.

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
* [[!UICONTROL Détails de l’interaction MediaAnalytics]](../field-groups/event/mediaanalytics-interaction.md)
* [[!UICONTROL Détails de la demande de devis]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Détails de la réservation]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Détails web]](../field-groups/event/web-details.md)

## Annexe

La section suivante contient des informations supplémentaires sur la classe [!UICONTROL XDM ExperienceEvent].

### Valeurs acceptées pour `eventType` {#eventType}

Le tableau suivant décrit les valeurs acceptées pour `eventType`, ainsi que leurs définitions :

| Valeur | Définition |
| --- | --- |
| `advertising.clicks` | Cet événement suit le moment où une action de sélection d’une publicité se produit. |
| `advertising.completes` | Cet événement effectue le suivi lorsqu’une ressource multimédia minutée a été visionnée jusqu’à la fin. Cela ne signifie pas nécessairement que le spectateur a visionné toute la vidéo, car il aurait pu sauter devant. |
| `advertising.conversions` | Cet événement effectue le suivi d’une action prédéfinie effectuée par un client qui déclenche un événement pour l’évaluation des performances. |
| `advertising.federated` | Cet événement effectue le suivi de la création ou non d’un événement d’expérience par le biais d’une fédération de données (partage de données entre clients). |
| `advertising.firstQuartiles` | Cet événement effectue le suivi lorsqu’une publicité vidéo numérique a été lue pendant 25 % de sa durée à une vitesse normale. |
| `advertising.impressions` | Cet événement suit les impressions d’une publicité destinée à un client ayant le potentiel d’être visionné. |
| `advertising.midpoints` | Cet événement effectue le suivi lorsqu’une publicité vidéo numérique a été lue pendant 50 % de sa durée à une vitesse normale. |
| `advertising.starts` | Cet événement effectue le suivi du début de la lecture d’une publicité vidéo numérique. |
| `advertising.thirdQuartiles` | Cet événement effectue le suivi lorsqu’une publicité vidéo numérique a été lue pendant 75 % de sa durée à une vitesse normale. |
| `advertising.timePlayed` | Cet événement effectue le suivi de la durée passée par un utilisateur sur une ressource multimédia minutée spécifique. |
| `application.close` | Cet événement suit le moment où une application a été fermée ou envoyée en arrière-plan. |
| `application.launch` | Cet événement suit le moment où une application a été lancée ou mise en premier plan. |
| `click` | **Obsolète** Utilisez à la place `decisioning.propositionInteract`. |
| `commerce.backofficeCreditMemoIssued` | Cet événement suit lorsqu’un avis de crédit a été émis à un client. |
| `commerce.backofficeOrderCancelled` | Cet événement effectue le suivi lorsqu’un processus d’achat initié précédemment a été arrêté avant la fin. |
| `commerce.backofficeOrderItemsShipped` | Cet événement suit le moment où les articles achetés ont été physiquement envoyés au client. |
| `commerce.backofficeOrderPlaced` | Cet événement suit le placement d’une commande. |
| `commerce.backofficeShipmentCompleted` | Cet événement effectue le suivi de la réussite de l’ensemble du processus d’expédition. |
| `commerce.checkouts` | Cet événement effectue le suivi lorsqu’un événement de passage en caisse s’est produit pour une liste de produits. Il peut y avoir plusieurs événements de passage en caisse s’il existe plusieurs étapes dans un processus de passage en caisse. S’il y a plusieurs étapes, l’horodatage et la page/expérience référencée pour chaque événement sont utilisés pour identifier chaque événement individuel (étape), représenté dans l’ordre. |
| `commerce.productListAdds` | Cet événement effectue le suivi lorsqu’un produit a été ajouté à la liste de produits ou au panier. |
| `commerce.productListOpens` | Cet événement suit lorsqu’une nouvelle liste de produits (panier) a été initialisée ou créée. |
| `commerce.productListRemovals` | Cet événement suit lorsqu’une entrée de produit a été supprimée d’une liste de produits ou d’un panier. |
| `commerce.productListReopens` | Cet événement suit lorsqu’une liste de produits (panier) qui n’était plus accessible (abandonnée) a été réactivée par un client, par exemple par le biais d’une activité de remarketing. |
| `commerce.productListViews` | Cet événement suit lorsqu’une liste de produits ou un panier a reçu une consultation. |
| `commerce.productViews` | Cet événement effectue le suivi lorsqu’un produit a reçu une ou plusieurs consultations. |
| `commerce.purchases` | Cet événement effectue le suivi lorsqu’une commande a été acceptée. Il s’agit de la seule action requise lors dʼune conversion commerciale. Un événement d’achat doit avoir une liste de produits référencée. |
| `commerce.saveForLaters` | Cet événement effectue le suivi lorsqu’une liste de produits a été enregistrée pour une utilisation ultérieure, telle qu’une liste de souhaits de produits. |
| `decisioning.propositionDisplay` | Cet événement est utilisé lorsque le SDK Web envoie automatiquement des informations sur les éléments affichés sur une page. Cependant, vous n’avez pas besoin de ce type d’événement si vous incluez déjà des informations d’affichage d’une autre manière, comme avec les accès en haut et en bas de page. Pour les accès en bas de page, vous pouvez choisir n’importe quel type d’événement de votre choix. |
| `decisioning.propositionDismiss` | Ce type d’événement est utilisé lorsqu’un message intégré à Adobe Journey Optimizer ou une carte de contenu est ignoré. |
| `decisioning.propositionFetch` | Utilisé pour indiquer qu’un événement sert principalement à récupérer la prise de décision. Adobe Analytics abandonnera cet événement automatiquement. |
| `decisioning.propositionInteract` | Ce type d’événement est utilisé pour effectuer le suivi des interactions, telles que les clics, sur le contenu personnalisé. |
| `decisioning.propositionSend` | Cet événement suit le moment où il a été décidé d’envoyer à un client potentiel une recommandation ou une offre à prendre en compte. |
| `decisioning.propositionTrigger` | Les événements de ce type sont stockés en local par le [SDK Web](../../web-sdk/home.md), mais ne sont pas envoyés à Experience Edge. Chaque fois qu’un ensemble de règles est satisfait, un événement est généré et stocké dans un stockage local (si ce paramètre est activé). |
| `delivery.feedback` | Cet événement effectue le suivi des événements de retour pour une diffusion, tels qu’une diffusion par email. |
| `directMarketing.emailBounced` | Cet événement suit le moment où un message électronique à une personne a fait l’objet d’un rebond. |
| `directMarketing.emailBouncedSoft` | Cet événement suit le moment où un email à une personne rebondit doucement. |
| `directMarketing.emailClicked` | Cet événement suit le moment où une personne a cliqué sur un lien dans un courrier électronique marketing. |
| `directMarketing.emailDelivered` | Cet événement suit le moment où un message électronique a été correctement envoyé au service de messagerie d’une personne. |
| `directMarketing.emailOpened` | Cet événement est suivi lorsqu’une personne a ouvert un courrier électronique marketing. |
| `directMarketing.emailSent` | Cet événement suit le moment où un email marketing a été envoyé à une personne. |
| `directMarketing.emailUnsubscribed` | Cet événement suit lorsqu’une personne se désabonne d’un email marketing. |
| `display` | **Obsolète** Utilisez à la place `decisioning.propositionDisplay`. |
| `inappmessageTracking.dismiss` | Cet événement suit le rejet d’un message in-app. |
| `inappmessageTracking.display` | Cet événement effectue le suivi de l’affichage d’un message in-app. |
| `inappmessageTracking.interact` | Cet événement suit le moment où un message in-app a été interagi avec . |
| `leadOperation.callWebhook` | Cet événement suit le moment où un webhook a été appelé en réponse à une piste. |
| `leadOperation.changeCampaignStream` | Cet événement signifie un changement dans la stratégie de marketing ou d’engagement pour un prospect particulier. |
| `leadOperation.changeEngagementCampaignCadence` | Cet événement effectue le suivi lorsqu’un prospect a été modifié dans le cadre d’une campagne. |
| `leadOperation.convertLead` | Cet événement effectue le suivi lorsqu’une piste a été convertie. |
| `leadOperation.interestingMoment` | Cet événement suit quand un moment intéressant a été enregistré pour une personne. |
| `leadOperation.mergeLeads` | Cet événement suit le moment où les informations provenant de plusieurs pistes qui font référence à la même entité ont été consolidées. |
| `leadOperation.newLead` | Cet événement effectue le suivi de la création d’une piste. |
| `leadOperation.scoreChanged` | Cet événement suit le moment où la valeur de l’attribut de score du prospect a été modifiée. |
| `leadOperation.statusInCampaignProgressionChanged` | Cet événement suit le moment où l’état d’une piste dans une campagne a changé. |
| `listOperation.addToList` | Cet événement suit le moment où une personne a été ajoutée à une liste marketing. |
| `listOperation.removeFromList` | Cet événement suit le moment où une personne a été supprimée d’une liste marketing. |
| `media.adBreakComplete` | Cet événement signale la fin d’une coupure publicitaire. |
| `media.adBreakStart` | Cet événement signale le début d’une coupure publicitaire. |
| `media.adComplete` | Cet événement signale la fin d’une publicité. |
| `media.adSkip` | Cet événement signale lorsqu’une publicité a été ignorée. |
| `media.adStart` | Cet événement signale le début d’une publicité. |
| `media.bitrateChange` | Cet événement signale un changement de débit. |
| `media.bufferStart` | Le type d’événement `media.bufferStart` est envoyé au début de la mise en mémoire tampon. Il n’existe pas de type d’événement `bufferResume` spécifique ; la mise en mémoire tampon est considérée comme ayant repris lorsqu’un événement `play` est envoyé suite à un événement `bufferStart`. |
| `media.chapterComplete` | Cet événement signale la fin d’un chapitre. |
| `media.chapterSkip` | Cet événement est déclenché lorsqu’un utilisateur passe d’une section ou d’un chapitre à l’autre ou en revient en arrière. |
| `media.chapterStart` | Cet événement signale le début d’un chapitre. |
| `media.downloaded` | Cet événement effectue le suivi lorsque le contenu téléchargé par le média s’est produit. |
| `media.error` | Cet événement signale lorsqu’une erreur s’est produite au cours de la lecture multimédia. |
| `media.pauseStart` | Cet événement effectue le suivi lorsqu’un événement `pauseStart` s’est produit. Cet événement est déclenché lorsqu’un utilisateur lance une pause dans la lecture multimédia. Il n’existe aucun type d’événement resume . Une reprise est déduite lorsque vous envoyez un événement de lecture après un `pauseStart`. |
| `media.ping` | Le type d’événement `media.ping` est utilisé pour indiquer l’état de lecture en cours. Pour le contenu principal, cet événement doit être envoyé toutes les 10 secondes pendant la lecture, en commençant 10 secondes après le début de la lecture. Pour le contenu de la publicité, il doit être envoyé toutes les secondes pendant le suivi publicitaire. Les événements ping ne doivent pas inclure la carte params dans le corps de la requête. |
| `media.play` | Le type d’événement `media.play` est envoyé lorsque le lecteur passe à l’état `playing` à partir d’un autre état, tel que `buffering,` `paused` (lorsqu’il est repris par l’utilisateur) ou `error` (lorsqu’il est récupéré), y compris les scénarios de lecture automatique. Cet événement est déclenché par le rappel `on('Playing')` du lecteur. |
| `media.sessionComplete` | Cet événement est envoyé lorsque la fin du contenu principal est atteinte. |
| `media.sessionEnd` | Le type d’événement `media.sessionEnd` avertit le serveur principal Media Analytics de fermer immédiatement une session lorsqu’un utilisateur abandonne l’affichage et ne risque pas de revenir. Si cet événement n’est pas envoyé, la session expire après 10 minutes d’inactivité ou 30 minutes sans mouvement du curseur de lecture. Tous les appels de médias suivants avec cet ID de session seront ignorés. |
| `media.sessionStart` | Le type d’événement `media.sessionStart` est envoyé avec l’appel de lancement de session. Lors de la réception d’une réponse, l’ID de session est extrait de l’en-tête Emplacement et utilisé pour tous les appels d’événement suivants au serveur de collecte. |
| `media.statesUpdate` | Cet événement effectue le suivi lorsqu’un événement `statesUpdate` s’est produit. Les fonctionnalités de suivi de l’état du lecteur peuvent être associées à un flux audio ou vidéo. Les états standard sont : `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` et `inFocus`. |
| `opportunityEvent.addToOpportunity` | Cet événement suit le moment où une personne a été ajoutée à une opportunité. |
| `opportunityEvent.opportunityUpdated` | Cet événement suit le moment où une opportunité a été mise à jour. |
| `opportunityEvent.removeFromOpportunity` | Cet événement suit le moment où une personne a été supprimée d’une opportunité. |
| `personalization.request` | **Obsolète** Utilisez à la place `decisioning.propositionFetch`. |
| `pushTracking.applicationOpened` | Cet événement est suivi lorsqu’une personne a ouvert une application à partir d’une notification push. |
| `pushTracking.customAction` | Cet événement suit lorsqu’une personne a sélectionné une action personnalisée dans une notification push. |
| `web.formFilledOut` | Cet événement suit le moment où une personne remplit un formulaire sur une page web. |
| `web.webinteraction.linkClicks` | L’événement signale qu’un clic sur un lien a été automatiquement enregistré par le SDK Web. |
| `web.webpagedetails.pageViews` | Ce type d’événement est la méthode standard pour marquer l’accès en tant que page vue. |
| `location.entry` | Cet événement effectue le suivi de l’entrée d’une personne ou d’un appareil à un emplacement spécifique. |
| `location.exit` | Cet événement effectue le suivi de la sortie d’une personne ou d’un appareil à partir d’un emplacement spécifique. |

{style="table-layout:auto"}

### Valeurs suggérées pour `producedBy` {#producedBy}

Le tableau suivant présente quelques-unes des valeurs acceptées pour `producedBy` :

| Valeur | Définition |
| --- | --- |
| `self` | Self |
| `system` | Système |
| `salesRef` | Représentant commercial |
| `customerRep` | Représentant du client |
