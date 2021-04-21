---
solution: Experience Platform
title: Générer des exemples de données pour un Schéma XDM dans l’interface utilisateur
description: Découvrez comment générer des données JSON d’exemple en fonction d’un schéma existant dans l’interface utilisateur de Adobe Experience Platform.
topic-legacy: user guide
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Générer des données d’exemple pour un schéma XDM dans l’interface utilisateur

Pour importer des données dans Adobe Experience Platform, le format et la structure des données doivent respecter un schéma de modèle de données d’expérience (XDM) existant. En fonction de la complexité du schéma d&#39;un jeu de données particulier, il peut s&#39;avérer difficile de déterminer la forme exacte des données attendues par le jeu lors de l&#39;assimilation.

Pour tout schéma défini dans l’interface utilisateur de l’Experience Platform, vous pouvez générer un exemple d’objet JSON conforme à la structure du schéma. Cet objet peut servir de modèle pour toute donnée ingérée dans des jeux de données qui utilisent le schéma en question.

Dans l’interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche. Sous l&#39;onglet **[!UICONTROL Parcourir]**, recherchez le schéma pour lequel vous souhaitez générer des données d&#39;exemple. Sélectionnez-la dans la liste et les mises à jour du rail de droite pour afficher des détails sur le schéma. À partir de là, sélectionnez **[!UICONTROL Télécharger le fichier exemple]**.

![](../images/ui/sample/sample-data.png)

Un exemple de fichier JSON est téléchargé par le navigateur. Vous pouvez désormais utiliser ce fichier comme référence pour structurer vos données lors de l&#39;assimilation dans des jeux de données qui utilisent ce schéma.

## Étapes suivantes

Ce guide explique comment générer un exemple de fichier JSON à partir d’un schéma XDM dans l’interface utilisateur de la plate-forme. Pour savoir comment générer des données d’exemple à l’aide de l’API de registre de Schéma, consultez le [guide du point de terminaison des données d’exemple](../api/sample-data.md).

Une fois que vous êtes prêt à début de l’assimilation de données, consultez le didacticiel sur le [mappage d’un fichier CSV à XDM](../../ingestion/tutorials/map-a-csv-file.md) pour savoir comment mapper un fichier de données plat (tel qu’un CSV) à un schéma XDM et l’intégrer dans la plate-forme. Vous pouvez également établir une connexion [source](../../sources/home.md) pour importer vos données d&#39;une source externe et les mapper à XDM.

Pour plus d&#39;informations sur les fonctionnalités de l&#39;espace de travail [!UICONTROL Schémas] dans l&#39;interface utilisateur, consultez la section [[!UICONTROL Présentation de l&#39;espace de travail ] Schémas](./overview.md).
