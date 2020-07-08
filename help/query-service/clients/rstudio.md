---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Se connecter avec RStudio
topic: connect
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 2%

---


# Se connecter avec RStudio

Ce document traverse les étapes pour connecter R Studio à Adobe Experience Platform Requête Service.

Après avoir installé RStudio, sur l&#39;écran *Console* qui s&#39;affiche, vous devrez d&#39;abord préparer votre script R pour utiliser PostgreSQL.

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

Une fois que vous avez préparé votre script R pour utiliser PostgreSQL, vous pouvez maintenant connecter RStudio à Requête Service en chargeant le pilote PostgreSQL.

```r
drv <- dbDriver("PostgreSQL")
con <- dbConnect(drv, 
 dbname = "{DATABASE_NAME}",
 host="{HOST_NUMBER}",
 port={PORT_NUMBER},
 user="{USERNAME}",
 password="{PASSWORD}")
```

| Propriété | Description |
| -------- | ----------- |
| `{DATABASE_NAME}` | Nom de la base de données qui sera utilisée. |
| `{HOST_NUMBER` et `{PORT_NUMBER}` | Point de terminaison hôte et son port pour Requête Service. |
| `{USERNAME}` et `{PASSWORD}` | Identifiants de connexion qui seront utilisés. Le nom d&#39;utilisateur prend la forme de `ORG_ID@AdobeOrg`. |

>[!NOTE]
>
>Pour plus d’informations sur la recherche de votre nom de base de données, de votre hôte, de votre port et de vos informations d’identification de connexion, consultez la page [d’identification sur Platform](https://platform.adobe.com/query/configuration). Pour rechercher vos informations d’identification, connectez-vous à Platform, cliquez sur **Requêtes**, puis sur **Informations d’identification**.

## Étapes suivantes

Maintenant que vous êtes connecté à Requête Service, vous pouvez écrire des requêtes pour exécuter et modifier des instructions SQL. Par exemple, vous pouvez utiliser `dbGetQuery(con, sql)` pour exécuter des requêtes, où `sql` est la requête SQL à exécuter.

La requête suivante utilise un jeu de données contenant [ExperienceEvents](../creating-queries/experience-event-queries.md) et crée un histogramme des vues de page d’un site Web, en fonction de la hauteur d’écran du périphérique.

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

Une réponse positive renvoie les résultats de la requête :

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

Pour plus d&#39;informations sur la façon d&#39;écrire et d&#39;exécuter des requêtes, veuillez lire le guide [des requêtes](../creating-queries/creating-queries.md)en cours d&#39;exécution.