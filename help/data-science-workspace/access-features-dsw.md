---
keywords: Experience Platform;home;Data Science Workspace;popular topics;access control;sandbox;intelligence pack;dsw features;dsw access;Adobe Experience Platform Intelligence;intelligence;aep intelligence package
solution: Experience Platform
title: Accès et fonctionnalités à l’espace de travail Data Science
topic: Access and features for data science workspace
description: 'Le document suivant décrit les autorisations de Data Science Workspace et l’accès aux fonctionnalités. '
translation-type: tm+mt
source-git-commit: 40181fc9b1b08c2e21f806caae76b8af0ec9e5e6
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 27%

---


# Accès et fonctionnalités à l’espace de travail Data Science

Le document suivant décrit les autorisations de Data Science Workspace et l’accès aux fonctionnalités.

![Onglets DSW](./images/access/platform-tabs.png)

- **Ordinateurs portables :** Fournit un environnement de développement interactif ([JupyterLab](./jupyterlab/overview.md)) pour explorer, analyser et modéliser vos données sur l’Experience Platform.
- **Modèles :** Fournit des outils utilisés pour créer, publier et stocker des recettes et des modèles d’apprentissage automatique avancés. Pour plus d’informations, consultez le didacticiel [Création et publication d’un modèle](./models-recipes/create-publish-model.md) d’apprentissage automatique.
- **Services :** Contient à la fois des services fournis par l’Adobe tels que [Intelligent Services](../intelligent-services/home.md) et tous les services personnalisés que vous avez créés avec Data Science Workspace.

Pourquoi ne vois-je que l&#39;onglet Services ?

- Votre organisation peut uniquement avoir droit à la plate-forme de données client en temps réel (RTCDP), qui comprend l’API client du service intelligent.

Si vous ne parvenez pas à afficher l’un des onglets **Data Science** et souhaitez utiliser les fonctionnalités de Data Science Workspace, contactez votre administrateur de société pour vérifier si vous disposez d’une licence Adobe Experience Platform Intelligence.

## Ajout du package Adobe Experience Platform Intelligence

Le tableau suivant présente quelques-unes des principales différences entre Data Science Workspace et l’add-on Adobe Experience Platform Intelligence :

>[!NOTE]
>
>Vous pouvez activer la licence de plusieurs modules complémentaires de la solution Intelligence et la capacité accrue est ajoutée à vos droits globaux. Par exemple, si vous avez concédé sous licence 2 ajouts de paquets Adobe Experience Platform Intelligence, vous avez droit à un total de 20 utilisateurs de blocs-notes simultanés.

|  | [!DNL Data Science Workspace] | [!DNL Data Science Workspace] avec l’ajout du package Intelligence |
| --- | :---: | :---: |
| Nombre d&#39;utilisateurs de portables pris en charge. | 5 utilisateurs simultanés | Le premier pack comprend 5 utilisateurs simultanés et les achats supplémentaires 10 utilisateurs simultanés par pack. |
| Permet l&#39;intégration des ordinateurs portables Jupyter pour l&#39;analyse des données exploratoires et la création de modèles (R, Python, Scala, PySpark) | X | X |
| Intégration native avec Requête Service. Possibilité d&#39;explorer et de modeler des jeux de données à l&#39;aide de SQL dans les ordinateurs portables. | X | X |
| Accès à des modèles préconçus de blocs-notes pour les analyses prédictives. | X | X |
| Entraînez et marquez manuellement des modèles à l&#39;aide de portables Jupyter. | X | X |
| Déployer et mettre en oeuvre des modèles qui permettent de planifier des tâches de formation et d&#39;orientation. |  | X |
| Une structure de recettes pour configurer, évaluer, former, marquer et publier facilement des modèles en production. |  | X |
| Expérimentation et évaluation de modèles pilotés par l&#39;interface utilisateur. |  | X |
| Prise en charge de l’apprentissage approfondie des modèles Tensorflow (GPU Compute). |  | X |
| Ordinateur distribué basé sur Spark pour former et marquer des jeux de données volumineux (10 MM + lignes). |  | X |

## Contrôle d’accès

Le contrôle d’accès d’Experience Platform est géré à l’aide d’[Adobe Admin Console](https://adminconsole.adobe.com). Cette fonctionnalité exploite les profils de produit dans Admin Console, liant les utilisateurs à des autorisations et des environnements de test. Pour plus d’informations, consultez la [présentation du contrôle d’accès](../access-control/home.md).

Pour utiliser Data Science Workspace, l’autorisation « Gestion de Data Science Workspace » doit être activée. Le tableau suivant décrit les effets de l’activation ou de la désactivation de cette autorisation :

| Autorisation | Activé | Désactivé |
|---|---|---|
| Gestion de Data Science Workspace | Permet d’accéder à tous les services de Data Science Workspace. | L’accès à l’API et à l’interface utilisateur à tous les services de l’espace de travail Data Science est désactivé. Lorsque cette option est désactivée, la sélection des pages **Ordinateurs portables**, **Modèles** et **Services** n’est pas autorisée. <li>L’accès aux **Services** peut encore être disponible via la plateforme de données client en temps réel (RTCDP).</li> |

## Prise en charge des environnements de test

Les environnements de test sont des partitions virtuelles au sein d’une instance unique d’Experience Platform. Chaque instance de Platform prend en charge un environnement de test de production et plusieurs environnements de test hors production, chacun conservant sa propre bibliothèque de ressources de Platform. Les environnements de test hors production vous permettent de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter votre environnement de test de production. Pour plus d’informations sur les environnements de test, consultez la [présentation des environnements de test](../sandboxes/home.md).

Actuellement, Data Science Workspace présente la limite de sandbox suivante :

- Les ressources de calcul sont partagées entre les environnements de test de production et les environnements de test hors production.

## Étapes suivantes

Ce document décrit les différents types d’accès et fonctionnalités disponibles dans Data Science Workspace.

Pour en savoir plus sur l’espace de travail des sciences de données, par exemple un flux de travail complet au quotidien, lisez tout d’abord la documentation de la Présentation [de l’espace de travail des sciences de](./walkthrough.md) données. For more general information, visit the [Data Science Workspace overview](./home.md).