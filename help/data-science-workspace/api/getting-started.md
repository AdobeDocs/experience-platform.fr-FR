---
keywords: Experience Platform;guide de développement;point de terminaison;Data Science Workspace;rubriques populaires;espace de travail Data Science;science des données
solution: Experience Platform
title: Guide de l’API d’apprentissage automatique Sensei
description: L’API Sensei Machine Learning permet aux développeurs d’effectuer des opérations CRUD sur diverses ressources Data Science Workspace. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
role: Developer
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 62%

---

# Guide de l’API [!DNL Sensei Machine Learning]

L’API [!DNL Sensei Machine Learning] fournit un mécanisme permettant aux spécialistes des données d’organiser et de gérer les services d’apprentissage automatique, de l’intégration des algorithmes à l’expérimentation et au déploiement des services.

Ce guide de développement décrit les étapes à suivre pour vous aider à prendre en main l’[API Sensei Machine Learning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) et présente les appels d’API visant à effectuer des opérations CRUD sur diverses ressources de l’espace de travail de science des données.

## Prise en main

Vous devez avoir terminé le tutoriel [authentication](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) afin d’avoir accès aux en-têtes de requête suivants pour effectuer des appels vers les API [!DNL Adobe Experience Platform] :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

* x-sandbox-name : `{SANDBOX_NAME}`

Pour plus d’informations sur les sandbox dans [!DNL Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* Content-Type: application/json

## Étapes suivantes

Une fois que vous disposez des informations d’authentification requises, vous pouvez accéder aux sections suivantes de ce guide de développement afin de consulter des exemples d’appels API aux groupes de points d’entrée suivants :

* [Moteurs](./engines.md)
* [Expériences](./experiments.md)
* [Insights](./insights.md)
* [MLInstances (Recettes)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modèles](./models.md)
* [Annexe](./appendix.md)
