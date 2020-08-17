---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics;data science workspace;data science
solution: Experience Platform
title: Guide de développement de l’API Sensei Machine Learning
topic: Developer guide
description: Ce guide de développement décrit les étapes à suivre pour vous aider à prendre en main l’API Sensei Machine Learning et présente les appels d’API visant à effectuer des opérations CRUD sur diverses ressources de Data Science Workspace.
translation-type: tm+mt
source-git-commit: 8f7ce97cdefd4fe79cb806e71e12e936caca3774
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 70%

---


# [!DNL Sensei Machine Learning] Guide du développeur d’API

The [!DNL Sensei Machine Learning] API provides a mechanism for data scientists to organize and manage machine learning services, from algorithm onboarding through experimentation and to service deployment.

Ce guide de développement décrit les étapes à suivre pour vous aider à prendre en main l’[API Sensei Machine Learning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) et présente les appels d’API visant à effectuer des opérations CRUD sur diverses ressources de Data Science Workspace.

## Prise en main

Vous devez avoir suivi le tutoriel portant sur l’[authentification](../../tutorials/authentication.md) pour pouvoir accéder aux en-têtes de requête suivants afin de passer des appels aux API [!DNL Adobe Experience Platform]

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* Content-Type: application/json

## Étapes suivantes

Une fois que vous disposez des informations d’authentification requises, vous pouvez accéder aux sections suivantes de ce guide de développement afin de consulter des exemples d’appels API aux groupes de points de terminaison suivants :

* [Moteurs](./engines.md)
* [Expériences](./experiments.md)
* [Insights](./insights.md)
* [MLInstances (recettes)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modèles](./models.md)
* [Annexe](./appendix.md)