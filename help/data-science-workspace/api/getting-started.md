---
keywords: Experience Platform;guide de développement;point d’entrée;Workspace de science des données;rubriques populaires;espace de travail de science des données;science des données
solution: Experience Platform
title: Guide de l’API Sensei Machine Learning
description: L’API Sensei Machine Learning permet aux développeurs d’effectuer des opérations CRUD sur diverses ressources Workspace de science des données. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
role: Developer
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 56%

---

# Guide de l’API [!DNL Sensei Machine Learning]

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

L’API [!DNL Sensei Machine Learning] fournit un mécanisme aux spécialistes des données pour organiser et gérer les services de machine learning, de l’intégration des algorithmes à l’expérimentation et au déploiement des services.

Ce guide de développement décrit les étapes à suivre pour vous aider à prendre en main l’[API Sensei Machine Learning](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) et présente les appels d’API visant à effectuer des opérations CRUD sur diverses ressources de l’espace de travail de science des données.

## Prise en main

Vous devez avoir suivi le tutoriel [authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) pour pouvoir accéder aux en-têtes de requête suivants afin de passer des appels aux API [!DNL Adobe Experience Platform] :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

* x-sandbox-name : `{SANDBOX_NAME}`

Pour plus d’informations sur les sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* Content-Type: application/json

## Étapes suivantes

Une fois que vous disposez des informations d’authentification requises, vous pouvez accéder aux sections suivantes de ce guide de développement afin de consulter des exemples d’appels API aux groupes de points d’entrée suivants :

* [Moteurs](./engines.md)
* [Expériences](./experiments.md)
* [Insights](./insights.md)
* [MLInstances (recettes)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modèles](./models.md)
* [Annexe](./appendix.md)
