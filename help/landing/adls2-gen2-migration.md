---
source-git-commit: b9816767556b9d50cf2ff5268816d1de6b85fc63
workflow-type: tm+mt
translation-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---
# Migration de Adobe Experience Platform Data Lake vers Gen2

Adobe Experience Platform migre vers le lac de données Gen2. Il s’agit d’une nouvelle génération de lacs de données qui offrent aux utilisateurs de la plate-forme des avantages tels que la réplication de la région géographique, des contrôles d&#39;accès basés sur les rôles plus précis (RBAC) et une meilleure mise à l’échelle.

## Impact utilisateur

Pendant que l&#39;Adobe migre le lac Data de Gen1 à Gen 2, les utilisateurs pourront **lire** à partir du lac Data, mais toutes les capacités qui **écrivent** dans le lac Data seront affectées. Voici une liste des capacités affectées :

- **Sources**: Les données provenant des sources et de divers workflows d&#39;assimilation des données seront retardées. Les utilisateurs verront leurs données une fois la migration terminée.
- **Requête Service**: Les utilisateurs peuvent effectuer des requêtes mais ne pourront pas écrire la sortie de la requête dans un jeu de données.
- **Profil** client en temps réel : Les données ingérées dans le magasin de Profils par ingestion par **lot** ne seront pas disponibles pendant la migration. Cependant, les données ingérées par **flux continu** par assimilation seront disponibles pendant la migration. En outre, les exportations de Profil ne seront pas disponibles pendant la migration.
- **Espace de travail** des sciences de données : Les écritures issues de Data Science Workspace échoueront.
- **Service** de segmentation : Les Audiences dérivées de la segmentation par **lot** ne peuvent pas être activées pendant la migration. Les Audiences dérivées de la segmentation **en flux continu** ne seront pas affectées.
- **Customer Journey Analytics**: Les données des rapports des Customer Journey Analytics peuvent être obsolètes et ne seront pas actualisées pendant la migration, car les lots ne sont pas ingérés dans Data Lake.

## Communication avec les utilisateurs de la plate-forme

L&#39;Adobe contactera les administrateurs système pour discuter en détail de l&#39;impact de la migration et confirmer les dates et heures de migration pour certaines organisations IMS.