---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour d’Experience Platform, 15 janvier 2020
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 66%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 15 janvier 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] Système (XDM)  {#xdm}

La normalisation et l&#39;interopérabilité sont les concepts clés qui sous-tendent [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), piloté par l’Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Elle fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Restrictions liées au type de champ pour les champs de hiérarchie égale | Une fois qu&#39;un champ XDM a été défini comme un certain type, tous les autres champs du même nom et de la même hiérarchie doivent utiliser le même type de champ, indépendamment des classes ou des groupes de champs de schéma dans lesquels ils sont utilisés. Par exemple, si un groupe de champs pour la classe XDM [!DNL Profile] contient un champ `profile.age` de type &quot;integer&quot;, un groupe de champs similaire pour XDM [!DNL ExperienceEvent] ne peut pas avoir un champ `profile.age` de type &quot;string&quot;. Pour utiliser un type de champ différent, le champ doit appartenir à une hiérarchie différente de celle précédemment définie (par exemple, `profile.person.age`). Cette fonctionnalité est destinée à prévenir les conflits lorsque les schémas sont rassemblés dans une union. Bien que la contrainte n’affecte pas les schémas existants de façon rétroactive, il est vivement recommandé de vérifier vos schémas à la recherche d’éventuels conflits de type de champ et de les modifier si nécessaire. |
| Validation de champ sensible à la casse | Les champs personnalisés de même niveau doivent porter des noms différents, indépendamment de la casse. Par exemple, si vous ajoutez un champ personnalisé nommé « E-mail », vous ne pouvez pas ajouter au même niveau un autre champ personnalisé nommé « e-mail ». |

**Problèmes connus**

* Aucun

Pour en savoir plus sur l&#39;utilisation de XDM à l&#39;aide de l&#39;API [!DNL Schema Registry] et de l&#39;interface utilisateur [!DNL Schema Editor], consultez la [documentation du système XDM](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

Les nouvelles réglementations légales et organisationnelles donnent aux utilisateurs le droit d’accéder à leurs données personnelles et de les supprimer de vos banques de données sur demande. Adobe Experience Platform [!DNL Privacy Service] fournit une API RESTful et une interface utilisateur pour vous aider à gérer ces requêtes de données de vos clients. Avec [!DNL Privacy Service], vous pouvez envoyer des demandes d&#39;accès et de suppression de données clients privées ou personnelles des applications Adobe Experience Cloud, ce qui vous permet de respecter automatiquement les réglementations légales et de confidentialité de l&#39;entreprise.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| [!DNL Privacy Service] recomposition | Le service appelé auparavant &quot;Service RGMD&quot; a été renommé [!DNL Privacy Service], car il a grandi pour appuyer d&#39;autres règlements en plus du RGMD. |
| Nouveaux points de terminaison de l’API | Le chemin de base de l&#39;API [!DNL Privacy Service] a été mis à jour de `/data/privacy/gdpr` à `/data/core/privacy/jobs`. |
| Nouvelle propriété `regulation` requise | Lors de la création de nouvelles tâches dans l&#39;API [!DNL Privacy Service], une propriété `regulation` doit être fournie dans la charge utile de la demande pour indiquer la réglementation sous laquelle effectuer le suivi de la tâche. Les valeurs acceptées sont `gdpr` et `ccpa`. |
| Prise en charge de [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] accepte désormais les demandes d’accès/de suppression provenant d’Adobe  [!DNL Primetime Authentication],  `primetimeAuthentication` en utilisant comme valeur de produit. |
| Améliorations de l’interface utilisateur de Privacy Service | Pages de suivi des tâches distinctes pour les règlements RGPD et CCPA. Nouvelle **liste déroulante de type de règlement **pour basculer entre les données de suivi pour le RGPD et l&#39;ACCP. |

**Problèmes connus**

* Aucun

Pour plus d&#39;informations sur [!DNL Privacy Service], veuillez début en lisant la [présentation du Privacy Service](../../privacy-service/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Prise en charge des données d’attributs clients | Prise en charge de l’interface utilisateur et de l’API pour la création de connecteurs de flux continu pour ingérer les données d’attributs clients. |
| Prise en charge de formats de fichier supplémentaires pour le stockage dans le cloud | L’ingestion de fichiers à partir du stockage dans le cloud prend désormais en charge les formats de fichier Parquet et JSON compatibles avec XDM. |
| Prise en charge des autorisations de contrôle d’accès | La structure de contrôle d’accès d’Adobe Experience Platform fournit les autorisations nécessaires pour accorder l’accès aux sources dans le cadre de l’ingestion de données. En fonction de son niveau d’autorisation, un utilisateur peut afficher des sources, gérer des sources ou se voir totalement refuser l’accès. |

**Autorisations de contrôle d’accès**

| Catégorie | Autorisation | Description |
|--- | --- | ---|
| Ingestion de données | Gestion des sources | Accès à la lecture, la création, la modification et la désactivation des sources. |
| Ingestion de données | Affichage des sources | Accès en lecture seule aux sources disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux sources authentifiées dans l’onglet **[!UICONTROL Parcourir]**. |

**Problèmes connus**

* Aucun

Pour plus d’informations sur les sources, consultez la [présentation des sources](../../sources/home.md).

## Destinations  {#destinations}

Dans [CDP en temps réel](../../rtcdp/overview.md), les destinations sont des intégrations préétablies avec les plateformes de destination qui activent les données à ces partenaires de manière transparente.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Prise en charge des autorisations de contrôle d’accès | La fonctionnalité de destinations de la plateforme de données clients en temps réel fonctionne avec les autorisations de contrôle d’accès d’Adobe Experience Platform. Selon le niveau d’autorisation de l’utilisateur, vous pouvez afficher, gérer et activer les destinations. |

**Autorisations de contrôle d’accès**

| Catégorie | Autorisation | Description |
|--- | --- | ---|
| Destinations | Gestion des destinations | Accès à la lecture, la création, la modification et la désactivation des destinations. |
| Destinations | Affichage des destinations | Accès en lecture seule aux destinations disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux destinations authentifiées dans l’onglet **Parcourir**. |
| Destinations | Activation des destinations | Possibilité d’activer les données vers les destinations. Cette autorisation nécessite l’ajout de « Gestion des destinations » ou « Affichage des destinations » au profil de produits. |

**Problèmes connus**

* Aucun

Pour plus d’informations, consultez la [présentation des destinations](../../destinations/home.md).
