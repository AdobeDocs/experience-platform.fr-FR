---
title: Notes de mise à jour d’Adobe Experience Platform Septembre 2019
description: Notes de mise à jour de septembre 2019 pour Adobe Experience Platform.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 55%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 10 septembre 2019**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform fournit un ensemble riche de fonctionnalités permettant d’ingérer n’importe quel type et n’importe quelle latence de données. Adobe Experience Platform [!DNL Data Ingestion] fournit plusieurs alternatives pour l’ingestion de données, notamment des API par lots, des API de diffusion en continu, des connecteurs d’Adobe natifs, des partenaires d’intégration de données ou l’interface utilisateur de Adobe Experience Platform.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ----------- | ---------- |
| Nouveau domaine pour l’ingestion par flux | Le domaine `dcs.data.adobe.net` a été déplacé vers le nouveau domaine commun de collecte de données `dcs.adobedc.net`. Les utilisateurs doivent mettre à jour leurs mises en œuvre conformément à la documentation révisée sur l’ingestion par flux d’Adobe Experience Platform. Toute la documentation relative à l’ingestion par flux d’Adobe Experience Platform a été mise à jour pour utiliser le nouveau domaine. |

Pour plus d’informations, consultez la [documentation sur Data Ingestion](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] est un service entièrement géré au sein d’ [!DNL Experience Platform] qui permet aux spécialistes des données de générer en toute transparence des informations à partir de données et de contenu sur les solutions Adobe et les systèmes tiers en créant et en mettant en oeuvre des modèles d’apprentissage automatique. [!DNL Data Science Workspace] est étroitement intégré à et alimente le cycle de vie de la science des données de bout en bout, y compris l’exploration et la préparation des données XDM, puis le développement et la mise en œuvre de modèles pour enrichir automatiquement avec des insights d’apprentissage automatique.[!DNL Platform][!DNL Real-time Customer Profile]

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| -----------| ---------- |
| Planification des services via l’interface utilisateur | Intégré à [!DNL Platform] Orchestration Service pour automatiser la formation et la notation des modèles avec des plannings définis par l’utilisateur à l’aide de l’interface utilisateur. |
| [!DNL Service Gallery] | Parcourir, surveiller et accéder aux services d’apprentissage automatique avec la possibilité de planifier des tâches de formation et de notation automatisées, le tout dans le cadre de la reconception [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Améliorations de l’interface utilisateur. |

**Problèmes connus**

* Il n’existe actuellement aucun moyen accessible dans la variable [!DNL Service Gallery] pour supprimer un service existant. En attendant, consultez la [référence de l’API Sensei Machine Learning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) pour supprimer un service existant par le biais d’appels API.
* Le [!DNL Service Gallery] ne prend pas en charge la pagination pour filtrer les exécutions de formation et de notation d’un service.
* Lors de la configuration d’exécutions de formation ou de notation planifiées dans la variable [!DNL Service Gallery], la définition de la fréquence sur une valeur horaire empêche l’application du planning.

Pour plus d’informations, consultez la section [Présentation de Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] permet d’utiliser des commandes SQL standard pour rechercher des données dans Adobe Experience Platform afin de prendre en charge divers cas d’utilisation d’analyse et de gestion des données. Il s’agit d’un outil sans serveur qui vous permet de joindre des jeux de données à partir de la variable [!DNL Data Lake] et capturer les résultats de la requête en tant que nouveau jeu de données à utiliser dans les rapports, [!DNL Data Science Workspace]ou pour l’ingestion dans [!DNL Real-time Customer Profile].

Vous pouvez utiliser [!DNL Query Service] pour créer des écosystèmes d’analyse des données, en créant une image des clients sur leurs différents canaux d’interaction. Ces canaux peuvent inclure les systèmes de point de vente, le Web, les applications mobiles ou les systèmes de gestion de la relation client (CRM).

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| -----------| ---------- |
| Améliorations apportées à [!DNL Query Editor] | Ajout d’une fonction d’enregistrement qui vous permet d’enregistrer une requête et d’y revenir ultérieurement. Ajout d’un onglet &quot;Parcourir&quot; à la variable [!DNL Query Service] interface utilisateur de Adobe Experience Platform qui affiche les requêtes enregistrées par les utilisateurs de votre entreprise. Mise en place d’un panneau « Détails de la requête » qui affiche des métadonnées utiles sur la requête en cours de consultation. |
| Nouvelles fonctions d’attribution | Fonctions définies par Adobe dans [!DNL Query Service] pour interroger l’attribution de canaux avec des paramètres d’expiration. |
| Améliorations apportées à la syntaxe SQL | Prise en charge de la syntaxe iLike. |
| Génération de jeux de données avec un schéma XDM défini | Ajout d’une nouvelle clause dans les requêtes Create Table as Select (CTAS) qui permet de spécifier un schéma cible. |

Pour plus d’informations, consultez la [documentation de Query Service](../../query-service/home.md).
