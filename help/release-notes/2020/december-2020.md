---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour d’Experience Platform, 9 décembre 2020
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 39%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 9 décembre 2020**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [[!DNL Dataflows]](#dataflows)

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

Les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Platform. Ces flux de données sont configurés sur différents services, ce qui permet de déplacer des données des connecteurs sources vers des jeux de données cibles, vers Identity Service et Profile Service, ainsi que vers des destinations.

**Fonctionnalité clé**

| Fonctionnalité | Description |
| ------- | ----------- |
| Transparence des flux de données | Vous pouvez surveiller les flux de données pour les sources et les destinations. Pour plus d’informations, consultez le [tutoriel sur les sources de surveillance](../../dataflows/ui/monitor-sources.md) ou le [tutoriel sur les destinations de surveillance](../../dataflows/ui/monitor-destinations.md). |

Pour en savoir plus sur les flux de données, consultez la [présentation des flux de données](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utilise le machine learning et l’intelligence artificielle pour exploiter les informations contenues dans vos données. Intégré à Adobe Experience Platform, Data Science Workspace vous aide à obtenir des prévisions en utilisant votre contenu et des ressources de données de l’ensemble des solutions Adobe.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| --- | ---|
| Module complémentaire Adobe Experience Platform Intelligence | Le module complémentaire Adobe Experience Platform Intelligence est une mise à niveau de Data Science Workspace qui libère des fonctionnalités clés supplémentaires telles que : <li> Expérience et évaluation de modèles pilotés par l’interface utilisateur.</li><li> Possibilité de déployer et de mettre en oeuvre des modèles avec une formation planifiée et des tâches de référencement.</li><li> Prise en charge de l’apprentissage profond dans les modèles Tensorflow (GPU Compute).</li><li> Ordinateur distribué basé sur Spark pour entraîner et noter des jeux de données volumineux (10 MM + lignes).</li><li>Plus</li> |

Pour en savoir plus sur le module complémentaire Adobe Experience Platform Intelligence, consultez la documentation sur [Data Science Workspace access and features](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mise à jour des détails de compte et de connexion pour les sources de diffusion en continu | Vous pouvez désormais mettre à jour les noms, descriptions et informations d’identification des connexions en continu existantes à l’aide de l’API [!DNL Flow Service] et de l’interface utilisateur. Pour plus d’informations, consultez le tutoriel sur la [mise à jour des connexions à l’aide de l’API](../../sources/tutorials/api/update.md) et la [modification des détails du compte à l’aide de l’interface utilisateur](../../sources/tutorials/ui/monitor.md). |
| Suppression de flux de données | Les flux de données en flux continu contenant des erreurs ou devenus inutiles peuvent désormais être supprimés à l’aide de l’API [!DNL Flow Service] et de l’interface utilisateur. Pour plus d’informations, consultez le tutoriel sur la [suppression des flux de données à l’aide de l’API](../../sources/tutorials/api/delete-dataflows.md) et la [suppression des flux de données à l’aide de l’interface utilisateur](../../sources/tutorials/ui/delete.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
