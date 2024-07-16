---
title: Notes de mise à jour d’Adobe Experience Platform – Novembre 2021
description: Les notes de mise à jour de novembre 2021 pour Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 86%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 17 novembre 2021**

## Nouvelles fonctionnalités

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [Édition B2B de Real-Time Customer Data Platform](#B2B)
- [(Beta) Activation des segments d’audience vers des destinations par lots via l’API d’activation ad hoc](#ad-hoc-activation)

## Mises à jour des fonctionnalités existantes

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [IA dédiée à l’attribution](#attribution-ai)
- [IA dédiée aux clients](#customer-ai)

### Édition B2B de Real-Time Customer Data Platform {#B2B}

**Date de publication : 12 novembre 2021**

Basée sur Real-time Customer Data Platform (Real-time CDP), l’édition B2B de Real-time CDP a été conçue pour les professionnels du marketing travaillant dans un modèle de service business-to-business. Elle rassemble des données provenant de sources multiples et les combine en une vue unique des profils de comptes et d’utilisateurs. Ces données unifiées permettent aux spécialistes marketing de cibler précisément des audiences spécifiques afin de stimuler leur engagement sur tous les canaux disponibles.

Des améliorations ont été apportées à diverses fonctionnalités d’Adobe Experience Platform, distinguant ainsi l’édition B2B de Real-time CDP de son équivalent B2C. Il s’agit notamment d’améliorations du modèle de données d’expérience (XDM) pour les cas d’utilisation B2B, de mises à niveau de la résolution d’identité et de la segmentation de profil, ainsi que d’un connecteur et d’une destination personnalisés pour Marketo Engage. Le connecteur Marketo permet aux marques B2B de connecter ses données d’engagement B2B de pointe aux informations comportementales afin d’encourager les prospects et d’améliorer les opérations marketing basées sur les comptes.

-[Nouvelles éditions B2B et B2P](#editions)
-[Nouveaux connecteurs de source de données et de destination Marketo](#marketo)
-[XDM B2B standard](#XDM)

### Nouvelles éditions B2B et B2P {#editions}

De nouvelles éditions B2B et B2P qui apportent des données et des fonctionnalités B2B aux produits Real-Time CDP et Platform Activation sont disponibles à l’achat.

Pour en savoir plus sur Real-Time CDP B2B Edition, consultez la [présentation](../../rtcdp/overview.md).

### Nouveaux connecteurs de source de données et de destination Marketo {#marketo}

Les nouveaux connecteurs de source de données et de destination Marketo diffusent les données Marketo vers Platform et les audiences de Platform vers Marketo. Disponible pour tous les utilisateurs de Platform.

| Fonctionnalité | Description |
|----------|-------------|
| Connecteur source Marketo Engage | Le [connecteur source Marketo Engage](../../sources/connectors/adobe-applications/marketo/marketo.md) permet aux marketeurs d’ingérer en toute transparence des données de leurs instances Marketo dans leur instance Adobe Experience Platform et fournit une solution complète pour la gestion des prospects et les spécialistes du marketing B2B. |
| Destination Marketo Engage | La [Destination Marketo](../../destinations/catalog/adobe/marketo-engage.md) permet aux spécialistes marketing de pousser les segments créés dans Adobe Experience Platform vers Marketo où ils apparaîtront sous forme de listes statiques. |

### XDM B2B standard {#XDM}

Les classes, groupes de champs et types de données XDM B2B standard sont disponibles pour tous les utilisateurs de Platform.

| Fonctionnalité | Description |
|-----------|--------------|
| Classes XDM B2B standard | L’édition B2B de Real-Time Customer Data Platform fournit plusieurs XDM standard qui capturent des détails sur les entités de données B2B essentielles, telles que les comptes, les opportunités, les campagnes, etc. |

Pour en savoir plus sur la capture d’entités de données B2B, consultez la documentation [Schémas dans Real-Time Customer Data Platform B2B Edition](../../rtcdp/schemas/b2b.md) .

### (Beta) Activation des segments d’audience vers des destinations par lots via l’API d’activation ad hoc {#ad-hoc-activation}

L’API d’activation ad hoc permet aux spécialistes du marketing d’activer par programmation les segments d’audience vers les destinations, de manière rapide et efficace, dans les cas où une activation immédiate est requise. L’activation des audiences ad hoc n’est prise en charge que par les [destinations basées sur des fichiers par lots](../../destinations/destination-types.md#file-based) et est actuellement en version bêta. Pour plus d’informations, consultez la [documentation sur l’API d’activation ad hoc](../../destinations/api/ad-hoc-activation-api.md).

### IA dédiée à l’attribution {#attribution-ai}

L’IA dédiée à l’attribution est utilisée pour attribuer des crédits aux points de contact qui génèrent des événements de conversion. Il peut aider les spécialistes du marketing à quantifier l’impact publicitaire de chaque point de contact marketing sur le parcours client.

| Fonctionnalité | Description |
|-----------|---------------|
| Prise en charge de plusieurs jeux de données | L’IA dédiée à l’attribution peut désormais ingérer facilement plusieurs jeux de données directement dans l’interface utilisateur sans avoir à mapper et assembler chaque jeu de données. Cette nouvelle fonctionnalité qui permet de gagner du temps fournit des scores plus puissants et plus précis avec des données plus riches issues de plusieurs jeux de données. |
| Mappage des champs des canaux médias et des campagnes | L’IA dédiée à l’attribution prend désormais en charge le mappage des champs de canal multimédia et de campagne. Le mappage des canaux multimédia entre les jeux de données améliore les informations dérivées de l’IA dédiée à l’attribution et permet de fournir des résultats plus clairs et faciles à interpréter. |

Pour plus d’informations sur l’IA dédiée à l’attribution, reportez-vous à la section [Documentation Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### IA dédiée aux clients {#customer-ai}

L’IA dédiée aux clients disponible dans Real-time Customer Data Platform est utilisée pour générer des scores de propension personnalisés tels que l’attrition et la conversion pour des profils individuels à grande échelle. Cette opération s’effectue sans qu’il soit nécessaire de transformer les besoins professionnels en un problème de machine learning ou d’avoir recours à un algorithme, à une formation ou à un déploiement.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
|-----------|-------------|
| Prise en charge de plusieurs jeux de données | L’IA dédiée aux clients peut désormais ingérer facilement plusieurs jeux de données directement dans l’interface utilisateur sans avoir à mapper et assembler chaque jeu de données. Cette nouvelle fonctionnalité qui permet de gagner du temps fournit des scores plus puissants et plus précis avec des données plus riches issues de plusieurs jeux de données. |
| Attributs de profil personnalisés | L’IA dédiée aux clients prend désormais en charge la définition de champs de jeu de données de profil personnalisés (avec horodatages) dans vos données en plus des champs d’événement standard. L’utilisation de cette option vous permet d’ajouter des attributs de profil supplémentaires que vous estimez influents, ce qui peut améliorer la qualité de votre modèle et fournir des résultats plus précis. |

Pour plus d’informations sur l’IA dédiée aux clients, consultez la [Documentation sur l’IA dédiée aux clients](../../intelligent-services/customer-ai/overview.md).
