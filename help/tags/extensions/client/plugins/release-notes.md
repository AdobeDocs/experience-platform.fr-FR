---
title: Notes de mise à jour de l’extension des modules externes courants Analytics
description: Dernières notes de mise à jour pour l’extension des balises de modules externes d’analyses courants dans Adobe Experience Platform.
exl-id: 5ea4b709-4e21-4f5d-be99-e72e4889ed99
TQID: https://experienceleague.adobe.com/94sa-1F-LVCY4pzDc4wdQ6okxEjupdZB1ddN0lLHbgE
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 364
ht-degree: 97%

---

# Notes de mise à jour des modules externes courants Analytics

## samedi 3 juin 2022

### Extension de modules externes courants 3.0.7

#### Fonctionnalités

* Les modules externes qui définissent des cookies utilisent désormais l’indicateur sécurisé

## jeudi 23 juin 2021

### Extension de modules externes courants 3.0.6

#### Correctifs

* Correction d’un problème en raison duquel getPercentPageViewed se rompait lors de l’utilisation de caractères spéciaux.

## vendredi 20 mai 2021

### Extension de modules externes courants 3.0.5

#### Correctifs

* Correction d’un problème en raison duquel getTimeParting ne s’initialisait pas correctement lors de l’utilisation de l’action d’initialisation générique.

## samedi 26 mars 2021

### Extension de modules externes courants 3.0.4

#### Correctifs

* Correction d’un problème en raison duquel getPageLoadTime définissait incorrectement des variables sur l’objet de fenêtre
* Correction d’un problème en raison duquel getQueryParam revenait non défini au lieu de &quot;&quot; si queryParam n’était pas présent dans la chaîne de requête
* Correction d’un problème en raison duquel des numéros de version incorrects s’affichaient dans l’action Initialiser

## samedi 19 mars 2021

### Extension de modules externes courants 3.0.2

#### Fonctionnalités

* Mise à jour de tous les modules externes afin d’inclure automatiquement les informations de version sous forme de données contextuelles
* Ajout du module externe getPercentPageViewed
* Ajout des éléments de données pour les modules externes suivants
   * getGeoCoordinates
   * getNewRepeat
   * getPageName
   * getResponsiveLayout
   * getTimeParting
   * getTimeSinceLastVisit
   * getVisitDuration
   * getVisitNum
* Mise à jour des styles

## vendredi 9 avril 2020

### Extension de modules externes courants 2.2.0

#### Correctifs

* Correction de la formulation dans les affichages de l’extension

#### Fonctionnalités

* Mise à jour de la documentation pour l’action Initialiser

## vendredi 5 décembre 2019

### Extension de modules externes courants 2.1.1

#### Correctifs

* Correction d’un problème qui empêchait la compatibilité descendante avec les versions 2.0.X
* Correction d’un problème qui faisait rediriger les liens de la documentation vers une mauvaise documentation
* Correction d’un problème où `getTimeSinceLastVisit` apparaissait deux fois dans l’action Initialiser

## samedi 15 novembre 2019

### Extension de modules externes courants 2.1.0

#### Correctifs

* Réintroduction des actions de module externe individuelles pour prendre en charge la rétrocompatibilité
* Correction d’un problème lié au module externe `cleanStr`
* Correction d’un problème lié au module externe `getResponsiveLayout`
* Correction d’un problème lié au module externe `getPageName`

#### Fonctionnalités

* Mise à jour de la version de `getTimeParting`
* Mise à jour de la version de `numberSuite`
* Mise à jour de la version de `getNewRepeat`
* Mise à jour de la documentation pour tous les modules externes

## jeudi 30 octobre 2019

### Extension de modules externes courants 2.0.3

#### Correctifs

* Correction d’un problème de liens rompus vers la documentation

## samedi 11 octobre 2019

### Extension de modules externes courants 2.0.2

#### Fonctionnalités

* Ajout de 15 modules externes à l’extension
* Création d’une nouvelle action Initialiser pour faciliter les implémentations

## vendredi 11 juillet 2019

### Extension de modules externes courants 1.0.4

#### Fonctionnalités

* Extension publiée avec sept modules externes
* Actions individuelles d’initialisation de chaque module externe
