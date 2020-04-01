---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide du développeur de Privacy Service
description: Utilisez l’API RESTful pour gérer les données personnelles de vos sujets de données dans les applications Adobe Experience Cloud.
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a28ad2725094e0748e2860276ab2e7581d790ac

---


# Guide du développeur de Privacy Service

Le service de confidentialité d’Adobe Experience Platform fournit une API RESTful et une interface utilisateur qui vous permettent de gérer (d’accéder et de supprimer) les données personnelles de vos sujets de données (clients) dans les applications Adobe Experience Cloud. Privacy Service fournit également un mécanisme central d’audit et de journalisation qui vous permet d’accéder à l’état et aux résultats des tâches impliquant des applications Experience Cloud.

Ce guide explique comment utiliser l’API de Privacy Service. Pour plus d’informations sur l’utilisation de l’interface utilisateur, reportez-vous à la présentation [de l’interface utilisateur de](../ui/overview.md)Privacy Service. Pour obtenir un complet de tous les points de fin disponibles dans l’API de Privacy Service, consultez la référence [de l’](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)API.

## Prise en main

Ce guide nécessite une bonne compréhension des fonctionnalités de la plateforme d’expérience suivantes :

* [Privacy Service](../home.md): Fournit une API RESTful et une interface utilisateur qui vous permettent de gérer les demandes d’accès et de suppression de vos sujets de données (clients) dans les applications Adobe Experience Cloud.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir effectuer des appels vers l’API de Privacy Service.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](https://www.adobe.io/apis/experienceplatform/home/services/troubleshooting.html#!api-specification/markdown/narrative/technical_overview/platform_faq_and_troubleshooting/platform_faq_and_troubleshooting.md) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

* Content-Type : application/json

## Étapes suivantes

Maintenant que vous comprenez les en-têtes à utiliser, vous êtes prêt à lancer des appels à l’API de Privacy Service. Le sur les tâches [de](privacy-jobs.md) confidentialité passe en revue les différents appels d’API que vous pouvez effectuer à l’aide de l’API Privacy Service. Chaque exemple d’appel comprend le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.
