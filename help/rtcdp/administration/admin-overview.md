---
keywords: Présentation de l’administration rtcdp;présentation de l’administration
title: Présentation de l’administration Real-time Customer Data Platform
description: Ce document présente les fonctionnalités d’administration d’Adobe Real-time Customer Data Platform, optimisées par Adobe Experience Platform.
feature: Access Control, Get Started, Sandboxes
exl-id: c5bdeac6-345a-4ef1-bc5a-a993f565b9d6
source-git-commit: a8c9543bb003a99dcd85712d202482511c0a5608
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 21%

---

# Présentation de l’administration Real-time Customer Data Platform

Ce document présente les fonctionnalités d’administration d’ [!DNL Adobe Real-Time Customer Data Platform], avec Adobe Experience Platform.

[!DNL Experience Platform] permet aux administrateurs de gérer le contrôle d’accès en fonction du rôle pour les utilisateurs, ainsi que de gérer les environnements de test virtuels pour le développement d’applications.

Les sections suivantes présentent les principales composantes de [!DNL Experience Platform] fonctionnalités d’administration et comprend des liens vers [!DNL Experience Platform] documentation où des informations plus détaillées sont fournies.

## Contrôle d’accès

Le contrôle d’accès basé sur les attributs est géré via l’interface utilisateur Autorisations. Cette fonctionnalité exploite les rôles dans l’interface utilisateur d’autorisations, ce qui vous permet de lier les utilisateurs à des autorisations et des environnements de test. Grâce à cette fonctionnalité, les administrateurs peuvent accorder ou restreindre l’accès à des fonctionnalités spécifiques de la plateforme CDP en temps réel pour des ensembles d’utilisateurs définis.

Pour en savoir plus sur le contrôle d’accès, voir [contrôle d’accès basé sur les attributs - Aperçu](/help/access-control/abac/overview.md) dans le [!DNL Experience Platform] la documentation.

>[!IMPORTANT]
>
>Pour obtenir un guide détaillé sur l’octroi de l’accès aux fonctionnalités Real-Time CDP, notamment sur l’activation de la visibilité dans l’interface utilisateur, suivez les étapes fournies dans la section [guide d’utilisation du contrôle d’accès](../../access-control/ui/overview.md), en particulier pour la gestion des détails et des services supplémentaires pour un profil de produit.

## Sandbox

Adobe Experience Platform (et la plateforme CDP en temps réel par extension) est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

Pour répondre à ce besoin, Adobe Experience Platform fournit *sandbox*, vous permettant de partitionner une seule [!DNL Platform] dans des environnements virtuels distincts qui peuvent être utilisés pour développer et faire évoluer des applications d’expérience numérique. Vous pouvez utiliser la fonction d’outil d’environnement de test pour améliorer la précision de la configuration dans les environnements de test et exporter et importer en toute transparence les configurations d’environnement de test entre les environnements de test. Suivez les étapes fournies dans la section [guide de l’interface utilisateur de l’outil Sandbox](../../sandboxes/ui/sandbox-tooling.md).

Pour plus d’informations sur les environnements de test, voir [Présentation des environnements de test](../../sandboxes/home.md) dans le [!DNL Experience Platform] la documentation.
