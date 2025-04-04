---
keywords: Experience Platform;accueil;Workspace de science des données;rubriques populaires;contrôle d’accès;sandbox;pack d’intelligence;fonctionnalités dsw;accès dsw;Intelligence Adobe Experience Platform;intelligence;package d’intelligence aep
solution: Experience Platform
title: Accès au Workspace de science des données et fonctionnalités
description: Le document suivant décrit les autorisations du Workspace de science des données et l’accès aux fonctionnalités.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 15%

---

# Accès à l’espace de travail de science des données et fonctionnalités associées

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

Le document suivant décrit les autorisations du Workspace de science des données et l’accès aux fonctionnalités.

![Onglets DSW](./images/access/platform-tabs.png)

- **Notebooks :** fournit un environnement de développement interactif ([JupyterLab](./jupyterlab/overview.md)) pour explorer, analyser et modéliser vos données sur Experience Platform.
- **Modèles :** fournit des outils utilisés pour créer, publier et stocker des recettes et des modèles de machine learning avancés. Pour plus d’informations, consultez le tutoriel [créer et publier un modèle de machine learning](./models-recipes/create-publish-model.md).
- **Services :** contient à la fois les services fournis par Adobe, tels que les services [AI/ML](../intelligent-services/home.md) et les services personnalisés que vous avez créés avec le Workspace de science des données.

Pourquoi est-ce que je ne vois que l’onglet Services ?

- Votre organisation peut uniquement être autorisée à accéder à Adobe Real-Time Customer Data Platform (Real-Time CDP) qui inclut le service IA dédiée aux clients/ML.

Si aucun des onglets **Science des données** ne s’affiche et que vous souhaitez utiliser les fonctionnalités de Workspace de science des données, contactez l’administrateur ou l’administratrice de votre société pour vérifier si vous disposez d’une licence Adobe Experience Platform Intelligence.

## Package Workspace de science des données

Les fonctionnalités de Workspace de science des données sont disponibles dans le package d’intelligence de Adobe Experience Platform et le module complémentaire de pack d’intelligence avancée

Le tableau suivant présente certaines des principales différences entre les droits d’accès aux Workspace de science des données avec et sans le module complémentaire du pack d’intelligence avancée :

>[!NOTE]
>
>Vous pouvez acquérir plusieurs licences pour le module complémentaire de pack d’intelligence avancé et la capacité accrue sera ajoutée à vos droits globaux. Par exemple, si vous disposez d’une licence pour 2 compléments Adobe Experience Platform Advanced Intelligence Pack, vous avez droit à un total de 20 utilisateurs de Notebook simultanés.

| Droits du Workspace de science des données | Package d’intelligence Adobe Experience Platform uniquement | Module complémentaire Adobe Experience Platform Intelligence plus Advanced Intelligence Pack |
| --- | :---: | :---: |
| Nombre d&#39;utilisateurs Notebook pris en charge. | 5 utilisateurs simultanés | Le premier pack ajoute 5 utilisateurs simultanés et les achats supplémentaires ajoutent 10 utilisateurs simultanés par package. |
| Permet les notebooks Jupyter intégrés pour l’analyse exploratoire des données et la création de modèles. | X (prend en charge les bibliothèques R, Python et Scala) | X (ajoute les bibliothèques PySpark et Spark ML) |
| Intégration native à Query Service. Possibilité d’explorer et de mettre en forme des jeux de données à l’aide de SQL dans les notebooks. | X | X |
| Accès aux modèles de notebooks préconfigurés pour l’analyse prédictive. | X | X |
| Entraînez et notez manuellement des modèles avec les notebooks Jupyter. | X | X |
| Déployer et opérationnaliser des modèles avec la possibilité de planifier des formations et d’inférer des traitements. | | X |
| Framework de recette permettant de configurer, d’évaluer, de former, de noter et de publier facilement des modèles en production. |  | X |
| Expérimentation et évaluation de modèles pilotés par l’interface utilisateur. | | X |
| Prise en charge de l’apprentissage profond pour les modèles Tensorflow (GPU Compute). | | X |
| Calcul distribué basé sur Spark pour entraîner et noter des jeux de données volumineux (10 MM + lignes). | | X |

## Contrôle d’accès

Le contrôle d’accès d’Experience Platform est géré à l’aide d’[Adobe Admin Console](https://adminconsole.adobe.com). Cette fonctionnalité exploite les profils de produit dans Admin Console, liant les utilisateurs à des autorisations et des sandbox. Pour plus d’informations, consultez la [présentation du contrôle d’accès](../access-control/home.md).

Pour utiliser le Workspace de science des données, l’autorisation « Gérer le Workspace de science des données » doit être activée. Le tableau suivant décrit les effets de l’activation ou de la désactivation de cette autorisation :

| Autorisation | Activé | Désactivé |
|---|---|---|
| Gestion de l’espace de travail de science des données | Permet d’accéder à tous les services de l’espace de travail de science des données. | L’accès aux API et aux interfaces utilisateur de tous les services dans le Workspace de science des données est désactivé. Lorsque cette option est désactivée, il est impossible de sélectionner les pages **Notebooks**, **Modèles** et **Services**. <li>L’accès à **Services** peut toujours être disponible via Adobe Real-Time Customer Data Platform (Real-Time CDP).</li> |

## Prise en charge des sandbox

Les sandbox sont des partitions virtuelles au sein d’une instance unique d’Experience Platform. Chaque instance Experience Platform prend en charge plusieurs sandbox de production et hors production, chacun conservant sa propre bibliothèque de ressources Experience Platform. Les sandbox hors production vous permettent de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter vos sandbox de production. Pour plus d’informations sur les sandbox, consultez la [présentation des sandbox](../sandboxes/home.md).

Actuellement, le Workspace de science des données présente la limite de sandbox suivante :

- Les ressources de calcul sont partagées dans les sandbox de production et hors production.

## Étapes suivantes

Ce document décrit les différents types d’accès et de fonctionnalités disponibles dans le Workspace de science des données.

Pour en savoir plus sur le Workspace de science des données, tel qu’un workflow complet au jour le jour, commencez par lire la documentation de la [présentation du Workspace de science des données](./walkthrough.md). Pour des informations plus générales, consultez la [présentation de Data Science Workspace](./home.md).
