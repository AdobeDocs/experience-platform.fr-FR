---
title: Présentation du développement d’extension
description: Découvrez les Principaux composants des différents types d’extensions de balises et le processus de développement d’extensions dans Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 69%

---

# Présentation du développement d’extension

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

L’un des Principaux objectifs de Adobe Experience Platform est de créer un écosystème ouvert où les ingénieurs en dehors de l’équipe d’ingénierie principale peuvent exposer des fonctionnalités supplémentaires au moyen de balises. Cela peut être fait grâce aux extensions Reactor. Une fois qu’une extension a été installée sur une propriété de balise par un utilisateur, cette extension est alors disponible pour tous les utilisateurs de la propriété.

Ce document décrit les composants Principaux de différents types d’extensions et fournit des liens vers d’autres documents pour vous guider dans le processus de développement de l’extension.

## Modules Bibliothèque

Les modules Bibliothèque sont des éléments de code réutilisables fournis par une extension émise dans la bibliothèque du runtime de balises. Selon que vous développez une extension web ou une extension Edge, les types de module disponibles et leur utilisation diffèrent. Reportez-vous aux sous-sections suivantes pour un aperçu des modules pour chaque type d’extension :

* [Modules pour les extensions web](#web-modules)
* [Modules pour les extensions Edge](#edge-modules)

### Modules pour les extensions web {#web-modules}

Dans les extensions web, les règles sont déclenchées par des événements qui peuvent alors exécuter des actions spécifiques si un ensemble donné de conditions est satisfait. Consultez la présentation du [flux de module dans les extensions web](./web/flow.md) pour en savoir davantage.

Outre les [modules principaux](./web/core.md) fournis par Adobe, vous pouvez définir les types suivants de module de bibliothèque dans vos extensions web :

* [Types d’événements](#web-event)
* [Types de condition](#web-condition)
* [Types d’actions](#web-action)
* [Types d’éléments de données](#web-data-element)
* [Modules partagés](#shared)

>[!NOTE]
>
>Pour plus d’informations sur le format requis pour l’implémentation des modules de bibliothèque dans les extensions web, consultez la [présentation du format de module](./web/format.md).

#### Types d’événements {#web-event}

Un événement de règle est une activité qui doit se produire avant le déclenchement d’une règle.

Par exemple, une extension peut fournir un type d’événement « mouvement » qui surveille un certain mouvement de souris ou de toucher. Une fois le mouvement effectué, la logique de l’événement déclenche la règle.

Les types d’événement consistent généralement en (1) une vue affichée dans l’interface utilisateur de la collecte de données qui permet aux utilisateurs de modifier les paramètres de l’événement et (2) un module Bibliothèque émis dans la bibliothèque du runtime de balises pour interpréter les paramètres et surveiller l’apparition d’une certaine activité.

[En savoir plus](./web/event-types.md)

#### Types de condition {#web-condition}

Une condition de règle est évaluée après qu’un événement de règle se soit produit. Toutes les conditions doivent renvoyer la valeur vraie pour que la règle continue son traitement. Une exception survient lorsque les utilisateurs placent explicitement des conditions dans un compartiment « exception », auquel cas toutes les conditions du compartiment doivent renvoyer la valeur fausse pour que la règle puisse continuer le traitement.

Par exemple, une extension peut fournir un type de condition « viewport contains » dans lequel l’utilisateur peut spécifier un sélecteur CSS. Lorsque la condition est évaluée sur le site web du client, l’extension peut trouver des éléments correspondant au sélecteur CSS et renvoyer si la fenêtre d’affichage de l’utilisateur contient l’un d’entre eux.

Les types de conditions consistent généralement en (1) une vue affichée dans l’interface utilisateur de la collecte de données qui permet aux utilisateurs de modifier les paramètres de la condition et (2) un module Bibliothèque émis dans la bibliothèque du runtime de balises pour interpréter les paramètres et évaluer une condition.

[En savoir plus](./web/condition-types.md)

#### Types d’actions {#web-action}

Une action de règle est exécutée une fois que l’événement de règle est survenu et que les conditions ont réussi l’évaluation.

Par exemple, une extension peut fournir un type d’action « show support chat » qui peut afficher une boîte de dialogue de conversation d’assistance pour aider les utilisateurs qui ont du mal à payer leur commande.

Les types d’actions consistent généralement en (1) une vue affichée dans l’interface utilisateur de la collecte de données qui permet aux utilisateurs de modifier les paramètres de l’action et (2) un module Bibliothèque émis dans la bibliothèque du runtime de balises pour interpréter les paramètres et exécuter une action.

[En savoir plus](./web/action-types.md)

#### Types d’éléments de données {#web-data-element}

Les éléments de données sont essentiellement des alias de données d’une page, que ces données se trouvent dans des paramètres de chaîne de requête, des cookies, des éléments DOM ou ailleurs. Un élément de données peut être référencé par des règles et agit comme une abstraction pour l’accès à ces données. Lorsque l’emplacement des données changera à l’avenir (par exemple, de `innerHTML` d’un élément DOM à la valeur d’une variable JavaScript), un seul élément de données peut être reconfiguré tandis que toutes les règles référençant cet élément de données peuvent rester inchangées.

Un type d’élément de données permet aux utilisateurs de configurer des éléments de données pour accéder à une donnée d’une manière particulière. Par exemple, une extension peut fournir un type d’élément de données « élément d’enregistrement local » dans lequel l’utilisateur de peut spécifier un nom d’élément d’enregistrement local. Lorsque l’élément de données est référencé par une règle, l’extension peut rechercher la valeur de l’élément d’enregistrement local en utilisant le nom d’élément d’enregistrement local que l’utilisateur a fourni lors de la configuration de l’élément de données.

Les types d’éléments de données consistent généralement en (1) une vue affichée dans l’interface utilisateur de la collecte de données qui permet aux utilisateurs de modifier les paramètres de l’élément de données et (2) un module Bibliothèque émis dans la bibliothèque du runtime de balises pour interpréter les paramètres et récupérer des éléments de données.

[En savoir plus](./web/data-element-types.md)

#### Modules partagés {#shared}

Un module partagé est un module exposé par une extension à laquelle une autre peut accéder. Ce mécanisme peut être très utile pour communiquer entre les extensions. Par exemple, l’extension A peut charger un élément de données de manière asynchrone et le rendre accessible à l’extension B via une [promesse](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/Promise).

Les modules partagés sont inclus dans la bibliothèque même s’ils ne sont jamais appelés à partir d’autres extensions. Afin de ne pas augmenter inutilement la taille de la bibliothèque, vous devez faire attention à ce que vous exposez comme module partagé.

Les modules partagés ne comportent pas de composant de vue.

[En savoir plus](./web/shared.md)

### Modules pour les extensions Edge {#edge-modules}

Dans les extensions Edge, les règles sont déclenchées par des contrôles de condition qui exécutent ensuite des actions spécifiques si ces contrôles réussissent. Pour plus d’informations, consultez la présentation [flux de module dans les extensions Edge](./edge/flow.md).

Vous pouvez définir vos propres modules de bibliothèque dans vos extensions Edge. Ils peuvent être classés parmi les types suivants :

* [Types de condition](#condition)
* [Types d’actions](#action)
* [Types d’éléments de données](#data-element)

>[!NOTE]
>
>Pour plus d’informations sur le format requis pour l’implémentation des modules de bibliothèque dans les extensions Edge, consultez la [présentation du format de module](./edge/format.md).

#### Types de condition {#condition}

Une condition de règle est évaluée après qu’un événement de règle se soit produit. Toutes les conditions doivent renvoyer la valeur vraie pour que la règle continue son traitement. Une exception survient lorsque les utilisateurs placent explicitement des conditions dans un compartiment « exception », auquel cas toutes les conditions du compartiment doivent renvoyer la valeur fausse pour que la règle puisse continuer le traitement.

Par exemple, une extension peut fournir un type de condition « viewport contains » dans lequel l’utilisateur peut spécifier un sélecteur CSS. Lorsque la condition est évaluée sur le site web du client, l’extension peut trouver des éléments correspondant au sélecteur CSS et renvoyer si la fenêtre d’affichage de l’utilisateur contient l’un d’entre eux.

Les types de conditions consistent généralement en (1) une vue affichée dans l’interface utilisateur de la collecte de données qui permet aux utilisateurs de modifier les paramètres de la condition et (2) un module Bibliothèque émis dans la bibliothèque du runtime de balises pour interpréter les paramètres et évaluer une condition.

[En savoir plus](./web/condition-types.md)

#### Types d’actions {#action}

Une action de règle est exécutée après que les conditions de la règle ont satisfait à l’évaluation.

Par exemple, une extension peut fournir un type d’action « show support chat » qui peut afficher une boîte de dialogue de conversation d’assistance pour aider les utilisateurs qui ont du mal à payer leur commande.

Les types d’actions consistent généralement en (1) une vue affichée dans l’interface utilisateur de la collecte de données qui permet aux utilisateurs de modifier les paramètres de l’action et (2) un module Bibliothèque émis dans la bibliothèque du runtime de balises pour interpréter les paramètres et exécuter une action.

[En savoir plus](./web/action-types.md)

#### Types d’éléments de données {#data-element}

Les éléments de données sont essentiellement des alias vers des données sur une page, quel que soit l’emplacement de ces données dans l’événement reçu par le serveur. Un élément de données peut être référencé par des règles et agit comme une abstraction pour l’accès à ces données. Lorsque l’emplacement des données changera à l’avenir (par exemple, en cas de modification de la clé de l’événement contenant la valeur), un seul élément de données pourra être reconfiguré tandis que toutes les règles référençant cet élément de données pourront rester inchangées.

Les types d’éléments de données consistent généralement en (1) une vue affichée dans l’interface utilisateur de la collecte de données qui permet aux utilisateurs de modifier les paramètres de l’élément de données et (2) un module Bibliothèque émis dans la bibliothèque du runtime de balises pour interpréter les paramètres et récupérer des éléments de données.

[En savoir plus](./web/data-element-types.md)

## Configuration d’extension

La configuration d’une extension fait référence à la manière dont elle rassemble les paramètres globaux d’un utilisateur. Prenons l’exemple d’une extension qui permet à l’utilisateur d’envoyer une balise à l’aide d’une action Envoyer la balise : la balise doit toujours contenir un identifiant de compte. Nous ne voulons pas troubler les utilisateurs en leur demandant l’identifiant de compte chaque fois qu’ils configurent une action Envoyer la balise. Au lieu de cela, l’extension doit demander une fois l’identifiant de compte à partir de la vue de configuration de l’extension. Chaque fois qu’une balise doit être envoyée, le module Bibliothèque d’action Envoyer la balise peut extraire l’identifiant de compte de la configuration de l’extension et l’ajouter à la balise.

Lorsque les utilisateurs installent une extension sur une propriété de balise, la vue de configuration de l’extension s’affiche. Ils ne peuvent pas terminer l’installation de l’extension sans avoir terminé la configuration de l’extension.

La configuration de l’extension consiste en un composant d’affichage qui exportera les paramètres qui sont ensuite émis dans la bibliothèque du runtime de balises en tant qu’objet simple.

[En savoir plus](./configuration.md)

## Structure de l’extension

Une extension est un répertoire de fichiers. Voici un aperçu de la façon dont ces fichiers doivent être structurés. Vous trouverez des informations détaillées sur le contenu des fichiers dans d’autres sections.

Un fichier [`extension.json`](./manifest.md) doit exister à la racine du répertoire. Ce fichier décrira, entre autres, la composition de l’extension et l’emplacement de certains fichiers dans le répertoire. Il existe des similitudes avec un fichier [`package.json`](https://docs.npmjs.com/files/package.json) dans [npm](https://www.npmjs.com/).

Chaque module de bibliothèque (la logique à émettre dans la bibliothèque du runtime de balises) doit être son propre fichier dont le contenu respecte la [norme du module CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1.1). Par exemple, si nous créons un type d’action « envoyer la balise », nous devons disposer d’un fichier contenant la logique d’envoi de balise. Le contenu de ce fichier sera émis dans la bibliothèque du runtime de balises. Vous pouvez l’appeler `sendBeacon.js`. L’emplacement du fichier dans le répertoire n’est pas important, car `extension.json` décrit son emplacement.

Chaque vue doit être un fichier HTML pouvant être chargé dans un iframe dans l’application de balises. La vue doit inclure un script fourni par des balises et se conformer à une petite API pour communiquer avec l’application. Il n’y a aucune restriction quant aux bibliothèques utilisées dans vos vues. En d’autres termes, vous pouvez utiliser jQuery, Underscore, React, Angular, Bootstrap ou d’autres bibliothèques. Nous espérons toutefois que votre extension aura un aspect similaire à celui de l’application.

Il est recommandé de placer tous les fichiers liés aux vues (HTML, CSS, JavaScript) dans un seul sous-répertoire isolé des fichiers du module Bibliothèque. Dans `extension.json`, vous décrivez l’emplacement de ce sous-répertoire de vue. Platform servira alors ce sous-répertoire (et uniquement ce sous-répertoire) à partir de ses serveurs web.
