---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour d’Experience Platform, 10 septembre 2019
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 57%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 10 septembre 2019**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform fournit un ensemble riche de fonctionnalités permettant d’ingérer n’importe quel type et n’importe quelle latence de données. Adobe Experience Platform [!DNL Data Ingestion] offre plusieurs alternatives pour l’assimilation de données, notamment les API de lot, les API de diffusion en continu, les connecteurs d’Adobe natifs, les partenaires d’intégration de données ou l’interface utilisateur Adobe Experience Platform.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ----------- | ---------- |
| Nouveau domaine pour l’ingestion par flux | Le domaine `dcs.data.adobe.net` a été déplacé vers le nouveau domaine commun de collecte de données `dcs.adobedc.net`. Les utilisateurs doivent mettre à jour leurs mises en œuvre conformément à la documentation révisée sur l’ingestion par flux d’Adobe Experience Platform. Toute la documentation relative à l’ingestion par flux d’Adobe Experience Platform a été mise à jour pour utiliser le nouveau domaine. |

Pour plus d’informations, consultez la [documentation sur Data Ingestion](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] est un service entièrement géré au sein de [!DNL Experience Platform] qui permet aux spécialistes des données de générer en toute transparence des informations à partir des données et du contenu sur les solutions d&#39;Adobe et les systèmes tiers en construisant et en mettant en oeuvre des modèles d&#39;apprentissage automatique. [!DNL Data Science Workspace] est étroitement intégré à et alimente le cycle de vie de la science des données de bout en bout, y compris l’exploration et la préparation des données XDM, puis le développement et la mise en œuvre de modèles pour enrichir automatiquement avec des insights d’apprentissage automatique.[!DNL Platform][!DNL Real-time Customer Profile]

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| -----------| ---------- |
| Planification des services via l’interface utilisateur | Intégré à [!DNL Platform] Orchestration Service pour automatiser la formation et la notation des modèles avec des planifications définies par l&#39;utilisateur à l&#39;aide de l&#39;interface utilisateur. |
| [!DNL Service Gallery] | Parcourez, surveillez et accédez aux services d’apprentissage automatique en planifiant des tâches de formation et de notation automatisées, le tout dans le cadre de la refonte [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Améliorations de l’interface utilisateur. |

**Problèmes connus**

* Il n&#39;existe actuellement aucun moyen accessible dans [!DNL Service Gallery] de supprimer un service existant. En attendant, consultez la [référence de l’API Sensei Machine Learning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) pour supprimer un service existant par le biais d’appels API.
* [!DNL Service Gallery] ne prend pas en charge la pagination pour filtrer les exécutions de formation et de notation d&#39;un service.
* Lors de la configuration d&#39;une formation planifiée ou d&#39;une notation, [!DNL Service Gallery] est exécuté, la définition de la fréquence horaire empêche l&#39;application de la planification.

Pour plus d’informations, consultez la section [Présentation de Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] permet d’utiliser des commandes SQL standard pour rechercher des données dans Adobe Experience Platform afin de prendre en charge divers cas d’utilisation d’analyse et de gestion des données. Il s&#39;agit d&#39;un outil sans serveur qui vous permet de joindre des jeux de données à partir de [!DNL Data Lake] et de capturer les résultats de la requête sous la forme d&#39;un nouveau jeu de données à utiliser dans le rapports, [!DNL Data Science Workspace] ou pour l&#39;assimilation dans [!DNL Real-time Customer Profile].

Vous pouvez utiliser [!DNL Query Service] pour créer des écosystèmes d&#39;analyse de données, en créant une image des clients sur leurs différents canaux d&#39;interaction. Ces canaux peuvent inclure les systèmes de point de vente, le Web, les applications mobiles ou les systèmes de gestion de la relation client (CRM).

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| -----------| ---------- |
| Améliorations apportées à [!DNL Query Editor] | Ajout d’une fonction d’enregistrement qui vous permet d’enregistrer une requête et d’y revenir ultérieurement. Ajouté un onglet &quot;Parcourir&quot; dans l&#39;interface utilisateur [!DNL Query Service] de Adobe Experience Platform qui affiche les requêtes enregistrées par les utilisateurs de votre organisation. Mise en place d’un panneau « Détails de la requête » qui affiche des métadonnées utiles sur la requête en cours de consultation. |
| Nouvelles fonctions d’attribution | Fonctions définies par Adobe dans [!DNL Query Service] à la requête pour l&#39;attribution de canal avec des paramètres d&#39;expiration. |
| Améliorations apportées à la syntaxe SQL | Prise en charge de la syntaxe iLike. |
| Génération de jeux de données avec un schéma XDM défini | Ajout d’une nouvelle clause dans les requêtes Create Table as Select (CTAS) qui permet de spécifier un schéma cible. |

Pour plus d’informations, consultez la [documentation de Query Service](../../query-service/home.md).