---
title: Notes de mise à jour de l’extension Adobe Target
description: Notes de mise à jour les plus récentes pour l’extension de balise Adobe Target dans Adobe Experience Platform.
source-git-commit: 573c13f5136a4efc3accf2838783a91ea914e949
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 77%

---

# Notes de mise à jour d’Adobe Target

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

## 24 juillet 2020

### Extension Adobe Target 0.11.3

* Correction d’un bug en cas d’échec de l’extension si un script ou un code ajoute la propriété `default` à la `window` ou au `document`.

## 15 juin 2020

### Extension Adobe Target 0.11.2

* Correction d’un problème lors de l’utilisation du remplacement CNAME et Edge, en raison duquel at.js 1.x pouvait créer un domaine de serveur incorrect, entraînant ainsi l’échec de la demande de Target.

## 25 mars 2020

### Extension Adobe Target 0.11.1

* Mise à jour d’at.js vers la version 1.8.1.
* Correction d’un problème qui entraînait un mauvais traitement des paramètres et des paramètres de chargement des pages.

## 10 octobre 2019

### Extension Adobe Target 0.11.0

* Mise à jour d’at.js vers la version 1.8.
* Amélioration des performances pour les intégrations entre la bibliothèque d’Experience Cloud ID (ECID) version 4.4 et at.js version 1.8.
* Auparavant, la bibliothèque ECID effectuait deux appels de blocage avant qu’at.js puisse récupérer des expériences. Cela a été réduit à un seul appel, ce qui améliore considérablement les performances.

>[!NOTE]
>Mettez à niveau votre extension de balise ECID pour Adobe Experience Platform vers la version 4.4.1 pour tirer parti de cette amélioration des performances.

## 31 juillet 2019

### Extension Adobe Target 0.10.1

* Correctif pour les paramètres qui gèrent l’extension de balise pour Adobe Target

## 4 mai 2019

### Extension Adobe Target 0.10.0

* Correction d’un problème d’éléments de données causé par les dernières modifications de Google Chrome.

## 14 mars 2019

### Extension Adobe Target 0.9.3

* Version d’extension mise à jour pour utiliser at.js 1.7.1.

## 20 février 2019

### Extension Adobe Target 0.9.2

* Correction des conditions de concurrence entre les extensions Target et Analytics.

## 12 février 2019

### Extension Adobe Target 0.9.1

#### **Fonctionnalités**

* Mise à jour de l’extension afin d’utiliser at.js 1.7.0 avec la fonctionnalité de confidentialité d’accord préalable prise en charge via les balises pour contrôler comment et quand la balise Target est déclenchée. Veuillez consulter la documentation sur les balises pour savoir comment configurer votre mise en oeuvre d’Opt-in. Ajout de la possibilité de choisir si un paramètre mbox associé à une valeur vide doit être envoyé à Target ou non.

## 23 janvier 2019

### Extension Adobe Target 0.8.4

* Mise à jour du fichier at.js vers la version 1.6.4.
* Migration de l’interface utilisateur de l’extension vers Adobe Spectrum.

## 15 novembre 2018

### Extension Adobe Target 0.8.2

* Mise à jour du fichier at.js vers la version 1.6.3.

## 24 octobre 2018

### Extension Adobe Target 0.8.1

* Mise à jour du fichier at.js vers la version 1.6.2.

## 23 août 2018

### Extension Adobe Target 0.8.0

* Mise à jour du fichier at.js vers la version 1.6.0.

## 10 août 2018

### Extension Adobe Target 0.7.2

* Modifications mineures
* Mise à jour de la propriété `exchangeUrl` dans le fichier `extension.json`.

## 1er août 2018

### Extension Adobe Target 0.7.1

* Corrections mineures.

## 18 juin 2018

### Extension Adobe Target 0.7.0

* Mise à jour du fichier at.js vers la version 1.5.0.
* Correction d’un problème en raison duquel Media Optimizer générait une erreur de référence NULL dans IE 11.

## 15 juin 2018

### Extension Adobe Target 0.6.0

#### **Fonctionnalités**

* L’extension Target a été mise à jour pour utiliser le fichier at.js version 1.3.1. Lorsque vous déployez Target avec Analytics, Analytics ne se déclenche qu’une fois que tous les appels Target ont été résolus (y compris les offres de redirection), ce qui résout la condition de concurrence qui existait précédemment.

## 22 février 2018

### Extension Adobe Target 0.4.1

#### **Fonctionnalités**

* Ajout d’une liste Adobe Exchange à extension.json.
* Ajout de vérifications permettant de savoir si Target est désactivé et si la fonctionnalité Authoring (Création) est activée.

#### **Correctifs**

* Correction d’une erreur dans l’extension Adobe Target qui empêchait Visual Experience Composer d’afficher la page lors d’un déploiement via des balises.

## 8 février 2018

### Extension Adobe Target 0.4.0

#### **Fonctionnalités**

* Mise à jour des affichages dans les écrans de configuration de l’extension.
* Mise à jour du fichier at.js vers la version 1.2.3 (ajout de la prise en charge pour les offres JSON).
