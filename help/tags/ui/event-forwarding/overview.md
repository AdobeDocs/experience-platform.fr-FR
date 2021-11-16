---
title: Présentation du transfert dʼévénements
description: Découvrez le transfert dʼévénements dans Adobe Experience Platform, qui vous permet dʼutiliser Platform Edge Network afin dʼexécuter des tâches sans modifier votre mise en œuvre de balises.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 100%

---

# Présentation du transfert dʼévénements

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Le transfert dʼévénements dans Adobe Experience Platform réduit le poids de la page web et de lʼapplication en utilisant Adobe Experience Platform Edge Network pour exécuter les tâches normalement exécutées sur le client. Les règles de transfert dʼévénements peuvent transformer et envoyer des données vers de nouvelles destinations sans modifier les mises en œuvre côté client.

Le transfert dʼévénements, associé aux kits SDK web et mobile dʼAdobe Experience Platform, permet de :

* Effectuer un seul appel à partir de la page qui contient un payload de données. Les données sont ensuite fédérées côté serveur afin de réduire le trafic réseau côté client et offrir une expérience plus rapide aux clients.
* Réduire le temps nécessaire au chargement des pages web pour que votre site soit conforme aux bonnes pratiques du secteur en matière de performances.
* Augmenter la transparence et le contrôle des types de données envoyés à lʼemplacement souhaité, sur lʼensemble des propriétés de balises.
* Créer une règle de transfert dʼévénements pour envoyer les données précédemment suivies vers une nouvelle destination.

## Amélioration des performances

Dans un environnement de plus en plus concurrentiel, les entreprises doivent donner la priorité aux performances pour maintenir et accroître leur part de marché. Le transfert dʼévénements améliore les performances des sites web et des applications sur les appareils mobiles, IoT et OTT. Les taux de conversion des sites web peuvent augmenter en raison de délais de chargement plus courts, les applications mobiles ne déchargent pas les batteries aussi rapidement et les applications OTT semblent aussi réactives que celles qui sont exécutées sur les appareils mobiles. À mesure que les performances augmentent, il est également courant que les taux de conversion augmentent.

## Meilleure gouvernance des données

À mesure que la pile de technologies se développe et que les données sont envoyées à de plus en plus de destinations, le défi consistant à contrôler les données et leur destination devient plus difficile. La normalisation de règlements comme le RGPD et le CCPA force les sociétés à exercer un plus grand contrôle sur un problème de données qui devient de plus en plus difficile.

Le transfert dʼévénements permet aux équipes marketing de développer leur activité tout en contrôlant les données. Il réduit le nombre de technologies côté client que les spécialiste du marketing doivent utiliser pour atteindre leur marché cible et envoyer des données vers des destinations non-Adobe. Cela permet aux équipes d’implémentation de gérer plus facilement les données circulant entre le client et différentes destinations.

## Différences entre le transfert dʼévénements et les balises

Il est important de prendre en compte les différences suivantes entre le transfert dʼévénements et les balises :

* Segmentation d’éléments de données en unités lexicales

   * Balises : dans une règle, les éléments de données sont segmentés en unités lexicales avec `%` au début et à la fin du nom de lʼélément de données. Par exemple : `%viewportHeight%`.

   * Transfert dʼévénements : dans une règle, les éléments de données sont segmentés en unités lexicales avec `{{` au début et `}}` à la fin du nom de lʼélément de données. Par exemple : `{{viewportHeight}}`.

* Comment les données sont référencées

   Pour référencer des données à partir du réseau Edge, le chemin d’accès de l’élément de données doit être `arc.event._<element>_`.

   `arc` désigne Adobe Response Context.

   Par exemple : `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Si ce chemin dʼaccès nʼest pas spécifié correctement, les données ne sont pas collectées.


* Séquence des actions de règle

   Dans la section Action dʼune règle, les règles de transfert dʼévénements sont toujours exécutées de manière séquentielle. Assurez-vous que l’ordre des actions est correct lorsque vous enregistrez une règle. Cette séquence dʼexécution ne peut pas être choisie, à la différence des balises.

<!--doc Adobe Cloud Connector extension, get from Jon-->
