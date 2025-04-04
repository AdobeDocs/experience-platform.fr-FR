---
keywords: Experience Platform;accueil;rubriques les plus consultées;Query service;query service;RStudio;rstudio;se connecter à query service;
solution: Experience Platform
title: Connexion de RStudio à Query Service
description: Ce document décrit les étapes à suivre pour connecter RStudio à Adobe Experience Platform Query Service.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 11%

---

# Connecter [!DNL RStudio] à Query Service

Ce document décrit les étapes à suivre pour connecter [!DNL RStudio] à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> [!DNL RStudio] est désormais rebaptisé [!DNL Posit]. [!DNL RStudio] produits ont été renommés [!DNL Posit Connect], [!DNL Posit Workbench], [!DNL Posit Package] Manager, [!DNL Posit Cloud] et [!DNL Posit Academy].
>
> Ce guide suppose que vous avez déjà accès à [!DNL RStudio] et que vous savez comment l’utiliser. Vous trouverez plus d’informations sur les [!DNL RStudio] dans la [documentation [!DNL RStudio] officielle](https://rstudio.com/products/rstudio/).
> 
> De plus, pour utiliser [!DNL RStudio] avec Query Service, vous devez installer le pilote JDBC 4.2 [!DNL PostgreSQL]. Vous pouvez télécharger le pilote JDBC sur le [[!DNL PostgreSQL] site officiel](https://jdbc.postgresql.org/download/).

## Créer une connexion [!DNL Query Service] dans l’interface [!DNL RStudio]

Après avoir installé [!DNL RStudio], vous devez installer le package RJDBC . Les instructions sur la [connexion d’une base de données via la ligne de commande](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r) se trouvent dans la documentation officielle de Posit.

Si vous utilisez un système d’exploitation Mac, vous pouvez sélectionner **[!UICONTROL Outils]** dans la barre de menus, puis **[!UICONTROL Installer des packages]** dans le menu déroulant. Vous pouvez également sélectionner l’onglet **[!DNL Packages]** dans l’interface utilisateur de RStudio, puis sélectionner **[!DNL Install]**.

Une fenêtre contextuelle s’affiche, affichant l’écran **[!DNL Install Packages]**. Assurez-vous que **[!DNL Repository (CRAN)]** est sélectionné pour la section **[!DNL Install from]** . La valeur de **[!DNL Packages]** doit être `RJDBC`. Assurez-vous que **[!DNL Install dependencies]** est sélectionné. Après avoir confirmé que toutes les valeurs sont correctes, sélectionnez **[!DNL Install]** pour installer les packages. Maintenant que le package RJDBC a été installé, redémarrez [!DNL RStudio] pour terminer le processus d’installation.

Après le redémarrage d’[!DNL RStudio], vous pouvez maintenant vous connecter à Query Service. Sélectionnez le package **[!DNL RJDBC]** dans le volet de **[!DNL Packages]**, puis saisissez la commande suivante dans la console :

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Où `{PATH TO THE POSTGRESQL JDBC JAR}` représente le chemin d’accès au fichier JAR JDBC [!DNL PostgreSQL] qui a été installé sur votre ordinateur.

Vous pouvez maintenant créer votre connexion à Query Service. Saisissez la commande suivante dans la console :

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>Consultez la [[!DNL Query Service] documentation SSL](./ssl-modes.md) pour en savoir plus sur la prise en charge SSL pour les connexions tierces à Adobe Experience Platform Query Service et comment se connecter à l’aide `verify-full` mode SSL.

Pour plus d’informations sur la recherche du nom, de l’hôte, du port et des informations de connexion de votre base de données, consultez le guide [informations d’identification](../ui/credentials.md). Pour trouver vos informations d’identification, connectez-vous à [!DNL Experience Platform], puis sélectionnez **[!UICONTROL Requêtes]**, **[!UICONTROL Informations d’identification]**.

Un message dans la sortie de la console confirme la connexion à Query Service.

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

Pour plus d’informations sur l’écriture et l’exécution de requêtes, consultez le guide sur l’[exécution de requêtes](../best-practices/writing-queries.md).
