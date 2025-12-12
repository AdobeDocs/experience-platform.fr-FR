---
title: Notes de mise à jour de l’extension Adobe Target
description: Dernières notes de mise à jour pour lʼextension de balise Adobe Target dans Adobe Experience Platform.
exl-id: ba29f614-c3cd-4e0b-b043-2b1c17567def
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 97%

---

# Notes de mise à jour d’Adobe Target

## 16 septembre 2021

### Extension Adobe Target 0.11.4

* Mise à jour d’at.js version 1.8.3
* Ajout d’attributs `SameSite=None` et `Secure` lors de la définition de cookies

## 24 juillet 2020

### Extension Adobe Target 0.11.3

* Correction d’un bug en cas d’échec de l’extension si un script ou un code ajoute la propriété `default` à la `window` ou au `document`.

## 15 juin 2020

### Extension Adobe Target 0.11.2

* Correction d’un problème lors de l’utilisation du remplacement CNAME et Edge, en raison duquel at.js 1.x pouvait créer un domaine de serveur incorrect, entraînant ainsi l’échec de la demande de Target.

## 25 mars 2020

### Extension Adobe Target 0.11.1

* Mise à jour d’at.js vers la version 1.8.1.
* Correction d’un problème qui entraînait un mauvais traitement des paramètres et des paramètres de chargement des pages.

## 10 octobre 2019

### Extension Adobe Target 0.11.0

* Mise à jour d’at.js vers la version 1.8.
* Amélioration des performances pour les intégrations entre la bibliothèque d’Experience Cloud ID (ECID) version 4.4 et at.js version 1.8.
* Auparavant, la bibliothèque ECID effectuait deux appels de blocage avant qu’at.js puisse récupérer des expériences. Cela a été réduit à un seul appel, ce qui améliore considérablement les performances.

>[!NOTE]
>Mettez à niveau votre extension de balise ECID pour Adobe Experience Platform vers la version 4.4.1 afin de profiter de cette amélioration des performances.

## 31 juillet 2019

### Extension Adobe Target 0.10.1

* Correctif pour les paramètres qui gèrent l’extension de balise pour Adobe Target

## 4 mai 2019

### Extension Adobe Target 0.10.0

* Correction d’un problème d’éléments de données causé par les dernières modifications de Google Chrome.

## 14 mars 2019

### Extension Adobe Target 0.9.3

* Version d’extension mise à jour pour utiliser at.js 1.7.1.

## 20 février 2019

### Extension Adobe Target 0.9.2

* Correction des conditions de concurrence entre les extensions Target et Analytics.

## 12 février 2019

### Extension Adobe Target 0.9.1

#### **Fonctionnalités**

* Mise à jour dʼextension pour utiliser le fichier at.js 1.7.0 avec la fonctionnalité dʼaccord préalable prise en charge par les balises pour contrôler comment et quand la balise Target est déclenchée. Consultez la documentation relative aux balises pour savoir comment paramétrer la mise en œuvre de la fonctionnalité dʼaccord préalable. Ajout de la possibilité de choisir si un paramètre mbox associé à une valeur vide doit être envoyé à Target ou non.

## 23 janvier 2019

### Extension Adobe Target 0.8.4

* Mise à jour du fichier at.js vers la version 1.6.4.
* Migration de l’interface utilisateur de l’extension vers Adobe Spectrum.

## 15 novembre 2018

### Extension Adobe Target 0.8.2

* Mise à jour du fichier at.js vers la version 1.6.3.

## 24 octobre 2018

### Extension Adobe Target 0.8.1

* Mise à jour du fichier at.js vers la version 1.6.2.

## 23 août 2018

### Extension Adobe Target 0.8.0

* Mise à jour du fichier at.js vers la version 1.6.0.

## 10 août 2018

### Extension Adobe Target 0.7.2

* Modifications mineures
* Mise à jour de la propriété `exchangeUrl` dans le fichier `extension.json`.

## 1er août 2018

### Extension Adobe Target 0.7.1

* Corrections mineures.

## 18 juin 2018

### Extension Adobe Target 0.7.0

* Mise à jour du fichier at.js vers la version 1.5.0.
* Correction d’un problème en raison duquel Adobe Media Optimizer générait une erreur de référence NULL dans IE 11.

## 15 juin 2018

### Extension Adobe Target 0.6.0

#### **Fonctionnalités**

* L’extension Target a été mise à jour pour utiliser le fichier at.js version 1.3.1. Lorsque vous déployez Target avec Analytics, Analytics ne se déclenche qu’une fois que tous les appels Target ont été résolus (y compris les offres de redirection), ce qui résout la condition de concurrence qui existait précédemment.

## 22 février 2018

### Extension Adobe Target 0.4.1

#### **Fonctionnalités**

* Ajout d’une liste Adobe Exchange à extension.json.
* Ajout de vérifications permettant de savoir si Target est désactivé et si la fonctionnalité Authoring (Création) est activée.

#### **Correctifs**

* Correction dʼune erreur dans lʼextension Adobe Target qui empêchait Visual Experience Composer dʼafficher la page en cas de déploiement via les balises.

## 8 février 2018

### Extension Adobe Target 0.4.0

#### **Fonctionnalités**

* Mise à jour des affichages dans les écrans de configuration de l’extension.
* Mise à jour du fichier at.js vers la version 1.2.3 (ajout de la prise en charge pour les offres JSON).
