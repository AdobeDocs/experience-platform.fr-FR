---
title: Notes de mise à jour d’Adobe Experience Platform - Janvier 2020
description: Notes de mise à jour de janvier 2020 pour Adobe Experience Platform.
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
TQID: https://experienceleague.adobe.com/0s9NHA5BzWTX8TySxaSY3RyW8gv47BW7BAFp1HqN70Q
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: ed0d8d0e-04b9-4326-be72-a0fbca265377
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 899
ht-degree: 71%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : jeudi 15 janvier 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## Système d’[!DNL Experience Data Model] (XDM) {#xdm}

La normalisation et l&#39;interopérabilité sont les concepts clés de [!DNL Experience Platform]. [!DNL Experience Data Model] Le modèle de données d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences digitales. Elle fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types d’audiences par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Restrictions liées au type de champ pour les champs de hiérarchie égale | Une fois qu’un champ XDM a été défini comme un certain type, tous les autres champs du même nom et de la même hiérarchie doivent utiliser le même type de champ, quels que soient les classes ou les groupes de champs de schéma dans lesquels ils sont utilisés. Par exemple, si un groupe de champs pour la classe [!DNL Profile] XDM contient un champ `profile.age` de type « entier », un groupe de champs similaire pour la [!DNL ExperienceEvent] XDM ne peut pas avoir de champ `profile.age` de type « chaîne ». Pour utiliser un type de champ différent, le champ doit appartenir à une hiérarchie différente de celle précédemment définie (par exemple, `profile.person.age`). Cette fonctionnalité est destinée à prévenir les conflits lorsque les schémas sont rassemblés dans une union. Bien que la contrainte n’affecte pas les schémas existants de façon rétroactive, il est vivement recommandé de vérifier vos schémas à la recherche d’éventuels conflits de type de champ et de les modifier si nécessaire. |
| Validation de champ sensible à la casse | Les champs personnalisés de même niveau doivent porter des noms différents, indépendamment de la casse. Par exemple, si vous ajoutez un champ personnalisé nommé « E-mail », vous ne pouvez pas ajouter au même niveau un autre champ personnalisé nommé « e-mail ». |

**Problèmes connus**

* Aucune

Pour en savoir plus sur l’utilisation de XDM à l’aide de l’API [!DNL Schema Registry] et de [!DNL Schema Editor]’interface utilisateur, consultez la [documentation du système XDM](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

Les nouvelles réglementations légales et organisationnelles donnent aux utilisateurs le droit d’accéder à leurs données personnelles et de les supprimer de vos banques de données sur demande. Adobe Experience Platform [!DNL Privacy Service] fournit une API RESTful et une interface d’utilisation pour vous aider à gérer ces requêtes de données de votre clientèle. Grâce à [!DNL Privacy Service], vous pouvez envoyer des demandes d’accès et de suppression de données clientèle personnelles depuis les applications Adobe Experience Cloud. Cela facilite l’automatisation de la mise en conformité concernant les réglementations légales et organisationnelles liées à la confidentialité.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Nouveau nom [!DNL Privacy Service] | Le « Service RGPD » a été renommé [!DNL Privacy Service], ce service ayant été élargi pour prendre en compte des réglementations autres que le RGPD. |
| Nouveaux points d’entrée de l’API | Le chemin d’accès de base de l’API [!DNL Privacy Service] a été mis à jour de `/data/privacy/gdpr` à `/data/core/privacy/jobs`. |
| Nouvelle propriété `regulation` requise | Lors de la création de tâches dans l’API [!DNL Privacy Service], une propriété `regulation` doit être fournie dans la payload de la demande pour indiquer la réglementation à prendre en compte pour effectuer le suivi de la tâche. Les valeurs acceptées sont `gdpr` et `ccpa`. |
| Prise en charge de [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] accepte désormais les demandes d’accès/de suppression des [!DNL Primetime Authentication] Adobe, en utilisant `primetimeAuthentication` comme valeur de produit. |
| Améliorations de l’interface utilisateur de Privacy Service | Pages de suivi des tâches distinctes pour les règlements RGPD et CCPA. Nouvelle liste déroulante **Type de règlement** pour passer d’un ensemble de données de suivi à un autre dans le cadre du RGPD et de la CCPA. |

**Problèmes connus**

* Aucune

Pour plus d’informations sur [!DNL Privacy Service], commencez par lire la présentation de Privacy Service [&#128279;](../../privacy-service/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Experience Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Prise en charge des données d’attributs clients | Prise en charge de l’interface utilisateur et de l’API pour la création de connecteurs de flux continu pour ingérer les données d’attributs clients. |
| Prise en charge de formats de fichier supplémentaires pour le stockage dans le cloud | L’ingestion de fichiers à partir du stockage dans le cloud prend désormais en charge les formats de fichier Parquet et JSON compatibles avec XDM. |
| Prise en charge des autorisations de contrôle d’accès | La structure de contrôle d’accès d’Adobe Experience Platform fournit les autorisations nécessaires pour accorder l’accès aux sources dans le cadre de l’ingestion de données. En fonction de son niveau d’autorisation, un utilisateur peut afficher des sources, gérer des sources ou se voir totalement refuser l’accès. |

**Autorisations de contrôle d’accès**

| Catégorie | Autorisation | Description |
|--- | --- | ---|
| Ingestion de données | Gestion des sources | Accès à la lecture, la création, la modification et la désactivation des sources. |
| Ingestion de données | Affichage des sources | Accès en lecture seule aux sources disponibles dans l’onglet **[!UICONTROL Catalog]** et aux sources authentifiées dans l’onglet **[!UICONTROL Browse]** . |

**Problèmes connus**

* Aucun

Pour plus d’informations sur les sources, consultez la [présentation des sources](../../sources/home.md).

## Destinations {#destinations}

Dans [&#128279;](../../rtcdp/overview.md), les destinations sont des intégrations préconfigurées à des plateformes de destination qui activent les données vers ces partenaires de manière transparente.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Prise en charge des autorisations de contrôle d’accès | La fonctionnalité Destinations de Real-Time CDP fonctionne avec les autorisations de contrôle d’accès de Adobe Experience Platform. Selon le niveau d’autorisation de l’utilisateur, vous pouvez afficher, gérer et activer les destinations. |

**Autorisations de contrôle d’accès**

| Catégorie | Autorisation | Description |
|--- | --- | ---|
| Destinations | Gestion des destinations | Accès à la lecture, la création, la modification et la désactivation des destinations. |
| Destinations | Affichage des destinations | Accès en lecture seule aux destinations disponibles dans l’onglet **[!UICONTROL Catalog]** et aux destinations authentifiées dans l’onglet **Parcourir**. |
| Destinations | Activation des destinations | Possibilité d’activer les données vers les destinations. Cette autorisation nécessite l’ajout de « Gestion des destinations » ou « Affichage des destinations » au profil de produits. |

**Problèmes connus**

* Aucun

Pour plus d’informations, consultez la [présentation des destinations](../../destinations/home.md).
