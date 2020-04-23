---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience 15 janvier 2020
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 5199a344a66381ef9d7eea1ea8314e5de7152e3b

---


# Notes de mise à jour d’Adobe Experience Platform

## Date de publication : 15 janvier 2020

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [Système XDM (Experience Data Model)](#xdm)
* [Service confidentialité](#privacy)
* [Sources](#sources)
* [Destinations](#destinations)

## Système XDM (Experience Data Model) {#xdm}

La normalisation et l’interopérabilité sont les concepts clés de la plateforme d’expérience. Le modèle de données d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des  pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Il fournit des structures et des définitions communes à toute application pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des  de  clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonction | Description |
|--- | ---|
| Restrictions de type champ pour les champs de hiérarchie égale | Une fois qu’un champ XDM a été défini comme un certain type, tous les autres champs du même nom et de la même hiérarchie doivent utiliser le même type de champ, quelles que soient les classes ou les mixins dans lesquels ils sont utilisés. Par exemple, si un mixin pour la classe de XDM contient un `profile.age` champ de type &quot;integer&quot;, un mixin similaire pour XDM ExperienceEvent ne peut pas avoir un `profile.age` champ de type &quot;string&quot;. Pour utiliser un type de champ différent, le champ doit être d’une hiérarchie différente de celle définie précédemment (par exemple, `profile.person.age`). Cette fonctionnalité est destinée à prévenir les conflits lorsque des  sont rassemblés dans un  de. Bien que la contrainte n’affecte pas rétroactivement les  de existantes, il est vivement recommandé de vérifier votre pour les conflits de type champ et de les modifier si nécessaire. |
| Validation de champ sensible à la casse | Les champs personnalisés du même niveau doivent porter des noms différents, indépendamment de la casse. Par exemple, si vous ajoutez un champ personnalisé nommé &quot;Courriel&quot;, vous ne pouvez pas ajouter un autre champ personnalisé au même niveau nommé &quot;Courriel&quot;. |

**Problèmes connus**

* None (Aucun)

Pour en savoir plus sur l&#39;utilisation de XDM à l&#39;aide de l&#39;API de registre des et de l&#39;interface utilisateur de l&#39;éditeur de  de, consultez la documentation [du système](../../xdm/home.md)XDM.

## Service confidentialité {#privacy}

Les nouvelles réglementations légales et organisationnelles donnent aux utilisateurs le droit d&#39;accéder à vos données personnelles ou de les supprimer de vos entrepôts de données sur demande. Le service de confidentialité d’Adobe Experience Platform fournit une API RESTful et une interface utilisateur pour vous aider à gérer ces requêtes de données de vos clients. Avec Privacy Service, vous pouvez envoyer des demandes d’accès et de suppression de données clients privées ou personnelles des applications Adobe Experience Cloud, ce qui facilite la conformité automatisée aux réglementations légales et de confidentialité de l’entreprise.

**Nouvelles fonctionnalités**

| Fonction | Description |
|--- | ---|
| Refonte de la marque Privacy Service | Le Service de protection des renseignements personnels, anciennement appelé &quot;Service RMMD&quot;, a été renommé Service de protection des renseignements personnels, car il a pris de l&#39;expansion pour appuyer d&#39;autres règlements en plus du RMMD. |
| Nouveaux points de fin API | Le chemin de base de l’API Privacy Service a été mis à jour de `/data/privacy/gdpr` vers `/data/core/privacy/jobs`. |
| Nouvelle `regulation` propriété obligatoire | Lors de la création de nouvelles tâches dans l’API de Privacy Service, une `regulation` propriété doit être fournie dans la charge utile de la demande pour indiquer la réglementation sous laquelle effectuer le suivi de la tâche. Les valeurs acceptées sont `gdpr` et `ccpa`. |
| Prise en charge de l’authentification Adobe Primetime | Privacy Service accepte désormais les demandes d’accès/de suppression d’Adobe Primetime Authentication, en utilisant `primetimeAuthentication` comme valeur de produit. |
| Améliorations de l’interface utilisateur de Privacy Service | Pages de suivi des tâches distinctes pour les règlements sur le RMR et l&#39;ACCP. Nouvelle liste déroulante Type _de_ règlement pour basculer entre les données de suivi pour le RDPC et l&#39;ACCP. |

**Problèmes connus**

* None (Aucun)

Pour plus d&#39;informations sur Privacy Service, veuillez  en lisant la présentation [](../../privacy-service/home.md)Privacy Service.

## Sources {#sources}

Adobe Experience Platform peut assimiler des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de plateforme. Vous pouvez assimiler des données à partir de diverses sources, telles que des applications Adobe, des  basés sur le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source pour divers fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des systèmes de  et des services de gestion de la relation client externes, de définir les heures d&#39;exécution de l&#39;assimilation et de gérer le débit d&#39;assimilation des données.

**Nouvelles fonctionnalités**

| Fonction | Description |
|--- | ---|
| Prise en charge des données d’attributs du client | Prise en charge de l’interface utilisateur et de l’API pour la création de connecteurs de flux continu pour assimiler les données d’attributs du client. |
| Prise en charge supplémentaire des formats de fichier pour le  cloud  | L’assimilation de fichiers à partir du Cloud  prend désormais en charge les formats de fichiers Parquet et JSON compatibles XDM. |
| Prise en charge des  d’autorisation des | La structure de  de d’Adobe Experience Platform fournit les autorisations nécessaires pour accorder l’accès aux sources dans l’assimilation des données. En fonction de leur niveau d’autorisation, un utilisateur peut  des sources, gérer des sources ou se voir totalement refuser l’accès. |

**d’accès**

| Catégorie | Autorisation | Description |
|--- | --- | ---|
| Ingestion des données | Gestion des sources | Accès à la lecture, à la création, à la modification et à la désactivation des sources. |
| Ingestion des données | Sources de  | Accès en lecture seule aux sources disponibles dans l’onglet *Catalogue* et aux sources authentifiées dans l’onglet *Parcourir* . |

**Problèmes connus**

* None (Aucun)

For more information about sources, see the [sources overview](../../sources/home.md)

## Destinations {#destinations}

Dans le CDP [en temps réel d’](../../rtcdp/overview.md)Adobe, les destinations sont des intégrations prédéfinies avec des plateformes de destination qui activent les données de manière transparente vers ces partenaires.

**Nouvelles fonctionnalités**

| Fonction | Description |
|--- | ---|
| Prise en charge des  d’autorisation des | La fonctionnalité Destinations de la plateforme des données clients en temps réel fonctionne avec les autorisations de contrôle d’accès d’Adobe Experience Platform. Selon le niveau d’autorisation de l’utilisateur, vous pouvez afficher, gérer et activer les destinations. |

**d’accès**

| Catégorie | Autorisation | Description |
|--- | --- | ---|
| Destinations | Gérer les destinations | Accès à des destinations de lecture, de création, de modification et de désactivation. |
| Destinations | Destinations  | Accès en lecture seule aux destinations disponibles dans l’onglet _Catalogue_ et aux destinations authentifiées dans l’onglet _Parcourir_ . |
| Destinations | Activer les destinations | Possibilité d’activer les données vers les destinations. Cette autorisation nécessite l’ajout de &quot;Gérer les destinations&quot; ou de &quot;Destinations &quot; à l’ du produit. |

**Problèmes connus**

* None (Aucun)

Pour plus d’informations, consultez [Présentation des destinations](../../rtcdp/destinations/destinations-overview.md).