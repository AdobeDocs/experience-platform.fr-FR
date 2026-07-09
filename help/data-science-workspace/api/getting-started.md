---
keywords: Experience Platform;guide de développement;point d’entrée;Workspace de science des données;rubriques populaires;espace de travail de science des données;science des données
solution: Experience Platform
title: Guide de l’API de machine learning d’Adobe AI
description: L’API Adobe AI Machine Learning permet aux développeurs d’effectuer des opérations CRUD sur diverses ressources Workspace de science des données. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
role: Developer
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
TQID: https://experienceleague.adobe.com/CXuMFUClC9RJvEH6Q4Cbp7L8D4XclUrm42eGM75VNJE
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bcc5edb5-84c3-4940-9f84-ed88b6c16274id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 9eb5b266c15495d852a671829d46fd127ad33ac9
workflow-type: tm+mt
source-wordcount: 282
ht-degree: 42%

---

# Guide de l’API de machine learning d’Adobe AI

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

L’API Adobe AI Machine Learning fournit un mécanisme permettant aux spécialistes des données d’organiser et de gérer les services de machine learning, de l’intégration des algorithmes à l’expérimentation et au déploiement des services.

Ce guide de développement décrit les étapes à suivre pour commencer à utiliser l’API [Adobe AI Machine Learning](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) et présente les appels API pour effectuer des opérations CRUD sur diverses ressources Workspace de science des données.

## Prise en main

Vous devez avoir suivi le tutoriel [authentification](/help/landing/api-authentication.md) pour pouvoir accéder aux en-têtes de requête suivants afin de passer des appels aux API [!DNL Adobe Experience Platform] :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

* x-sandbox-name : `{SANDBOX_NAME}`

Pour plus d’informations sur les sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant une payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

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
