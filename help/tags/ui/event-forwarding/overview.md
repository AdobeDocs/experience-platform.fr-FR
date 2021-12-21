---
title: Présentation du transfert dʼévénements
description: Découvrez Adobe Experience Platform, qui vous permet dʼutiliser Platform Edge Network afin dʼexécuter des tâches sans modifier votre implémentation de balises.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: 82ce288d55e57f05910fd8290c38f44b1846f48e
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 12%

---

# Présentation du transfert dʼévénements

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Le transfert d’événement dans Adobe Experience Platform vous permet d’envoyer les données d’événement collectées vers une destination pour le traitement côté serveur. Le transfert d’événement réduit le poids des pages web et des applications en utilisant Adobe Experience Platform Edge Network pour exécuter les tâches normalement effectuées sur le client. Mis en oeuvre de la même manière que les balises, les règles de transfert d’événement peuvent transformer et envoyer des données vers de nouvelles destinations. Cependant, au lieu d’envoyer ces données depuis une application cliente comme un navigateur web, elles sont envoyées depuis les serveurs de l’Adobe.

Ce document présente de manière générale le transfert d’événement dans Platform.

![Transfert d’événement dans l’écosystème de collecte de données](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>Pour plus d’informations sur la façon dont le transfert d’événement s’insère dans l’écosystème de collecte de données de Platform, voir la section [présentation de la collecte de données](../../../collection/home.md).

Transfert d’événement associé à Adobe Experience Platform [SDK Web](../../../edge/home.md) et [SDK Mobile](https://aep-sdks.gitbook.io/docs/) offre les avantages suivants :

**Performances**:

* Effectuez un seul appel à partir d’une page qui contient une payload de données qui est ensuite fédérée côté serveur afin de réduire le trafic réseau côté client et offrir une expérience plus rapide aux clients.
* Réduire le temps nécessaire au chargement des pages web pour améliorer les performances du site.
* Réduire le nombre de technologies côté client requises pour fournir votre expérience et envoyer des données à de nombreuses destinations.

**Gouvernance des données**:

* Augmentez la transparence et le contrôle des données envoyées à l’emplacement de l’ensemble des propriétés.

## Différences entre le transfert dʼévénements et les balises

En termes de configuration, le transfert d’événement utilise plusieurs des mêmes concepts que les balises, tels que : [rules](../managing-resources/rules.md), [éléments de données](../managing-resources/data-elements.md), et [extensions](../managing-resources/extensions/overview.md). La principale différence entre les deux peut être résumée comme suit :

* Balises **collecte** les données d’événement d’un site web ou d’une application mobile native et les envoie à Platform Edge Network.
* Transfert d’événement **sends** données d’événement entrantes de Platform Edge Network vers un point de terminaison qui représente une destination finale ou un point de terminaison qui fournit des données que vous souhaitez enrichir la charge utile d’origine.

Tandis que les balises collectent les données d’événement directement sur votre site ou application mobile native à l’aide des SDK Web et Mobile Platform, le transfert d’événement nécessite que les données d’événement soient déjà envoyées via Platform Edge Network afin de les transférer vers les destinations. En d’autres termes, vous devez mettre en oeuvre le SDK Web ou mobile Platform sur votre propriété numérique (par le biais de balises ou à l’aide de code brut) afin d’utiliser le transfert d’événement.

### Propriétés

Le transfert d’événement conserve sa propre banque de propriétés séparées des balises, que vous pouvez afficher dans l’interface utilisateur de la collecte de données en sélectionnant **[!UICONTROL Transfert d’événement]** dans le volet de navigation de gauche.

![Propriétés de transfert d’événement dans l’interface utilisateur de la collecte de données](../../images/ui/event-forwarding/overview/properties.png)

Toutes les propriétés de transfert d’événement **[!UICONTROL Edge]** comme leur plateforme. Ils ne font pas la distinction entre le web et le mobile, car ils traitent uniquement les données reçues de Platform Edge Network, qui peut lui-même recevoir des données d’événement des plateformes web et mobiles.

### Extensions {#extensions}

Le transfert d’événement possède son propre catalogue d’extensions compatibles, telles que le [Core](../../extensions/web/core/event-forwarding.md) extension et [Connecteur Adobe Cloud](../../extensions/web/cloud-connector/overview.md) extension . Vous pouvez afficher les extensions disponibles pour les propriétés de transfert d’événement dans l’interface utilisateur en sélectionnant **[!UICONTROL Extensions]** dans le volet de navigation de gauche, suivi de **[!UICONTROL Catalogue]**.

![Extensions de transfert d’événement dans l’interface utilisateur de la collecte de données](../../images/ui/event-forwarding/overview/extensions.png)

### Éléments de données

Les types d’éléments de données disponibles dans le transfert d’événement sont limités au catalogue des éléments compatibles. [extensions](#extensions) qui les fournissent.

Bien que les éléments de données eux-mêmes soient créés et configurés de la même manière dans le transfert d’événement que pour les balises, il existe d’importantes différences de syntaxe concernant la manière dont ils référencent des données à partir de Platform Edge Network.

#### Référence aux données de Platform Edge Network

Pour référencer des données à partir de Platform Edge Network, vous devez créer un élément de données qui fournit un chemin d’accès valide à ces données. Lors de la création de l’élément de données dans l’interface utilisateur, sélectionnez **[!UICONTROL Core]** pour l’extension et **[!UICONTROL Chemin]** pour le type .

Le **[!UICONTROL Chemin]** la valeur de l’élément de données doit suivre le modèle `arc.event.{ELEMENT}` (par exemple : `arc.event.xdm.web.webPageDetails.URL`). Ce chemin d’accès doit être spécifié correctement pour que les données soient envoyées.

![Exemple d’élément de données de type chemin pour le transfert d’événement](../../images/ui/event-forwarding/overview/data-reference.png)

### Règles

La création de règles dans les propriétés de transfert d’événement fonctionne de la même manière que les balises. La principale différence réside dans le fait que vous ne pouvez pas sélectionner d’événements en tant que composants de règle. À la place, une règle de transfert d’événement traite tous les événements qu’elle reçoit de l’événement [datastream](../../../edge/fundamentals/datastreams.md) et transfère ces événements vers les destinations si certaines conditions sont remplies.

![Règles de transfert d’événement dans l’interface utilisateur de la collecte de données](../../images/ui/event-forwarding/overview/rules.png)

#### Segmentation d’éléments de données en unités lexicales

Dans les règles de balise, les éléments de données sont segmentés en unités lexicales avec une `%` au début et à la fin du nom de l’élément de données (par exemple : `%viewportHeight%`). Dans les règles de transfert d’événement, les éléments de données sont à la place segmentés en unités lexicales avec `{{` au début et `}}` à la fin du nom de l’élément de données (par exemple : `{{viewportHeight}}`).

![Exemple d’élément de données de type chemin pour le transfert d’événement](../../images/ui/event-forwarding/overview/tokenization.png)

#### Séquence des actions de règle

Le [!UICONTROL Actions] d’une règle de transfert d’événement est toujours exécutée de manière séquentielle. Assurez-vous que l’ordre des actions est correct lorsque vous enregistrez une règle. Cette séquence d’exécution ne peut pas être exécutée de manière asynchrone comme elle le peut avec des balises .

## Secrets

Le transfert d’événements vous permet de créer, gérer et stocker des secrets qui peuvent être utilisés pour vous authentifier sur les serveurs auxquels vous envoyez des données. Consultez le guide sur la [secrets](./secrets.md) sur les différents types de types de secrets disponibles et la manière dont ils sont implémentés dans l’interface utilisateur.

## Étapes suivantes

Ce document présente de manière générale le transfert d’événement. Pour plus d’informations sur la configuration de cette fonctionnalité pour votre entreprise, voir [guide de prise en main](./getting-started.md).
