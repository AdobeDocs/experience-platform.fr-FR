---
title: Notes de mise à jour de l’extension Service d’identités d’Adobe Experience Cloud
description: Dernières notes de mise à jour pour lʼextension de balise Service dʼidentités dʼAdobe Experience Cloud dans Adobe Experience Platform.
exl-id: f9bfbed7-1eec-4916-9235-a75b5e2efcf8
source-git-commit: 04dfe55fec06d08a0caef7aee5bf8d85c6056149
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 86%

---

# Notes de mise à jour de l’extension Service d’identités d’Adobe Experience Cloud

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Pour les notes de mise à jour du Service d’identités d’Experience Cloud lui-même et pas uniquement de l’extension Adobe Experience Platform Launch, veuillez consulter : [https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html?lang=fr](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html?lang=fr)

## 9 mars 2022

### Extension 5.4.0 d’Experience Cloud ID

#### **Fonctionnalités**

* Cette version contient la dernière version 5.4.0 du visiteur, qui comprend les mises à jour suivantes :

   * Possibilité de configurer la durée de vie de la variable `s_ecid` cookie utilisant la configuration cookieLifetime
   * Mise à jour d’un problème de navigateur Firefox qui se produit lorsqu’une page est chargée dans un iFrame enfant

## 10 octobre 2021

### Extension 5.3.1 d’Experience Cloud ID

#### **Fonctionnalités**

* Cette version contient la dernière version 5.3.0 du visiteur, qui comporte les nouvelles mises à jour suivantes :

   * Mise à jour de l’algorithme pour générer l’ECID local
   * Dernier accord préalable avec `Secure` et `SameSite` indicateurs du cookie de confidentialité
   * Correction d’un problème de navigateur Firefox lorsqu’une page est chargée dans un iFrame enfant.

## 12 janvier 2021

### Extension 5.2.0 d’Experience Cloud ID

#### **Fonctionnalités**

* Mise à jour du correctif VisitorJS 5.2.0 avec un correctif pour lʼélément de données ECID qui ne pouvait pas être mis à jour lors de la réception du consentement.

## 3 novembre 2020

### Extension 5.2.1 d’Experience Cloud ID

#### **Fonctionnalités**

* Ce patch contient un correctif permettant d’écrire des cookies à partir d’un iFrame avec l’attribut `SameSite=None` dans le navigateur Google Chrome.

## 27 octobre 2020

### Extension 5.1.0 d’Experience Cloud ID

#### **Fonctionnalités**

* Ajouter la configuration `sameSiteCookie` pour spécifier l’attribut `SameSite` du cookie `AMCV`. Cette configuration prend en charge les valeurs suivantes pour l’attribut `SameSite` :

   * `Strict`
   * `Lax`
   * `None`

Les détails de ces valeurs d’attribut sont sur [web.dev](https://web.dev/samesite-cookies-explained/) et [chrome](https://www.chromium.org/updates/same-site).


## 13 août 2020

### Extension 5.0.1 d’Experience Cloud ID

#### **Fonctionnalités**

* Mise à jour du patch VisitorJS 5.0.1 avec un correctif pour l’ajout de l’indicateur d_cf lorsque la chaîne de consentement IAB a été modifiée.

## 15 juin 2020

### Extension 5.0.0 d’Experience Cloud ID

#### **Fonctionnalités**

* Ajout du support pour le `IAB TCF` - Transparency and Consent Framework - `Version 2.0`.

## 13 avril 2020

### Extension 4.6.0 d’Experience Cloud ID

#### **Fonctionnalités**

* L’indicateur `loadSSL` est activé par défaut. Tous les appels à Identity Service seront par défaut en `https`. Les clients peuvent définir ce paramètre sur false s’ils souhaitent appeler Identity Service en HTTP à partir de leurs pages non-SSL.
* Mise à jour de la fonction utilisée pour détecter la version d’Internet-Explorer (IE), afin de corriger un problème signalé par ESLint.
* Correction d’un bogue pour un problème de performances sur Internet-Explorer (IE) 11 lorsque l’inclusion pre-approval est accordée à ECID et que ce dernier est mis à jour ultérieurement.

## 22 janvier 2020

### Extension 4.5.2 d’Experience Cloud ID

#### **Fonctionnalités**

* Mise à jour du fichier visitor.js vers la version 4.5.2.
* La version 4.5.1 du fichier visitor.js comprend un correctif relatif au plug-in IAB pour l’inclusion.
* Mise à jour de la méthode `setCustomerIDs` pour rejeter les ID vides envoyés.

## 7 janvier 2020

### Extension 4.4.2 d’Experience Cloud ID

#### **Fonctionnalités**

* Mise à jour du fichier visitor.js vers la version 4.4.2.
* Améliorations de la méthode `getVisitorValues` pour récupérer les valeurs plus rapidement.


## 19 septembre 2019

### Extension 4.4.1 d’Experience Cloud ID

#### **Fonctionnalités**

* Mise à jour du fichier visitor.js vers la version 4.4.1
* Correction d’un bogue concernant l’obtention de l’entrée de preApprovals en opt-in
* VIDEO_ANALYTICS renommé MEDIA_ANALYTICS dans preOptInApprovals

   ![](../../../images/ecid-media-analytics.png)

## 17 juillet 2019

### Extension 4.4.0 d’Experience Cloud ID

#### **Fonctionnalités**

* Mise à jour du fichier visitor.js vers la version 4.4.0
* Ajout de la prise en charge du hachage SHA-256 pour setCustomerIDs

   ![](../../../images/ecid-setCustomerIDs-hash.png)

## 13 mai 2019

### Extension 4.3.1 d’Experience Cloud ID

#### **Fonctionnalités**

* Mise à jour du fichier visitor.js vers la version 4.3
* Type d’élément de données ajouté pour ECID dans le cadre de l’extension de balise

   ![](../../../images/ecid-data-element.png)

## 9 avril 2019

### Extension 4.2.0 d’Experience Cloud ID

#### **Fonctionnalités**

* Mise à jour du fichier visitor.js vers la version 4.2 incluant la prise en charge du plug-in IAB TCF pour Audience Manager.

## 25 février 2019

### Extension 4.1.0 d’Experience Cloud ID

#### **Fonctionnalités**

* Mise à jour de visitor.js vers la version 4.1, qui mettait à jour publishDestinations par nouvelle modification de l’API. Avec cette mise à jour, les informations du référent de la page peuvent être exposées pendant la synchronisation ID, si nécessaire.

## 15 février 2019

### Extension 4.0.0 d’Experience Cloud ID

#### **Fonctionnalités**

* Mise à jour du fichier visitor.js vers la version 4.0
* Ajout d’options de configuration pour le nouvel objet intégré d’accord préalable. Les paramètres d’accord préalable peuvent être utilisés pour supprimer les cookies et les appels de balises des solutions Adobe pour mieux prendre en charge les réglementations comme le RGPD

   ![](../../../images/ext-mcid-opt-in.png)

## 20 mars 2018

### Extension 3.1.0 d’Experience Cloud ID

#### **Fonctionnalités**

* Mise à jour du fichier visitor.js vers la version 3.1
* Ajout de deux propriétés de configuration : `resetBeforeVersion` et `serverState`.
