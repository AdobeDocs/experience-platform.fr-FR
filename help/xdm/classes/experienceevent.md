---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: XDM ExperienceEvent, classe
topic: overview
description: Ce document fournit un aperçu de la classe XDM ExperienceEvent.
translation-type: tm+mt
source-git-commit: b7b57c0b70b1af3a833f0386bc809bb92c9b50f8
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 6%

---


# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] est une classe XDM standard qui vous permet de créer un instantané horodaté du système lorsqu&#39;un événement spécifique se produit ou qu&#39;un certain ensemble de conditions a été atteint.

Un Événement d’expérience est un enregistrement factuel de ce qui s’est produit, y compris le moment et l’identité de la personne concernée. Les événements peuvent être explicites (actions humaines directement observables) ou implicites (soulevées sans action humaine directe) et sont enregistrés sans agrégation ni interprétation. Pour plus d&#39;informations de haut niveau sur l&#39;utilisation de cette classe dans l&#39;écosystème de la plate-forme, consultez la présentation [de](../home.md#data-behaviors)XDM.

La [!DNL XDM ExperienceEvent] classe elle-même fournit plusieurs champs liés aux séries chronologiques à un schéma. Les valeurs de certains de ces champs sont automatiquement renseignées lors de l’assimilation des données :

<img src="../images/classes/experienceevent.png" width="650" /><br />

| Propriété | Description |
| --- | --- |
| `_id` | Identificateur de chaîne unique généré par le système pour le événement. Ce champ permet de suivre l&#39;unicité d&#39;un événement individuel, d&#39;éviter la duplication des données et de rechercher ce événement dans les services en aval. Ce champ étant généré par le système, il ne doit pas être fourni de valeur explicite lors de l’assimilation des données.<br><br>Il est important de distinguer que ce champ ne **représente pas** une identité liée à une personne, mais plutôt l&#39;enregistrement des données proprement dites. Les données d&#39;identité relatives à une personne doivent être reléguées aux champs [d&#39;](../schema/composition.md#identity) identité. |
| `eventMergeId` | ID du lot assimilé à l&#39;origine de la création de l&#39;enregistrement. Ce champ est automatiquement renseigné par le système lors de l’assimilation des données. |
| `eventType` | Chaîne indiquant le Principal type d&#39;événement de l’enregistrement. Les valeurs acceptées et leurs définitions figurent dans la section [de l&#39;](#eventType)annexe. |
| `identityMap` | Champ de mappage contenant un ensemble d’identités d’espacement de noms pour la personne à laquelle le événement s’applique. Ce champ est automatiquement mis à jour par le système lorsque des données d&#39;identité sont saisies. Afin d’utiliser correctement ce champ pour le Profil [client en temps](../../profile/home.md)réel, n’essayez pas de mettre à jour manuellement le contenu du champ dans vos opérations de données.<br /><br />Consultez la section sur les cartes d&#39;identité dans les [bases de la composition](../schema/composition.md#identityMap) des schémas pour plus d&#39;informations sur leur cas d&#39;utilisation. |
| `timestamp` | Heure à laquelle le événement ou l&#39;observation s&#39;est produit. |

## mixins compatibles {#mixins}

Adobe fournit plusieurs mixins standard à utiliser avec la [!DNL XDM ExperienceEvent] classe. Voici une liste de certains mixins couramment utilisés pour la classe :

* [[!UICONTROL ID d’utilisateur final ExperienceEvent]](../mixins/event/enduserids.md)
* [[!UICONTROL Détails de l’environnement ExperienceEvent]](../mixins/event/environment-details.md)

## Annexe

La section suivante contient des informations supplémentaires sur la classe [!UICONTROL XDM ExperienceEvent] .

### Valeurs acceptées pour xdm:eventType {#eventType}

Le tableau suivant présente les valeurs acceptées pour `xdm:eventType`, ainsi que leurs définitions :

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
| `web.webinteraction.linkClicks` | Un lien a reçu un ou plusieurs clics. |
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