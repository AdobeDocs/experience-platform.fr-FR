---
title: Notes de mise à jour de l’extension Adobe Client Data Layer (ACDL)
description: Notes de mise à jour les plus récentes pour l’extension de balise (ACDL) dans Adobe Experience Platform.
exl-id: 8fa3a210-6c85-4162-84cf-15c6e3cfcb9e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 100%

---

# Notes de mise à jour de l’extension Adobe Client Data Layer (ACDL)

## Version 2.0.2

* Chargement de la bibliothèque principale ACDL (version 2.0.2)
* La version 2.0.0 de la bibliothèque principale ACDL a supprimé la possibilité d’exploiter event.beforeState et event.afterState. Par conséquent, nous avons modifié ces objets pour toujours renvoyer des objets vides. Les implémentations qui reposent sur cette fonctionnalité devront être mises à jour lors du passage à cette version.

## Version 1.1.3

* Chargement de la bibliothèque principale ACDL (version 1.1.3)

## Version 1.1.2

Les fonctionnalités suivantes sont fournies par l’extension dans la version initiale :

* Chargement de la bibliothèque principale ACDL (version 1.1.1)
* Changement du nom de la couche de données d’Adobe
* Événements :
   * Écoute de tous les événements
   * Écoute de toutes les données transmises
   * Écoute d’un événement spécifique envoyé
   * Tous les événements peuvent être écoutés dans des portées différentes.
* Éléments de données :
   * État calculé : état global ou spécifique
   * Taille de couche de données
* Actions :
   * Réinitialisez la taille de la couche de données (en conservant la dernière version de l’état calculé).
   * Envoyer l’objet à la couche de données
