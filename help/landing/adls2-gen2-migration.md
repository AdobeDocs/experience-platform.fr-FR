---
title: Migration du lac de données vers la version Gen2
description: Découvrez les nouvelles fonctionnalités offertes par la migration du lac de données vers la version Gen2 dans Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Migration du lac de données Adobe Experience Platform vers Gen2

Adobe Experience Platform migre vers le lac de données Gen2. Il s’agit d’une nouvelle génération de lac de données qui offre aux utilisateurs de Platform des avantages tels que la réplication géorégionale, des contrôles d’accès plus précis basés sur les rôles et une meilleure mise à l’échelle.

## Impact de l’utilisateur

Pendant que Adobe migre le lac de données de Gen1 vers Gen 2, les utilisateurs pourront **read** à partir du lac de données, mais **write** dans le lac de données sera affecté. Vous trouverez ci-dessous une liste des fonctionnalités affectées :

- **Sources**: Les données provenant des sources et de divers workflows d’ingestion de données seront retardées. Les utilisateurs verront leurs données une fois la migration terminée.
- **Query Service**: Les utilisateurs peuvent exécuter des requêtes, mais ne pourront pas écrire la sortie de la requête dans un jeu de données.
- **Profil client en temps réel**: Données ingérées dans la banque de profils via **batch** L’ingestion ne sera pas disponible pendant la migration. Cependant, les données ingérées par **diffusion en continu** l’ingestion sera disponible pendant la migration. En outre, les exportations de profils ne seront pas disponibles pendant la migration.
- **Data Science Workspace**: Les écritures de Data Science Workspace échoueront.
- **Segmentation Service**: Audiences dérivées de **batch** la segmentation ne peut pas être activée lors de la migration. Audiences dérivées de **diffusion en continu** la segmentation ne sera pas affectée.
- **Customer Journey Analytics**: Les données des rapports Customer Journey Analytics peuvent être obsolètes et ne s’actualiseront pas lors de la migration, car les lots ne sont pas ingérés dans le lac de données.

## Communication avec les utilisateurs de Platform

Adobe contactera les administrateurs système pour discuter en détail de l’impact de la migration et confirmer les dates et heures de migration pour certaines organisations IMS.
