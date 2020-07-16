---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriels de segmentation
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 55%

---


# Tutoriels de segmentation

Adobe Experience Platform [!DNL Segmentation Service] provides a user interface and RESTful API that allows you to build segments and generate audiences from your [!DNL Real-time Customer Profile] data. These segments are centrally configured and maintained on [!DNL Platform], and are readily accessible by any Adobe solution. Pour en savoir plus sur la segmentation, commencez par lire la [présentation de Segmentation Service](../segmentation/home.md).

## Création d’une définition de segment

Une définition de segment correspond au jeu de règles utilisé pour décrire les caractéristiques principales ou le comportement d’une audience cible. Une fois conceptualisées, les règles décrites dans une définition de segment sont utilisées pour déterminer les membres de l’audience admissibles à un segment. The developing, testing, previewing, and saving of a segment definition can be done using the [!DNL Platform] user interface or APIs. Pour créer une définition de segment, suivez le [tutoriel création d’une API de segments](../segmentation/tutorials/create-a-segment.md) ou le [guide d’utilisation de l’interface utilisateur du créateur de segments](../segmentation/ui/overview.md).

## Évaluation d’un segment et accès aux résultats

Une fois que vous avez développé, testé et enregistré votre définition de segment, vous pouvez ensuite évaluer le segment soit par une évaluation planifiée soit par l’évaluation sur demande. L’évaluation planifiée (également appelée « segmentation planifiée ») vous permet de créer un planning récurrent d’exécution d’une tâche d’exportation d’une période spécifique, bien que l’évaluation sur demande implique la création d’une tâche de segmentation pour créer immédiatement l’audience. Pour en savoir plus, rendez-vous sur le tutoriel [Évaluation des résultats de segmentation](../segmentation/tutorials/evaluate-a-segment.md).

## Exportation des données de segment

Exporting segments containing [!DNL Profile] data requires first [creating a dataset into which the data will be exported](../segmentation/tutorials/create-dataset-export-segment.md), then initiating a new export job. Vous pouvez trouver les étapes de génération d’une tâche d’exportation dans le [tutoriel de l’API d’exportation](../segmentation/tutorials/export-data.md).

## Configuration des stratégies de fusion

Adobe Experience Platform permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chaque client. When bringing this data together, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create that unified view. À l’aide d’API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation dans l’interface utilisateur. To work with merge policies in the [!DNL Platform] UI, visit the [merge policies user guide](../profile/ui/merge-policies.md). To work with merge policies using the [!DNL Real-time Customer Profile] API, see the [merge policies developer guide](../profile/api/merge-policies.md).

## Application de la conformité à l’utilisation des données pour les segments

Segments that are enabled for use in [!DNL Real-time Customer Profile] contain a merge policy ID within their segment definition. Cette stratégie de fusion contient des informations sur les jeux de données à inclure dans le segment, qui à leur tour contiennent les libellés d’utilisation de données applicables. Pour connaître les étapes spécifiques à l’application de la conformité de l’utilisation des données pour un segment ciblé, suivez le [tutoriel sur l’application de la conformité de l’utilisation des données pour les segments](../segmentation/tutorials/governance.md).

## Segmentation par flux

La segmentation en flux continu permet d’évaluer instantanément un client dès qu’un événement entre dans un groupe de segments particulier. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées lorsque les données sont transmises à l’Adobe Experience Platform, ce qui signifie que l’appartenance à un segment est tenue à jour sans exécuter de tâches de segmentation planifiées. Pour en savoir plus, consultez la [présentation de la segmentation par flux](../segmentation/api/streaming-segmentation.md).

## Segmentation d’entités multiples

Multi-entity segmentation is the ability to extend [!DNL Profile] data with additional data based on products, stores, or other non-profile classes. Once connected, data from additional classes becomes available as if they were native to the [!DNL Profile] schema. Pour en savoir plus, consultez la [documentation sur la segmentation d’entités multiples](../segmentation/multi-entity-segmentation.md).