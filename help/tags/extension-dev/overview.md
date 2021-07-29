---
title: Présentation du développement d’extension
description: Découvrez les Principaux composants des différents types d’extensions de balises et le processus de développement d’extensions dans Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 19%

---

# Présentation du développement d’extension

>[!NOTE]
>
>Adobe Experience Platform Launch a été rebaptisé en tant que suite de technologies de collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

L’un des Principaux objectifs des balises dans Adobe Experience Platform est de créer un écosystème ouvert où les ingénieurs en dehors de l’Adobe peuvent exposer des fonctionnalités supplémentaires sur leurs sites web et applications mobiles. Pour ce faire, vous devez utiliser les extensions de balise . Une fois qu’une extension a été installée sur une propriété de balise, la fonctionnalité de cette extension est alors disponible pour tous les utilisateurs de la propriété.

Ce document décrit les Principaux composants d’une extension et fournit des liens vers d’autres documents pour vous aider à vous guider dans le processus de développement de l’extension.

## Structure de l’extension

Une extension est un répertoire de fichiers. Plus précisément, une extension se compose d’un fichier manifeste, de modules de bibliothèque et de vues.

### Fichier de manifeste 

Un fichier de manifeste ([`extension.json`](./manifest.md)) doit exister à la racine du répertoire. Ce fichier décrit la composition de l’extension et l’emplacement de certains fichiers dans le répertoire. Le manifeste fonctionne de la même manière qu’un fichier [`package.json`](https://docs.npmjs.com/files/package.json) dans un projet [npm](https://www.npmjs.com/).

### Modules Bibliothèque

Les modules Bibliothèque sont les fichiers qui décrivent les différents [composants](#components) fournis par une extension (en d’autres termes, la logique à émettre dans la bibliothèque du runtime de balise). Le contenu de chaque fichier de module de bibliothèque doit respecter la [norme du module CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1.1).

Par exemple, si vous créez un type d’action appelé &quot;envoyer une balise&quot;, vous devez disposer d’un fichier contenant la logique qui envoie la balise. Si vous utilisez JavaScript, le fichier peut être appelé `sendBeacon.js`. Le contenu de ce fichier sera émis dans la bibliothèque du runtime de balises.

Vous pouvez placer des fichiers de module de bibliothèque n’importe où dans le répertoire d’extension, à condition que vous décriviez leur emplacement dans `extension.json`.

### Vues

Une vue est un fichier HTML pouvant être chargé dans un élément [`iframe` ](https://developer.mozilla.org/fr-FR/docs/Web/HTML/Element/iframe) dans l’application de balises, en particulier via l’interface utilisateur de collecte de données. La vue doit inclure un script fourni par l’extension et se conformer à une petite API pour communiquer avec l’application.

Le fichier d’affichage le plus important pour toute extension est sa configuration. Voir la section [Configurations de l’extension](#configuration) pour plus d’informations.

Il n’y a aucune restriction quant aux bibliothèques utilisées dans vos vues. En d’autres termes, vous pouvez utiliser jQuery, Underscore, React, Angular, Bootstrap ou d’autres. Toutefois, il est toujours recommandé de faire en sorte que votre extension ait une apparence similaire à celle de l’interface utilisateur de la collecte de données.

Il est recommandé de placer tous les fichiers liés aux vues (HTML, CSS, JavaScript) dans un seul sous-répertoire isolé des fichiers du module Bibliothèque. Dans `extension.json`, vous pouvez décrire l’emplacement de ce sous-répertoire de vue. Platform servira alors ce sous-répertoire (et uniquement ce sous-répertoire) à partir de ses serveurs web.

## Composants de bibliothèque {#components}

Chaque extension définit un ensemble de fonctionnalités. Ces fonctionnalités sont implémentées en étant incluses dans une [bibliothèque](../ui/publishing/libraries.md) déployée sur votre site web ou votre application. Les bibliothèques sont un ensemble de composants individuels, notamment des conditions, des actions, des éléments de données, etc. Chaque composant de bibliothèque est un élément de code réutilisable (fourni par une extension) émis dans l’exécution de balise.

Selon que vous développez une extension web ou une extension Edge, les types de composants disponibles et leurs cas d’utilisation diffèrent. Reportez-vous aux sous-sections ci-dessous pour une présentation des composants disponibles pour chaque type d’extension.

### Composants des extensions web {#web}

Dans les extensions web, les règles sont déclenchées par des événements qui peuvent alors exécuter des actions spécifiques si un ensemble donné de conditions est satisfait. Consultez la présentation du [flux de module dans les extensions web](./web/flow.md) pour en savoir davantage.

Outre les [modules principaux](./web/core.md) fournis par Adobe, vous pouvez définir les composants de bibliothèque suivants dans vos extensions web :

* [Événements](./web/event-types.md)
* [Conditions](./web/condition-types.md)
* [Actions](./web/action-types.md)
* [Éléments de données](./web/data-element-types.md)
* [Modules partagés](./web/shared.md)

>[!NOTE]
>
>Pour plus d’informations sur le format requis pour l’implémentation des composants de bibliothèque dans les extensions web, consultez la [présentation du format de module](./web/format.md).

### Composants des extensions Edge {#edge}

Dans les extensions Edge, les règles sont déclenchées par des contrôles de condition qui exécutent ensuite des actions spécifiques si ces contrôles réussissent. Pour plus d’informations, consultez la présentation du [flux d’extension Edge](./edge/flow.md) .

Vous pouvez définir les composants de bibliothèque suivants dans vos extensions Edge :

* [Conditions](./edge/condition-types.md)
* [Actions](./edge/action-types.md)
* [Éléments de données](./edge/data-element-types.md)

>[!NOTE]
>
>Pour plus d’informations sur le format requis pour l’implémentation des modules de bibliothèque dans les extensions Edge, consultez la [présentation du format de module](./edge/format.md).

## Configuration d’extension {#configuration}

La configuration d’une extension fait référence à la manière dont elle rassemble les paramètres globaux d’un utilisateur. La configuration se compose d’un composant d’affichage qui exporte et émet des paramètres dans la bibliothèque du runtime de balises en tant qu’objet brut.

Prenons l’exemple d’une extension qui permet à l’utilisateur d’envoyer une balise à l’aide d’une action &quot;Envoyer la balise&quot;, et la balise doit toujours contenir un identifiant de compte. Plutôt que de demander aux utilisateurs un ID de compte chaque fois qu’ils configurent une action &quot;Envoyer la balise&quot;, l’extension doit demander l’ID de compte une fois à partir de la vue de configuration de l’extension. Chaque fois qu’une balise doit être envoyée, l’action &quot;Envoyer la balise&quot; peut extraire l’ID de compte de la configuration de l’extension et l’ajouter à la balise.

Lorsque les utilisateurs installent une extension sur une propriété dans l’interface utilisateur, la vue de configuration de l’extension leur est présentée, qu’ils doivent compléter pour terminer l’installation.

Pour en savoir plus, consultez le guide sur les [configurations d’extension](./configuration.md).

## Envoi d’extensions

Une fois la création de votre extension terminée, vous pouvez la soumettre pour qu’elle soit répertoriée dans le catalogue d’extensions de Platform. Pour plus d’informations, consultez la [présentation du processus d’envoi de l’extension](./submit/overview.md) .