---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Tutoriels de segmentation
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Segmentation Service propose une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir des données Real-time Customer Profile. Ces segments sont configurés et conservés de manière centralisée sur Platform et sont facilement accessibles depuis n’importe quelle solution Adobe.
exl-id: e45de6b5-ff71-4908-ad79-898084763704
source-git-commit: 36f64b3a1e75c9badaee29e28408504eabac64fe
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 57%

---

# Tutoriels de segmentation

Adobe Experience Platform [!DNL Segmentation Service] fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir de vos données [!DNL Real-time Customer Profile]. Ces segments sont configurés et conservés de manière centralisée sur [!DNL Platform] et sont facilement accessibles par toute solution d’Adobe. Pour en savoir plus sur la segmentation, commencez par lire la [présentation de Segmentation Service](../segmentation/home.md).

## Création d’une définition de segment

Une définition de segment correspond au jeu de règles utilisé pour décrire les caractéristiques principales ou le comportement d’une audience cible. Une fois conceptualisées, les règles décrites dans une définition de segment sont utilisées pour déterminer les membres de l’audience admissibles à un segment. Le développement, le test, la prévisualisation et l’enregistrement d’une définition de segment peuvent être effectués à l’aide de l’interface utilisateur [!DNL Platform] ou des API. Pour créer une définition de segment, suivez le [tutoriel création d’une API de segments](../segmentation/tutorials/create-a-segment.md) ou le [guide d’utilisation de l’interface utilisateur du créateur de segments](../segmentation/ui/overview.md).

## Évaluation d’un segment et accès aux résultats

Une fois que vous avez développé, testé et enregistré votre définition de segment, vous pouvez ensuite évaluer le segment soit par une évaluation planifiée soit par l’évaluation sur demande. L’évaluation planifiée (également appelée « segmentation planifiée ») vous permet de créer un planning récurrent d’exécution d’une tâche d’exportation d’une période spécifique, bien que l’évaluation sur demande implique la création d’une tâche de segmentation pour créer immédiatement l’audience. Pour en savoir plus, rendez-vous sur le tutoriel [Évaluation des résultats de segmentation](../segmentation/tutorials/evaluate-a-segment.md).

## Exportation des données de segment

L’exportation de segments contenant des données [!DNL Profile] nécessite d’abord [la création d’un jeu de données dans lequel les données seront exportées](../segmentation/tutorials/create-dataset-export-segment.md), puis le lancement d’une nouvelle tâche d’exportation. Vous trouverez les étapes de génération d’une tâche d’exportation dans le tutoriel sur l’[évaluation d’un segment](../segmentation/tutorials/evaluate-a-segment.md).

## Configuration des stratégies de fusion

Adobe Experience Platform permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chaque client. Lorsque vous rassemblez ces données, les stratégies de fusion sont les règles utilisées par [!DNL Platform] pour déterminer la priorité des données et les données qui seront combinées pour créer cette vue unifiée. À l’aide d’API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation dans l’interface utilisateur. Pour en savoir plus sur les stratégies de fusion et le rôle qu’elles jouent dans Experience Platform, commencez par lire la [présentation des stratégies de fusion](../profile/merge-policies/overview.md).

## Application de la conformité à l’utilisation des données pour les segments

Les segments activés pour une utilisation dans [!DNL Real-time Customer Profile] contiennent un ID de stratégie de fusion dans leur définition de segment. Cette stratégie de fusion contient des informations sur les jeux de données à inclure dans le segment, qui à leur tour contiennent les libellés d’utilisation de données applicables. Pour connaître les étapes spécifiques à l’application de la conformité de l’utilisation des données pour un segment ciblé, suivez le [tutoriel sur l’application de la conformité de l’utilisation des données pour les segments](../segmentation/tutorials/governance.md).

## Segmentation par flux

La segmentation par flux permet d’évaluer instantanément un client dès qu’un événement entre dans un groupe de segments particulier. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées au fur et à mesure que les données sont transmises à Adobe Experience Platform, ce qui signifie que l’adhésion au segment sera conservée à jour sans exécuter les tâches de segmentation planifiées. Pour en savoir plus, consultez la [présentation de la segmentation par flux](../segmentation/api/streaming-segmentation.md).

## Segmentation d’entités multiples

La segmentation d’entités multiples permet d’étendre les données [!DNL Profile] avec des données supplémentaires basées sur des produits, des magasins ou d’autres classes hors profil. Une fois connectées, les données d’autres classes deviennent disponibles comme si elles étaient natives du schéma [!DNL Profile]. Pour en savoir plus, consultez la [documentation sur la segmentation d’entités multiples](../segmentation/multi-entity-segmentation.md).
