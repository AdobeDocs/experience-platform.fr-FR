---
title: Déploiement asynchrone
description: Découvrez comment déployer les bibliothèques de balises d’Adobe Experience Platform de manière asynchrone sur votre site web.
exl-id: ed117d3a-7370-42aa-9bc9-2a01b8e7794e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 98%

---

# Déploiement asynchrone {#asynchronous-deployment}

>[!CONTEXTUALHELP]
>id="platform_tags_asynchronous_deployment"
>title="Déploiement asynchrone"
>abstract="Si cette option est activée, lorsque cette balise script est analysée, le navigateur commencera à charger le fichier JavaScript, mais au lieu d’attendre que la bibliothèque soit chargée et exécutée, il continuera à analyser et à rendre le reste du document. Cela peut améliorer les performances des pages web, mais a des implications importantes en ce qui concerne l’exécution de certaines règles. Voir la documentation pour plus de détails."

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Les performances et le déploiement sans blocage des bibliothèques JavaScript exigés par nos produits sont de plus en plus importants pour les utilisateurs dʼAdobe Experience Cloud. Des outils tels que [[!DNL Google PageSpeed]](https://developers.google.com/speed/pagespeed/insights/) recommandent aux utilisateurs de modifier leur manière de déployer les bibliothèques Adobe sur leur site. Cet article explique comment utiliser les bibliothèques JavaScript dʼAdobe de manière asynchrone.

## Synchrone et asynchrone

### Déploiement synchrone

Souvent, les bibliothèques sont chargées de manière synchrone dans la balise `<head>` d’une page. Par exemple :

```markup
<script src="example.js"></script>
```

Par défaut, le navigateur analyse le document et atteint cette ligne, puis commence à récupérer le fichier JavaScript à partir du serveur. Le navigateur attend que le fichier soit renvoyé, puis analyse et exécute le fichier JavaScript. Enfin, il continue d’analyser le reste du document HTML.

Si l’analyseur rencontre la balise `<script>` avant de rendre le contenu visible, l’affichage du contenu est retardé. Si le fichier JavaScript en cours de chargement n’est pas absolument nécessaire pour présenter le contenu à vos utilisateurs, vous exigez inutilement que vos visiteurs attendent le contenu. Plus la bibliothèque est grande, plus le retard est important. C’est la raison pour laquelle des outils de test des performances de site web tels que [!DNL Google PageSpeed] ou [!DNL Lighthouse] marquent souvent des scripts chargés de manière synchrone.

Les bibliothèques de gestion des balises peuvent rapidement prendre de l’ampleur si vous disposez de nombreuses balises à gérer.

### Déploiement asynchrone

Vous pouvez charger n’importe quelle bibliothèque de manière asynchrone en ajoutant un attribut `async` à la balise `<script>`. Par exemple :

```markup
<script src="example.js" async></script>
```

Cela indique au navigateur que, lorsque cette balise script est analysée, il doit commencer à charger le fichier JavaScript, mais au lieu d’attendre que la bibliothèque soit chargée et exécutée, il doit continuer à analyser et à effectuer le rendu du reste du document.

## Considérations en matière de déploiement asynchrone

Comme décrit ci-dessus, dans le cas des déploiements synchrones, le navigateur suspend l’analyse et le rendu de la page pendant le chargement et l’exécution de la bibliothèque de balises Adobe Experience Platform. D’autre part, dans le cas des déploiements asynchrones, le navigateur poursuit l’analyse et le rendu de la page pendant le chargement de la bibliothèque. La variabilité du moment où le chargement de la bibliothèque de balises peut prendre fin par rapport à l’analyse et au rendu de la page doit être prise en compte.

Tout d’abord, puisque le chargement de la bibliothèque peut prendre fin avant ou après l’analyse et l’exécution du bas de la page, vous ne devriez plus appeler `_satellite.pageBottom()` depuis votre code de page (`_satellite` ne sera disponible qu’une fois la bibliothèque chargée). Ceci est expliqué dans [Chargement asynchrone du code intégré aux balises](#loading-the-tags-embed-code-asynchronously).

Ensuite, le chargement de la bibliothèque de balises peut se terminer avant ou après que l’événement de navigateur [`DOMContentLoaded`](https://developer.mozilla.org/fr-FR/docs/Web/Events/DOMContentLoaded) (DOM Ready) soit survenu.

Pour ces deux raisons, il est important de montrer comment les types d’événements [Library Loaded (Bibliothèque chargée)](../../extensions/client/core/overview.md#library-loaded-page-top), [Page Bottom (Bas de page)](../../extensions/client/core/overview.md#page-bottom), [DOM Ready (Prêt pour DOM)](../../extensions/client/core/overview.md#page-bottom), et [Window Loaded (Fenêtre chargée)](../../extensions/client/core/overview.md#window-loaded) provenant de l’extension Core fonctionnent lors du chargement asynchrone d’une bibliothèque.

Si votre propriété de balise contient les quatre règles suivantes :

* Règle A : utilise le type d’événement Library Loaded (Bibliothèque chargée).
* Règle B : utilise le type d’événement Page Bottom (Bas de page).
* Règle C : utilise le type d’événement DOM Ready (Prêt pour DOM).
* Règle D : utilise le type d’événement Window Loaded (Fenêtre chargée).

Quel que soit le moment auquel le chargement de la bibliothèque de balises se termine, l’exécution de toutes les règles est garantie, et ce dans l’ordre suivant :

Règle A → Règle B → Règle C → Règle D

Bien que l’ordre soit toujours suivi, il se peut que certaines règles soient exécutées immédiatement lorsque le chargement de la bibliothèque de balises se termine, tandis que d’autres pourront être exécutées ultérieurement. Les actions suivantes se produisent lorsque le chargement de la bibliothèque de balises se termine :

1. La règle A est exécutée immédiatement.
1. Si l’événement de navigateur `DOMContentLoaded` (DOM Ready (Prêt pour DOM)) est déjà survenu, la règle B et la règle C sont exécutées immédiatement. Dans le cas contraire, les règles B et C sont exécutées ultérieurement lorsque l’événement de navigateur [`DOMContentLoaded`](https://developer.mozilla.org/fr-FR/docs/Web/Events/DOMContentLoaded) survient.
1. Si l’événement de navigateur [`load`](https://developer.mozilla.org/fr-FR/docs/Web/Events/load) (Window Loaded [Fenêtre chargée]) est déjà survenu, la règle D est exécutée immédiatement. Dans le cas contraire, la règle D est exécutée ultérieurement lorsque l’événement de navigateur [`load`](https://developer.mozilla.org/fr-FR/docs/Web/Events/load) survient. Veillez noter que si vous avez installé la bibliothèque de balises conformément aux instructions, le chargement de la bibliothèque se termine *toujours* avant la survenue de l’événement de navigateur [`load`](https://developer.mozilla.org/fr-FR/docs/Web/Events/load).

Lorsque vous appliquez ces principes à votre propre site web, tenez compte des points suivants :

* **Une règle utilisant le type d’événement Library Loaded (Bibliothèque chargée) peut s’exécuter avant que la couche de données ne soit complètement chargée.** Cela peut entraîner l’exécution d’actions de règle avec des données manquantes, car les données n’étaient pas encore disponibles sur la page. Ces types de problèmes peuvent être atténués en ajustant la configuration de votre règle. À titre d’exemple, au lieu d’avoir une règle déclenchée par le type d’événement Library Loaded (Bibliothèque chargée), vous pouvez utiliser les types d’événements Custom Event (Événement personnalisé) ou Direct Call (Appel direct) qui sont déclenchés par votre code de page dès la fin du chargement de votre couche de données.
* **Le type d’événement Page Bottom (Bas de page) ne fournit pas spécialement de valeur lorsque la bibliothèque est chargée de manière asynchrone.** Prenez plutôt en compte les types d’événements Library Loaded (Bibliothèque chargée), DOM Ready (Prêt pour DOM), Window Loaded (Fenêtre chargée) ou autres.

Si vous constatez que des actions se produisent dans le désordre, il est probable que vous deviez faire face à certains problèmes de délai. Les déploiements qui nécessitent un délai précis peuvent exiger le recours à des récepteurs d’événements ou à des types d’événements Custom Event (Événement personnalisé) ou Direct Call (Appel direct) pour rendre leurs mises en œuvre plus solides et cohérentes.

## Chargement asynchrone du code intégré aux balises

Les balises proposent un bouton d’activation/désactivation permettant d’activer le chargement asynchrone lors de la création d’un code intégré au moment de la configuration d’un [environnement](../publishing/environments.md). Vous pouvez également configurer vous-même le chargement asynchrone :

1. Ajoutez un attribut asynchrone à la balise `<script>` pour charger le script de manière asynchrone.

   Pour le code intégré aux balises, cela revient à modifier ceci :

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js"></script>
   ```

   en ceci :

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js" async></script>
   ```

1. Supprimez le code que vous avez précédemment ajouté au bas de votre balise :

   ```markup
   <script type="text/javascript">_satellite.pageBottom();</script>
   ```

   Ce code indique à Experience Platform que l’analyseur du navigateur a atteint le bas de la page. Étant donné qu’il est probable que les balises n’aient pas été chargées et exécutées avant ce moment, l’invocation de `_satellite.pageBottom()` provoque une erreur, et le type d’événement Page Bottom (Bas de page) se comportera peut-être de façon inattendue.
