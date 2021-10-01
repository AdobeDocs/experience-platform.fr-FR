---
keywords: Experience Platform;accueil;rubriques les plus consultées;dépannage des environnements de test
solution: Experience Platform
title: Guide de dépannage des environnements de test
topic-legacy: troubleshooting guide
description: Ce document apporte des réponses aux questions fréquentes sur les environnements de test dans Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 95%

---

# Guide de dépannage des environnements de test

Ce document apporte des réponses aux questions fréquentes sur les environnements de test dans Adobe Experience Platform. Pour les questions et le dépannage relatifs aux autres services Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

Les environnements de test divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique. Pour plus d’informations, consultez la [Présentation des environnements de test](home.md).

## Qu’est-ce qu’un environnement de test ?

Les environnements de test sont des partitions virtuelles au sein d’une instance unique d’Experience Platform. Chaque environnement de test conserve sa propre bibliothèque indépendante de ressources Platform (qui comprend des schémas, des jeux de données, des profils, etc.). Tout le contenu et les actions réalisés dans un environnement de test sont limités à celui-ci et n’en affectent aucun autre. Pour plus d’informations, consultez la [Présentation des environnements de test](home.md).

## Quels sont les types d’environnements de test disponibles et quelles sont leurs différences ?

Deux types d’environnements de test sont disponibles dans Experience Platform :

* Environnement de test de production
* Environnement de test hors production

Experience Platform fournit un environnement de test de production unique, qui ne peut pas être supprimé ou réinitialisé. Il ne peut y avoir qu’un seul environnement de test de production pour une instance Platform unique.

Par comparaison, il est possible de créer plusieurs environnements de test hors production par administrateurs d’environnement de test pour une instance Platform unique. Les environnements de test hors production vous permettent de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter votre environnement de test de production. En outre, les environnements de test hors production disposent d’une fonctionnalité de réinitialisation supprimant de l’environnement de test toutes les ressources créées par les clients. Les environnements de test hors production ne peuvent pas être convertis en environnements de test de production. Une licence Experience Platform par défaut vous accorde cinq environnements de test (un de production et quatre de non-production). Vous pouvez ajouter des packs de dix environnements de test hors production jusqu’à 75 environnements de test au total. Contactez votre administrateur dʼorganisation IMS ou votre représentant commercial Adobe pour plus de détails.

Pour plus d’informations, consultez la [Présentation des environnements de test](./home.md).

## Puis-je accéder à une ressource depuis plusieurs environnements de test ?

Les environnements de test sont des partitions isolées d’une instance Platform unique pour laquelle chaque environnement de test conserve sa propre bibliothèque indépendante de ressources. Il n’est pas possible d’accéder à une ressource qui existe dans un environnement de test depuis un autre environnement de test, quel que soit le type d’environnement de test (production ou hors production).

## De combien d’environnements de test de production puis-je disposer ?

Experience Platform ne prend en charge qu’un environnement de test de production par organisation IMS qui est fourni prêt à l’emploi. Bien qu’il soit possible de renommer l’environnement de test de production, il ne peut être ni supprimé ni réinitialisé. Les utilisateurs possédant des droits d’administration pour les environnements de test peuvent seulement créer, réinitialiser et supprimer des environnements de test hors production.

## De combien d’environnements de test hors production puis-je disposer ?

Pour le moment, vous pouvez avoir jusqu’à 15 environnements de test hors production actifs dans Experience Platform au sein d’une organisation IMS unique.

## Je viens de créer un environnement de test. Comment puis-je définir des autorisations pour les utilisateurs qui travailleront avec cet environnement de test ?

Adobe Admin Console lie les utilisateurs aux environnements de test et aux autorisations via l’utilisation de profils de produits. Après avoir créé un nouvel environnement de test, rendez-vous dans l’onglet **Autorisations** du profil de produits auquel vous souhaitez accorder l’accès, puis cliquez sur **Environnements de test**. De là, vous pouvez ajouter ou supprimer l’accès au nouvel environnement de test de la même manière que pour les autres autorisations.

Si vous souhaitez ajouter des autorisations uniques aux utilisateurs d’un environnement de test spécifique, vous pouvez avoir besoin de créer un nouveau profil de produits pour lequel vous aurez appliqué les environnements de test et les autorisations appropriées et attribuez ces utilisateurs à ce profil.

Pour plus d’informations sur la gestion des environnements de test et des autorisations dans Admin Console, consultez le [guide d’utilisation du contrôle d’accès](../access-control/ui/overview.md).
