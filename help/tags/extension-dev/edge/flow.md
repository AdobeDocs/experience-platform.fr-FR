---
title: Flux d’extension Edge
description: Découvrez comment les composants d’une extension Edge dans Adobe Experience Platform interagissent les uns avec les autres au moment de l’exécution.
exl-id: 99058e22-3e14-4ec6-858e-bb1c1fafdb7c
TQID: https://experienceleague.adobe.com/1cYf-3uRV0NSFBaEr2C5yaHfF9XQ0jcZfFgOozG7ElA
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 240
ht-degree: 77%

---

# Flux d’extension Edge

Dans les extensions Edge, chaque condition, action et type d’élément de donnée comporte à la fois une vue qui permet aux utilisateurs de modifier les paramètres et un module de bibliothèque leur permettant d’agir sur ces paramètres définis par l’utilisateur.

Comme le montre le diagramme de haut niveau suivant, la vue du type d’action de l’extension sera affichée dans un iframe dans l’application intégrée à Adobe Experience Platform. La vue est ensuite utilisée pour modifier les paramètres qui sont ensuite enregistrés dans Experience Platform. Lorsque la bibliothèque d’exécution des balises est créée, le module Bibliothèque de type d’action de l’extension ainsi que les paramètres définis par l’utilisateur sont inclus dans la bibliothèque d’exécution. Cette bibliothèque est ensuite déployée sur le nœud Edge. Les paramètres définis par l’utilisateur d’Experience Platform sont injectés dans le module Bibliothèque au moment de l’exécution.

![diagramme de flux d’extension](../images/flow/edge/event-processing-flow.png)

Dans le diagramme suivant, vous pouvez voir le lien entre les événements, les conditions et les actions dans le flux de traitement des règles.

![diagramme de flux de traitement des règles](../images/flow/edge/rule-processing-flow.png)

Le flux de traitement des règles contient les phases suivantes :

1. La méthode `settings` et la méthode `trigger` sont fournies au module de bibliothèque d’événements au démarrage.
1. Lorsque le module de bibliothèque d’événements détermine que l’événement s’est produit, le module de bibliothèque d’événements appelle `trigger`.
1. Experience Platform transmet les `settings` dans les modules de bibliothèque de type de condition de la règle dans lesquels les conditions sont évaluées.
1. Chaque type de condition effectue un renvoi indiquant si une condition est évaluée comme vraie.
1. Si toutes les conditions sont remplies, les actions de la règle sont exécutées.
