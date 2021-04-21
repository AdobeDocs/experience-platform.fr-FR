---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Tutoriels de segmentation
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Segmentation Service propose une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir des données Real-time Customer Profile. Ces segments sont configurés et conservés de manière centralisée sur Platform et sont facilement accessibles depuis n’importe quelle solution Adobe.
exl-id: e45de6b5-ff71-4908-ad79-898084763704
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 55%

---

# Tutoriels de segmentation

Adobe Experience Platform [!DNL Segmentation Service] fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir de vos données [!DNL Real-time Customer Profile]. Ces segments sont configurés et maintenus de manière centralisée sur [!DNL Platform] et sont facilement accessibles par toute solution d&#39;Adobe. Pour en savoir plus sur la segmentation, commencez par lire la [présentation de Segmentation Service](../segmentation/home.md).

## Création d’une définition de segment

Une définition de segment correspond au jeu de règles utilisé pour décrire les caractéristiques principales ou le comportement d’une audience cible. Une fois conceptualisées, les règles décrites dans une définition de segment sont utilisées pour déterminer les membres de l’audience admissibles à un segment. Vous pouvez développer, tester, prévisualiser et enregistrer une définition de segment à l’aide de l’[!DNL Platform] interface utilisateur ou des API. Pour créer une définition de segment, suivez le [tutoriel création d’une API de segments](../segmentation/tutorials/create-a-segment.md) ou le [guide d’utilisation de l’interface utilisateur du créateur de segments](../segmentation/ui/overview.md).

## Évaluation d’un segment et accès aux résultats

Une fois que vous avez développé, testé et enregistré votre définition de segment, vous pouvez ensuite évaluer le segment soit par une évaluation planifiée soit par l’évaluation sur demande. L’évaluation planifiée (également appelée « segmentation planifiée ») vous permet de créer un planning récurrent d’exécution d’une tâche d’exportation d’une période spécifique, bien que l’évaluation sur demande implique la création d’une tâche de segmentation pour créer immédiatement l’audience. Pour en savoir plus, rendez-vous sur le tutoriel [Évaluation des résultats de segmentation](../segmentation/tutorials/evaluate-a-segment.md).

## Exportation des données de segment

Pour exporter des segments contenant des données [!DNL Profile], il faut d&#39;abord [créer un jeu de données dans lequel les données seront exportées](../segmentation/tutorials/create-dataset-export-segment.md), puis lancer une nouvelle tâche d&#39;exportation. Vous trouverez les étapes de création d’une tâche d’exportation dans le didacticiel sur [l’évaluation d’un segment](../segmentation/tutorials/evaluate-a-segment.md).

## Configuration des stratégies de fusion

Adobe Experience Platform permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chaque client. Lorsque ces données sont regroupées, les stratégies de fusion sont les règles que [!DNL Platform] utilise pour déterminer comment les données seront hiérarchisées et quelles données seront combinées pour créer cette vue unifiée. À l’aide d’API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation dans l’interface utilisateur. Pour utiliser les stratégies de fusion dans l&#39;interface utilisateur [!DNL Platform], consultez le [guide de l&#39;utilisateur des stratégies de fusion](../profile/ui/merge-policies.md). Pour utiliser les stratégies de fusion à l&#39;aide de l&#39;API [!DNL Real-time Customer Profile], consultez le [guide du développeur des stratégies de fusion](../profile/api/merge-policies.md).

## Application de la conformité à l’utilisation des données pour les segments

Les segments qui sont activés pour une utilisation dans [!DNL Real-time Customer Profile] contiennent un ID de stratégie de fusion dans leur définition de segment. Cette stratégie de fusion contient des informations sur les jeux de données à inclure dans le segment, qui à leur tour contiennent les libellés d’utilisation de données applicables. Pour connaître les étapes spécifiques à l’application de la conformité de l’utilisation des données pour un segment ciblé, suivez le [tutoriel sur l’application de la conformité de l’utilisation des données pour les segments](../segmentation/tutorials/governance.md).

## Segmentation par flux

La segmentation en flux continu permet d’évaluer instantanément un client dès qu’un événement entre dans un groupe de segments particulier. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées lorsque les données sont transmises à Adobe Experience Platform, ce qui signifie que l’appartenance à un segment est mise à jour sans exécuter de tâches de segmentation planifiées. Pour en savoir plus, consultez la [présentation de la segmentation par flux](../segmentation/api/streaming-segmentation.md).

## Segmentation d’entités multiples

La segmentation multientité permet d&#39;étendre les données [!DNL Profile] avec des données supplémentaires basées sur des produits, des magasins ou d&#39;autres classes non profils. Une fois connecté, les données d&#39;autres classes deviennent disponibles comme si elles étaient natives du schéma [!DNL Profile]. Pour en savoir plus, consultez la [documentation sur la segmentation d’entités multiples](../segmentation/multi-entity-segmentation.md).
