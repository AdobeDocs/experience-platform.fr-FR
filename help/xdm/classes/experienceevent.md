---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;identityMap;mappage dʼidentités;Mappage dʼidentités;Conception du schéma;mappage;Mappage;modélisation des événements;modélisation d’événements;bonnes pratiques;événement;événements;
solution: Experience Platform
title: Classe XDM ExperienceEvent
description: Découvrez la classe XDM ExperienceEvent et les bonnes pratiques pour la modélisation des données d’événement.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: dc333f30f9a2cb7cd485d1cb13272c078da0bd76
workflow-type: tm+mt
source-wordcount: '2728'
ht-degree: 35%

---

# Classe [!DNL XDM ExperienceEvent]

[!DNL XDM ExperienceEvent] est une classe XDM (modèle de données d’expérience) standard. Utilisez cette classe pour créer un instantané horodaté du système lorsqu’un événement spécifique se produit ou qu’un certain ensemble de conditions a été atteint.

Un événement dʼexpérience est un enregistrement factuel de ce qui s’est passé, y compris le moment et l’identité de la personne impliquée. Les événements peuvent être explicites (actions humaines directement observables) ou implicites (obtenus sans action humaine directe) et sont enregistrés sans agrégation ni interprétation. Pour plus d’informations détaillées sur l’utilisation de cette classe dans l’écosystème Experience Platform, reportez-vous à la [ présentation de XDM](../home.md#data-behaviors).

La classe [!DNL XDM ExperienceEvent] elle-même fournit plusieurs champs temporels à un schéma. Deux de ces champs (`_id` et `timestamp`) sont **obligatoires** pour tous les schémas basés sur cette classe, tandis que les autres sont facultatifs. Les valeurs de certains champs sont automatiquement renseignées lors de l’ingestion des données.

![Structure de XDM ExperienceEvent tel qu’il apparaît dans l’interface utilisateur d’Experience Platform.](../images/classes/experienceevent/structure.png)

| Propriété | Description |
| --- | --- |
| `_id`<br>**(Obligatoire)** | Le champ `_id` de classe d’événements d’expérience identifie de manière unique les événements individuels qui sont ingérés dans Adobe Experience Platform. Ce champ permet de déterminer l’unicité d’un événement individuel, d’éviter la duplication des données et de rechercher cet événement dans les services en aval.<br><br>Lorsque des événements en double sont détectés, les applications et services Experience Platform peuvent gérer la duplication différemment. Par exemple, les événements en double dans le service de profil sont ignorés si l’événement portant le même `_id` existe déjà dans la banque de profils. Toutefois, ces événements sont toujours enregistrés dans le lac de données.<br><br>Dans certains cas, `_id` peut être un [Identifiant universel unique (UUID)](https://datatracker.ietf.org/doc/html/rfc4122) ou un [Identifiant global unique (GUID)](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Si vous diffusez des données à partir d’une connexion source ou si vous ingérez directement à partir d’un fichier Parquet, vous devez générer cette valeur en concaténant une certaine combinaison de champs qui rendent l’événement unique. Parmi les exemples d’événements qui peuvent être concaténés, citons l’identifiant principal, l’horodatage, le type d’événement, etc. La valeur concaténée doit être une chaîne formatée `uri-reference`, ce qui signifie que tout caractère deux-points doit être supprimé. La valeur concaténée doit ensuite être hachée à l’aide de lʼalgorithme SHA-256 ou d’un autre de votre choix.<br><br>Il est important de distinguer que **ce champ ne représente pas une identité liée à une personne individuelle**, mais plutôt lʼenregistrement de données lui-même. Les données d’identité relatives à une personne doivent plutôt être reléguées dans des [champs d’identité](../schema/composition.md#identity) fournis par des groupes de champs compatibles. |
| `eventMergeId` | Si vous utilisez le [SDK web Adobe Experience Platform](/help/collection/js/js-overview.md) pour lʼingestion des données, cela représente l’identifiant du lot ingéré à l’origine de la création de l’enregistrement. Ce champ est automatiquement renseigné par le système lors de l’ingestion des données. L’utilisation de ce champ en dehors du cadre d’une implémentation du SDK web n’est pas prise en charge. |
| `eventType` | Chaîne indiquant le type ou la catégorie de l’événement. Ce champ peut être utilisé pour distinguer différents types d’événements au sein dʼun même schéma et dʼun même jeu de données. Par exemple, pour une société active dans la vente au détail, vous pouvez souhaiter distinguer un événement de consultation de produit d’un événement dʼajout au panier.<br><br>Les valeurs standard de cette propriété sont fournies dans la [section annexe](#eventType), y compris des descriptions de leur cas d’utilisation prévu. Ce champ est une énumération extensible, ce qui signifie que vous pouvez également utiliser vos propres chaînes de type d’événement pour classer les événements dont vous effectuez le suivi.La propriété <br><br>`eventType` vous limite à l’utilisation d’un seul événement par accès sur votre application. Par conséquent, vous devez utiliser des champs calculés pour indiquer au système quel événement est le plus important. Pour plus d’informations, consultez la section dédiée aux [bonnes pratiques relatives aux champs calculés](#calculated). |
| `producedBy` | Valeur de chaîne qui décrit le déclencheur ou l’origine de l’événement. Ce champ peut être utilisé, si nécessaire, pour filtrer certains déclencheurs d’événements à des fins de segmentation.<br><br>Certaines valeurs suggérées pour cette propriété sont indiquées dans la [section annexe](#producedBy). Ce champ est une énumération extensible, ce qui signifie que vous pouvez également utiliser vos propres chaînes pour représenter différents déclencheurs d’événements. |
| `identityMap` | Champ de mappage contenant un jeu d’identités d’espace de noms pour l’individu auquel l’événement s’applique. Ce champ est automatiquement mis à jour par le système lors de l’ingestion des données d’identité. Pour utiliser correctement ce champ pour [Real-Time Customer Profile](../../profile/home.md), n’essayez pas de mettre à jour manuellement le contenu du champ dans vos opérations de données.<br /><br />Pour plus d’informations sur les cas d’utilisation des mappages dʼidentités, consultez la section correspondante sur la page consacrée aux [principes de base de la composition des schémas](../schema/composition.md#identityMap). |
| `timestamp`<br>**(Obligatoire)** | Horodatage ISO 8601 du moment où l’événement s’est produit, formaté selon la norme [RFC 3339 (section 5.6)](https://datatracker.ietf.org/doc/html/rfc3339). Cet horodatage **doit** se produire dans le passé, mais **doit** a lieu à partir de 1970. Pour connaître les bonnes pratiques relatives à l’utilisation de ce champ, consultez la section ci-dessous relative aux [horodatages](#timestamps). |

{style="table-layout:auto"}

## Bonnes pratiques relatives à la modélisation des événements

Les sections suivantes décrivent les bonnes pratiques pour la conception de vos schémas XDM (Modèle de données d’expérience) basés sur des événements dans Adobe Experience Platform.

### Horodatages {#timestamps}

Le champ racine `timestamp` d’un schéma d’événement peut **uniquement** représenter l’observation de l’événement lui-même et doit se produire dans le passé. Cependant, l&#39;événement **doit** se dérouler à partir de 1970. Si vos cas d’utilisation de segmentation nécessitent l’utilisation d’horodatages qui peuvent se produire dans le futur, ces valeurs doivent être inscrites ailleurs dans votre schéma d’événement d’expérience.

Par exemple, si une entreprise active dans le secteur du voyage et de l’hôtellerie modélise un événement de réservation de vol, le champ `timestamp` au niveau de la classe représente lʼheure à laquelle l’événement de réservation a été observé. D’autres horodatages liés à l’événement, tels que la date de début de la réservation de voyage, doivent être capturés dans des champs distincts fournis par des groupes de champs standard ou personnalisés.

![Exemple de schéma d’événement d’expérience avec réservation de vol et date de début en surbrillance.](../images/classes/experienceevent/timestamps.png)

En séparant l’horodatage au niveau de la classe des autres valeurs datetime associées dans vos schémas d’événement, vous pouvez implémenter des cas d’utilisation de segmentation flexibles tout en conservant un compte horodaté des parcours client dans votre application d’expérience.

### Utiliser des champs calculés {#calculated}

Certaines interactions dans vos applications d’expérience peuvent entraîner plusieurs événements associés partageant techniquement le même horodatage d’événement et pouvant donc être représentés comme un seul enregistrement d’événement. Si, par exemple, un client consulte un produit sur votre site web, un enregistrement d’événement comportant deux valeurs `eventType` potentielles peut être généré : un événement « vue du produit » (`commerce.productViews`) ou un événement générique « page vue » (`web.webpagedetails.pageViews`). Dans ces cas, vous pouvez utiliser des champs calculés pour capturer les attributs les plus importants lors d’une capture de plusieurs événements dans un seul accès.

Utilisez la préparation de données [Adobe Experience Platform](../../data-prep/home.md) pour mapper, transformer et valider les données vers et depuis XDM. En utilisant les [fonctions de mappage](../../data-prep/functions.md) fournies par le service, vous pouvez appeler des opérateurs logiques pour prioriser, transformer et/ou consolider des données provenant d’enregistrements multi-événements lors de leur ingestion dans Experience Platform. Dans l’exemple ci-dessus, vous pouvez désigner `eventType` comme champ calculé qui donne la priorité à une « vue du produit » plutôt qu’à une « vue de page » lorsquʼelles se produisent toutes les deux.

Si vous ingérez manuellement des données dans Experience Platform via l’interface utilisateur, consultez le guide sur les [champs calculés](../../data-prep/ui/mapping.md#calculated-fields) pour obtenir des instructions spécifiques sur la création de champs calculés.

Si vous diffusez des données en continu vers Experience Platform à l’aide d’une connexion source, vous pouvez configurer la source pour qu’elle utilise à la place des champs calculés. Consultez la [documentation de votre source spécifique](../../sources/home.md) pour obtenir des instructions sur lʼimplémentation de champs calculés lors de la configuration de la connexion.

## Groupes de champs de schéma compatibles {#field-groups}

>[!NOTE]
>
>Les noms de plusieurs groupes de champs ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../field-groups/name-updates.md).

Adobe fournit plusieurs groupes de champs standard à utiliser avec la classe [!DNL XDM ExperienceEvent]. Voici une liste de groupes de champs couramment utilisés pour la classe :

* [[!UICONTROL Adobe Analytics ExperienceEvent Full Extension]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension]](../field-groups/event/advertising-full-extension.md)
* [[!UICONTROL Balance Transfers]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL Campaign Marketing Details]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Card Actions]](../field-groups/event/card-actions.md)
* [[!UICONTROL Channel Details]](../field-groups/event/channel-details.md)
* [[!UICONTROL Commerce Details]](../field-groups/event/commerce-details.md)
* [[!UICONTROL Deposit Details]](../field-groups/event/deposit-details.md)
* [[!UICONTROL Device Trade-In Details]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL Dining Reservation]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL End User ID Details]](../field-groups/event/enduserids.md)
* [[!UICONTROL Environment Details]](../field-groups/event/environment-details.md)
* [[!UICONTROL Flight Reservation]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL IAB TCF 2.0 Consent]](../field-groups/event/iab.md)
* [[!UICONTROL Lodging Reservation]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL MediaAnalytics Interaction Details]](../field-groups/event/mediaanalytics-interaction.md)
* [[!UICONTROL Quote Request Details]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Reservation Details]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Web Details]](../field-groups/event/web-details.md)

## Annexe

La section suivante contient des informations supplémentaires sur la classe [!UICONTROL XDM ExperienceEvent].

### Valeurs acceptées pour `eventType` {#eventType}

Le tableau suivant décrit les valeurs acceptées pour `eventType`, ainsi que leurs définitions :

| Valeur | Définition |
| --- | --- |
| `advertising.clicks` | Cet événement effectue le suivi lorsqu’une action de sélection d’une publicité se produit. |
| `advertising.completes` | Cet événement indique à quel moment une ressource de média horodatée a été visionnée jusqu’à la fin. Cela ne signifie pas nécessairement que le spectateur a visionné l’ensemble de la vidéo, car il a pu avancer dans celle-ci. |
| `advertising.conversions` | Cet événement effectue le suivi d’une action prédéfinie effectuée par un client qui déclenche un événement pour l’évaluation des performances. |
| `advertising.federated` | Cet événement contrôle si un événement d’expérience a été créé par le biais d’une fédération de données (partage de données entre les clients). |
| `advertising.firstQuartiles` | Cet événement effectue le suivi lorsqu’une publicité vidéo numérique a été lue pendant 25 % de sa durée à vitesse normale. |
| `advertising.impressions` | Cet événement permet de suivre les impressions d’une publicité auprès d’un client avec la possibilité d’être visionnée. |
| `advertising.midpoints` | Cet événement effectue le suivi lorsqu’une publicité vidéo numérique a été lue pendant 50 % de sa durée à une vitesse normale. |
| `advertising.starts` | Cet événement permet de déterminer à quel moment une publicité de vidéo numérique a commencé à être lue. |
| `advertising.thirdQuartiles` | Cet événement effectue le suivi lorsqu’une publicité vidéo numérique a été lue pendant 75 % de sa durée à vitesse normale. |
| `advertising.timePlayed` | Cet événement effectue le suivi du temps passé par un utilisateur sur une ressource de média horodatée spécifique. |
| `application.close` | Cet événement effectue le suivi lorsqu’une application a été fermée ou envoyée en arrière-plan. |
| `application.launch` | Cet événement permet de suivre le moment où une application a été lancée ou mise au premier plan. |
| `click` | **Obsolète** Utilisez plutôt `decisioning.propositionInteract`. |
| `commerce.backofficeCreditMemoIssued` | Cet événement permet de suivre le moment où un avis de crédit a été émis pour un client. |
| `commerce.backofficeOrderCancelled` | Cet événement permet de suivre le moment où un processus d’achat précédemment lancé a été arrêté avant la fin. |
| `commerce.backofficeOrderItemsShipped` | Cet événement permet de suivre le moment où les articles achetés ont été physiquement expédiés au client. |
| `commerce.backofficeOrderPlaced` | Cet événement effectue le suivi du placement d’une commande. |
| `commerce.backofficeShipmentCompleted` | Cet événement effectue le suivi de la réussite de l’ensemble du processus d’expédition. |
| `commerce.checkouts` | Cet événement permet de déterminer à quel moment un événement de passage en caisse s’est produit pour une liste de produits. Il peut y avoir plusieurs événements de passage en caisse s’il existe plusieurs étapes dans un processus de passage en caisse. S’il y a plusieurs étapes, l’horodatage et la page/expérience référencée pour chaque événement sont utilisés pour identifier chaque événement individuel (étape), représenté dans l’ordre. |
| `commerce.productListAdds` | Cet événement effectue le suivi lorsqu’un produit a été ajouté à la liste de produits ou au panier. |
| `commerce.productListOpens` | Cet événement indique à quel moment une nouvelle liste de produits (panier) a été initialisée ou créée. |
| `commerce.productListRemovals` | Cet événement effectue le suivi lorsqu’une entrée de produit a été supprimée d’une liste de produits ou d’un panier. |
| `commerce.productListReopens` | Cet événement indique à quel moment une liste de produits (panier) qui n’était plus accessible (abandonnée) a été réactivée par un client, par exemple via une activité de remarketing. |
| `commerce.productListViews` | Cet événement permet de déterminer à quel moment une liste de produits ou un panier a été consulté. |
| `commerce.productViews` | Cet événement permet de déterminer à quel moment un produit a été consulté une ou plusieurs fois. |
| `commerce.purchases` | Cet événement permet de déterminer à quel moment une commande a été acceptée. Il s’agit de la seule action requise lors dʼune conversion commerciale. Un événement d’achat doit avoir une liste de produits référencée. |
| `commerce.saveForLaters` | Cet événement permet de déterminer à quel moment une liste de produits a été enregistrée en vue d’une utilisation ultérieure, telle qu’une liste de souhaits. |
| `decisioning.propositionDisplay` | Cet événement est utilisé lorsque le SDK Web envoie automatiquement des informations sur ce qui s’affiche sur une page. Cependant, vous n’avez pas besoin de ce type d’événement si vous incluez déjà des informations d’affichage d’autres manières, comme avec les accès en haut et en bas de la page. Pour les accès au bas de la page, vous pouvez choisir le type d’événement de votre choix. |
| `decisioning.propositionDismiss` | Ce type d’événement est utilisé lorsqu’un message in-application ou une carte de contenu Adobe Journey Optimizer est ignoré. |
| `decisioning.propositionFetch` | Utilisé pour indiquer qu’un événement sert principalement à récupérer la prise de décision. Adobe Analytics déposera automatiquement cet événement. |
| `decisioning.propositionInteract` | Ce type d’événement est utilisé pour effectuer le suivi des interactions, telles que les clics, sur le contenu personnalisé. |
| `decisioning.propositionSend` | Cet événement permet de suivre le moment où il a été décidé d’envoyer à un client potentiel une recommandation ou une offre à prendre en compte. |
| `decisioning.propositionTrigger` | Les événements de ce type sont stockés en local par le Web SDK, mais ne sont pas envoyés à Edge Network. Chaque fois qu’un ensemble de règles est satisfait, un événement est généré et stocké dans le stockage local (si ce paramètre est activé). |
| `delivery.feedback` | Cet événement effectue le suivi des événements de retour pour une diffusion, telle qu’une diffusion e-mail. |
| `directMarketing.emailBounced` | Cet événement effectue le suivi du rebond d’un e-mail envoyé à une personne. |
| `directMarketing.emailBouncedSoft` | Cet événement effectue le suivi des soft bounces d&#39;un e-mail envoyé à une personne. |
| `directMarketing.emailClicked` | Cet événement effectue le suivi lorsqu’une personne clique sur un lien dans un e-mail marketing. |
| `directMarketing.emailDelivered` | Cet événement effectue le suivi lorsqu’un e-mail a été correctement envoyé au service de messagerie d’une personne. |
| `directMarketing.emailOpened` | Cet événement effectue le suivi lorsqu’une personne a ouvert un e-mail marketing. |
| `directMarketing.emailSent` | Cet événement effectue le suivi lorsqu’un e-mail marketing a été envoyé à une personne. |
| `directMarketing.emailUnsubscribed` | Cet événement effectue le suivi lorsqu’une personne s’est désabonnée d’un e-mail marketing. |
| `display` | **Obsolète** Utilisez plutôt `decisioning.propositionDisplay`. |
| `inappmessageTracking.dismiss` | Cet événement effectue le suivi lorsqu’un message in-app a été ignoré. |
| `inappmessageTracking.display` | Cet événement effectue le suivi de l’affichage d’un message in-app. |
| `inappmessageTracking.interact` | Cet événement effectue le suivi de l’interaction avec un message in-app. |
| `leadOperation.callWebhook` | Cet événement permet de déterminer à quel moment un webhook a été appelé en réponse à un prospect. |
| `leadOperation.changeCampaignStream` | Cet événement signifie un changement dans la stratégie de marketing ou d’engagement d’un chef d’entreprise particulier. |
| `leadOperation.changeEngagementCampaignCadence` | Cet événement permet de suivre le moment où un changement est intervenu dans la fréquence des interactions d’un prospect dans le cadre d’une campagne. |
| `leadOperation.convertLead` | Cet événement permet de suivre le moment où un prospect a été converti. |
| `leadOperation.interestingMoment` | Cet événement permet de déterminer à quel moment un moment intéressant a été enregistré pour une personne. |
| `leadOperation.mergeLeads` | Cet événement permet de déterminer à quel moment les informations provenant de plusieurs prospects qui se rapportent à la même entité ont été consolidées. |
| `leadOperation.newLead` | Cet événement permet de suivre la date de création d’un prospect. |
| `leadOperation.scoreChanged` | Cet événement effectue le suivi lorsque la valeur de l’attribut de score du prospect a été modifiée. |
| `leadOperation.statusInCampaignProgressionChanged` | Cet événement permet de déterminer à quel moment le statut d’un prospect dans une campagne a changé. |
| `listOperation.addToList` | Cet événement permet de déterminer à quel moment une personne a été ajoutée à une liste marketing. |
| `listOperation.removeFromList` | Cet événement effectue le suivi lorsqu’une personne a été supprimée d’une liste marketing. |
| `media.adBreakComplete` | Cet événement signale la fin d’une coupure publicitaire. |
| `media.adBreakStart` | Cet événement signale le début d’une coupure publicitaire. |
| `media.adComplete` | Cet événement signale la fin d’une publicité. |
| `media.adSkip` | Cet événement signale lorsqu’une publicité a été ignorée. |
| `media.adStart` | Cet événement signale le début d’une publicité. |
| `media.bitrateChange` | Cet événement signale un changement de débit. |
| `media.bufferStart` | Le type d’événement `media.bufferStart` est envoyé lorsque la mise en mémoire tampon commence. Il n’existe aucun type d’événement `bufferResume` spécifique ; la mise en mémoire tampon est considérée comme ayant repris lorsqu’un événement `play` est envoyé à la suite d’un événement `bufferStart`. |
| `media.chapterComplete` | Cet événement signale la fin d’un chapitre. |
| `media.chapterSkip` | Cet événement est déclenché lorsqu’un utilisateur passe en amont ou en aval d’une autre section ou d’un autre chapitre. |
| `media.chapterStart` | Cet événement marque le début d’un chapitre. |
| `media.downloaded` | Cet événement permet de déterminer à quel moment du contenu multimédia téléchargé a été diffusé. |
| `media.error` | Cet événement signale lorsqu’une erreur s’est produite lors de la lecture du média. |
| `media.pauseStart` | Cet événement effectue le suivi lorsqu’un événement `pauseStart` s’est produit. Cet événement est déclenché lorsqu’un utilisateur lance une pause dans la lecture du média. Il n’existe aucun type d’événement de reprise. Une reprise est déduite lorsque vous envoyez un événement de lecture après une `pauseStart`. |
| `media.ping` | Le type d’événement `media.ping` est utilisé pour indiquer le statut de la lecture en cours. Pour le contenu principal, cet événement doit être envoyé toutes les 10 secondes pendant la lecture, en commençant 10 secondes après le début de la lecture. Pour le contenu publicitaire, il doit être envoyé toutes les secondes pendant le suivi publicitaire. Les événements ping ne doivent pas inclure la carte des paramètres dans le corps de la requête. |
| `media.play` | Le type d’événement `media.play` est envoyé lorsque le lecteur passe à l’état `playing` à partir d’un autre état, tel que `buffering,` `paused` (lorsque l’utilisateur le reprend) ou `error` (lorsqu’il est récupéré), y compris les scénarios tels que la lecture automatique. Cet événement est déclenché par le rappel `on('Playing')` du lecteur. |
| `media.sessionComplete` | Cet événement est envoyé lorsque la fin du contenu principal est atteinte. |
| `media.sessionEnd` | Le type d’événement `media.sessionEnd` indique au serveur principal Media Analytics de fermer immédiatement une session lorsqu’un utilisateur ou une utilisatrice abandonne son affichage et qu’il est peu probable qu’il revienne. Si cet événement n’est pas envoyé, la session expire après 10 minutes d’inactivité ou 30 minutes sans déplacement du curseur de lecture. Tous les appels multimédias suivants avec cet ID de session seront ignorés. |
| `media.sessionStart` | Le type d’événement `media.sessionStart` est envoyé avec l’appel d’initiation de session. Lors de la réception d’une réponse, l’ID de session est extrait de l’en-tête de l’emplacement et utilisé pour tous les appels d’événement suivants au serveur de collecte. |
| `media.statesUpdate` | Cet événement effectue le suivi lorsqu’un événement `statesUpdate` s’est produit. Les fonctionnalités de suivi de l’état du lecteur peuvent être associées à un flux audio ou vidéo. Les états standard sont les suivants : `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` et `inFocus`. |
| `opportunityEvent.addToOpportunity` | Cet événement permet de suivre le moment où une personne a été ajoutée à une opportunité. |
| `opportunityEvent.opportunityUpdated` | Cet événement indique à quel moment une opportunité a été mise à jour. |
| `opportunityEvent.removeFromOpportunity` | Cet événement permet de déterminer à quel moment une personne a été retirée d’une opportunité. |
| `personalization.request` | **Obsolète** Utilisez plutôt `decisioning.propositionFetch`. |
| `pushTracking.applicationOpened` | Cet événement effectue le suivi lorsqu’une personne a ouvert une application à partir d’une notification push. |
| `pushTracking.customAction` | Cet événement indique quand une personne a sélectionné une action personnalisée dans une notification push. |
| `web.formFilledOut` | Cet événement effectue le suivi lorsqu’une personne a rempli un formulaire sur une page web. |
| `web.webinteraction.linkClicks` | L’événement indique qu’un clic sur un lien a été automatiquement enregistré par le SDK Web. |
| `web.webpagedetails.pageViews` | Ce type d’événement est la méthode standard pour marquer l’accès comme une page vue. |
| `location.entry` | Cet événement effectue le suivi de l’entrée d’une personne ou d’un appareil à un emplacement spécifique. |
| `location.exit` | Cet événement effectue le suivi de la sortie d’une personne ou d’un appareil d’un emplacement spécifique. |

{style="table-layout:auto"}

### Valeurs suggérées pour `producedBy` {#producedBy}

Le tableau suivant présente quelques-unes des valeurs acceptées pour `producedBy` :

| Valeur | Définition |
| --- | --- |
| `self` | Self |
| `system` | Système |
| `salesRef` | Représentant commercial |
| `customerRep` | Représentant du client |
