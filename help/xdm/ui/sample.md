---
solution: Experience Platform
title: Génération d’exemples de données pour un schéma XDM dans l’interface utilisateur
description: Découvrez comment générer des exemples de données JSON en fonction d’un schéma existant dans l’interface utilisateur de Adobe Experience Platform.
topic-legacy: user guide
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Génération d’exemples de données pour un schéma XDM dans l’interface utilisateur

Pour ingérer des données dans Adobe Experience Platform, le format et la structure des données doivent respecter un schéma de modèle de données d’expérience (XDM) existant. Selon la complexité du schéma pour un jeu de données spécifique, il peut être difficile de déterminer la forme exacte des données attendues par le jeu de données lors de l’ingestion.

Pour tout schéma que vous définissez dans l’interface utilisateur de l’Experience Platform, vous pouvez générer un exemple d’objet JSON conforme à la structure du schéma. Cet objet peut servir de modèle pour toute donnée ingérée dans des jeux de données qui utilisent le schéma en question.

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche. Sous l’onglet **[!UICONTROL Parcourir]** , localisez le schéma pour lequel vous souhaitez générer des données d’exemple. Sélectionnez-la dans la liste et le rail de droite se met à jour pour afficher des détails sur le schéma. À partir de là, sélectionnez **[!UICONTROL Télécharger le fichier d’exemple]**.

![](../images/ui/sample/sample-data.png)

Un exemple de fichier JSON est téléchargé par le navigateur. Vous pouvez désormais utiliser ce fichier comme référence pour structurer vos données lors de l’ingestion dans des jeux de données qui utilisent ce schéma.

## Étapes suivantes

Ce guide explique comment générer un exemple de fichier JSON à partir d’un schéma XDM dans l’interface utilisateur de Platform. Pour savoir comment générer des données d’exemple à l’aide de l’API Schema Registry, consultez le [guide d’exemple de point de terminaison de données](../api/sample-data.md).

Une fois que vous êtes prêt à commencer à ingérer des données, consultez le tutoriel sur le [mappage d’un fichier CSV à XDM](../../ingestion/tutorials/map-a-csv-file.md) pour savoir comment mapper un fichier de données plat (tel qu’un fichier CSV) à un schéma XDM et l’ingérer dans Platform. Vous pouvez également établir une [connexion source](../../sources/home.md) pour importer vos données d’une source externe et les mapper à XDM.

Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schémas] dans l’interface utilisateur, reportez-vous à la [[!UICONTROL Présentation des schémas] de l’espace de travail](./overview.md).
