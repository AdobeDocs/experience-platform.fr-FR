---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide du développeur de Privacy Service
description: Utilisez l’API RESTful pour gérer les données personnelles de vos sujets de données dans les applications Adobe Experience Cloud.
topic: developer guide
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 2%

---


# Guide du développeur de Privacy Service

Adobe Experience Platform Privacy Service fournit une API RESTful et une interface utilisateur qui vous permettent de gérer (d’accéder et de supprimer) les données personnelles de vos personnes de données (clients) dans les applications Adobe Experience Cloud. Privacy Service fournit également un mécanisme central d’audit et de consignation qui vous permet d’accéder à l’état et aux résultats des tâches impliquant des applications Experience Cloud.

Ce guide explique comment utiliser l’API de Privacy Service. Pour plus d’informations sur l’utilisation de l’interface utilisateur, consultez la présentation [de l’interface utilisateur de](../ui/overview.md)Privacy Service. Pour obtenir une liste complète de tous les points de terminaison disponibles dans l’API de Privacy Service, consultez la référence [de l’](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)API.

## Prise en main

Ce guide nécessite une bonne compréhension des fonctionnalités suivantes de la plateforme d’expérience :

* [Privacy Service](../home.md): Fournit une API RESTful et une interface utilisateur qui vous permettent de gérer les requêtes d’accès et de suppression de vos sujets de données (clients) dans les applications Adobe Experience Cloud.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer l’API de Privacy Service.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

* Content-Type : application/json

## Étapes suivantes

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l’API de Privacy Service. Le document sur les tâches [de](privacy-jobs.md) confidentialité passe en revue les différents appels d’API que vous pouvez effectuer à l’aide de l’API Privacy Service. Chaque exemple d’appel comprend le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.
