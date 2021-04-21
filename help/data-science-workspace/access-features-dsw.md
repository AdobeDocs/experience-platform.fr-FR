---
keywords: Experience Platform ; accueil ; Espace de travail des sciences de données ; sujets populaires ; contrôle d'accès ; sandbox ; intelligence pack ; fonctionnalités dsw ; dsw access ; Adobe Experience Platform Intelligence ; intelligence ; package de renseignement aep
solution: Experience Platform
title: Accès et fonctionnalités à l’espace de travail Data Science
topic-legacy: Access and features for data science workspace
description: Le document suivant décrit les autorisations de Data Science Workspace et l’accès aux fonctionnalités.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 26%

---

# Accès et fonctionnalités à l’espace de travail Data Science

Le document suivant décrit les autorisations de Data Science Workspace et l’accès aux fonctionnalités.

![Onglets DSW](./images/access/platform-tabs.png)

- **Ordinateurs portables :** fournit un environnement de développement interactif ([JupyterLab](./jupyterlab/overview.md)) pour explorer, analyser et modéliser vos données sur l’Experience Platform.
- **Modèles :** fournit des outils utilisés pour créer, publier et stocker des recettes et des modèles d’apprentissage automatique avancés. Pour plus d&#39;informations, consultez le [didacticiel de création et de publication d&#39;un modèle d&#39;apprentissage automatique](./models-recipes/create-publish-model.md).
- **Services :** contient à la fois des services fournis par l’Adobe, tels que des  [services ](../intelligent-services/home.md) intelligents, et tous les services personnalisés que vous avez créés avec Data Science Workspace.

Pourquoi ne vois-je que l&#39;onglet Services ?

- Votre organisation peut uniquement avoir droit à la plate-forme de données client en temps réel (RTCDP), qui comprend l’API client du service intelligent.

Si vous ne parvenez pas à afficher l&#39;un des onglets **Data Science** et souhaitez utiliser les fonctionnalités de Data Science Workspace, contactez votre administrateur de société pour vérifier si vous disposez d&#39;une licence Adobe Experience Platform Intelligence.

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
| Gestion de Data Science Workspace | Permet d’accéder à tous les services de Data Science Workspace. | L’accès à l’API et à l’interface utilisateur à tous les services de l’espace de travail Data Science est désactivé. Bien que désactivé, la sélection des pages **Notebooks**, **Models** et **Services** est évitée. <li>L&#39;accès aux **services** peut encore être disponible via la plateforme de données client en temps réel (RTCDP).</li> |

## Prise en charge des environnements de test

Les environnements de test sont des partitions virtuelles au sein d’une instance unique d’Experience Platform. Chaque instance de Platform prend en charge un environnement de test de production et plusieurs environnements de test hors production, chacun conservant sa propre bibliothèque de ressources de Platform. Les environnements de test hors production vous permettent de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter votre environnement de test de production. Pour plus d’informations sur les environnements de test, consultez la [présentation des environnements de test](../sandboxes/home.md).

Actuellement, Data Science Workspace présente la limite de sandbox suivante :

- Les ressources de calcul sont partagées entre les environnements de test de production et les environnements de test hors production.

## Étapes suivantes

Ce document décrit les différents types d’accès et fonctionnalités disponibles dans Data Science Workspace.

Pour en savoir plus sur Data Science Workspace, par exemple un flux de travail complet au jour le jour, lisez tout d&#39;abord la documentation [Data Science Workspace. ](./walkthrough.md) Pour obtenir des informations plus générales, consultez la section [Présentation de Data Science Workspace](./home.md).
