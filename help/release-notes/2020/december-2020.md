---
title: Notes De Mise À Jour De Adobe Experience Platform - Décembre 2020
description: Les notes de mise à jour de décembre 2020 pour Adobe Experience Platform.
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 29%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : jeudi 9 décembre 2020**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [[!DNL Dataflows]](#dataflows)

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

Les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Experience Platform. Ces flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers des jeux de données cibles, vers le service d’identités et de profils, et vers des destinations.

**Fonction clé**

| Fonctionnalité | Description |
| ------- | ----------- |
| Transparence des flux de données | Vous pouvez surveiller les flux de données pour les sources et les destinations. Pour plus d’informations, veuillez lire le [tutoriel sur la surveillance des sources](../../dataflows/ui/monitor-sources.md) ou le [tutoriel sur la surveillance des destinations](../../dataflows/ui/monitor-destinations.md). |

Pour en savoir plus sur les flux de données, consultez la [présentation des flux de données](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

L’espace de travail de science des données utilise le machine learning et l’intelligence artificielle pour exploiter les informations contenues dans vos données. Intégré à Adobe Experience Platform, l’espace de travail de science des données vous aide à obtenir des prévisions en utilisant votre contenu et des ressources de données de l’ensemble des solutions Adobe.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| --- | ---|
| Module complémentaire du package Intelligence de Adobe Experience Platform | Le module complémentaire de package d’intelligence de Adobe Experience Platform est une mise à niveau du Workspace de science des données qui déverrouille d’autres fonctionnalités essentielles, telles que : <li> Expérimentation et évaluation de modèles pilotés par l’interface utilisateur.</li><li> Possibilité de déployer et de rendre opérationnels des modèles avec des tâches de formation et d’inférence planifiées.</li><li> Prise en charge du deep learning dans les modèles Tensorflow (GPU Compute).</li><li> Calcul distribué basé sur Spark pour entraîner et noter des jeux de données volumineux (10 MM + lignes).</li><li>Et en plus</li> |

Pour en savoir plus sur l’addon du package Intelligence de Adobe Experience Platform, consultez la documentation sur [l’accès et les fonctionnalités de Workspace en science des données](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Experience Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mettre à jour les détails du compte et de la connexion pour les sources en flux continu | Vous pouvez désormais mettre à jour les noms, descriptions et informations d’identification des connexions en continu existantes à l’aide de l’API [!DNL Flow Service] et de l’interface utilisateur. Pour plus d’informations, consultez le tutoriel sur [la mise à jour des connexions à l’aide de l’API](../../sources/tutorials/api/update.md) et [ la modification des détails du compte à l’aide de l’interface utilisateur](../../sources/tutorials/ui/monitor.md). |
| Supprimer des flux de données | Les flux de données en continu qui contiennent des erreurs ou sont devenus inutiles peuvent désormais être supprimés à l’aide de l’API [!DNL Flow Service] et de l’interface utilisateur. Pour plus d’informations, consultez le tutoriel sur [la suppression de flux de données à l’aide de l’API](../../sources/tutorials/api/delete-dataflows.md) et [la suppression de flux de données à l’aide de l’interface utilisateur](../../sources/tutorials/ui/delete.md). |

Pour en savoir plus sur les sources, consultez la [vue d’ensemble des sources](../../sources/home.md).
