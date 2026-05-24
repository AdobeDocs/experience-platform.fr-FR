---
title: Migration du lac de données vers Gen2
description: Découvrez les nouvelles fonctionnalités offertes par la migration du lac de données vers Gen2 dans Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
TQID: https://experienceleague.adobe.com/aIxIYwMSLKe28qlQfZucxqynk--7Nr8hPYzVoOCesmk
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2: id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 291
ht-degree: 0%

---

# Migration du lac de données de Adobe Experience Platform vers Gen2

Adobe Experience Platform migre vers le lac de données Gen2. Il s’agit d’une nouvelle génération de lac de données qui offre aux utilisateurs d’Experience Platform des avantages tels que la réplication géorégionale, des contrôles d’accès basés sur les rôles plus précis et une meilleure mise à l’échelle.

## Impact de l’utilisateur

Pendant la migration du lac de données de la génération 1 vers la génération 2 par Adobe, les utilisateurs pourront **lire** à partir du lac de données, mais toutes les fonctionnalités **écriture** dans le lac de données seront affectées. Vous trouverez ci-dessous une liste des fonctionnalités affectées :

- **Sources** : les données provenant des sources et divers workflows d’ingestion de données seront retardés. Les utilisateurs verront leurs données une fois la migration terminée.
- **Query Service** : les utilisateurs peuvent effectuer des requêtes, mais ne pourront pas écrire la sortie de la requête dans un jeu de données.
- **Real-Time Customer Profile** : les données ingérées dans la banque de profils par le biais de l’ingestion **par lots** ne seront pas disponibles pendant la migration. Toutefois, les données ingérées par le biais de l’ingestion **streaming** seront disponibles pendant la migration. En outre, les exportations de profils ne seront pas disponibles pendant la migration.
- Workspace de science des données **: les écritures du Workspace de science des données échoueront.**
- **Service de segmentation** : la segmentation des audiences dérivées de **par lots** ne peut pas être activée pendant la migration. Les audiences dérivées de la segmentation **streaming** ne seront pas affectées.
- **Customer Journey Analytics** : les données des rapports Customer Journey Analytics peuvent être obsolètes et ne seront pas actualisées pendant la migration, car les lots ne sont pas ingérés dans le lac de données.

## Communication aux utilisateurs d’Experience Platform

Adobe contactera les administrateurs système pour discuter en détail de l’impact de la migration et confirmer les dates et heures de migration pour des organisations spécifiques.
