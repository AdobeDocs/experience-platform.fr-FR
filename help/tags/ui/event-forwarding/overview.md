---
title: Présentation du transfert d’événement
description: Découvrez le transfert d’événement dans Adobe Experience Platform, qui vous permet d’utiliser le réseau Platform Edge pour exécuter des tâches sans modifier votre mise en oeuvre des balises.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 39%

---

# Transfert d’événement - Aperçu

>[!NOTE]
>
>Adobe Experience Platform Launch a été rebaptisé en tant que suite de technologies de collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Le transfert d’événements dans Adobe Experience Platform réduit le poids des pages web et des applications en utilisant Adobe Experience Platform Edge Network pour exécuter les tâches normalement effectuées sur le client. Les règles de transfert d’événements peuvent transformer et envoyer des données vers de nouvelles destinations sans modifier les mises en oeuvre côté client.

Le transfert d’événement associé aux SDK Web et Mobile Adobe Experience Platform permet d’effectuer les opérations suivantes :

* Effectuez un seul appel à partir de la page qui contient un payload de données. Les données fédérent ensuite le côté serveur afin de réduire le trafic réseau côté client et de fournir une expérience plus rapide aux clients.
* Réduire le temps nécessaire au chargement des pages web pour que votre site soit conforme aux bonnes pratiques du secteur en matière de performances.
* Augmentez la transparence et le contrôle des types de données envoyés à l’emplacement de l’ensemble des propriétés de balise.
* Créez une règle de transfert d’événement pour envoyer les données précédemment suivies vers une nouvelle destination.

## Amélioration des performances

Dans un environnement de plus en plus concurrentiel, les entreprises doivent donner la priorité aux performances pour maintenir et accroître leur part de marché. Le transfert d’événements améliore les performances des sites web et des applications sur les appareils mobiles, IoT et OTT. Les taux de conversion des sites web peuvent augmenter en raison de délais de chargement plus courts, les applications mobiles ne déchargent pas les batteries aussi rapidement et les applications OTT semblent aussi réactives que celles qui sont exécutées sur les appareils mobiles. À mesure que les performances augmentent, il est également courant que les taux de conversion augmentent.

## Meilleure gouvernance des données

À mesure que la pile de technologies se développe et que les données sont envoyées à de plus en plus de destinations, le défi consistant à contrôler les données et leur destination devient plus difficile. La normalisation de réglementations comme le RGPD et le CCPA oblige les entreprises à exercer un plus grand contrôle sur un problème de données qui devient de plus en plus difficile.

Le transfert d’événements permet aux équipes marketing de développer leur activité tout en contrôlant les données. Il réduit le nombre de technologies côté client que les spécialiste du marketing doivent utiliser pour atteindre leur marché cible et envoyer des données vers des destinations non-Adobe. Cela permet aux équipes d’implémentation de gérer plus facilement les données circulant entre le client et différentes destinations.

## Différences entre le transfert d’événement et les balises

Il est important de noter les différences suivantes entre le transfert d’événement et les balises :

* Segmentation d’éléments de données en unités lexicales

   * Balises : Dans une règle, les éléments de données sont segmentés en unités lexicales avec une valeur `%` au début et à la fin du nom de l’élément de données. Par exemple : `%viewportHeight%`.

   * Transfert d’événement : Dans une règle, les éléments de données sont segmentés en unités lexicales avec `{{` au début et `}}` à la fin du nom de l’élément de données. Par exemple : `{{viewportHeight}}`.

* Comment les données sont référencées

   Pour référencer des données à partir du réseau Edge, le chemin d’accès de l’élément de données doit être `arc.event._<element>_`.

   `arc` désigne Adobe Response Context.

   Par exemple : `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Si ce chemin n’est pas spécifié correctement, les données ne sont pas collectées.


* Séquence des actions de règle

   Dans la section Action d’une règle, les règles de transfert d’événement sont toujours exécutées de manière séquentielle. Assurez-vous que l’ordre des actions est correct lorsque vous enregistrez une règle. Cette séquence d’exécution ne peut pas être choisie comme elle le peut avec les balises .

* Versions JavaScript du code personnalisé

   Les balises utilisent la version es5 de JavaScript. Le transfert d’événement utilise la version es6.

<!--doc Adobe Cloud Connector extension, get from Jon-->
