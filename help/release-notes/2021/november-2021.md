---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour de novembre 2021 pour Adobe Experience Platform.
source-git-commit: aa8cafc9a40748eda3098b2af732a828d39204b2
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 27%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 17 novembre 2021**

## Nouvelles fonctionnalités

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [Édition B2B de Real-time Customer Data Platform](#B2B)

## Mises à jour des fonctionnalités existantes

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Attribution AI](#attribution-ai)
- [Customer AI](#customer-ai)

### Édition B2B de Real-time Customer Data Platform {#B2B}

**Date de publication : 12 novembre 2021**

Basée sur Real-time Customer Data Platform (Real-time CDP), l’édition B2B de Real-time CDP a été conçue pour les professionnels du marketing travaillant dans un modèle de service business-to-business. Elle rassemble des données provenant de sources multiples et les combine en une vue unique des profils de comptes et d’utilisateurs. Ces données unifiées permettent aux professionnels du marketing de cibler précisément des audiences spécifiques afin de stimuler leur engagement sur tous les canaux disponibles.

Des améliorations ont été apportées à diverses fonctionnalités d’Adobe Experience Platform, distinguant ainsi l’édition B2B de Real-time CDP de son équivalent B2C. Ils incluent des améliorations du modèle de données d’expérience (XDM) pour les cas d’utilisation B2B, des mises à niveau de la résolution des identités et de la segmentation des profils, ainsi qu’un connecteur et une destination personnalisés pour Marketo Engage. Le connecteur Marketo permet aux marques B2B de connecter leurs données d’engagement B2B leaders du secteur à des informations comportementales afin d’alimenter les pistes et d’améliorer les opérations marketing basées sur les comptes.

-[Nouvelles éditions B2B et B2P](#editions)
-[Nouveaux connecteurs de source de données et de destination Marketo](#marketo)
-[XDM B2B standard](#XDM)

### Nouvelles éditions B2B et B2P {#editions}

De nouvelles éditions B2B et B2P qui apportent des données et des fonctionnalités B2B à la fois à la plateforme de données clients en temps réel et aux produits d’activation de plateforme sont disponibles à l’achat.

Pour en savoir plus sur l’édition B2B de la plateforme CDP en temps réel, voir [aperçu](../../rtcdp/overview.md).

### Nouveaux connecteurs de source de données et de destination Marketo {#marketo}

Les nouveaux connecteurs de source de données et de destination Marketo diffusent les données Marketo dans les audiences Platform et Platform vers Marketo. Disponible pour tous les utilisateurs de Platform.

| Fonctionnalité | Description |
|-----------|--------------|
| Connecteur source Marketo Engage | Le [Connecteur source Marketo Engage](../../sources/connectors/adobe-applications/marketo/marketo.md) permet aux marketeurs d’ingérer en toute transparence des données d’une ou de plusieurs instances Marketo dans leur instance Adobe Experience Platform et offre une solution complète pour la gestion des pistes et les spécialistes du marketing B2B. |
| Destination du Marketo Engage | Le [Destination Marketo](../../destinations/catalog/adobe/marketo-engage.md) permet aux marketeurs de pousser les segments créés dans Adobe Experience Platform vers Marketo où ils apparaîtront sous forme de listes statiques. |

### XDM B2B standard {#XDM}

Les classes XDM B2B standard, les groupes de champs et les types de données sont disponibles pour tous les utilisateurs de Platform.

| Fonctionnalité | Description |
|----------|-------------|
| Classes XDM B2B standard | L’édition B2B de Real-time Customer Data Platform fournit plusieurs XDM standard qui capturent des détails sur les entités de données B2B essentielles, telles que les comptes, les opportunités, les campagnes, etc. |

Voir [Schémas dans Real-time Customer Data Platform version B2B](../../rtcdp/schemas/b2b.md) documentation pour en savoir plus sur la capture d’entités de données B2B.

### Attribution AI {#attribution-ai}

Attribution AI est utilisé pour attribuer des crédits aux points de contact qui génèrent des événements de conversion. Il peut aider les spécialistes du marketing à quantifier l’impact publicitaire de chaque point de contact marketing sur le parcours client.

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de plusieurs jeux de données | Attribution AI peut désormais ingérer facilement plusieurs jeux de données directement dans l’interface utilisateur sans avoir à mapper et assembler chaque jeu de données. Cette nouvelle fonctionnalité de gain de temps fournit des scores plus puissants et plus précis avec des données plus riches issues de plusieurs jeux de données. |
| Mappage des champs des canaux médias et des campagnes | Attribution AI prend désormais en charge le mappage des champs de canal multimédia et de campagne. Le mappage des canaux multimédia entre les jeux de données améliore les informations dérivées d’Attribution AI et permet de fournir des résultats plus clairs et faciles à interpréter. |

Pour plus d’informations sur Attribution AI, reportez-vous à la section [Documentation Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### Customer AI {#customer-ai}

Customer AI disponible dans Real-time Customer Data Platform est utilisé pour générer des scores de propension personnalisés tels que l’attrition et la conversion pour des profils individuels à grande échelle. Cette opération s’effectue sans qu’il soit nécessaire de transformer les besoins professionnels en un problème de machine learning ou d’avoir recours à un algorithme, à une formation ou à un déploiement.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de plusieurs jeux de données | Customer AI peut désormais ingérer facilement plusieurs jeux de données directement dans l’interface utilisateur sans avoir à mapper et assembler chaque jeu de données. Cette nouvelle fonctionnalité de gain de temps fournit des scores plus puissants et plus précis avec des données plus riches issues de plusieurs jeux de données. |
| Attributs de profil personnalisés | Customer AI prend désormais en charge la définition de champs de jeu de données de profil personnalisés (avec horodatages) dans vos données en plus des champs d’événement standard. L’utilisation de cette option vous permet d’ajouter des attributs de profil supplémentaires que vous estimez influents, ce qui peut améliorer la qualité de votre modèle et fournir des résultats plus précis. |

Pour plus d’informations sur Customer AI, voir [Documentation de Customer AI](../../intelligent-services/customer-ai/overview.md).
