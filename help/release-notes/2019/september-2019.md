---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience le 10 septembre 2019
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 4%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 10 septembre 2019**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [Incorporation de données](#ingestion)
* [Espace de travail Data Science](#dsw)
* [Requête Service](#query)

## Incorporation de données {#ingestion}

Adobe Experience Platform fournit un ensemble riche de fonctionnalités permettant d’assimiler n’importe quel type de données et de latence. L’intégration des données de la plate-forme Adobe Experience Platform offre plusieurs alternatives pour l’assimilation des données, notamment les API de lot, les API de diffusion en continu, les connecteurs Adobe natifs, les partenaires d’intégration des données ou l’interface utilisateur de la plate-forme Adobe Experience Platform.

**Nouvelles fonctionnalités**

| Fonction | Description |
| ----------- | ---------- |
| Nouveau domaine pour l’assimilation en flux continu | Le `dcs.data.adobe.net` domaine a été déplacé vers le nouveau domaine commun de collecte de données `dcs.adobedc.net`. Les utilisateurs doivent mettre à jour leurs mises en oeuvre conformément à la documentation révisée sur l’assimilation en flux continu d’Adobe Experience Platform. Toute la documentation relative à l’assimilation en flux continu d’Adobe Experience Platform a été mise à jour afin d’utiliser le nouveau domaine. |

Pour plus d&#39;informations, consultez la documentation [sur l&#39;](../../ingestion/home.md)importation de données.

## Espace de travail Data Science {#dsw}

Adobe Experience Platform Data Science Workspace est un service entièrement géré au sein d’Experience Platform qui permet aux spécialistes des données de générer en toute transparence des informations issues des données et du contenu sur les solutions Adobe et les systèmes tiers en créant et en mettant en oeuvre des modèles d’apprentissage automatique. Data Science Workspace est étroitement intégré à la plate-forme et alimente le cycle de vie des données de bout en bout, y compris l&#39;exploration et la préparation des données XDM, puis le développement et l&#39;exploitation de modèles pour enrichir automatiquement le Profil client en temps réel avec des connaissances d&#39;apprentissage automatique.

**Nouvelles fonctionnalités**

| Fonction | Description |
| -----------| ---------- |
| Planification des services via l’interface utilisateur | Intégration avec Platform Orchestration Service pour automatiser la formation et le score des modèles avec des planifications définies par l&#39;utilisateur à l&#39;aide de l&#39;interface utilisateur. |
| Galerie de services | Parcourez, surveillez et accédez aux services d’apprentissage automatique grâce à la possibilité de planifier des tâches de formation et de notation automatisées, le tout dans la galerie de services repensée. |
| JupyterLab 5.0.0 | Améliorations de l’interface utilisateur de JupyterLab. |

**Problèmes connus**

* Il n&#39;existe actuellement aucun moyen accessible dans la Galerie de services pour supprimer un service existant. En attendant, reportez-vous à la référence [de l&#39;API d&#39;apprentissage automatique](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei pour supprimer un service existant par le biais d&#39;appels d&#39;API.
* La Galerie de services ne prend pas en charge la pagination pour filtrer les exécutions de formation et de notation d&#39;un service.
* Lors de la configuration d’une formation planifiée ou d’un score, la définition de la fréquence sur horaire empêche l’application de la planification.

Pour en savoir plus, consultez la section Présentation [de](../../data-science-workspace/home.md)Data Science Workspace.

## Requête Service {#query}

Requête Service permet d’utiliser des données SQL standard pour la requête dans Adobe Experience Platform afin de prendre en charge divers cas d’analyse et d’utilisation de datas Management. Il s’agit d’un outil sans serveur qui vous permet de joindre des jeux de données de Data Lake et de capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans rapports, Data Science Workspace ou pour l’assimilation dans le Profil client en temps réel.

Vous pouvez utiliser Requête Service pour créer des écosystèmes d’analyse de données, en créant une image des clients sur leurs différents canaux d’interaction. Ces canaux peuvent inclure des systèmes de point de vente, des systèmes Web, mobiles ou CRM.

**Nouvelles fonctionnalités**

| Fonction | Description |
| -----------| ---------- |
| Améliorations apportées à l’éditeur de Requêtes | Ajout d’une fonction d’enregistrement qui vous permet d’enregistrer une requête et d’y travailler ultérieurement. Ajout d’un onglet &quot;Parcourir&quot; à l’interface utilisateur de Requête Service sur Adobe Experience Platform pour afficher les requêtes enregistrées par les utilisateurs de votre entreprise. Mise en oeuvre d’un panneau &quot;Détails de la Requête&quot; qui affiche des métadonnées utiles sur la requête affichée. |
| Nouvelles fonctions d&#39;attribution | Fonctions définies par Adobe dans Requête Service à la requête pour l’attribution de canaux avec des paramètres d’expiration. |
| Améliorations de la syntaxe SQL | Prise en charge de la syntaxe iLike. |
| Générer des jeux de données avec un Schéma XDM défini | Ajout d’une nouvelle clause dans les requêtes Create Table as Select (CTAS) qui vous permet de spécifier un schéma de cible. |

For more information, refer to the [Query Service documentation](../../query-service/home.md).