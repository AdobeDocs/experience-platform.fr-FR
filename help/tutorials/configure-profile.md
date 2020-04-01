---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Didacticiels sur les  des clients en temps réel
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# Configuration du service d’identité et de la  des clients en temps réel

Pour configurer les  de clients en temps réel pour votre entreprise, vous devez exécuter plusieurs  de distincts. Ce décrit les étapes à suivre et fournit des liens vers des didacticiels pour compléter chaque flux de travail individuel. Pour en savoir plus sur les  de clients en temps réel, lisez d’abord l’aperçu [de la  du](../profile/home.md).

## Activation des  de pour la  et l’identité des

Avant que les données ne puissent être assimilées à Adobe Experience Platform et utilisées dans la création d’un client en temps réel, un doit être créé pour fournir la structure des données qui seront assimilées et ce  doit être activé pour une utilisation dans le service d’identité de la plateforme d’expérience et d’Adobe Experience Platform. Pour obtenir des instructions étape par étape sur la création d’un  activé pour les services d’identité et d’ de, reportez-vous aux didacticiels de [création d’un  à l’aide de l’API](../xdm/tutorials/create-schema-api.md) de registre des [d’analyse ou de](../xdm/tutorials/create-schema-ui.md)création d’un à l’aide de l’interface utilisateurdu Générateur de.

## Configuration d’un jeu de données pour les  et l’identité du

Pour commencer à ingérer des données dans les  de, vous devez disposer d’un jeu de données qui a été correctement configuré pour une utilisation avec le service d’identité et de client en temps réel. Pour commencer, suivez le didacticiel [Configuration d’un jeu de données pour les  et les identités](../profile/tutorials/dataset-configuration.md).

## Configuration des stratégies de fusion

Adobe Experience Platform vous permet de rassembler des données à partir de plusieurs sources et de les combiner afin de voir un  complet de chacun de vos clients individuels. Les stratégies de fusion sont les règles utilisées par Platform pour déterminer quelle est la priorité des données et quelles données seront combinées pour créer cette vue unifiée. A l’aide des API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre entreprise. Pour utiliser des stratégies de fusion dans l’interface utilisateur de la plate-forme, consultez le guide [utilisateur des stratégies de](../profile/ui/merge-policies.md)fusion. Pour utiliser des stratégies de fusion à l’aide de l’API  client en temps réel, consultez le guide [du développeur des stratégies de](../profile/api/merge-policies.md)fusion.

## Configuration des projections de bord

Afin d’offrir des expériences coordonnées, cohérentes et personnalisées à vos clients sur plusieurs  en temps réel, les données appropriées doivent être facilement disponibles et mises à jour en permanence au fur et à mesure des changements. Adobe Experience Platform permet cet accès en temps réel aux données grâce à l’utilisation de ce que l’on appelle les contours. Un bord est un serveur géographiquement placé qui stocke les données et les rend facilement accessibles aux applications. Les données sont acheminées vers un bord par une projection, avec une destination de projection définissant le bord auquel les données seront envoyées et une configuration de projection définissant les informations spécifiques qui seront rendues disponibles sur le bord. Pour plus d’informations et pour commencer à travailler avec les arêtes, reportez-vous au [sous-guide API  client en temps réel sur les projections](../profile/api/edge-projections.md)des arêtes.

## Étapes suivantes

Une fois que vous avez configuré des  de clients en temps réel pour votre entreprise, vous pouvez commencer à ajouter des données à des  de clients individuels et à créer des segments de  en fonction d’attributs de clients spécifiques. Pour commencer, reportez-vous aux didacticiels suivants :

* [Ajouter les données au client en temps réel](../profile/tutorials/add-profile-data.md)
* [Création d’un segment](../segmentation/tutorials/create-a-segment.md)