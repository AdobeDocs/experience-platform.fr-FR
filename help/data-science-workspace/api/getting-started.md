---
keywords: Experience Platform ; guide du développeur ; point de terminaison ; Espace de travail des sciences des données ; sujets populaires ; espace de travail des sciences des données ; sciences des données
solution: Experience Platform
title: Guide de développement de l’API Sensei Machine Learning
topic: Developer guide
description: Ce guide de développement décrit les étapes à suivre pour vous aider à prendre en main l’API Sensei Machine Learning et présente les appels d’API visant à effectuer des opérations CRUD sur diverses ressources de Data Science Workspace.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 65%

---


# Guide du développeur de l’API [!DNL Sensei Machine Learning]

L&#39;API [!DNL Sensei Machine Learning] fournit un mécanisme permettant aux chercheurs de données d&#39;organiser et de gérer les services d&#39;apprentissage automatique, de l&#39;intégration des algorithmes à l&#39;expérimentation en passant par le déploiement des services.

Ce guide de développement décrit les étapes à suivre pour vous aider à prendre en main l’[API Sensei Machine Learning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) et présente les appels d’API visant à effectuer des opérations CRUD sur diverses ressources de Data Science Workspace.

## Prise en main

Vous devez avoir suivi le tutoriel portant sur l’[authentification](https://www.adobe.com/go/platform-api-authentication-en) pour pouvoir accéder aux en-têtes de requête suivants afin de passer des appels aux API [!DNL Adobe Experience Platform]

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform] sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* x-sandbox-name: `{SANDBOX_NAME}`

Pour plus d&#39;informations sur les sandbox dans [!DNL Platform], consultez la [documentation d&#39;aperçu de sandbox](../../sandboxes/home.md).

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