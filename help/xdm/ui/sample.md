---
solution: Experience Platform
title: Génération de données d’exemple pour un schéma XDM dans l’interface utilisateur
description: Découvrez comment générer des exemples de données JSON en fonction d’un schéma existant dans l’interface utilisateur de Adobe Experience Platform.
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 14%

---

# Générer des données d’exemple pour un schéma XDM dans l’interface d’utilisation {#generate-sample-data-for-an-xdm-schema}

>[!CONTEXTUALHELP]
>id="platform_xdm_downloadsamplefile"
>title="Télécharger le fichier d’exemple"
>abstract="Générez un exemple d’objet JSON conforme à la structure du schéma de votre choix. Cet objet peut servir de modèle pour vous assurer que vos données sont correctement formatées pour l’ingestion dans les jeux de données qui utilisent ce schéma. L’exemple de fichier JSON sera téléchargé par votre navigateur."

Pour ingérer des données dans Adobe Experience Platform, leur format et structure doivent être conformes à un schéma de modèle de données d’expérience (XDM) existant. En fonction de la complexité du schéma pour un jeu de données spécifique, il peut être difficile de déterminer la forme exacte des données attendues par le jeu de données lors de l’ingestion.

Pour tout schéma que vous définissez dans l’interface utilisateur d’Experience Platform, vous pouvez générer un exemple d’objet JSON conforme à la structure du schéma. Cet objet peut servir de modèle pour toutes les données ingérées dans les jeux de données qui utilisent le schéma en question.

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche. Sous l’onglet **[!UICONTROL Parcourir]**, recherchez le schéma pour lequel vous souhaitez générer des données d’exemple. Sélectionnez-le dans la liste, et le rail de droite se met à jour pour afficher les détails du schéma. À partir de là, sélectionnez **[!UICONTROL Télécharger l’exemple de fichier]**.

![Onglet Parcourir de l’espace de travail Schémas avec un schéma sélectionné et un exemple de fichier de téléchargement en surbrillance.](../images/ui/sample/sample-data.png)

Un exemple de fichier JSON est téléchargé par le navigateur. Vous pouvez désormais utiliser ce fichier comme référence pour savoir comment structurer vos données lors de l’ingestion dans des jeux de données qui utilisent ce schéma.

## Étapes suivantes

Ce guide explique comment générer un exemple de fichier JSON à partir d’un schéma XDM dans l’interface utilisateur d’Experience Platform. Pour savoir comment générer des exemples de données à l’aide de l’API Schema Registry, consultez le guide [exemple de point d’entrée de données](../api/sample-data.md).

Une fois que vous êtes prêt à commencer à ingérer des données, consultez le tutoriel sur [le mappage d’un fichier CSV à XDM](../../ingestion/tutorials/map-csv/overview.md) pour savoir comment mapper un fichier de données plat (un fichier CSV, par exemple) à un schéma XDM et l’ingérer dans Experience Platform. Vous pouvez également établir une [connexion source](../../sources/home.md) pour importer vos données d’une source externe et les mapper à XDM.

Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schémas] dans l’interface utilisateur, consultez la présentation de l’espace de travail [[!UICONTROL Schémas]](./overview.md).
