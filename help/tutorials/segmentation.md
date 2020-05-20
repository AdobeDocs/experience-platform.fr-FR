---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Didacticiels de segmentation
topic: tutorial
translation-type: tm+mt
source-git-commit: 6705cb699b0785e317a6e437fc8a01ca77266f84
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 8%

---


# Didacticiels de segmentation

Le service de segmentation de la plateforme Adobe Experience Platform fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir de vos données de Profil client en temps réel. Ces segments sont configurés et maintenus de manière centralisée sur la plate-forme et sont facilement accessibles par toute solution Adobe. Pour en savoir plus sur la segmentation, lisez tout d’abord l’aperçu [du service de](../segmentation/home.md)segmentation.

## Création d’une définition de segment

Une définition de segment est le jeu de règles utilisé pour décrire les principales caractéristiques ou le comportement d’une audience de cible. Une fois conceptualisée, les règles décrites dans une définition de segment sont utilisées pour déterminer les membres d’audience admissibles pour un segment. Le développement, le test, la prévisualisation et l’enregistrement d’une définition de segment peuvent être effectués à l’aide de l’interface utilisateur ou des API de la plateforme. Pour créer une définition de segment, suivez le didacticiel [de](../segmentation/tutorials/create-a-segment.md) création d’une API de segment ou le guide [d’utilisateur de l’interface utilisateur du créateur de](../segmentation/ui/overview.md)segments.

## Évaluer un segment et accéder aux résultats

Une fois que vous avez développé, testé et enregistré votre définition de segment, vous pouvez ensuite évaluer le segment par le biais d’une évaluation planifiée ou d’une évaluation à la demande. L’évaluation planifiée (également appelée &quot;segmentation planifiée&quot;) vous permet de créer un calendrier récurrent pour l’exécution d’une tâche d’exportation à un moment donné, tandis que l’évaluation à la demande implique la création d’une tâche de segment afin de créer l’audience immédiatement. Pour en savoir plus, consultez le tutoriel pour [évaluer les résultats](../segmentation/tutorials/evaluate-a-segment.md)des segments et y accéder.

## Exporter des données de segment

Pour exporter des segments contenant des données de Profil, il faut d&#39;abord [créer un jeu de données dans lequel les données seront exportées](../segmentation/tutorials/create-dataset-export-segment.md), puis lancer une nouvelle tâche d&#39;exportation. Vous trouverez les étapes de création d’une tâche d’exportation dans le didacticiel [de l’API d’](../segmentation/tutorials/export-data.md)exportation.

## Configuration des stratégies de fusion

Adobe Experience Platform vous permet de rassembler des données à partir de plusieurs sources et de les combiner afin d’obtenir une vue complète de chacun de vos clients. Les stratégies de fusion sont les règles utilisées par Platform pour déterminer quelle est la priorité des données et quelles données seront combinées pour créer cette vue unifiée. A l’aide des API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre entreprise. Pour utiliser des stratégies de fusion dans l’interface utilisateur de la plate-forme, consultez le guide [d’utilisation des stratégies de](../profile/ui/merge-policies.md)fusion. Pour utiliser des stratégies de fusion à l’aide de l’API Profil client en temps réel, consultez le guide [du développeur des stratégies de](../profile/api/merge-policies.md)fusion.

## Appliquer la conformité d’utilisation des données aux segments

Les segments qui sont activés pour une utilisation dans le Profil client en temps réel contiennent un identifiant de stratégie de fusion dans leur définition de segment. Cette stratégie de fusion contient des informations sur les jeux de données à inclure dans le segment, qui contiennent à leur tour les étiquettes d’utilisation des données applicables. Pour connaître les étapes spécifiques à l&#39;application de la conformité à l&#39;utilisation des données pour un segment d&#39;audience, suivez le tutoriel d&#39;application de la conformité à l&#39;utilisation des [données pour les segments](../segmentation/tutorials/governance.md).

## (bêta) Segmentation de diffusion en continu

>[!NOTE]
>La segmentation en flux continu est en version bêta et sera disponible sur demande. Les fonctionnalités et la documentation peuvent être modifiées.

La segmentation en flux continu (également appelée évaluation continue de la requête) permet d’évaluer instantanément un client dès qu’un événement entre dans un groupe de segments particulier. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées lorsque les données sont transmises à Adobe Experience Platform, ce qui signifie que l’appartenance à un segment est mise à jour sans exécuter les tâches de segmentation planifiées. Pour en savoir plus, consultez la présentation [de la segmentation](../segmentation/api/streaming-segmentation.md)en flux continu.

## Segmentation multientité

La segmentation multientité permet d’étendre les données de Profil avec des données supplémentaires basées sur des produits, des magasins ou d’autres classes non profils. Une fois connecté, les données d’autres classes deviennent disponibles comme si elles étaient natives du schéma de profil. Pour en savoir plus sur les déplacements, consultez la documentation [sur la segmentation](../segmentation/multi-entity-segmentation.md)multientité.