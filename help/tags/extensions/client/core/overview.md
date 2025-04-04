---
title: Présentation de l’extension Core
description: Découvrez lʼextension de balise Core dans Adobe Experience Platform.
exl-id: 841f32ad-a6a8-49fb-a131-ef4faab47187
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '5447'
ht-degree: 95%

---

# Présentation de l’extension Core

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

L’extension de balise Core est l’extension par défaut disponible avec Adobe Experience Platform.

Ce document fournit des informations sur les options disponibles lors de l’utilisation de l’extension Core pour créer une règle.

## Types d’événements de l’extension Core {#core-extension-event-types}

Cette section décrit les types d’événements disponibles dans l’extension Core. Pour plus d’informations sur les options pouvant être définies pour plusieurs types d’événements différents, voir la section [Options](#options).

### Événements basés sur le navigateur

#### Tab Blur

L’événement tab-blur déclenche l’action lorsqu’un onglet perd le focus. Il n’existe aucun paramètre pour ce type d’événement.

#### Tab Focus

L’événement tab-focus déclenche l’action lorsqu’un onglet reçoit le focus. Il n’existe aucun paramètre pour ce type d’événement.

### Form

#### Blur

L’événement blur déclenche l’action lorsqu’un formulaire perd le focus. Voir la section [Options](#options) pour plus d’informations sur les paramètres d’événement personnalisables.

#### Focus

L’événement focus déclenche l’action lorsqu’un formulaire reçoit le focus. Voir la section [Options](#options) pour plus d’informations sur les paramètres d’événement personnalisables.

#### Submit

L’événement submit déclenche l’action lors de l’envoi d’un formulaire. Voir la section [Options](#options) pour plus d’informations sur les paramètres d’événement personnalisables.

### Événements contrôlés par le clavier

#### Key Press

L’événement se déclenche lorsqu’une touche est enfoncée. Voir la section [Options](#options) pour plus d’informations sur les paramètres d’événement personnalisables.

### Événements basés sur un média

#### Media Ended

L’événement se déclenche lorsque le média prend fin. Voir la section [Options](#options) pour plus d’informations sur les paramètres d’événement personnalisables.

#### Media-Loaded Data

L’événement est déclenché lorsque le fichier multimédia charge des données. Voir la section [Options](#options) pour plus d’informations sur les paramètres d’événement personnalisables.

#### Media Pause

L’événement se déclenche lorsque le fichier multimédia est en pause. Voir la section [Options](#options) pour plus d’informations sur les paramètres d’événement personnalisables.

#### Media Play

L’événement est déclenché lors de la lecture du fichier multimédia. Voir la section [Options](#options) pour plus d’informations sur les paramètres d’événement personnalisables.

#### Media Stalled

L’événement se déclenche si le média se bloque. Voir la section [Options](#options) pour plus d’informations sur les paramètres d’événement personnalisables.

#### Media-Time Played

L’événement se déclenche si le fichier multimédia est lu pendant une durée spécifiée. Pour déclencher l’événement, vous devez spécifier la durée de lecture du fichier multimédia. Voir la section [Options](#options) pour plus d’informations sur les paramètres d’événement personnalisables.


#### Media-Volume Changed

L’événement se déclenche en cas d’augmentation ou de réduction de volume. Voir la section [Options](#options) pour plus d’informations sur les paramètres d’événement personnalisables.

### Événements orientés appareil mobile

#### Orientation Change

L’événement se déclenche si l’orientation de l’appareil change. Pour déclencher l’événement, vous devez spécifier la durée pendant laquelle la modification d’orientation doit se produire. Il n’existe aucun paramètre pour ce type d’événement.

#### Zoom Change

L’événement se déclenche si l’utilisateur effectue un zoom avant ou arrière. Il n’existe aucun paramètre pour ce type d’événement.

### Événements contrôlés par la souris

#### Click

L’événement se déclenche si l’élément spécifié est sélectionné (par un clic). Vous pouvez éventuellement spécifier des valeurs de propriété qui doivent être vraies pour l’élément avant que l’événement ne soit déclenché.

Si lʼélément est une balise de type ancre (`<a>`) de lien vers un contenu, vous pouvez également indiquer si la navigation doit être retardée pendant un certain intervalle de temps. Cela peut sʼavérer utile si votre règle nécessite un délai dʼexécution supplémentaire et nʼest normalement pas terminée avant que la page ne sʼouvre.

>[!WARNING]
>
>Cette option doit être utilisée avec une extrême prudence en raison des conséquences négatives potentielles quʼelle peut entraîner pour lʼexpérience utilisateur si elle est mal utilisée.

Lorsque vous utilisez un délai de lien, Experience Platform empêche le navigateur de quitter la page. Il effectue ensuite une redirection JavaScript vers la destination d’origine après la temporisation spécifiée. C’est particulièrement risqué lorsque le balisage de votre page comporte des balises `<a>` où la fonctionnalité prévue ne permet pas de rediriger l’utilisateur en dehors de la page. S’il vous est impossible de résoudre ce problème d’une autre manière, soyez extrêmement précis quant à la définition de votre sélecteur afin que cet événement se déclenche exactement là où vous en avez besoin et nulle part ailleurs.

La valeur par défaut du délai de lien est de 100 millisecondes. Notez que les balises attendront toujours l’intervalle de temps spécifié et ne sont en aucun cas liées à l’exécution des actions de la règle. Il est possible que le délai oblige l’utilisateur à attendre plus longtemps que nécessaire et qu’il ne soit pas suffisant pour permettre à toutes les actions de la règle de se terminer correctement. Des retards plus longs donnent plus de temps à l’exécution des règles, mais dégradent également l’expérience client.

Pour appliquer le retard, il est nécessaire de fournir à la fois l’élément sélectionné qui déclenche l’événement et l’intervalle de temps précis à respecter avant que l’événement ne soit déclenché.

Pour plus d’informations au sujet des options avancées, reportez-vous à la section [Options](#options).

#### Hover

L’événement se déclenche si l’utilisateur survole un élément spécifié. De plus, indiquez si la règle doit être déclenchée de façon instantanée ou après un certain nombre de millisecondes. Voir la section [Options](#options) pour plus d’informations sur les paramètres d’événement personnalisables.

### Autres événements

#### Custom Event

L’événement se déclenche si un type d’événement personnalisé se produit. Les fonctions JavaScript nommées et définies ailleurs dans le codebase peuvent être utilisées comme type d’événement personnalisé. Vous devez indiquer le nom du type d’événement personnalisé, puis configurer les autres paramètres tel que décrit dans la section [Options](#options) ci-dessous.

#### Data Element Changed

L’événement se déclenche en cas de modification d’un élément de données spécifié. Vous devez fournir un nom pour l’élément de données. Vous pouvez sélectionner lʼélément de données en saisissant son nom dans le champ de texte ou en sélectionnant lʼicône de lʼélément de données à droite du champ de texte et en effectuant ensuite une sélection dans une liste fournie dans la boîte de dialogue qui sʼaffiche.

#### Appel direct {#direct-call-event}

Un événement dʼappel direct contourne les systèmes de détection et de recherche dʼévénements. Les règles d’appel direct sont adaptées aux situations dans lesquelles vous devez indiquer au système ce qui se passe exactement. Elles s’avèrent également très utiles lorsque le système ne peut pas détecter un événement dans le DOM.

Lors de la définition d’un événement d’appel direct, vous devez spécifier une chaîne qui agira comme identifiant de cet événement. Si une [action Déclencher lʼappel direct](#direct-call-action) contenant le même identifiant est déclenchée, toutes les règles d’événement d’appel direct correspondant à cet identifiant s’exécuteront.

![Capture d’écran d’un événement d’appel direct dans l’interface utilisateur de la collecte de données](../../../images/extensions/client/core/direct-call-event.png)

#### Element Exists

L’événement se déclenche s’il existe un élément spécifié. Voir la section [Options](#options) pour plus d’informations sur les paramètres d’événement personnalisables.

#### Enters Viewport

L’événement se déclenche si l’utilisateur entre dans une fenêtre d’affichage spécifiée. Vous devez fournir un sélecteur CSS en tant que critère permettant de cibler les éléments correspondants. Vous devez également configurer si la règle doit être déclenchée de façon instantannée ou après un nombre spécifié de millisecondes, et si l’événement doit se déclencher chaque fois qu’il se produit ou uniquement la première fois.

Voir la section [Options](#options) pour plus d’informations sur les paramètres d’événement personnalisables.

#### History change

Lʼévénement se déclenche si un événement « pushState » ou « hashchange » se produit. Il n’existe aucun paramètre pour ce type d’événement.

#### Time-Spent on Page

L’événement se déclenche si l’utilisateur reste sur la page pendant un certain nombre de secondes. Indiquez le nombre de secondes qui doivent s’écouler avant le déclenchement de l’événement.

### Événements de chargement de page

#### DOM Ready

L’événement se déclenche lorsque le DOM est prêt et que l’utilisateur peut interagir avec la page. Il n’existe aucun paramètre pour ce type d’événement.

#### Library Loaded (Page Top) {#library-loaded-page-top}

L’événement se déclenche dès que la bibliothèque de balises est chargée. Il n’existe aucun paramètre pour ce type d’événement.

#### Page Bottom {#page-bottom}

L’événement se déclenche une fois que `_satellite.pageBottom();` a été appelé. Ce type d’événement ne doit pas être utilisé lors du chargement asynchrone de la bibliothèque de balises. Il n’existe aucun paramètre pour ce type d’événement.

#### Window Loaded

L’événement se déclenche lorsque le navigateur appelle onLoad et que le chargement de la page est terminé. Il n’existe aucun paramètre pour ce type d’événement.

### Options {#options}

Chacun des types d’événements de formulaire utilise les paramètres suivants :

#### Specific Elements \| Any Element

* Si vous choisissez **[!UICONTROL Éléments spécifiques]**, les options permettant de sélectionner les éléments et les valeurs de propriété s’affichent.
* Si vous choisissez **[!UICONTROL N’importe quel élément]**, aucune autre option n’est nécessaire pour réduire les éléments.

#### Elements matching the CSS selector

Entrez le sélecteur CSS permettant d’identifier les éléments qui déclenchent l’événement.

#### And having certain property values

Lorsque vous sélectionnez cette option, les paramètres suivants deviennent disponibles :

* `property=value`

  Indiquez la valeur de la propriété.

* Regex

  Activez si `property=value` est une expression régulière.

* Add

  Ajoutez une autre paire `property=value`.

#### Advanced options (Bubbling)

* Exécuter cette règle même lorsque l’événement provient d’un élément descendant
* Autoriser cette règle à s’exécuter même si l’événement a déjà déclenché une règle qui cible un élément descendant
* Une fois la règle exécutée, empêcher l’événement de déclencher des règles qui ciblent des éléments ancêtres

## Types de conditions de l’extension Core

Cette section décrit les types de conditions disponibles dans l’extension Core. Ces types de condition peuvent être utilisés avec le type de logique normal ou Exception.

### Données

#### Cookie

Spécifiez le nom et la valeur du cookie devant exister pour qu’un événement déclenche une action.

1. Indiquez un nom de cookie.
1. Entrez la valeur qui doit exister dans le cookie si l’événement doit déclencher une action.
1. (Facultatif) Activez les Regex s’il s’agit d’une expression régulière.

#### Custom Code

Spécifiez un code personnalisé qui doit exister comme condition de l’événement.

>[!NOTE]
>
>ES6+ JavaScript est désormais pris en charge dans le code personnalisé. Notez que certains navigateurs plus anciens ne prennent pas en charge ES6+. Pour comprendre l’impact de l’utilisation des fonctions ES6+, testez-les par rapport à tous les navigateurs web qui doivent être pris en charge.

Utilisez l’éditeur de code intégré pour saisir le code personnalisé :

1. Sélectionnez **[!UICONTROL Ouvrir l’éditeur]**.
1. Saisissez le Custom Code.
1. Sélectionnez **[!UICONTROL Enregistrer]**.

Une variable nommée `event` sera automatiquement disponible et vous pouvez y faire référence à partir de votre Custom Code. L’objet `event` contient des informations utiles sur l’événement qui a déclenché la règle. Le moyen le plus simple de déterminer les données d’événement disponibles consiste à connecter `event` à la console à partir du code personnalisé :

```javascript
console.log(event);
return true;
```

Exécutez la règle dans un navigateur et examinez l’objet d’événement consigné dans la console du navigateur. Une fois que vous avez compris quelles informations sont disponibles, vous pouvez les utiliser pour la prise de décision par programmation dans votre Custom Code.

*Séquençage de conditions*

Lorsque l’option « Exécuter les composants de règle en séquence » dans les paramètres de propriété est activée, vous pouvez faire attendre les composants de règle suivants pendant que votre condition effectue une tâche asynchrone.

Lorsque la condition renvoie une [promesse](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/Promise), la prochaine condition de la règle ne s’exécutera pas tant que la promesse renvoyée n’aura pas été résolue. Si la promesse est refusée, les balises considèrent que la condition a échoué et aucune autre condition ou action de cette règle ne sera exécutée.

Exemple de condition qui renvoie une promesse :

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

#### Value Comparison (Comparaison de valeurs) {#value-comparison}

Compare deux valeurs afin de déterminer si cette condition renvoie true (vrai).

Si vous disposez d’une règle avec plusieurs conditions, il est possible que cette condition renvoie true (vrai), mais que la règle ne se déclenche toujours pas, car les autres conditions sont considérées comme false (faux) ou l’une des exceptions est considérée comme true (vrai).

1. Donnez une valeur.
1. Sélectionnez l’opérateur. Pour plus d’informations, reportez-vous à la liste des opérateurs de comparaison de valeurs ci-dessous.
1. (Si nécessaire) Indiquez si la comparaison doit être sensible à la casse.
1. Donnez une autre valeur pour la comparaison.

Les opérateurs de comparaison de valeurs suivants sont disponibles :

**Equal :** la condition renvoie true (vrai) si les deux valeurs sont égales à l’aide d’une comparaison non stricte (dans JavaScript, l’opérateur ==). Les valeurs peuvent être de n’importe quel type. Lorsque vous saisissez un mot tel que _true_ (vrai), _false_ (faux), _null_ (nul) ou _undefined_ (non défini) dans un champ de valeur, le mot est comparé en tant que chaîne et n’est pas converti vers son équivalent JavaScript.

**Does Not Equal** (N’est pas égal à) : la condition renvoie true (vrai) si les deux valeurs ne sont pas égales à l’aide d’une comparaison non stricte (dans JavaScript, l’opérateur !=). Les valeurs peuvent être de n’importe quel type. Lorsque vous saisissez un mot tel que _true_ (vrai), _false_ (faux), _null_ (nul) ou _undefined_ (non défini) dans un champ de valeur, le mot est comparé en tant que chaîne et n’est pas converti vers son équivalent JavaScript.

**Contains :** la condition renvoie true (vrai) si la première valeur contient la seconde valeur. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition renvoie false (faux).

**Does Not Contain :** la condition renvoie true (vrai) si la première valeur ne contient pas la seconde valeur. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition va renvoyer true (vrai).

**Starts With :** la condition renvoie true (vrai) si la première valeur commence par la seconde valeur. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition renvoie false (faux).

**Does Not Start With :** la condition renvoie true (vrai) si la première valeur ne commence pas par la seconde valeur. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition renvoie true (vrai).

**Ends With :** la condition renvoie true (vrai) si la première valeur termine par la seconde valeur. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition renvoie false (faux).

**Does Not End With :** la condition renvoie true (vrai) si la première valeur ne se termine pas par la seconde valeur. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition renvoie true (vrai).

**Matches Regex :** la condition renvoie true (vrai) si la première valeur correspond à l’expression régulière. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition renvoie false (faux).

**Does Not Match Regex :** la condition renvoie true (vrai) si la première valeur ne correspond pas à l’expression régulière. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition renvoie true (vrai).

**Is Less Than :** la condition renvoie true (vrai) si la première valeur est inférieure à la seconde valeur. Les chaînes représentant des nombres sont converties en nombres. Pour toute autre valeur qu’un nombre ou une chaîne convertible, la condition renvoie false (faux).

**Is Less Than Or Equal To :** la condition renvoie true (vrai) si la première valeur est inférieure ou égale à la seconde valeur. Les chaînes représentant des nombres sont converties en nombres. Pour toute autre valeur qu’un nombre ou une chaîne convertible, la condition renvoie false (faux).

**Is Greater Than :** la condition renvoie true (vrai) si la première valeur est supérieure à la seconde valeur. Les chaînes représentant des nombres sont converties en nombres. Pour toute autre valeur qu’un nombre ou une chaîne convertible, la condition renvoie false (faux).

**Is Greater Than Or Equal To :** la condition renvoie true (vrai) si la première valeur est supérieure ou égale à la seconde valeur. Les chaînes représentant des nombres sont converties en nombres. Pour toute autre valeur qu’un nombre ou une chaîne convertible, la condition renvoie false (faux).

**Is True :** la condition renvoie true (vrai) si la valeur est une valeur booléenne dont la valeur est true (vrai). La valeur fournie n’est pas convertie en valeur booléenne s’il s’agit d’un autre type. Pour toute autre valeur qu’une valeur booléenne dont la valeur est true (vrai), la condition renvoie false (faux).

**Is Truthy :** la condition renvoie true (vrai) si la valeur est true (vrai) après avoir été convertie en valeur booléenne. Voir la [documentation sur la condition Truthy de MDN](https://developer.mozilla.org/fr-FR/docs/Glossaire/Truthy) pour des exemples de valeurs « truthy ».

**Is False :** la condition renvoie true (vrai) si la valeur est une valeur booléenne dont la valeur est false (faux). La valeur fournie n’est pas convertie en valeur booléenne s’il s’agit d’un autre type. Pour toute autre valeur qu’une valeur booléenne dont la valeur est false (faux), la condition renvoie false (faux).

**Is Falsy :** la condition renvoie true (vrai) si la valeur est false (faux) après avoir été convertie en valeur booléenne. Voir la [documentation sur la condition Falsy de MDN](https://developer.mozilla.org/fr-FR/docs/Glossaire/Falsy) pour des exemples de valeurs « falsy ».

#### Variable

Spécifiez le nom et la valeur de la variable JavaScript devant exister pour qu’un événement déclenche une action.

1. Spécifiez le nom de la variable JavaScript.
1. Spécifiez la valeur de la variable qui doit exister comme condition pour l’événement.
1. (Facultatif) Activez les Regex s’il s’agit d’une expression régulière.

### Engagement

#### Page de destination

Indiquez la page sur laquelle l’utilisateur doit entrer pour déclencher l’événement.

1. Indiquez la page de destination.
1. (Facultatif) Activez les Regex s’il s’agit d’une expression régulière.

#### New/Returning Visitor

Indiquez si le visiteur doit être un nouveau visiteur ou un visiteur récurrent pour qu’un événement déclenche une action.

Sélectionnez l’une des options suivantes :

* New Visitor
* Returning Visitor

#### Page Views

Configurez le nombre de fois où le visiteur doit consulter la page avant que l’action ne soit déclenchée.

1. Sélectionnez si le nombre de pages vues doit être supérieur, égal ou inférieur à la valeur indiquée.
1. Indiquez le nombre de pages vues qui déterminent si la condition est remplie.
1. Configurez le moment où les pages vues sont comptabilisées en sélectionnant l’une des options suivantes :
   * Lifetime
   * Current Session

#### Sessions

Déclenchez l’action si le nombre de sessions de l’utilisateur respecte les critères indiqués.

1. Indiquez si le nombre de sessions doit être supérieur, égal ou inférieur à la valeur indiquée.
1. Indiquez le nombre de sessions qui déterminent si la condition est remplie.

#### Temps passé sur le site

Déclenchez l’action si le nombre de sessions de l’utilisateur respecte les critères indiqués.

Configurez la durée pendant laquelle le visiteur doit se trouver sur le site avant que l’action ne soit déclenchée.

1. Sélectionnez si le nombre de minutes passées par l’utilisateur sur le site doit être supérieur, égal ou inférieur à la valeur indiquée.
1. Indiquez le nombre de minutes qui déterminent si la condition est remplie.

#### Traffic Source

Déclenchez l’action si le nombre de sessions de l’utilisateur respecte les critères indiqués.

Spécifiez la source du trafic du visiteur qui doit être true (vrai) pour que l’action soit déclenchée.

1. Indiquez la source du trafic.
1. (Facultatif) Activez les Regex s’il s’agit d’une expression régulière.

### Technologie

#### Browser

Sélectionnez le navigateur que le visiteur doit utiliser pour que l’action soit déclenchée.

Sélectionnez un ou plusieurs navigateurs parmi les suivants :

* Chrome
* Firefox
* Internet Explorer / Edge
* Internet Explorer Mobile
* Safari mobile
* OmniWeb
* Opera
* Opera Mini
* Opera Mobile
* Safari

#### Type d’appareil

Sélectionnez le type d’appareil que le visiteur doit utiliser pour que l’action soit déclenchée.

Sélectionnez un ou plusieurs types d’appareils parmi les suivants :

* Android
* BlackBerry
* Bureau
* iPad
* iPhone
* iPod
* Nokia
* Windows Phone

#### Operating System

Sélectionnez le système d’exploitation que le visiteur doit utiliser pour que l’action soit déclenchée.

Sélectionnez un ou plusieurs des systèmes d’exploitation suivants :

* Android
* BlackBerry
* iOS
* Linux
* MacOS
* Maemo
* Symbian OS
* Unix
* Windows

#### Screen Resolution

Sélectionnez la résolution d’écran que les visiteurs doivent utiliser sur leurs appareils pour que l’action soit déclenchée.

1. Indiquez si la largeur de résolution de l’écran de l’appareil du visiteur doit être supérieure, égale ou inférieure à la valeur spécifiée.
1. Indiquez le nombre de pixels requis pour la largeur de résolution d’écran.
1. Indiquez si la hauteur de résolution de l’écran de l’appareil du visiteur doit être supérieure, égale ou inférieure à la valeur spécifiée.
1. Indiquez le nombre de pixels requis pour la hauteur de résolution d’écran.

#### Window Size

Sélectionnez la taille de la fenêtre que les visiteurs doivent utiliser sur leurs appareils pour que l’action soit déclenchée.

1. Indiquez si la largeur de la taille de fenêtre de l’appareil du visiteur doit être supérieure ou égale à la valeur spécifiée.
1. Spécifiez le nombre de pixels requis pour la largeur de la taille de fenêtre.
1. Indiquez si la hauteur de la taille de fenêtre de l’appareil du visiteur doit être supérieure ou égale à la valeur spécifiée.
1. Spécifiez le nombre de pixels requis pour la hauteur de la taille de fenêtre.

### URL

#### Domaine

Indiquez le domaine du visiteur.

#### Hash

Indiquez un ou plusieurs modèles de hachage qui doivent exister dans l’URL.

>[!NOTE]
>
>Plusieurs modèles de hachage sont unis par un OR.

1. Indiquez le modèle de hachage.
1. (Facultatif) Activez les Regex s’il s’agit d’une expression régulière.
1. Ajoutez d’autres modèles de hachage.

#### Chemin Et Chaîne De Requête

Indiquez un ou plusieurs chemins d’accès qui doivent exister dans l’URL.  Cela inclut le chemin et la chaîne de requête.

>[!NOTE]
>
>Plusieurs chemins sont unis par un OR.

1. Indiquez le chemin d’accès.
1. (Facultatif) Activez les Regex s’il s’agit d’une expression régulière.
1. Ajoutez d’autres chemins d’accès.

#### Chemin sans chaîne de requête

Indiquez un ou plusieurs chemins d’accès qui doivent exister dans l’URL.  Cela inclut le chemin d’accès, mais n’inclut pas la chaîne de requête.

>[!NOTE]
>
>Plusieurs chemins sont unis par un OR.

1. Indiquez le chemin d’accès.
1. (Facultatif) Activez les Regex s’il s’agit d’une expression régulière.
1. Ajoutez d’autres chemins d’accès.

#### Protocol

Indiquez le protocole utilisé dans l’URL.

Sélectionnez l’une des options suivantes :

* HTTP
* HTTPS

#### Query String Parameter

Indiquez le paramètre d’URL utilisé dans l’URL.

1. Indiquez un nom de paramètre d’URL.
1. Indiquez la valeur utilisée pour le paramètre d’URL.
1. (Facultatif) Activez les Regex s’il s’agit d’une expression régulière.

#### Subdomain

Indiquez un ou plusieurs sous-domaines qui doivent exister dans l’URL.

>[!NOTE]
>
>Plusieurs sous-domaines sont unis par un OR.

1. Indiquez le sous-domaine.
1. (Facultatif) Activez les Regex s’il s’agit d’une expression régulière.
1. Ajoutez d’autres sous-domaines.

### Autre

#### Date Range

Spécifiez une plage de dates. Sélectionnez la date et l’heure auxquelles l’événement se produit après, la date à laquelle il se produit avant et le fuseau horaire.

#### Max Frequency

Indiquez le nombre maximal de fois où la condition renvoie true (vrai). Vous avez les choix suivants :

* Page view
* Sessions
* Visitor
* Seconds
* Minutes
* Days
* Weeks
* Months

Pour la fréquence maximale de la condition 1 par session, ces deux éléments `localStorage` sont comparés. Si la valeur `visitorTracking.sessionCount` est supérieure au nombre `maxFrequency.session`, la condition d’échantillonnage est vraie. S’ils sont égaux, la condition est fausse.

`sessionCount` est un élément `visitorTracking`. L’API du visiteur doit donc être activée pour que la condition d’échantillonnage fonctionne.

#### Sampling

Indiquez le pourcentage de fois où la condition renvoie true (vrai).

## Types d’actions de l’extension Core

Cette section décrit les types d’actions disponibles dans l’extension Core.

### Custom Code

>[!NOTE]
>
>ES6+ JavaScript est désormais pris en charge dans le code personnalisé. Notez que certains navigateurs plus anciens ne prennent pas en charge ES6+. Pour comprendre l’impact de l’utilisation des fonctions ES6+, testez-les par rapport à tous les navigateurs web qui doivent être pris en charge.

Fournissez le code qui s’exécute une fois que l’événement est déclenché et que les conditions sont évaluées.

1. Nommez le code d’action.
1. Sélectionnez le langage utilisé pour définir l’action :
   * JavaScript
   * HTML
1. Indiquez si le code d’action doit être exécuté globalement.
1. Sélectionnez **[!UICONTROL Ouvrir l’éditeur]**.
1. Modifiez le code, puis cliquez sur **[!UICONTROL Enregistrer]**.

Lorsque JavaScript est sélectionné comme langage, une variable nommée `event` est automatiquement disponible et vous pouvez y faire référence à partir de votre Custom Code. L’objet `event` contient des informations utiles sur l’événement qui a déclenché la règle. Le moyen le plus simple de déterminer les données d’événement disponibles consiste à connecter `event` à la console à partir du code personnalisé :

```javascript
console.log(event);
```

Exécutez la règle dans un navigateur et examinez l’objet d’événement consigné dans la console du navigateur. Une fois que vous avez compris quelles informations sont disponibles, vous pouvez les utiliser pour la prise de décision programmée dans votre code personnalisé, envoyer une partie de l’objet `event` à un serveur et bien plus encore.

### Traitement de l’action Custom Code

L’extension Core, disponible pour tous les utilisateurs d’Adobe Experience Platform, contient une action Code personnalisé pour l’exécution du code JavaScript ou HTML fourni par l’utilisateur. Il est souvent utile que les utilisateurs comprennent comment les règles avec les actions Custom Code sont traitées.

#### Règles utilisant les événements de haut ou de bas de page

Le code provenant d’actions personnalisées est incorporé dans la bibliothèque de balises principale. Le code est écrit dans le document à l’aide de document.write. Si une règle comporte plusieurs actions Custom Code, le code est écrit dans l’ordre configuré dans la règle.

#### Règles utilisant n’importe quel autre événement que haut de page ou bas de page

Le code provenant d’actions personnalisées est chargé depuis le serveur et écrit dans le document à l’aide de [Postscribe](https://github.com/krux/postscribe). Si une règle comporte plusieurs actions Custom Code, le code est chargé en parallèle depuis le serveur, mais écrit dans l’ordre configuré dans la règle.

Bien que l’utilisation de document.write après le chargement d’une page poserait généralement des problèmes, ce n’est pas problématique pour le code fourni via des actions Custom Code. Vous pouvez utiliser document.write dans des actions Custom Code, quelle que soit la date d’exécution du code.

#### Validation du Custom Code

Le programme de validation utilisé dans lʼéditeur de code de balises est conçu pour identifier les problèmes liés au code écrit par le développeur. Le code qui a fait l’objet d’un processus de minimisation (tel que le code AppMeasurement.js téléchargé depuis le Gestionnaire de code) peut être faussement signalé comme ayant des problèmes par le programme de validation de, lesquels peuvent généralement être ignorés.

#### Séquencage d’actions

Lorsque l’option « Exécuter les composants de règle en séquence » dans les paramètres de propriété est activée, vous pouvez faire attendre les composants de règle suivants pendant que votre action effectue une tâche asynchrone.  Cela fonctionne différemment pour le Custom Code JavaScript et HTML.

*JavaScript*

Lors de la création d’une action Custom Code JavaScript, vous pouvez renvoyer une [promesse](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/Promise) depuis votre action. L’action suivante de la règle sera exécutée uniquement lorsque la promesse renvoyée sera résolue. Si la promesse est refusée, les actions suivantes de la règle ne seront pas exécutées.

>[!NOTE]
>
>Cela ne fonctionne que si votre code JavaScript n’est pas défini pour s’exécuter globalement. Si vous exécutez votre action Custom Code dans la portée globale, les balises traitent la promesse comme résolue immédiatement et passent à l’élément suivant dans la file d’attente de traitement.

Exemple d’action Custom Code JavaScript renvoyant une promesse :

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

*HTML*

Lors de la création d’une action Custom Code HTML, une fonction nommée `onCustomCodeSuccess()` peut être utilisée dans votre Custom Code. Vous pouvez appeler cette fonction pour indiquer que votre Custom Code est terminé et que les balises peuvent passer à l’exécution des actions suivantes. D’un autre côté, si votre Custom Code a échoué d’une manière ou d’une autre, vous pouvez appeler `onCustomCodeFailure()`. Cette action indiquera aux balises de ne pas exécuter les actions suivantes à partir de cette règle.

Exemple d’action Custom Code HTML utilisant les nouveaux rappels :

```html
<script>
setTimeout(function() {
  if (new Date().getDay() === 5) {
    onCustomCodeSuccess();
  } else {
    onCustomCodeFailure();
  }
}, 1000);
</script>
```

### Déclencher lʼappel direct {#direct-call-action}

Cette action déclenche toutes les règles qui utilisent un [événement dʼappel direct](#direct-call-event) spécifique. Lors de la configuration de l’action, vous devez fournir la chaîne d’identifiant de l’événement dʼappel direct à déclencher. Vous pouvez également transmettre des données à l’événement dʼappel direct au moyen d’un objet `detail`, qui peut contenir un ensemble personnalisé de paires clé-valeur.

![Capture d’écran d’une action Déclencher lʼappel direct dans l’interface utilisateur de la collecte de données](../../../images/extensions/client/core/direct-call-action.png)

L’action mappe directement à la méthode [`track`](../../../ui/client-side/satellite-object.md#track) dans lʼobjet `satellite`, accessible par le code côté client.

## Types d’éléments de données de l’extension Core

Les types d’éléments de données sont déterminés par l’extension. Les types qui peuvent être créés ne sont pas limités.

Les sections suivantes décrivent les types d’éléments de données disponibles dans l’extension Core. D’autres extensions utilisent d’autres types d’éléments de données.

### Cookie

Tout cookie de domaine disponible peut être référencé dans le champ du nom du cookie.

#### Exemple :

`cookieName`

### Constant

Toute valeur de chaîne constante qui peut ensuite être référencée dans des actions ou des conditions.

#### Exemple :

`string`

### Custom code

>[!NOTE]
>
>ES6+ JavaScript est désormais pris en charge dans le code personnalisé. Notez que certains navigateurs plus anciens ne prennent pas en charge ES6+. Pour comprendre l’impact de l’utilisation des fonctions ES6+, testez-les par rapport à tous les navigateurs web qui doivent être pris en charge.

Il est possible d’entrer du code JavaScript personnalisé dans l’interface utilisateur en cliquant sur Open Editor et en insérant le code dans la fenêtre de l’éditeur.

Une instruction de retour est nécessaire dans la fenêtre de l’éditeur afin d’indiquer quelle valeur doit être utilisée en tant que valeur de l’élément de données. Si une instruction de retour n’est pas incluse ou que la valeur `null` ou `undefined` est renvoyée, la valeur par défaut de l’élément de données est utilisée comme valeur de l’élément de données.

**Exemple :**

```javascript
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

Si l’élément de données de Custom Code est récupéré dans le cadre de l’exécution d’une règle, une variable nommée `event` est automatiquement disponible et vous pouvez y faire référence à partir de votre code personnalisé. L’objet `event` contient des informations utiles sur l’événement qui a déclenché la règle. Le moyen le plus simple de déterminer les données d’événement disponibles consiste à connecter `event` à la console à partir du code personnalisé :

```javascript
console.log(event);
return true;
```

Exécutez la règle dans un navigateur et examinez l’objet d’événement consigné dans la console du navigateur. Une fois que vous avez compris quelles informations sont disponibles sous les différentes règles pouvant utiliser votre élément de données, vous pouvez les utiliser pour la prise de décision programmée dans votre code personnalisé ou renvoyer une partie de l’objet `event` comme valeur de l’élément de données.

### Attribut DOM

N’importe quelle valeur d’élément peut être récupérée (balise div ou H1, par exemple).

#### Exemple :

Chaîne de sélecteur CSS :

`id#dc logo img`

Obtention de la valeur de :

`src`

### Variable JavaScript

N’importe quelle variable ou n’importe quel objet JavaScript peut être référencé à l’aide du champ de chemin d’accès.

Les éléments de données de balise peuvent être utilisés pour recueillir vos variables JavaScript de balisage ou vos propriétés d’objet. Ces valeurs peuvent ensuite être utilisées dans vos extensions ou règles personnalisées en référençant les éléments de données de balise. Si la source des données change, il suffit de mettre à jour la référence à la source.

Dans l’exemple ci-dessous, l’annotation contient une variable JavaScript nommée `Page_Name`.

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

Lorsque vous créez l’élément de données, il vous suffit de fournir le chemin d’accès à cette variable.

Si vous utilisez un objet collecteur de données dans votre couche de données, utilisez la notation point dans le chemin pour faire référence à l’objet et à la propriété que vous souhaitez capturer dans l’élément de données, par exemple `_myData.pageName`, ou `digitalData.pageName`, etc.

#### Exemple :

`window.document.title`

### Stockage local

Indiquez le nom de votre élément de stockage local dans le champ Local Storage Item Name.

Le stockage local permet aux navigateurs de stocker des informations d’une page à l’autre ([https://www.w3schools.com/html/html5_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp)). Le stockage local est très similaire aux cookies, mais est beaucoup plus volumineux et plus souple.

Utilisez le champ fourni pour spécifier la valeur que vous avez créée pour un élément de stockage local, comme `lastProductViewed.`

### Objets fusionnés

Sélectionnez plusieurs éléments de données qui fourniront chacun un objet. Ces objets seront profondément (récursivement) fusionnés pour produire un nouvel objet. Les objets source ne seront pas modifiés. Si une propriété se trouve au même endroit sur plusieurs objets source, la valeur du dernier objet sera utilisée. Si la valeur d’une propriété source est `undefined`, elle ne remplacera pas une valeur provenant d’un objet source antérieur. Si des tableaux se trouvent au même endroit sur plusieurs objets source, les tableaux seront concaténés.

À titre d’exemple, supposons que vous sélectionniez un élément de données qui fournit l’objet suivant :

```
{
  "sport": {
    "name": "tennis"
  },
  "dessert": "ice cream",
  "fruits": [
    "apple",
    "banana"
  ]
}
```

Supposons que vous sélectionniez également un autre élément de données qui fournit l’objet suivant :

```
{
  "sport": {
    "name": "volleyball"
  },
  "dessert": undefined,
  "pet": "dog",
  "instrument": undefined,
  "fruits": [
    "cherry",
    "duku"
  ]
}
```

Le résultat de l’élément de données Objets fusionnés serait l’objet suivant :

```
{
  "sport": {
    "name": "volleyball"
  },
  "dessert": "ice cream",
  "pet": "dog",
  "instrument": undefined,
  "fruits": [
    "apple",
    "banana",
    "cherry",
    "duku"
  ]
}
```

### Informations sur la page

Utilisez ces points de données pour recueillir les informations sur la page à utiliser dans la logique votre règle ou pour envoyer des informations à Analytics ou à des systèmes de suivi externes.

Vous pouvez sélectionner l’un des attributs de page suivants à utiliser dans votre élément de données :

* URL
* Hostname
* Nom du chemin
* Protocol
* Référent
* Title

### Query String Parameter

Spécifiez un paramètre d’URL unique dans le champ URL Parameter.

Seule la section de nom est nécessaire. Les indicateurs spéciaux tels que « ? » ou « = » doivent être omis.

#### Exemple :

`contentType`

### Nombre aléatoire

Utilisez cet élément de données pour générer un nombre aléatoire. Elle est souvent utilisée pour échantillonner des données ou créer des identifiants, tels qu’un identifiant d’accès. Le nombre aléatoire peut également être utilisé pour obscurcir ou appliquer un salage aux données sensibles. Voici quelques exemples :

* Générer un ID d’accès
* Concaténer le nombre à un jeton utilisateur ou à un horodatage pour garantir l’unicité
* Réaliser un hachage unidirectionnel sur des données personnelles identifiables (PII)
* Déterminer de manière aléatoire à quel moment il convient d’afficher une demande d’enquête sur le site

Indiquez les valeurs minimale et maximale de votre nombre aléatoire.

**Valeurs par défaut :**

Minimum : 0

Maximum : 1 000 000 000

### Stockage de session

Indiquez le nom de votre élément de stockage de session dans le champ Session Storage Item Name.

Le stockage de session est similaire au stockage local, sauf que les données sont perdues une fois la session terminée, alors qu’un stockage local ou un cookie peut conserver les données.

### Comportement du visiteur

Semblable aux informations sur la page, cet élément de données utilise des types de comportement courants pour enrichir la logique dans les règles et autres solutions Experience Platform.

Sélectionnez l’un des attributs de comportement du visiteur suivants :

* Page de destination
* Traffic source
* Minutes on site
* Session count
* Session page view count
* Lifetime page view count
* Is new visitor

Voici quelques cas d’utilisation courants :

* Afficher une enquête une fois qu’un visiteur a consulté le site pendant cinq minutes
* S’il s’agit de la page de destination de la visite, renseigner une mesure Analytics
* Afficher une nouvelle offre au visiteur après un nombre de sessions égal à X
* Afficher un abonnement au bulletin d’information s’il s’agit d’un nouveau visiteur

### Valeur conditionnelle

Un wrapper pour la condition [Value Comparison](#value-comparison-value-comparison). En fonction du résultat de la comparaison, renverra l’une des deux valeurs disponibles dans le formulaire. Peut donc gérer les scénarios &quot;If... Then... Else...&quot; sans avoir besoin de règles supplémentaires.

### Environnement d’exécution

Permet de sélectionner l’une des variables suivantes :

* Étape de l’environnement - Renvoie `_satellite.environment.stage` pour différencier les environnements de développement/évaluation/production.
* Date de création de la bibliothèque - Renvoie `turbine.buildInfo.buildDate` qui contient la même valeur que `_satellite.buildInfo.buildDate`.
* Nom de la propriété - Renvoie `_satellite.property.name` pour obtenir le nom de la propriété Launch.
* ID de la propriété - Renvoie `_satellite.property.id` pour obtenir l’identifiant de la propriété Launch.
* Rule name - Renvoie `event.$rule.name` contenant le nom de la règle exécutée.
* Rule ID - Renvoie `event.$rule.id` contenant l’identifiant de la règle exécutée.
* Event type - Renvoie `event.$type` contenant le type d’événement qui a déclenché la règle.
* Event detail payload - Renvoie `event.detail` contenant la payload d’un événement personnalisé ou d’une règle d’appel direct.
* Direct call identifier - Renvoie `event.identifier` contenant l’identifiant d’une règle d’appel direct.

### Attributs de l’appareil

Renvoie l’un des attributs d’appareil du visiteur suivants :

* Taille de la fenêtre du navigateur
* Taille d’écran

### Outils JavaScript

Il s’agit d’un wrapper pour les opérations JavaScript courantes. Il reçoit un élément de données en entrée. Il renvoie le résultat de l’une des transformations suivantes de la valeur de l’élément de données :

* Manipulation de base des chaînes (remplacement, sous-chaîne, correspondance regex, premier et dernier index, division, tranche)
* Opérations de base sur les tableaux (division, liaison, affichage, déplacement)
* Opérations universelles de base (division, longueur)