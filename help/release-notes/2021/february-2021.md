---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour de l’Experience Platform pour le 24 février 2021.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: 7142d13b144f34d92087affe101c5ccfcb52d90e
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 36%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 24 février 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utilise l’apprentissage automatique et l’intelligence artificielle pour créer des informations à partir de vos données. Intégré à Adobe Experience Platform, Data Science Workspace vous aide à obtenir des prévisions en utilisant votre contenu et des ressources de données de l’ensemble des solutions Adobe.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Ordinateur portable JupyterLab EDA | Le bloc-notes Python de l&#39;analyse de données exploratoires (EDA) est maintenant disponible en Jupyterlab. Ce bloc-notes est conçu pour vous aider à découvrir des schémas dans les données, à vérifier l&#39;intégrité des données et à résumer les données pertinentes pour les modèles prédictifs. Pour plus d&#39;informations, consultez le didacticiel [consacré à l&#39;exploration des données Web pour les modèles prédictifs](../../data-science-workspace/jupyterlab/eda-notebook.md). |

Pour plus d’informations sur l’Espace de travail des sciences de données, consultez l’[Présentation de l’Espace de travail des sciences de données](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

Au Adobe Experience Platform, les données sont ingérées à partir d&#39;une grande variété de sources, analysées dans l&#39;Experience Platform et activées vers une grande variété de destinations. La plate-forme facilite le processus de suivi de ce flux de données potentiellement non linéaire en fournissant de la transparence avec les flux de données.

Les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Platform. Ces flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers des jeux de données de cible, où elles sont ensuite utilisées par [!DNL Identity Service] et [!DNL Real-time Customer Profile] avant d&#39;être finalement activées sur [!DNL Destinations].

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Nouveau tableau de bord de surveillance | Vous pouvez désormais utiliser le tableau de bord de surveillance pour une transparence entre services et des informations exploitables pour les ingérations de données source. Le nouveau tableau de bord de surveillance fournit une vue complète des données traitées de [!DNL Data Lake] à [!DNL Identity Service] et à [!DNL Profile], tout en vous permettant de surveiller les taux d&#39;assimilation, les réussites et les échecs. Pour plus d’informations, consultez le didacticiel sur [la surveillance des flux de données source dans l’interface utilisateur](../../dataflows/ui/monitor-sources.md). |

Pour des informations plus générales sur les flux de données, consultez l&#39;[aperçu des flux de données](../../dataflows/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

La normalisation et l&#39;interopérabilité sont les concepts clés qui sous-tendent [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), piloté par l’Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Elle fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Interface utilisateur de recherche mise à niveau | Les fonctionnalités de recherche améliorées sont désormais disponibles dans l&#39;onglet [!UICONTROL Parcourir] de l&#39;espace de travail [!UICONTROL Schémas] et dans la boîte de dialogue de sélection de mixin de [!DNL Schema Editor].<br><br>Lors de la recherche d’un terme précédemment, les résultats incluent uniquement les ressources XDM dont le nom correspond à la requête de recherche. Désormais, outre les ressources dont le nom correspond à la requête, les ressources contenant des attributs individuels qui correspondent au terme seront également incluses. Cela vous permet de rechercher des ressources XDM en fonction des attributs qu&#39;elles contiennent plutôt que par nom de ressource.<br><br>Pour plus d’informations, consultez les documents sur l’ [exploration des ](../../xdm/ui/explore.md) ressources XDM et la  [gestion des ](../../xdm/ui/resources/schemas.md) schémas dans l’interface utilisateur. |

Pour plus d&#39;informations sur XDM, consultez la section [Présentation du système XDM](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

Proposer des expériences numériques pertinentes nécessite une compréhension complète de votre client. Cela devient plus difficile lorsque les données de vos clients sont fragmentées entre plusieurs systèmes, chaque client semble donc posséder plusieurs « identités ».

Adobe Experience Platform [!DNL Identity Service] vous aide à mieux vue de votre client et de son comportement en rapprochant les identités entre les périphériques et les systèmes, ce qui vous permet de fournir des expériences numériques personnelles et impactées en temps réel.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Graphique d’identités lecteur | La visionneuse de graphiques d’identité vous permet de valider et de visualiser les identités assemblées ensemble dans l’interface utilisateur, ce qui permet d’améliorer le débogage et la transparence. Pour plus d&#39;informations, consultez le [document du lecteur de graphique d&#39;identité](../../identity-service/ui/identity-graph-viewer.md). |

Pour plus d&#39;informations générales sur [!DNL Identity Service], consultez la [Présentation du service d&#39;identité](../../identity-service/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles sources**

| Fonctionnalité | Description |
| --- | --- |
| [!DNL Google PubSub] | Vous pouvez désormais vous connecter à [!DNL Google PubSub] à [!DNL Experience Platform] à l&#39;aide de l&#39;API [!DNL Flow Service] ou de l&#39;interface utilisateur. Pour plus d&#39;informations, consultez l&#39;[[!DNL Google PubSub] aperçu du connecteur](../../sources/connectors/cloud-storage/google-pubsub.md). |
| [!DNL Oracle Object Storage] | Vous pouvez désormais vous connecter à [!DNL Oracle Object Storage] à [!DNL Experience Platform] à l&#39;aide de l&#39;API [!DNL Flow Service] ou de l&#39;interface utilisateur. Pour plus d&#39;informations, consultez l&#39;[[!DNL Oracle Object Storage] aperçu du connecteur](../../sources/connectors/cloud-storage/oracle-object-storage.md). |

Pour plus d&#39;informations générales sur les sources, consultez l&#39;[aperçu des sources](../../sources/home.md).
