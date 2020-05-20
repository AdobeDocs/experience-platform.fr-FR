---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Guide du développeur d'API d'apprentissage automatique Sensei
topic: Developer guide
translation-type: tm+mt
source-git-commit: b0b44f4aaf365f58086cfa17d27fbba6ed2a2a97
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 2%

---


# Guide du développeur d&#39;API d&#39;apprentissage automatique Sensei

L&#39;API d&#39;apprentissage automatique Sensei fournit un mécanisme permettant aux chercheurs de données d&#39;organiser et de gérer les services d&#39;apprentissage automatique, de l&#39;intégration d&#39;algorithmes à l&#39;expérimentation en passant par le déploiement de services.

Ce guide du développeur décrit les étapes à suivre pour vous aider à début à l’aide de l’API [d’apprentissage automatique](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)Sensei et présente les appels d’API pour effectuer des opérations CRUD sur diverses ressources de l’espace de travail Data Science.

## Prise en main

Vous devez avoir suivi le didacticiel d’ [authentification](../../tutorials/authentication.md) pour pouvoir accéder aux en-têtes de demande suivants afin d’effectuer des appels aux API Adobe Experience Platform :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

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