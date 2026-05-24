---
title: Notes de mise à jour de l’extension Adobe Target
description: Dernières notes de mise à jour pour lʼextension de balise Adobe Target dans Adobe Experience Platform.
exl-id: ba29f614-c3cd-4e0b-b043-2b1c17567def
TQID: https://experienceleague.adobe.com/BNYIC9e-tm16Vv2ODMD2E0gMwSUXU-21aJxmyIE9HLk
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: eb9732ab-8232-4b21-bc4c-89de86dbe4d7
  - id: ed0d8d0e-04b9-4326-be72-a0fbca265377
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
  - id: fc7979f3-56c3-43ca-9784-f1ea3dc69c4b
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 548
ht-degree: 90%

---

# Notes de mise à jour d’Adobe Target

## vendredi 16 septembre 2021

### Extension Adobe Target 0.11.4

* Mise à jour d’at.js version 1.8.3
* Ajout d’attributs `SameSite=None` et `Secure` lors de la définition de cookies

## samedi 24 juillet 2020

### Extension Adobe Target 0.11.3

* Correction d’un bug en cas d’échec de l’extension si un script ou un code ajoute la propriété `default` à la `window` ou au `document`.

## mardi 15 juin 2020

### Extension Adobe Target 0.11.2

* Correction d’un problème lors de l’utilisation du remplacement CNAME et Edge, en raison duquel at.js 1.x pouvait créer un domaine de serveur incorrect, entraînant ainsi l’échec de la demande de Target.

## jeudi 25 mars 2020

### Extension Adobe Target 0.11.1

* Mise à jour d’at.js vers la version 1.8.1.
* Correction d’un problème qui entraînait un mauvais traitement des paramètres et des paramètres de chargement des pages.

## vendredi 10 octobre 2019

### Extension Adobe Target 0.11.0

* Mise à jour d’at.js vers la version 1.8.
* Amélioration des performances pour les intégrations entre la bibliothèque d’Experience Cloud ID (ECID) version 4.4 et at.js version 1.8.
* Auparavant, la bibliothèque ECID effectuait deux appels de blocage avant qu’at.js puisse récupérer des expériences. Cela a été réduit à un seul appel, ce qui améliore considérablement les performances.

>[!NOTE]
>Mettez à niveau votre extension de balise ECID pour Adobe Experience Platform vers la version 4.4.1 afin de profiter de cette amélioration des performances.

## 31 juillet 2019

### Extension Adobe Target 0.10.1

* Correctif pour les paramètres qui gèrent l’extension de balise pour Adobe Target

## 30 mai 2019

### Extension Adobe Target 0.10.0

* Correction d’un problème d’éléments de données causé par les dernières modifications de Google Chrome.

## vendredi 14 mars 2019

### Extension Adobe Target 0.9.3

* Version d’extension mise à jour pour utiliser at.js 1.7.1.

## jeudi 20 février 2019

### Extension Adobe Target 0.9.2

* Correction des conditions de concurrence entre les extensions Target et Analytics.

## mercredi 12 février 2019

### Extension Adobe Target 0.9.1

#### **Fonctionnalités**

* Mise à jour dʼextension pour utiliser le fichier at.js 1.7.0 avec la fonctionnalité dʼaccord préalable prise en charge par les balises pour contrôler comment et quand la balise Target est déclenchée. Consultez la documentation relative aux balises pour savoir comment paramétrer la mise en œuvre de la fonctionnalité dʼaccord préalable. Ajout de la possibilité de choisir si un paramètre mbox associé à une valeur vide doit être envoyé à Target ou non.

## jeudi 23 janvier 2019

### Extension Adobe Target 0.8.4

* Mise à jour du fichier at.js vers la version 1.6.4.
* Migration de l’interface utilisateur de l’extension vers Adobe Spectrum.

## vendredi 15 novembre 2018

### Extension Adobe Target 0.8.2

* Mise à jour du fichier at.js vers la version 1.6.3.

## jeudi 24 octobre 2018

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

## mardi 18 juin 2018

### Extension Adobe Target 0.7.0

* Mise à jour du fichier at.js vers la version 1.5.0.
* Correction d’un problème en raison duquel Adobe Media Optimizer générait une erreur de référence NULL dans IE 11.

## samedi 15 juin 2018

### Extension Adobe Target 0.6.0

#### **Fonctionnalités**

* L’extension Target a été mise à jour pour utiliser at.js version 1.3.1. Lorsque vous déployez Target avec Analytics, nous attendons désormais que tous les appels Target soient résolus (y compris les offres de redirection) avant qu’Analytics ne se déclenche, ce qui résout la condition de concurrence qui existait auparavant.

## vendredi 22 février 2018

### Extension Adobe Target 0.4.1

#### **Fonctionnalités**

* Ajout d’une liste Adobe Exchange à extension.json.
* Ajout de vérifications permettant de savoir si Target est désactivé et si la fonctionnalité Authoring (Création) est activée.

#### **Correctifs**

* Correction dʼune erreur dans lʼextension Adobe Target qui empêchait Visual Experience Composer dʼafficher la page en cas de déploiement via les balises.

## vendredi 8 février 2018

### Extension Adobe Target 0.4.0

#### **Fonctionnalités**

* Mise à jour des affichages dans les écrans de configuration de l’extension.
* Mise à jour du fichier at.js vers la version 1.2.3 (ajout de la prise en charge pour les offres JSON).
