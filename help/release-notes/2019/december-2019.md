---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience 11 décembre 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 5%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 11 décembre 2019**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [Service de segmentation](#segmentation)
* [Service de prise de décision](#decisioning)
* [Sources](#sources)
* [Système de modèle de données d’expérience (XDM)](#xdm)

## Service de segmentation {#segmentation}

Le service de segmentation de la plateforme Adobe Experience Platform fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir de vos données de Profil client en temps réel. Ces segments sont configurés et conservés de manière centralisée sur la plate-forme, ce qui les rend facilement accessibles par toute application Adobe.

Le service de segmentation définit un sous-ensemble particulier de profils en décrivant les critères qui distinguent un groupe de personnes commercialisables au sein de votre base de clients. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries chronologiques représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonction | Description |
|--- | ---|
| Onglet Audiences fusionnées dans le créateur de segments | Les onglets _Segments_ et _Audiences_ du créateur de segments ont été combinés dans un seul onglet _Audiences_ . Cet onglet vous permet de rechercher des audiences existantes, que vous pouvez ensuite faire glisser dans le canevas du créateur de règles pour créer une nouvelle définition de segment. Le référencement d’une audience peut ajouter l’un des jeux de logique de règle suivants à la nouvelle définition de segment : Appartenance à l’Audience en tant que règle, ensemble complet de logique de règle qui a défini l’audience référencée. |
| Nouvel emplacement du sélecteur de stratégies de fusion | L’emplacement du sélecteur de stratégies de fusion dans le créateur de segments a été modifié. Pour sélectionner une stratégie de fusion pour une définition de segment, cliquez sur l&#39;icône d&#39;engrenage dans l&#39;onglet _Champs_ , puis utilisez le menu déroulant _Fusionner la stratégie_ pour sélectionner la stratégie de fusion à utiliser. |

**Problèmes connus**

* None (Aucun)

Pour plus d&#39;informations, consultez la présentation [du service](../../segmentation/home.md)de segmentation.

## Service de prise de décision {#decisioning}

Le service de prise de décision Adobe Experience Platform permet de sélectionner intelligemment et par programmation l’expérience optimale suivante à partir d’un ensemble d’options disponibles pour une personne donnée, de la diffuser sur n’importe quel canal ou application et d’effectuer des rapports et des analyses.

**Nouvelles fonctionnalités**

| Fonction | Description |
| -----------| ---------- |
| Fonctions de classement | L&#39;ordre des offres des profils est désormais déterminé par une fonction de classement, plutôt qu&#39;un ensemble fixe d&#39;offres sur tous les profils. |

**Problèmes connus**

* Aucun.

Consultez la présentation [du service de](../../decisioning-service/home.md) prise de décision pour une présentation complète du service.

## Sources {#sources}

Adobe Experience Platform peut assimiler des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de plate-forme. Vous pouvez ingérer des données à partir de diverses sources, telles qu’Adobe Solutions, un enregistrement cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source pour divers fournisseurs de données. Ces connexions source vous permettent de vous authentifier sur vos systèmes d’enregistrement et services de gestion de la relation client, de définir les heures d’exécution d’assimilation et de gérer le débit d’assimilation des données.

**Nouvelles fonctionnalités**

| Fonction | Description |
| ---------- | ------------ |
| Connexion en flux continu | L’assimilation en flux continu vous permet d’envoyer en temps réel des données des périphériques client et serveur vers Experience Platform. La version comprend une nouvelle interface utilisateur de connexion en flux continu. |
| Prise en charge du connecteur pour Google Cloud Store | Prise en charge de la collecte de données à partir de Google Cloud Store. |

**Problèmes connus**

* Aucun.

For more information about sources, see the [sources overview](../../sources/home.md).

## Système de modèle de données d’expérience (XDM) {#xdm}

La normalisation et l’interopérabilité sont des concepts clés de la plate-forme d’expérience. Le modèle de données d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Il fournit des structures et des définitions communes à toute application pour communiquer avec les services d’Adobe Experience Platform. En respectant les normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune offrant des informations d’une manière plus rapide et plus intégrée. Vous pouvez obtenir des informations précieuses sur les actions client, définir des audiences client par le biais de segments et utiliser les attributs client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonction | Description |
|--- | ---|
| Amélioration de la validation des schémas | De nouvelles vérifications permettent de s’assurer que les références se résolvent en champs supplémentaires comme prévu. Ajout de vérifications supplémentaires aux champs définis comme un tableau d’objets afin de s’assurer que les objets sont entièrement définis. Amélioration des messages d’erreur afin d’identifier et de résoudre les problèmes. |

**Corrections de bogues**

* Maintenance et améliorations liées au contrôle d&#39;accès et aux sandbox.
* Prise en charge `eTag` du point de terminaison `/descriptors` dans l’API de registre de Schéma.

**Problèmes connus**

* None (Aucun)

Pour en savoir plus sur l&#39;utilisation de XDM à l&#39;aide de l&#39;API de registre de Schéma et de l&#39;interface utilisateur de l&#39;éditeur de Schémas, consultez la documentation [du système](../../xdm/home.md)XDM.