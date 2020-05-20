---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience 15 janvier 2020
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 9%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 15 janvier 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [Système de modèle de données d’expérience (XDM)](#xdm)
* [Service confidentialité](#privacy)
* [Sources](#sources)
* [Destinations](#destinations)

## Système de modèle de données d’expérience (XDM) {#xdm}

La normalisation et l’interopérabilité sont des concepts clés de la plate-forme d’expérience. Le modèle de données d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Il fournit des structures et des définitions communes à toute application pour communiquer avec les services d’Adobe Experience Platform. En respectant les normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune offrant des informations d’une manière plus rapide et plus intégrée. Vous pouvez obtenir des informations précieuses sur les actions client, définir des audiences client par le biais de segments et utiliser les attributs client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonction | Description |
|--- | ---|
| Restrictions de type champ pour les champs de hiérarchie égale | Une fois qu&#39;un champ XDM a été défini comme un certain type, tous les autres champs du même nom et de la même hiérarchie doivent utiliser le même type de champ, indépendamment des classes ou mixins dans lesquels ils sont utilisés. Par exemple, si un mixin pour la classe de Profil XDM contient un `profile.age` champ de type &quot;integer&quot;, un mixin similaire pour XDM ExperienceEvent ne peut pas avoir un `profile.age` champ de type &quot;string&quot;. Pour utiliser un autre type de champ, celui-ci doit être d’une hiérarchie différente de celle du champ précédemment défini (par exemple `profile.person.age`). Cette fonction est destinée à prévenir les conflits lorsque des schémas sont rassemblés dans une union. Bien que la contrainte n&#39;affecte pas rétroactivement les schémas existants, il est vivement recommandé de vérifier vos schémas pour détecter les conflits de type champ et de les modifier si nécessaire. |
| Validation des champs sensible à la casse | Les champs personnalisés du même niveau doivent porter des noms différents, indépendamment de la casse. Par exemple, si vous ajoutez un champ personnalisé nommé &quot;Adresse électronique&quot;, vous ne pouvez pas ajouter un autre champ personnalisé au même niveau nommé &quot;Adresse électronique&quot;. |

**Problèmes connus**

* None (Aucun)

Pour en savoir plus sur l&#39;utilisation de XDM à l&#39;aide de l&#39;API de registre de Schéma et de l&#39;interface utilisateur de l&#39;éditeur de Schémas, consultez la documentation [du système](../../xdm/home.md)XDM.

## Service confidentialité {#privacy}

Les nouvelles réglementations légales et organisationnelles donnent aux utilisateurs le droit d&#39;accéder à vos données personnelles ou de les supprimer de vos entrepôts de données sur demande. Adobe Experience Platform Privacy Service fournit une API RESTful et une interface utilisateur pour vous aider à gérer ces requêtes de données de vos clients. Avec Privacy Service, vous pouvez envoyer des demandes d’accès et de suppression de données clients privées ou personnelles des applications Adobe Experience Cloud, ce qui vous permet de respecter automatiquement les règles de confidentialité légales et organisationnelles.

**Nouvelles fonctionnalités**

| Fonction | Description |
|--- | ---|
| Refonte de la marque Privacy Service | Le service appelé auparavant &quot;RMMD&quot; a été rebaptisé Service de la protection des renseignements personnels, car il s&#39;est développé pour appuyer d&#39;autres règlements en plus du RMMD. |
| Nouveaux points de terminaison API | Le chemin de base de l’API Privacy Service a été mis à jour de `/data/privacy/gdpr` à `/data/core/privacy/jobs`. |
| Nouvelle propriété `regulation` requise | Lors de la création de nouvelles tâches dans l’API de Privacy Service, une `regulation` propriété doit être fournie dans la charge utile de la demande pour indiquer la réglementation sous laquelle effectuer le suivi de la tâche. Les valeurs acceptées sont `gdpr` et `ccpa`. |
| Prise en charge de l’authentification Adobe Primetime | Privacy Service accepte désormais les demandes d’accès/de suppression d’Adobe Primetime Authentication, en utilisant `primetimeAuthentication` comme valeur de produit. |
| Améliorations de l’interface utilisateur de Privacy Service | Pages distinctes de suivi des tâches pour les règlements sur les RGMD et les ACCP. Nouvelle liste déroulante Type _de_ règlement permettant de basculer entre les données de suivi pour le RGPD et l&#39;ACCP. |

**Problèmes connus**

* None (Aucun)

Pour plus d&#39;informations sur Privacy Service, veuillez début en lisant la présentation [](../../privacy-service/home.md)Privacy Service.

## Sources {#sources}

Adobe Experience Platform peut assimiler des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de plate-forme. Vous pouvez ingérer des données à partir de diverses sources, telles que des applications Adobe, des enregistrements basés sur le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source pour divers fournisseurs de données. Ces connexions source vous permettent d’authentifier et de vous connecter à des systèmes d’enregistrement externes et à des services de gestion de la relation client, de définir les heures d’exécution d’assimilation et de gérer le débit d’assimilation des données.

**Nouvelles fonctionnalités**

| Fonction | Description |
|--- | ---|
| Prise en charge des données d’attributs du client | Prise en charge de l’interface utilisateur et de l’API pour la création de connecteurs de flux continu afin d’assimiler les données d’attributs du client. |
| Autres formats de fichier pris en charge pour les enregistrements cloud | L’assimilation de fichiers à partir d’enregistrements cloud prend désormais en charge les formats de fichiers Parquet et JSON compatibles XDM. |
| Prise en charge des autorisations de contrôle d&#39;accès | La structure de contrôle d&#39;accès d’Adobe Experience Platform fournit les autorisations nécessaires pour accorder l’accès aux sources lors de l’assimilation des données. En fonction de leur niveau d’autorisation, un utilisateur peut vue des sources, gérer des sources ou se voir totalement refuser l’accès. |

**Autorisations du Contrôle d&#39;accès**

| Catégorie | Autorisation | Description |
|--- | --- | ---|
| Incorporation de données | Gérer les sources | Accès à des sources lues, créées, modifiées et désactivées. |
| Incorporation de données | Sources de Vue | Accès en lecture seule aux sources disponibles dans l’onglet *Catalogue* et aux sources authentifiées dans l’onglet *Parcourir* . |

**Problèmes connus**

* None (Aucun)

For more information about sources, see the [sources overview](../../sources/home.md)

## Destinations {#destinations}

Dans [Adobe Real-time CDP](../../rtcdp/overview.md), les destinations sont des intégrations préétablies avec les plateformes de destination qui activent les données pour ces partenaires de manière transparente.

**Nouvelles fonctionnalités**

| Fonction | Description |
|--- | ---|
| Prise en charge des autorisations de contrôle d&#39;accès | La fonctionnalité Destinations de la plateforme des données clients en temps réel fonctionne avec les autorisations de contrôle d’accès d’Adobe Experience Platform. Selon le niveau d’autorisation de l’utilisateur, vous pouvez afficher, gérer et activer les destinations. |

**Autorisations du Contrôle d&#39;accès**

| Catégorie | Autorisation | Description |
|--- | --- | ---|
| Destinations | Gérer les destinations | Accès à des destinations de lecture, de création, de modification et de désactivation. |
| Destinations | Destinations des Vues | Accès en lecture seule aux destinations disponibles dans l’onglet _Catalogue_ et aux destinations authentifiées dans l’onglet _Parcourir_ . |
| Destinations | Activer les destinations | Capacité à activer les données vers les destinations. Cette autorisation nécessite l’ajout de &quot;Gérer les destinations&quot; ou de &quot;Destinations de Vue&quot; au profil de produits. |

**Problèmes connus**

* None (Aucun)

Pour plus d’informations, consultez [Présentation des destinations](../../rtcdp/destinations/destinations-overview.md).