---
title: Notes de mise à jour de l’extension Adobe Analytics
description: Notes de mise à jour les plus récentes pour l’extension de balise Adobe Analytics dans Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1221'
ht-degree: 94%

---

# Notes de mise à jour de l’extension Adobe Analytics

>[!NOTE]
>
>Adobe Experience Platform Launch a été rebaptisé en tant que suite de technologies de collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

## 6 août 2020

### Extension Adobe Analytics 1.8.5

#### Correctifs

* Le nom de cookie incorrect dans les paramètres du module AAM était en train d’être défini lorsque le champ a été laissé vide. Cela a désormais été corrigé.

#### Fonctionnalités

* Mise à jour d’[AppMeasurement vers la version 2.22.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=fr).
* Légère modification de l’interface utilisateur, de façon à ce que les paramètres supplémentaires apparaissent désormais réduits en accordéon plutôt que sous forme de case à cocher.

## 2 juin 2020

### Extension Adobe Analytics 1.8.4

#### Correctifs

* Correction d’un bogue en raison duquel les événements du panier (prodView, scAdd, scView, etc.) ne s’affichaient pas dans la liste déroulante des événements. Tous ces éléments sont maintenant sélectionnables dans la liste déroulante.

#### Fonctionnalités

* Vous pouvez désormais désactiver Activity Map dans l’extension sans avoir à utiliser de code personnalisé. Activity Map se charge sous la forme d’un module distinct (tout comme le module AAM) et vous pouvez le désactiver si vous le souhaitez.
* L’interface utilisateur a été nettoyée en minimisant les variables de hiérarchie et d’autres options.
* Un champ a été ajouté pour définir les identifiants d’achat à partir de l’interface utilisateur de configuration de l’extension.

## 10 mars 2020

### Extension Adobe Analytics 1.8.3

#### Correctifs

* Correction d’un bogue affectant la configuration de règle et qui générait une erreur lorsque vous tentiez de définir des variables si vous utilisiez une bibliothèque personnalisée et que vos suites de rapports n’étaient pas configurées dans Analytics.
* Lors de la création d’une eVar, un bogue empêchaitait d’afficher l’option « dupliquer à partir de » une prop ou vice versa. Ce problème a été corrigé afin de reproduire le comportement des versions précédentes.

#### Fonctionnalités

* [Mise à jour d’AppMeasurement vers la version 2.20.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html)

## 2 mars 2020

### Extension Adobe Analytics 1.8.2

#### Correctifs

* Correction d’un problème en raison duquel une syntaxe incorrecte était utilisée pour les événements numériques et la devise sérialisée.

#### Fonctionnalités

* [Mise à jour d’AppMeasurement vers la version 2.18.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html)
* Mise à jour de la bibliothèque DIL dans le module Audience Manager vers la version 9.4
* Augmentation de la longueur des champs d’entrée dans l’extension
* Les eVars et les props dans les configurations d’extension et d’action affichent désormais le nom convivial issu d’Analytics.
* Ajout d’une case à cocher dans la section « Cookies » de la configuration de l’extension qui vous permet d’écrire des cookies sécurisés.
* Ajout de trois nouvelles configurations au module Audience Manager. Ajout d’un paramètre pour l’activation de la journalisation, l’activation des destinations d’URL et l’activation des destinations de cookies.

## 13 novembre 2019

### Extension Adobe Analytics 1.8.1

#### Correctifs

* Correction d’un bogue en raison duquel les variables eVar et prop Premium n’étaient pas enregistrées.

## 1 novembre 2019

### Extension Adobe Analytics 1.8.0

#### Correctifs

* Correction d’un bogue en raison duquel certains clients ne voyaient pas les options de suite de rapports dans la liste déroulante
* Correction d’un bogue qui ne permettait pas de définir correctement les variables lors de l’utilisation de l’ECID

#### Fonctionnalités

* Trie numérique des eVars, des props et des événements dans la vue Extension.
* Changements de schéma principal pour la prise en charge des données contextuelles Magento

## 6 septembre 2019

### Extension Adobe Analytics 1.7.8

#### Correctifs

* Correction d’un bogue qui empêchait certains utilisateurs de voir les options de la suite de rapports dans la liste déroulante
* Correction d’un bogue qui empêchait les événements de se déclencher correctement

## 5 septembre 2019

### Extension Adobe Analytics 1.7.7

#### Fonctionnalités

* Mise à jour d’AppMeasurement vers la version 2.17
* Mise à jour du module Gestion de l’audience pour la prise en charge de DIL 9.3
* Mise à jour des largeurs de champ pour vous donner plus d’espace

#### Correctifs

* Correction d’un bogue de définition des inclusions/exclusions
* Correction d’un bogue qui ne permettait pas de définir correctement les variables lors de l’utilisation de l’ECID

## 18 juillet 2019

### Extension Adobe Analytics 1.7.6

#### Fonctionnalités

* Mise à jour de l’extension Adobe Analytics pour la prise en charge de DIL 9.2 pour Audience Manager

* Mise à jour de l’extension pour la prise en charge d’[AppMeasurement 2.15.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html#Version 2.15.0)
* Suppression de la case à cocher suivante qui n’est plus prise en charge : « Do not attach the destination publishing IFRAME to the DOM or fire destinations » (Ne joignez pas l’IFRAME de publication de destination au DOM ou aux destinations de déclenchement)

## 4 juin 2019

### Extension Adobe Analytics 1.7.5

#### Fonctionnalités

* Mise à jour de l’extension Adobe Analytics vers [AppMeasurement 2.14.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=fr#version-2.14.0) incluant un correctif pour un problème clearVars connu
* Ajout d’un lien Exchange à l’extension. Vous pouvez accéder à la liste eXchange en cliquant sur la liste déroulante et en sélectionnant « info extension »

#### Correctifs

* Correction d’un bogue de l’interface utilisateur qui entraînait la suppression d’une eVar incorrecte d’une liste
* Correction d’un bogue qui nécessitait un serveur de suivi SSL lors de l’ajout de plusieurs suites de rapports. Lors de l’ajout de plusieurs suites de rapports, un serveur de suivi est requis, mais le champ serveur de suivi SSL est facultatif.

## 15 avril 2019

### Extension Adobe Analytics 1.7.4

#### Correctifs

* Restauration de l’extension après la découverte d’un bogue dans AppMeasurement 2.13.0. AppMeasurement 2.13.0 générait un problème qui empêchait l’envoi de l’ECID. Si vous avez installé la version 1.7.3, nous vous recommandons donc d’effectuer une mise à niveau vers la version 1.7.4 pour éviter ce problème. Notez que le clearVars continuera jusqu’à ce qu’une version mise à jour d’AppMeasurement soit publiée

## 12 avril 2019

### Extension Adobe Analytics 1.7.3

#### Correctifs

* Mise à jour de l’extension Adobe Analytics vers AppMeasurement 2.13.0 incluant un correctif pour un problème clearVars connu.

## 21 mars 2019

### Extension Adobe Analytics 1.7.2

#### Fonctionnalités

* Mise à jour de l’extension Adobe Analytics vers DIL 9.1.
* Mise à jour de l’extension Adobe Analytics vers AppMeasurement 2.12.
* Mise à niveau de la vue d’extension Adobe Analytics vers React-Spectrum.
* Désormais, lors de la configuration des suites de rapports dans la page de configuration, une liste déroulante s’affiche pour toutes les suites de rapports de votre société, ce qui facilite la sélection de la suite de rapports appropriée.

## 7 mars 2019

### Extension Adobe Analytics 1.7.1

#### Correctifs

* Restauration de l’extension à la version 1.6 après la découverte d’un bogue dans la version 1.7.

## 11 février 2019

### Extension Adobe Analytics 1.6

#### Fonctionnalités

* Mise à jour de l’extension Adobe Analytics vers DIL 9.0 pour prendre en charge l’inclusion.
* Mise à jour de l’extension Adobe Analytics vers AppMeasurement 2.11 pour prendre en charge l’inclusion.

#### Correctifs

* Correction d’un conflit avec prototype.js. L’extension Analytics prend désormais en charge les bibliothèques prototype.js standard.

## 9 novembre 2018

### Extension Adobe Analytics 1.5.1

#### **Correctifs**

* Rétrogradation du module DIL vers la version 7.0 pour corriger un problème causant l’échec du déclenchement des balises Analytics

## 5 novembre 2018

### Extension Adobe Analytics 1.5

#### **Fonctionnalités**

* Mise à jour de l’extension Adobe Analytics pour la prise en charge de DIL 8.0 pour Audience Manager
* Séparation du champ « Serialize from value » (Sérialiser à partir de la valeur) en deux champs, « Event ID » (ID d’événement) et « Event Value » (Valeur d’événement). Cela corrige le problème qui affectait une valeur plutôt que de sérialiser un événement
   * Notez que si vous utilisez le champ actuel pour ajouter un ID à l’aide d’une chaîne (p. ex. Event7=3:abc123), vous devez mettre à jour votre entrée pour refléter l’ID dans le champ « Event ID » (ID d’événement).

#### **Correctifs**

* Correction d’un bogue qui empêchait le remplissage correct du code de devise

## 11 octobre 2018

### Extension Adobe Analytics 1.4

#### **Fonctionnalités**

* Migration du nom du cookie de suivi vers la configuration de l’extension.

#### **Correctifs**

* Correction d’un bogue afin que les variables de définition ne se bloquent pas lorsqu’aucun objet trackerProperties n’est disponible.

## 5 juin 2018

### Extension Adobe Analytics 1.3

#### **Fonctionnalités**

* Mise à jour de l’extension Adobe Analytics pour la prise en charge d’AppMeasurement 2.9.
* Ajout de la fonctionnalité « Make tracker globally accessible » (Rendre le suivi accessible de manière globale) dans l’extension Adobe Analytics, ce qui permet à l’outil de suivi d’être déployé de manière globale sous `windows.s`.

#### **Correctifs**

* Correction d’un bogue qui causait la réinitialisation de l’affichage liste lors du retour de l’affichage détails
* Correction de plusieurs bogues afin d’améliorer le chargement des ressources dans le sélecteur de révisions
* Correction d’un bogue causant le remplacement de s.events par plusieurs règles dans l’extension Adobe Analytics.

## 20 mars 2018

### Extension Adobe Analytics 1.2

#### **Fonctionnalités**

* Mise à jour du fichier AppMeasurement.js vers la version 2.8.0
* Ajout d’une prise en charge du transfert côté serveur

## 8 février 2018

### Extension Adobe Analytics 1.1

#### **Fonctionnalités**

* Mise à jour de l’AppMeasurement vers la version 2.6
* L’outil de suivi Analytics initialisé est désormais exposé par le biais d’un module partagé dans l’extension de balise Adobe Experience Platform afin que d’autres extensions puissent inclure du code pour interagir avec l’outil.

#### **Correctifs**

* Correction d’une erreur de l’extension Adobe Analytics ayant entraîné l’affichage du message « Error, missing Report Suite ID in AppMeasurement initialization » (Erreur, ID de suite de rapports manquante dans l’initialisation d’AppMeasurement) dans la console du navigateur.
