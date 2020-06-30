---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Guide du développeur d'API d'apprentissage automatique Sensei
topic: Developer guide
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 3%

---


# [!DNL Sensei Machine Learning] Guide du développeur d’API

L’ [!DNL Sensei Machine Learning] API fournit un mécanisme permettant aux chercheurs de données d’organiser et de gérer les services d’apprentissage automatique, de l’intégration des algorithmes à l’expérimentation en passant par le déploiement de services.

Ce guide du développeur décrit les étapes à suivre pour vous aider à début à l’aide de l’API [d’apprentissage automatique](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)Sensei et présente les appels d’API pour effectuer des opérations CRUD sur diverses ressources de l’espace de travail Data Science.

## Prise en main

Vous devez avoir suivi le didacticiel d’ [authentification](../../tutorials/authentication.md) pour pouvoir accéder aux en-têtes de demande suivants pour effectuer des appels aux [!DNL Adobe Experience Platform] API :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform] sont isolées à des sandbox virtuels spécifiques. Toutes les requêtes aux [!DNL Platform] API nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Pour plus d’informations sur les sandbox dans [!DNL Platform], voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

* Content-Type : application/json

## Étapes suivantes

Une fois que vous avez rassemblé les informations d’identification d’authentification requises, vous pouvez accéder aux sections suivantes de ce guide du développeur pour consulter des exemples d’appels d’API aux groupes de points de terminaison suivants :

* [Moteurs](./engines.md)
* [Expériences](./experiments.md)
* [Statistiques](./insights.md)
* [MLInstances (Recettes)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modèles](./models.md)
* [Annexe](./appendix.md)