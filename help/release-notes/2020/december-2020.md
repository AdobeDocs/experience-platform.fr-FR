---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour d’Experience Platform, 9 décembre 2020
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
translation-type: tm+mt
source-git-commit: ae353e6dda3f92647c32ee8e731be5785d24e5cb
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 35%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 9 décembre 2020**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [[!DNL Dataflows]](#dataflows)

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

Les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Platform. Ces flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs source vers les jeux de données de cible, vers Identity et Profil Service, ainsi que vers les destinations.

**Fonctionnalité clé**

| Fonctionnalité | Description |
| ------- | ----------- |
| Transparence des flux de données | Vous pouvez surveiller les flux de données pour les sources et les destinations. Pour plus d&#39;informations, veuillez lire le [tutoriel sur les sources de surveillance](../../dataflows/ui/monitor-sources.md) ou le [tutoriel sur les destinations de surveillance](../../dataflows/ui/monitor-destinations.md). |

Pour en savoir plus sur les flux de données, veuillez lire la [présentation des flux de données](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utilise l’apprentissage automatique et l’intelligence artificielle pour créer des informations à partir de vos données. Intégré à Adobe Experience Platform, Data Science Workspace vous aide à obtenir des prévisions en utilisant votre contenu et des ressources de données de l’ensemble des solutions Adobe.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| --- | ---|
| Ajout du package Adobe Experience Platform Intelligence | Le module complémentaire Adobe Experience Platform Intelligence est une mise à niveau de Data Science Workspace qui déverrouille d’autres fonctionnalités clés telles que : <li> Expérimentation et évaluation de modèles pilotés par l&#39;interface utilisateur.</li><li> Capacité à déployer et à mettre en oeuvre des modèles avec des formations planifiées et des tâches d&#39;infériorité.</li><li> Prise en charge de l&#39;apprentissage profond dans les modèles Tensorflow (GPU Compute).</li><li> Ordinateur distribué basé sur Spark pour former et marquer des jeux de données volumineux (10 MM + lignes).</li><li>Et plus</li> |

Pour en savoir plus sur l&#39;ajout de paquets Adobe Experience Platform Intelligence, consultez la documentation sur [Data Science Workspace access and features](../../data-science-workspace/access-features-dsw.md) (Accès et fonctionnalités de Data Science Workspace).

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mettre à jour les détails de compte et de connexion pour les sources de flux continu | Vous pouvez désormais mettre à jour les noms, descriptions et informations d’identification des connexions de flux continu existantes à l’aide de l’API [!DNL Flow Service] et de l’interface utilisateur. Pour plus d&#39;informations, consultez le didacticiel sur la mise à jour des connexions à l&#39;aide de l&#39;API](../../sources/tutorials/api/update.md) et de [modification des détails du compte à l&#39;aide de l&#39;interface utilisateur](../../sources/tutorials/ui/monitor.md).[ |
| Supprimer des flux de données | Les flux de données en flux continu contenant des erreurs ou devenus inutiles peuvent maintenant être supprimés à l’aide de l’API [!DNL Flow Service] et de l’interface utilisateur. Pour plus d&#39;informations, consultez le didacticiel sur la suppression des flux de données à l&#39;aide de l&#39;API](../../sources/tutorials/api/delete-dataflows.md) et [suppression des flux de données à l&#39;aide de l&#39;interface utilisateur](../../sources/tutorials/ui/delete.md).[ |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).


