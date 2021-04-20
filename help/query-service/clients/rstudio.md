---
keywords: Experience Platform ; accueil ; thèmes populaires ; service de Requête ; service de requête ; RStudio ; studio ; connexion au service de requête ;
solution: Experience Platform
title: Connexion de RStudio au service de Requête
topic: connect
description: Ce document décrit les étapes à suivre pour connecter RStudio à Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: f1b2fd7efd43f317a85c831cd64c09be29688f7a
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 18%

---


# Connecter [!DNL RStudio] au service de Requête

Ce document passe en revue les étapes de connexion de [!DNL RStudio] à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL RStudio] et que vous savez comment l&#39;utiliser. Vous trouverez plus d&#39;informations sur [!DNL RStudio] dans la [documentation officielle [!DNL RStudio] ](https://rstudio.com/products/rstudio/).
> 
> De plus, pour utiliser RStudio avec Requête Service, vous devez installer le pilote PostgreSQL JDBC 4.2. Vous pouvez télécharger le pilote JDBC à partir du [site officiel PostgreSQL](https://jdbc.postgresql.org/download.html).

## Créer une connexion [!DNL Query Service] dans l&#39;interface [!DNL RStudio]

Après avoir installé [!DNL RStudio], vous devez installer le package RJDBC. Accédez au volet **[!DNL Packages]**, puis sélectionnez **[!DNL Install]**.

![](../images/clients/rstudio/install-package.png)

Une fenêtre contextuelle s’affiche, affichant l’écran **[!DNL Install Packages]**. Vérifiez que **[!DNL Repository (CRAN)]** est sélectionné pour la section **[!DNL Install from]**. La valeur de **[!DNL Packages]** doit être `RJDBC`. Vérifiez que **[!DNL Install dependencies]** est sélectionné. Après avoir confirmé que toutes les valeurs sont correctes, sélectionnez **[!DNL Install]** pour installer les packages.

![](../images/clients/rstudio/install-jrdbc.png)

Maintenant que le package RJDBC a été installé, redémarrez RStudio pour terminer le processus d’installation.

Après le redémarrage de RStudio, vous pouvez désormais vous connecter à Requête Service. Sélectionnez le package **[!DNL RJDBC]** dans le volet **[!DNL Packages]**, puis saisissez la commande suivante dans la console :

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Où {PATH TO THE POSTGRESQL JDBC JAR} représente le chemin d’accès au JAR JDBC PostgreSQL qui a été installé sur votre ordinateur.

Vous pouvez maintenant créer votre connexion à Requête Service en entrant la commande suivante dans la console :

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!NOTE]
>
>Pour plus d’informations sur la manière dont trouver le nom, l’hôte et le port de la base de données ainsi que les informations d’identification de connexion, consultez la [page des informations d’identification sur Platform](https://platform.adobe.com/query/configuration). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, puis **[!UICONTROL Informations d’identification]**.

![](../images/clients/rstudio/connection-rjdbc.png)

## Rédaction de requêtes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez écrire des requêtes pour exécuter et modifier des instructions SQL. Par exemple, vous pouvez utiliser `dbGetQuery(con, sql)` pour exécuter des requêtes, où `sql` est la requête SQL que vous souhaitez exécuter.

La requête suivante utilise un jeu de données contenant [Événements d’expérience](../best-practices/experience-event-queries.md) et crée un histogramme des vues de page d’un site Web, en fonction de la hauteur d’écran du périphérique.

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

Pour plus d&#39;informations sur la façon d&#39;écrire et d&#39;exécuter des requêtes, veuillez lire le guide sur les [requêtes en cours d&#39;exécution](../best-practices/writing-queries.md).