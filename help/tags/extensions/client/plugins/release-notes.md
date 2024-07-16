---
title: Notes de mise à jour de l’extension des modules externes courants Analytics
description: Dernières notes de mise à jour pour l’extension des balises de modules externes d’analyses courants dans Adobe Experience Platform.
exl-id: 5ea4b709-4e21-4f5d-be99-e72e4889ed99
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 97%

---

# Notes de mise à jour des modules externes courants Analytics

## 3 juin 2022

### Extension de modules externes courants 3.0.7

#### Fonctionnalités

* Les modules qui définissent des cookies utilisent désormais l’indicateur sécurisé

## mercredi 23 juin 2021

### Extension de modules externes courants 3.0.6

#### Correctifs

* Correction d’un problème en raison duquel getPercentPageViewed se rompait lors de l’utilisation de caractères spéciaux.

## 20 mai 2021

### Extension de modules externes courants 3.0.5

#### Correctifs

* Correction d’un problème en raison duquel getTimeParting ne s’initialisait pas correctement lors de l’utilisation de l’action d’initialisation générique.

## 26 mars 2021

### Extension de modules externes courants 3.0.4

#### Correctifs

* Correction d’un problème en raison duquel getPageLoadTime définissait incorrectement des variables sur l’objet de fenêtre
* Correction d’un problème en raison duquel getQueryParam revenait non défini au lieu de &quot;&quot; si queryParam n’était pas présent dans la chaîne de requête
* Correction d’un problème en raison duquel des numéros de version incorrects s’affichaient dans l’action Initialiser

## 19 mars 2021

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

## 9 avril 2020

### Extension de modules externes courants 2.2.0

#### Correctifs

* Correction de la formulation dans les affichages de l’extension

#### Fonctionnalités

* Mise à jour de la documentation pour l’action Initialiser

## 5 décembre 2019

### Extension de modules externes courants 2.1.1

#### Correctifs

* Correction d’un problème qui empêchait la compatibilité descendante avec les versions 2.0.X
* Correction d’un problème qui faisait rediriger les liens de la documentation vers une mauvaise documentation
* Correction d’un problème où `getTimeSinceLastVisit` apparaissait deux fois dans l’action Initialiser

## 15 novembre 2019

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

## 30 octobre 2019

### Extension de modules externes courants 2.0.3

#### Correctifs

* Correction d’un problème de liens rompus vers la documentation

## 11 octobre 2019

### Extension de modules externes courants 2.0.2

#### Fonctionnalités

* Ajout de 15 modules externes à l’extension
* Création d’une nouvelle action Initialiser pour faciliter les implémentations

## 11 juillet 2019

### Extension de modules externes courants 1.0.4

#### Fonctionnalités

* Extension publiée avec sept modules externes
* Actions individuelles d’initialisation de chaque module externe
