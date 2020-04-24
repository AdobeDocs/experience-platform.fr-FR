---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience 11 décembre 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 11 décembre 2019**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [Service de segmentation](#segmentation)
* [Service de prise de décision](#decisioning)
* [Sources](#sources)
* [Système XDM (Experience Data Model)](#xdm)

## Service de segmentation {#segmentation}

Le service de segmentation de la plate-forme Adobe Experience Platform fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer   à partir de vos données de client en temps réel. Ces segments sont configurés et maintenus de manière centralisée sur la plateforme, ce qui les rend facilement accessibles par n’importe quelle application Adobe.

Le service de segmentation définit un sous-ensemble particulier de  de en décrivant les critères qui distinguent un groupe de personnes commercialisables au sein de votre base de clients. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des de séries chronologiques représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonction | Description |
|--- | ---|
| Onglet   de fusionné dans le créateur de segments | Les onglets _Segments_ et __ de dans le Créateur de segments ont été combinés dans un seul et même onglet de __ . Cet onglet vous permet de rechercher des  de  existantes, que vous pouvez ensuite faire glisser dans le canevas du créateur de règles pour créer une nouvelle définition de segment. Le référencement d’un   peut ajouter l’un des jeux de logique de règle suivants à la nouvelle définition de segment :  l’appartenance  comme une règle, l’ensemble complet de la logique de règle qui a défini le  référencé. |
| Nouvel emplacement du sélecteur de stratégies de fusion | L’emplacement du sélecteur de stratégie de fusion dans le créateur de segments a été modifié. Pour sélectionner une stratégie de fusion pour une définition de segment, cliquez sur l’icône d’engrenage dans l’onglet _Champs_ , puis utilisez le menu déroulant _Fusionner la stratégie_ pour sélectionner la stratégie de fusion à utiliser. |

**Problèmes connus**

* None (Aucun)

Pour plus d’informations, reportez-vous à la présentation [du service](../../segmentation/home.md)de segmentation.

## Service de prise de décision {#decisioning}

Le service de prise de décision Adobe Experience Platform permet de sélectionner intelligemment et par programmation la &quot;prochaine meilleure expérience&quot; à partir d’un ensemble d’options disponibles pour une personne donnée, de la diffuser à n’importe quel ou application, et d’exécuter des  et desde la plateforme.

**Nouvelles fonctionnalités**

| Fonction | Description |
| -----------| ---------- |
| Fonctions de classement | L’ordre des   pour les est maintenant dérivé par une fonction de classement, plutôt qu’un ensemble fixe dedans tous les. |

**Problèmes connus**

* Aucun.

Pour une présentation complète du service, reportez-vous à la présentation [du service](../../decisioning-service/home.md) de prise de décision.

## Sources {#sources}

Adobe Experience Platform peut assimiler des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de plateforme. Vous pouvez assimiler des données à partir de diverses sources, telles qu’Adobe Solutions, des  basés sur le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source pour divers fournisseurs de données. Ces connexions source vous permettent de vous authentifier auprès de vos  systèmes  et services de gestion de la relation client, de définir les heures d’exécution de l’assimilation et de gérer le débit d’assimilation des données.

**Nouvelles fonctionnalités**

| Fonction | Description |
| ---------- | ------------ |
| Connexion en flux continu | L’assimilation en flux continu vous permet d’envoyer en temps réel des données des périphériques client et serveur vers Experience Platform. La version comprend une nouvelle interface utilisateur de connexion en flux continu. |
| Prise en charge de Connector pour Google Cloud Store | Prise en charge de la collecte de données à partir du Google Cloud Store. |

**Problèmes connus**

* Aucun.

For more information about sources, see the [sources overview](../../sources/home.md).

## Système XDM (Experience Data Model) {#xdm}

La normalisation et l’interopérabilité sont les concepts clés de la plateforme d’expérience. Le modèle de données d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des  pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Il fournit des structures et des définitions communes à toute application pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des  de  clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonction | Description |
|--- | ---|
| Amélioration de la validation des  de | De nouvelles vérifications permettent de s’assurer que les références se résolvent en champs supplémentaires comme prévu. Ajout de vérifications supplémentaires aux champs définis comme un tableau d’objets pour s’assurer que les objets sont entièrement définis. Amélioration des messages d’erreur afin d’identifier et de résoudre les problèmes. |

**Corrections de bogues**

* Maintenance et améliorations liées aux  de et aux sandbox.
* Prise en charge `eTag` du `/descriptors` point de fin dans l’API de registre des .

**Problèmes connus**

* None (Aucun)

Pour en savoir plus sur l&#39;utilisation de XDM à l&#39;aide de l&#39;API de registre des et de l&#39;interface utilisateur de l&#39;éditeur de  de, consultez la documentation [du système](../../xdm/home.md)XDM.