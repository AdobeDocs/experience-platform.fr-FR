---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Didacticiels de segmentation
topic: tutorial
translation-type: tm+mt
source-git-commit: 6705cb699b0785e317a6e437fc8a01ca77266f84

---


# Didacticiels de segmentation

Le service de segmentation de la plate-forme Adobe Experience Platform fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer   à partir de vos données de client en temps réel. Ces segments sont configurés et maintenus de manière centralisée sur la plate-forme et sont facilement accessibles par n’importe quelle solution Adobe. Pour en savoir plus sur la segmentation, lisez tout d’abord l’aperçu [du service de](../segmentation/home.md)segmentation.

## Création d’une définition de segment

Une définition de segment est le jeu de règles utilisé pour décrire les principales caractéristiques ou le comportement d’un   . Une fois conceptualisée, les règles décrites dans une définition de segment sont utilisées pour déterminer les membres  admissibles  un segment. Le développement, le test, la prévisualisation et l’enregistrement d’une définition de segment peuvent être effectués à l’aide de l’interface utilisateur ou des API de la plateforme. Pour créer une définition de segment, suivez le didacticiel [de](../segmentation/tutorials/create-a-segment.md) création d’une API de segment ou le guide [d’utilisateur de l’interface utilisateur du créateur de](../segmentation/ui/overview.md)segments.

## Evaluer un segment et accéder aux résultats

Une fois que vous avez développé, testé et enregistré votre définition de segment, vous pouvez ensuite évaluer le segment par le biais d’une évaluation planifiée ou d’une évaluation à la demande. L’évaluation programmée (également appelée &quot;segmentation programmée&quot;) vous permet de créer un calendrier récurrent pour l’exécution d’une tâche d’exportation à un moment spécifique, tandis que l’évaluation à la demande implique la création d’une tâche de segment afin de créer immédiatement le  . Pour en savoir plus, consultez le didacticiel pour [évaluer les résultats](../segmentation/tutorials/evaluate-a-segment.md)des segments et y accéder.

## Exporter des données de segment

Pour exporter des segments contenant des données , vous devez d’abord [créer un jeu de données dans lequel les données seront exportées](../segmentation/tutorials/create-dataset-export-segment.md), puis lancer une nouvelle tâche d’exportation. Vous trouverez les étapes de génération d’une tâche d’exportation dans le didacticiel [API](../segmentation/tutorials/export-data.md)d’exportation.

## Configuration des stratégies de fusion

Adobe Experience Platform vous permet de rassembler des données à partir de plusieurs sources et de les combiner afin de voir un  complet de chacun de vos clients individuels. Les stratégies de fusion sont les règles utilisées par Platform pour déterminer quelle est la priorité des données et quelles données seront combinées pour créer cette vue unifiée. A l’aide des API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre entreprise. Pour utiliser des stratégies de fusion dans l’interface utilisateur de la plate-forme, consultez le guide [utilisateur des stratégies de](../profile/ui/merge-policies.md)fusion. Pour utiliser des stratégies de fusion à l’aide de l’API  client en temps réel, consultez le guide [du développeur des stratégies de](../profile/api/merge-policies.md)fusion.

## Appliquer la conformité d’utilisation des données aux segments

Les segments qui sont activés pour une utilisation dans le de clients en temps réel contiennent un ID de stratégie de fusion dans leur définition de segment. Cette stratégie de fusion contient des informations sur les jeux de données à inclure dans le segment, qui à son tour contiennent les étiquettes d’utilisation de données applicables. Pour connaître les étapes spécifiques à l’application de la conformité à l’utilisation des données pour un segment  de , suivez le didacticiel sur l’application de la conformité à l’utilisation des [données pour les segments](../segmentation/tutorials/governance.md).

## (bêta) Segmentation en flux continu

>[!NOTE]
>La segmentation en flux continu est en version bêta et sera disponible sur demande. Les fonctionnalités et la documentation peuvent être modifiées.

La segmentation en flux continu (également connue sous le nom d’évaluation  continue) permet d’évaluer instantanément un client dès qu’un  de arrive dans un groupe de segments particulier. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées lorsque les données sont transmises à Adobe Experience Platform, ce qui signifie que l’appartenance aux segments est maintenue à jour sans exécuter les tâches de segmentation programmée. Pour en savoir plus, consultez la présentation [de la segmentation en](../segmentation/api/streaming-segmentation.md)flux continu.

## Segmentation multientité

La segmentation multientité permet d’étendre les données  avec des données supplémentaires basées sur des produits, des magasins ou d’autres classes  non. Une fois connecté, les données d’autres classes deviennent disponibles comme si elles étaient natives du  . Pour en savoir plus sur le déplacement, consultez la documentation [sur la segmentation](../segmentation/multi-entity-segmentation.md)multientité.