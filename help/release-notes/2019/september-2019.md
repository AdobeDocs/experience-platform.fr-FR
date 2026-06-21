---
title: Notes de mise à jour d’Adobe Experience Platform - Septembre 2019
description: Les notes de mise à jour de septembre 2019 pour Adobe Experience Platform.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
TQID: https://experienceleague.adobe.com/EKDdp3hjLuAo17WGURXgyo0vXxKw56-xbvHqoxEhT1I
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: a230274e-7e6e-49eb-b817-514495a710ac
  - id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6
  - id: d1a87129-ba05-4f15-98b1-233618f1774a
  - id: ee602049-8a18-43df-9299-a689a025a371
  - id: f5efb499-54f9-432b-ac5c-599dbac103af
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 2cffcfd0dd4a076ba938286af1548677d76c2a9a
workflow-type: tm+mt
source-wordcount: 548
ht-degree: 41%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : mercredi 10 septembre 2019**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform fournit un ensemble riche de fonctionnalités permettant d’ingérer n’importe quel type et n’importe quelle latence de données. Adobe Experience Platform [!DNL Data Ingestion] propose plusieurs alternatives pour l’ingestion de données, notamment des API Batch, des API Streaming, des connecteurs Adobe natifs, des partenaires d’intégration de données ou l’interface utilisateur de Adobe Experience Platform.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ----------- | ---------- |
| Nouveau domaine pour l’ingestion en flux continu | Le domaine `dcs.data.adobe.net` a été déplacé vers le nouveau domaine commun de collecte de données `dcs.adobedc.net`. Les utilisateurs et utilisatrices doivent mettre à jour leurs mises en œuvre conformément à la documentation révisée sur l’ingestion en flux continu d’Adobe Experience Platform. Toute la documentation relative à l’ingestion en flux continu d’Adobe Experience Platform a été mise à jour pour utiliser le nouveau domaine. |

Pour plus d’informations, consultez la [documentation sur Data Ingestion](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] est un service entièrement géré au sein de [!DNL Experience Platform] qui permet aux spécialistes des données de générer en toute transparence des informations à partir de données et de contenu sur les solutions Adobe et les systèmes tiers en créant et en mettant en œuvre des modèles de machine learning. [!DNL Data Science Workspace] est étroitement intégré à [!DNL Experience Platform] et alimente le cycle de vie complet de la science des données, y compris l’exploration et la préparation des données XDM, suivies du développement et de la mise en œuvre de modèles pour enrichir automatiquement les [!DNL Real-Time Customer Profile] avec les informations de machine learning.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| -----------| ---------- |
| Planification des services via l’interface utilisateur | Intégration au service [!DNL Experience Platform] Orchestration pour automatiser la formation et la notation des modèles avec des plannings définis par l’utilisateur à l’aide de l’interface utilisateur. |
| [!DNL Service Gallery] | Parcourez, surveillez et accédez aux services de machine learning avec la possibilité de planifier des tâches de formation et de notation automatisées, le tout dans le cadre de la nouvelle [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | Améliorations de l’interface utilisateur de [!DNL JupyterLab]. |

**Problèmes connus**

* Il n’existe actuellement aucun moyen accessible dans le [!DNL Service Gallery] pour supprimer un service existant. En attendant, reportez-vous à la référence [API Adobe AI Machine Learning](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) pour supprimer un service existant par le biais d’appels API.
* Le [!DNL Service Gallery] ne dispose pas de la prise en charge de la pagination pour filtrer les exécutions de formation et de notation d’un service.
* Lors de la configuration de l’entraînement ou de la notation planifiés via [!DNL Service Gallery], la définition de la fréquence sur toutes les heures empêche l’application du planning.

Pour plus d’informations, consultez la section [Présentation de l’espace de travail de science des données](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] permet d’utiliser le langage SQL standard pour interroger les données dans Adobe Experience Platform afin de prendre en charge divers cas d’utilisation d’analyse et de gestion des données. Il s’agit d’un outil sans serveur qui vous permet de joindre des jeux de données à partir du [!DNL Data Lake] et de capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, les [!DNL Data Science Workspace] ou pour ingestion dans les [!DNL Real-Time Customer Profile].

Vous pouvez utiliser [!DNL Query Service] pour créer des écosystèmes d’analyse de données, créant ainsi une image des clients sur leurs différents canaux d’interaction. Ces canaux peuvent inclure les systèmes de point de vente, le Web, les applications mobiles ou les systèmes de gestion de la relation client (CRM).

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| -----------| ---------- |
| Améliorations apportées à [!DNL Query Editor] | Ajout d’une fonction d’enregistrement qui vous permet d’enregistrer une requête et d’y revenir ultérieurement. Ajout d’un onglet « Parcourir » à l’interface utilisateur [!DNL Query Service] de Adobe Experience Platform qui affiche les requêtes enregistrées par les utilisateurs de votre organisation. Mise en place d’un panneau « Détails de la requête » qui affiche des métadonnées utiles sur la requête en cours de consultation. |
| Nouvelles fonctions d’attribution | Fonctions définies par Adobe [!DNL Query Service] de demander l’attribution du canal avec des paramètres d’expiration. |
| Améliorations apportées à la syntaxe SQL | Prise en charge de la syntaxe iLike. |
| Génération de jeux de données avec un schéma XDM défini | Ajout d’une nouvelle clause dans les requêtes Create Table as Select (CTAS) qui permet de spécifier un schéma cible. |

Pour plus d’informations, consultez la [documentation du service de requête](../../query-service/home.md).
