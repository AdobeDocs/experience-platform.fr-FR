---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Didacticiels sur le Profil client en temps réel
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 6%

---


# Configuration du service d’Profil et d’identité client en temps réel

Pour configurer le Profil client en temps réel pour votre entreprise, vous devez exécuter plusieurs workflows distincts. Ce document décrit les étapes à suivre et fournit des liens vers des didacticiels permettant d’exécuter chaque processus individuel. Pour en savoir plus sur le Profil client en temps réel, lisez tout d’abord l’aperçu [du](../profile/home.md)Profil.

## Activer le schéma pour le Profil et l&#39;identité

Avant que les données puissent être ingérées dans Adobe Experience Platform et utilisées dans la création de Profils clients en temps réel, un schéma doit être créé pour fournir la structure des données qui seront ingérées et ce schéma doit être activé pour une utilisation dans Profil et Adobe Experience Platform Identity Service. Pour obtenir des instructions détaillées sur la création d&#39;un schéma activé pour Profil et Identity Service, reportez-vous aux didacticiels de [création d&#39;un schéma à l&#39;aide de l&#39;API](../xdm/tutorials/create-schema-api.md) de registre de Schéma ou de [création d&#39;un schéma à l&#39;aide de l&#39;interface utilisateur](../xdm/tutorials/create-schema-ui.md)du Schéma Builder.

## Configuration d’un jeu de données pour le Profil et l’identité

Pour commencer à ingérer des données dans le Profil, vous devez disposer d’un jeu de données correctement configuré pour une utilisation avec le Profil client en temps réel et le service d’identité. Pour commencer, suivez le didacticiel [](../profile/tutorials/dataset-configuration.md)Configuration d’un jeu de données pour le Profil et l’identité.

## Configuration des stratégies de fusion

Adobe Experience Platform vous permet de rassembler des données à partir de plusieurs sources et de les combiner afin d’obtenir une vue complète de chacun de vos clients. Les stratégies de fusion sont les règles utilisées par Platform pour déterminer quelle est la priorité des données et quelles données seront combinées pour créer cette vue unifiée. A l’aide des API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre entreprise. Pour utiliser des stratégies de fusion dans l’interface utilisateur de la plate-forme, consultez le guide [d’utilisation des stratégies de](../profile/ui/merge-policies.md)fusion. Pour utiliser des stratégies de fusion à l’aide de l’API Profil client en temps réel, consultez le guide [du développeur des stratégies de](../profile/api/merge-policies.md)fusion.

## Configurer des projections de bord

Afin d’offrir des expériences coordonnées, cohérentes et personnalisées à vos clients sur plusieurs canaux en temps réel, les données appropriées doivent être facilement disponibles et mises à jour en continu au fur et à mesure des changements. Adobe Experience Platform permet cet accès en temps réel aux données grâce à ce que l’on appelle les arêtes. Un bord est un serveur géographiquement placé qui stocke les données et les rend facilement accessibles aux applications. Les données sont acheminées vers un bord par une projection, avec une destination de projection qui définit le bord auquel les données seront envoyées et une configuration de projection qui définit les informations spécifiques qui seront rendues disponibles sur le bord. Pour plus d’informations et pour commencer à travailler avec les arêtes, consultez le [sous-guide API Profil client en temps réel sur les projections](../profile/api/edge-projections.md)des arêtes.

## Étapes suivantes

Une fois que vous avez configuré le Profil client en temps réel pour votre organisation, vous pouvez commencer à ajouter des données à des profils clients individuels et à créer des segments d’audience en fonction d’attributs de client spécifiques. Pour commencer, consultez les didacticiels suivants :

* [Ajouter de données au Profil client en temps réel](../profile/tutorials/add-profile-data.md)
* [Création d’un segment](../segmentation/tutorials/create-a-segment.md)