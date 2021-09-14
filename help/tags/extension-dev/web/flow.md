---
title: Flux d’extension web
description: Découvrez comment les composants d’extension web interagissent les uns avec les autres au moment de l’exécution dans Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: ht
source-wordcount: '270'
ht-degree: 100%

---

# Flux d’extension web

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Dans les extensions web, chaque type d’événement, de condition, d’action et d’élément de données comporte à la fois une vue qui permet aux utilisateurs de modifier les paramètres et un module de bibliothèque leur permettant d’agir sur ces paramètres définis par l’utilisateur.

Comme le montre le diagramme de haut niveau suivant, la vue de type d’événement de l’extension sera affichée dans un iframe dans l’application intégrée à Adobe Experience Platform. L’utilisateur utilise ensuite la vue pour modifier les paramètres qui sont alors enregistrés dans Platform. Lorsque la bibliothèque d’exécution de balises est créée, le module de bibliothèque de type d’événement de l’extension ainsi que les paramètres définis par l’utilisateur sont inclus dans la bibliothèque d’exécution. Au moment de l’exécution, Platform injectera les paramètres définis par l’utilisateur dans le module de bibliothèque.

![diagramme de flux d’extension](../images/flow/web/extension-flow.png)

Dans le diagramme suivant, vous pouvez voir le lien entre les événements, les conditions et les actions dans le flux de traitement des règles.

![diagramme de flux de traitement des règles](../images/flow/web/rule-processing-flow.png)

Le flux de traitement des règles contient les phases suivantes :

1. La méthode `settings` et la méthode `trigger` sont fournies au module de bibliothèque d’événements au démarrage.
1. Lorsque le module de bibliothèque d’événements détermine que l’événement s’est produit, le module de bibliothèque d’événements appelle `trigger`.
1. Les balises transmettent `settings` dans les modules de bibliothèque de conditions de la règle où les conditions sont évaluées.
1. Chaque module de bibliothèque de conditions renvoie si une condition est évaluée comme vraie.
1. Si toutes les conditions sont remplies, les actions de la règle sont exécutées.
