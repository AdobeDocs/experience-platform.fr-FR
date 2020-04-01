---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience 10 septembre 2019
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: 28a8fc496c85b334e89d0f0a130d3cc5c8956399

---


# Notes de mise à jour d’Adobe Experience Platform

## Date de publication : 10 septembre 2019

## Ingestion des données

Adobe Experience Platform offre un ensemble de fonctionnalités très complet pour assimiler tout type de données et leur latence. L’intégration des données d’Adobe Experience Platform propose plusieurs alternatives pour l’assimilation de données, notamment des API par lots, des API de diffusion en continu, des connecteurs Adobe natifs, des partenaires d’intégration de données ou l’interface utilisateur d’Adobe Experience Platform.

**Nouvelles fonctionnalités**

| Fonction | Description |
| ----------- | ---------- |
| Nouveau domaine pour l’assimilation en flux continu | Le `dcs.data.adobe.net` domaine a été déplacé vers le nouveau domaine commun de collecte de données `dcs.adobedc.net`. Les utilisateurs doivent mettre à jour leurs implémentations conformément à la documentation révisée sur l’assimilation en flux continu d’Adobe Experience Platform. Toute la documentation relative à l’assimilation en flux continu d’Adobe Experience Platform a été mise à jour pour utiliser le nouveau domaine. |

Pour plus d&#39;informations, consultez la documentation [sur l&#39;](../../ingestion/home.md)intégration des données.

## Espace de travail Data Science

Adobe Experience Platform Data Science Workspace est un service entièrement géré au sein d’Experience Platform qui permet aux spécialistes des données de générer en toute transparence des informations à partir de données et de contenu sur les solutions Adobe et les systèmes tiers en créant et en mettant en oeuvre des modèles d’apprentissage automatique. Data Science Workspace est étroitement intégré à la plate-forme et alimente le cycle de vie des données de bout en bout, y compris l&#39;exploration et la préparation des données XDM, puis le développement et la mise en oeuvre de modèles pour enrichir automatiquement les  de clients en temps réel avec des connaissances d&#39;apprentissage automatique.

**Nouvelles fonctionnalités**

| Fonction | Description |
| -----------| ---------- |
| Planification des services via l’interface utilisateur | Intégration avec Platform Orchestration Service afin d’automatiser la formation et la notation des modèles avec des calendriers définis par l’utilisateur à l’aide de l’interface utilisateur. |
| Galerie de services | Parcourez, surveillez et accédez aux services d’apprentissage automatique grâce à la possibilité de planifier des tâches de formation et de notation automatisées, le tout dans la nouvelle Galerie de services. |
| JupyterLab 5.0.0 | Améliorations de l’interface utilisateur de JupyterLab. |

**Problèmes connus**

* Il n’existe actuellement aucun moyen accessible dans la Galerie de services pour supprimer un service existant. En attendant, reportez-vous à la référence [API d’apprentissage automatique](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei pour supprimer un service existant par le biais d’appels d’API.
* La Galerie de services ne prend pas en charge la pagination pour filtrer les exécutions de formation et de notation d’un service.
* Lors de la configuration d’une formation planifiée ou d’une notation, la configuration de la fréquence horaire empêche l’application de la planification.

Pour plus d’informations, consultez la section Présentation [de](../../data-science-workspace/home.md)Data Science Workspace.

## Service 

Le service de  de permet d’utiliser SQL standard pour des données  dans Adobe Experience Platform afin de prendre en charge divers cas d’utilisation de l’et de l’utilisation de l’utilisation de l’. Il s’agit d’un outil sans serveur qui vous permet de joindre des jeux de données de Data Lake et de capturer les résultats de l’ en tant que nouveau jeu de données à utiliser dans , Data Science Workspace ou pour l’assimilation dans le  client en temps réel.

Vous pouvez utiliser le service de  pour créer des données  des écosystèmes de , en créant une image des clients dans leurensemble d’interactions. Ces  peuvent inclure des systèmes de point de vente, des systèmes Web, mobiles ou CRM.

**Nouvelles fonctionnalités**

| Fonction | Description |
| -----------| ---------- |
| Améliorations apportées à l’éditeur de  | Ajout d’une fonction d’enregistrement qui vous permet d’enregistrer un  et d’y travailler ultérieurement. Ajout d’un onglet &quot;Parcourir&quot; à l’interface utilisateur du service  sur Adobe Experience Platform, qui affiche les enregistrés par les utilisateurs de votre entreprise. Mise en oeuvre d’un panneau &quot;Détails &quot; qui affiche des métadonnées utiles sur le  en cours de consultation. |
| Nouvelles fonctions d&#39;attribution | Fonctions définies par Adobe dans le service de  au  pour l’attribution de  avec des paramètres d’expiration. |
| Améliorations de la syntaxe SQL | Prise en charge de la syntaxe iLike. |
| Générer des jeux de données avec un XDM défini  | Ajout d’une nouvelle clause dans le Create Table as Select (CTAS) qui vous permet de spécifier un  de. |

For more information, refer to the [Query Service documentation](../../query-service/home.md).