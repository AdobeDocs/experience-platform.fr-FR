---
title: Notes de mise à jour d’Adobe Experience Platform - Février 2021
description: Notes de mise à jour de février 2021 pour Adobe Experience Platform.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 90%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de mise à jour : 24 février 2021**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [Tableaux de bord (Beta)](#dashboards)

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Tableaux de bord (Beta) {#dashboards}

Adobe Experience Platform fournit de nombreux tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre entreprise, telles quʼelles sont capturées lors dʼinstantanés quotidiens.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Tableaux de bord relatifs aux profils, aux segments, aux destinations et à l’utilisation des licences (Beta) | **Remarque : la fonctionnalité Tableaux de bord est actuellement en version Beta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.**<br/><br/> Les tableaux de bord proposent un compte rendu des performances prêt à l’emploi sur les données de votre organisation. Ils sont directement intégrés au workflow du spécialiste marketing dans Experience Platform. La mise à disposition de ces tableaux de bord ne nécessite pas d’assistance informatique supplémentaire. En outre, ils offrent un gain de temps et d’effort en évitant de recourir à l’exportation et au traitement des données avec une conception et une implémentation d’entreposage de données supplémentaires. |

## [!DNL Data Science Workspace] {#dsw}

L’espace de travail de science des données utilise le machine learning et l’intelligence artificielle pour exploiter les informations contenues dans vos données. Intégré à Adobe Experience Platform, l’espace de travail de science des données vous aide à obtenir des prévisions en utilisant votre contenu et des ressources de données de l’ensemble des solutions Adobe.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Notebook AED JupyterLab | Le notebook Python d’analyse exploratoire des données (AED) est désormais disponible dans Jupyterlab. Ce notebook est conçu pour vous aider à découvrir des modèles au sein des données, à vérifier l’intégrité de ces dernières et à faire la synthèse des données pertinentes pour les modèles prédictifs. Pour plus d’informations, consultez le tutoriel consacré à l’[exploration des données web pour les modèles prédictifs](../../data-science-workspace/jupyterlab/eda-notebook.md). |

Pour plus d’informations sur l’espace de travail de science des données, consultez la [Présentation de l’espace de travail de science des données](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

Dans Adobe Experience Platform, les données sont ingérées à partir d’une grande variété de sources, analysées dans Experience Platform et activées vers un grand nombre de destinations. Experience Platform facilite le processus de suivi de ce flux de données potentiellement non linéaire en offrant de la transparence aux flux de données.

Les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Experience Platform. Ces flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers des jeux de données cibles, où elles sont ensuite utilisées par le [!DNL Identity Service] et le [!DNL Real-Time Customer Profile] avant d’être finalement activées vers les [!DNL Destinations].

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Nouveau tableau de bord de surveillance | Vous pouvez désormais utiliser le tableau de bord de surveillance pour bénéficier d’une transparence entre services et obtenir des informations exploitables pour les ingestions de données sources. Le nouveau tableau de bord de surveillance fournit une vue complète des données traitées de [!DNL Data Lake] au [!DNL Identity Service] et au [!DNL Profile], tout en vous permettant de surveiller les taux d’ingestion, les succès et les échecs. Pour plus d’informations, consultez le tutoriel consacré à la [surveillance des flux de données sources dans l’interface utilisateur](../../dataflows/ui/monitor-sources.md). |

Pour des informations plus générales sur les flux de données, reportez-vous à la [présentation des flux de données](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations**

| Destination | Description |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | La connexion [!DNL LinkedIn Matched Audiences] vous permet d’activer des audiences dans la plateforme sociale [!DNL LinkedIn]. |

Pour des informations plus générales sur les destinations, reportez-vous à la [présentation des destinations](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

La normalisation et l’interopérabilité sont des concepts clés pour [!DNL Experience Platform]. Le modèle de données [!DNL Experience Data Model] d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences digitales. Elle fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Mise à niveau de l’interface utilisateur de recherche | Les fonctionnalités de recherche améliorées sont désormais disponibles dans l’onglet [!UICONTROL Parcourir] de l’espace de travail [!UICONTROL Schémas] et dans la boîte de dialogue de sélection des groupes de champs de schémas dans le [!DNL Schema Editor].<br><br>Précédemment, lors d’une recherche de terme, les résultats n’incluaient que les ressources XDM dont le nom correspondait à la requête. Désormais, outre les ressources dont le nom correspond à la requête, les ressources contenant des attributs individuels qui correspondent au terme sont également incluses. Cela vous permet de rechercher des ressources XDM en fonction des attributs qu’elles contiennent plutôt que par le biais de leur nom.<br><br>Pour plus d’informations, consultez les documents sur l’[exploration des ressources XDM](../../xdm/ui/explore.md) et ceux sur la [gestion des schémas](../../xdm/ui/resources/schemas.md) dans l’interface utilisateur. |

Pour des informations plus générales sur XDM, reportez-vous à la [présentation du système XDM](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

Proposer des expériences digitales pertinentes nécessite une compréhension complète de votre client. Cela devient plus difficile lorsque les données de vos clients sont fragmentées entre plusieurs systèmes, chaque client semble donc posséder plusieurs « identités ».

Adobe Experience Platform [!DNL Identity Service] vous permet de mieux connaître vos clients et leurs comportements, en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences digitales personnelles et percutantes en temps réel.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Visionneuse de graphiques d’identités | L’observateur de graphique d’identités vous permet de valider et de visualiser les identités assemblées dans l’interface utilisateur, ce qui permet d’améliorer le débogage et la transparence. Pour plus d’informations, consultez le [document sur l’observateur de graphique d’identités](../../identity-service/features/identity-graph-viewer.md). |

Pour des informations plus générales sur le [!DNL Identity Service], reportez-vous à la [présentation du service d’identités](../../identity-service/home.md).

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Le profil client en temps réel offre une vue holistique de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le [!DNL Profile] vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Attributs calculés (Alpha) | ***Remarque : cette fonctionnalité est actuellement en version Alpha et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.*** <br/><br/>Les attributs calculés sont des fonctions utilisées pour regrouper des données au niveau de l’événement en attributs au niveau du profil. Vous pouvez ensuite utiliser les agrégats dans la segmentation, l’activation et la personnalisation. Ces fonctions incluent notamment le nombre, la somme, la moyenne, les valeurs min. et max. ou encore la valeur vrai/faux. Les attributs calculés sont actuellement disponibles uniquement via l’API. |

Pour plus d’informations sur le profil client en temps réel, notamment les bonnes pratiques et les tutoriels relatifs à l’utilisation des données [!DNL Profile], consultez tout d’abord la [ présentation du profil client en temps réel](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles sources**

| Fonctionnalité | Description |
| --- | --- |
| [!DNL Google PubSub] | Vous pouvez désormais connecter [!DNL Google PubSub] à [!DNL Experience Platform] à l’aide de l’interface utilisateur ou de l’API [!DNL Flow Service]. Pour plus d’informations, consultez la présentation du connecteur [[!DNL Google PubSub] ](../../sources/connectors/cloud-storage/google-pubsub.md). |
| [!DNL Oracle Object Storage] | Vous pouvez désormais connecter [!DNL Oracle Object Storage] à [!DNL Experience Platform] à l’aide de l’interface utilisateur ou de l’API [!DNL Flow Service]. Pour plus d’informations, consultez la présentation du connecteur [[!DNL Oracle Object Storage] ](../../sources/connectors/cloud-storage/oracle-object-storage.md). |

Pour des informations plus générales sur les sources, reportez-vous à la [présentation des sources](../../sources/home.md).
