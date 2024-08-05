---
keywords: Experience Platform;accueil;Data Science Workspace;rubriques les plus consultées;contrôle d’accès;sandbox;pack de renseignements;fonctionnalités dsw;accès dsw;intelligence Adobe Experience Platform;intelligence;package de renseignement aep
solution: Experience Platform
title: Accès et fonctionnalités de Data Science Workspace
description: Le document suivant décrit les autorisations de Data Science Workspace et l’accès aux fonctionnalités.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 15%

---

# Accès à l’espace de travail de science des données et fonctionnalités associées

>[!NOTE]
>
>Le Workspace Data Science n’est plus disponible à l’achat.
>
>Cette documentation est destinée aux clients existants disposant de droits préalables à la Workspace Data Science.

Le document suivant décrit les autorisations et l’accès aux fonctionnalités de l’Workspace Data Science.

![Onglets DSW](./images/access/platform-tabs.png)

- **Notebooks :** fournit un environnement de développement interactif ([JupyterLab](./jupyterlab/overview.md)) pour explorer, analyser et modéliser vos données sur Experience Platform.
- **Modèles :** fournit des outils utilisés pour créer, publier et stocker des recettes et des modèles d’apprentissage automatique avancés. Pour plus d’informations, consultez le didacticiel [Créer et publier un modèle](./models-recipes/create-publish-model.md) Machine Learning.
- **Services :** contient à la fois des services fournis par l’Adobe tels que des [services AI/ML](../intelligent-services/home.md) et tous les services personnalisés que vous avez créés avec Data Science Workspace.

Pourquoi est-ce que je ne vois que l’onglet Services ?

- Votre entreprise ne peut avoir droit qu’à Adobe Real-Time Customer Data Platform (Real-Time CDP) qui inclut le service Customer AI AI/ML.

Si vous ne parvenez pas à voir l’un des onglets **Data Science** et souhaitez utiliser les fonctionnalités de Data Science Workspace, contactez votre administrateur de société pour vérifier si vous disposez d’une licence Adobe Experience Platform Intelligence.

## Packaging du Workspace de la science des données

Les fonctionnalités de Workspace de la science des données sont disponibles dans le package Adobe Experience Platform Intelligence et le module complémentaire Advanced Intelligence Pack

Le tableau suivant présente certaines des principales différences entre les droits de Workspace Data Science avec et sans le module complémentaire Advanced Intelligence Pack :

>[!NOTE]
>
>Vous pouvez obtenir plus d’un module complémentaire Advanced Intelligence Pack et la capacité accrue est ajoutée à votre droit global. Par exemple, si vous avez obtenu une licence 2 modules complémentaires Advanced Intelligence Pack Adobe Experience Platform, vous avez droit à un total de 20 utilisateurs simultanés de blocs-notes.

| Droit au Workspace science des données | Adobe Experience Platform Intelligence Package uniquement | Module complémentaire Adobe Experience Platform Intelligence plus Advanced Intelligence Pack |
| --- | :---: | :---: |
| Nombre d’utilisateurs de notebook pris en charge. | 5 utilisateurs simultanés | Le premier pack ajoute 5 utilisateurs simultanés et 10 utilisateurs simultanés par package pour les achats supplémentaires. |
| Permet l’intégration de notebooks Jupyter pour l’analyse exploratoire des données et la création de modèles. | X (prend en charge les bibliothèques R, Python et Scala) | X (ajoute les bibliothèques PySpark et Spark ML) |
| Intégration native avec Query Service. Possibilité d’explorer et de façonner des ensembles de données à l’aide de SQL dans des blocs-notes. | X | X |
| Accès aux modèles de notebook prédéfinis pour les analyses prédictives. | X | X |
| Entraînez et notez manuellement les modèles avec les notebooks Jupyter. | X | X |
| Déployez et opérationnalisez des modèles avec la possibilité de planifier des tâches de formation et d’inférence. | | X |
| Cadre de recette pour configurer, évaluer, entraîner, noter et publier facilement des modèles en production. |  | X |
| Expérimentation et évaluation de modèles basés sur l’interface utilisateur. | | X |
| Prise en charge de l’apprentissage profond pour les modèles Tensorflow (GPU Compute). | | X |
| Calcul distribué basé sur Spark pour entraîner et noter des jeux de données volumineux (10 MM + lignes). | | X |

## Contrôle d’accès

Le contrôle d’accès d’Experience Platform est géré à l’aide d’[Adobe Admin Console](https://adminconsole.adobe.com). Cette fonctionnalité exploite les profils de produit dans Admin Console, liant les utilisateurs à des autorisations et des sandbox. Pour plus d’informations, consultez la [présentation du contrôle d’accès](../access-control/home.md).

Pour utiliser Data Science Workspace, l’autorisation &quot;Gérer Data Science Workspace&quot; doit être activée. Le tableau suivant décrit les effets de l’activation ou de la désactivation de cette autorisation :

| Autorisation | Activé | Désactivé |
|---|---|---|
| Gestion de l’espace de travail de science des données | Permet d’accéder à tous les services de l’espace de travail de science des données. | L’accès via l’API et l’interface utilisateur à tous les services dans Data Science Workspace est désactivé. Lorsque cette option est désactivée, la sélection des **pages Blocs-notes**, **Modèles** et **Services** est empêchée. <li>L’accès à **Services** peut toujours être disponible via Adobe Real-Time Customer Data Platform (Real-Time CDP).</li> |

## Prise en charge des sandbox

Les sandbox sont des partitions virtuelles au sein d’une instance unique d’Experience Platform. Chaque instance de Platform prend en charge plusieurs environnements de test de production et hors production, chacun conservant sa propre bibliothèque de ressources de Platform. Les environnements de test hors production vous permettent de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter vos environnements de test de production. Pour plus d’informations sur les sandbox, consultez la [présentation des sandbox](../sandboxes/home.md).

Actuellement, Data Science Workspace présente la limitation d’environnement de test suivante :

- Les ressources de calcul sont partagées dans les environnements de test de production et hors production.

## Étapes suivantes

Ce document décrit les différents types d’accès et les fonctionnalités disponibles dans Data Science Workspace.

Pour en savoir plus sur les Workspace de la science des données, telles qu’un flux de travail quotidien complet, commencez par lire la documentation pas à pas du Workspace](./walkthrough.md) de la [science des données. Pour plus d’informations générales, consultez la page d’aperçu](./home.md) de la Workspace de la [science des données.
