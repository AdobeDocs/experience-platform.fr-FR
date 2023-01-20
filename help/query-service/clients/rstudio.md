---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;service de requête;RStudio;studio;se connecter au service de requête;
solution: Experience Platform
title: Connexion de RStudio à Query Service
description: Ce document décrit les étapes à suivre pour connecter RStudio à Adobe Experience Platform Query Service.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 10%

---

# Connexion [!DNL RStudio] vers Query Service

Ce document décrit les étapes à suivre pour se connecter. [!DNL RStudio] avec Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> [!DNL RStudio] a été renommé [!DNL Posit]. [!DNL RStudio] Les produits ont été renommés [!DNL Posit Connect], [!DNL Posit Workbench], [!DNL Posit Package] Manager, [!DNL Posit Cloud], et [!DNL Posit Academy].
>
> Ce guide suppose que vous avez déjà accès à [!DNL RStudio] et connaissent comment l’utiliser. Plus d’informations sur [!DNL RStudio] se trouve dans la variable [officiel [!DNL RStudio] documentation](https://rstudio.com/products/rstudio/).
> 
> En outre, pour utiliser [!DNL RStudio] avec Query Service, vous devez installer le [!DNL PostgreSQL] Pilote JDBC 4.2. Vous pouvez télécharger le pilote JDBC à partir du [[!DNL PostgreSQL] site officiel](https://jdbc.postgresql.org/download/).

## Créez un [!DNL Query Service] dans la [!DNL RStudio] interface

Après installation [!DNL RStudio], vous devez installer le package RJDBC. Instructions sur la manière de procéder [connexion à une base de données via la ligne de commande](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r) Vous pouvez le trouver dans la documentation officielle de la publication.

Si vous utilisez un système d’exploitation Mac, vous pouvez sélectionner **[!UICONTROL Outils]** à partir de la barre de menus, suivie de **[!UICONTROL Installation de packages]** dans le menu déroulant. Vous pouvez également sélectionner la variable **[!DNL Packages]** dans l’interface utilisateur de RStudio, puis sélectionnez **[!DNL Install]**.

Une fenêtre contextuelle s’affiche, affichant la variable **[!DNL Install Packages]** écran. Assurez-vous que **[!DNL Repository (CRAN)]** est sélectionné pour le **[!DNL Install from]** . La valeur de **[!DNL Packages]** should `RJDBC`. Assurez-vous que **[!DNL Install dependencies]** est sélectionnée. Une fois que toutes les valeurs sont correctes, sélectionnez **[!DNL Install]** pour installer les packages. Maintenant que le package RJDBC a été installé, redémarrez [!DNL RStudio] pour terminer le processus d’installation.

Après [!DNL RStudio] a redémarré, vous pouvez désormais vous connecter à Query Service. Sélectionnez la **[!DNL RJDBC]** du module **[!DNL Packages]** et saisissez la commande suivante dans la console :

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Où `{PATH TO THE POSTGRESQL JDBC JAR}` représente le chemin d’accès à la variable [!DNL PostgreSQL] JDBC JAR installé sur votre ordinateur.

Vous pouvez maintenant créer votre connexion à Query Service. Saisissez la commande suivante dans la console :

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>Voir [[!DNL Query Service] Documentation SSL](./ssl-modes.md) pour en savoir plus sur la prise en charge du protocole SSL pour les connexions tierces à Adobe Experience Platform Query Service et sur la connexion à l’aide de `verify-full` Mode SSL.

Pour plus d’informations sur la recherche du nom de la base de données, de l’hôte, du port et des informations de connexion, consultez la section [guide des informations d’identification](../ui/credentials.md). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, suivie de **[!UICONTROL Informations d’identification]**.

Un message dans la sortie de console confirme la connexion à Query Service.

## Rédaction de requêtes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez écrire des requêtes pour exécuter et modifier des instructions SQL. Par exemple, vous pouvez utiliser `dbGetQuery(con, sql)` pour exécuter des requêtes, où `sql` est la requête SQL que vous souhaitez exécuter.

La requête suivante utilise un jeu de données contenant [Événements d’expérience](../../xdm/classes/experienceevent.md) et crée un histogramme des pages vues d’un site web, en fonction de la hauteur d’écran de l’appareil.

```sql
df_pageviews <- dbGetQuery(con,
"SELECT t.range AS buckets, 
 Count(*) AS pageviews 
FROM (SELECT CASE 
 WHEN device.screenheight BETWEEN 0 AND 99 THEN '0 - 99' 
 WHEN device.screenheight BETWEEN 100 AND 199 THEN '100-199' 
 WHEN device.screenheight BETWEEN 200 AND 299 THEN '200-299' 
 WHEN device.screenheight BETWEEN 300 AND 399 THEN '300-399' 
 WHEN device.screenheight BETWEEN 400 AND 499 THEN '400-499' 
 WHEN device.screenheight BETWEEN 500 AND 599 THEN '500-599' 
 ELSE '600-699' 
 end AS range 
 FROM aa_post_vals_3) t 
GROUP BY t.range 
ORDER BY buckets 
LIMIT 1000000")
```

Une réponse réussie renvoie les résultats de la requête :

```r
df_pageviews
 buckets pageviews
1 0 - 99 198985
2 500-599 67138
3 300-399 2147
4 200-299 354
5 400-499 6947
6 100-199 4415
7 600-699 3097040
```

## Étapes suivantes

Pour plus d’informations sur l’écriture et l’exécution de requêtes, veuillez lire le guide sur [exécution de requêtes](../best-practices/writing-queries.md).
