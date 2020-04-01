---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connexion avec RStudio
topic: connect
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Connexion avec RStudio

Ce décrit les étapes nécessaires pour connecter R Studio au service de Adobe Experience Platform.

Après avoir installé RStudio, sur l&#39;écran *Console* qui s&#39;affiche, vous devrez d&#39;abord préparer votre script R pour utiliser PostgreSQL.

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

Une fois que vous avez préparé votre script R pour utiliser PostgreSQL, vous pouvez maintenant connecter RStudio à Service en chargeant le pilote PostgreSQL.

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
| `{HOST_NUMBER` et `{PORT_NUMBER}` | Point de terminaison hôte et son port pour le service de . |
| `{USERNAME}` et `{PASSWORD}` | Informations de connexion qui seront utilisées. Le nom d&#39;utilisateur prend la forme de `ORG_ID@AdobeOrg`. |

>[!NOTE] Pour plus d’informations sur la recherche du nom de base de données, de l’hôte, du port et des informations d’identification de connexion, consultez la page [d’identification de la plateforme](https://platform.adobe.com/query/configuration). Pour rechercher vos informations d’identification, connectez-vous à Platform, cliquez sur ****, puis sur **Credentials**.

## Étapes suivantes

Maintenant que vous êtes connecté à  Service, vous pouvez écrire des  pour exécuter et modifier des instructions SQL. Par exemple, vous pouvez utiliser `dbGetQuery(con, sql)` pour exécuter , où `sql` se trouve le SQL que vous souhaitez exécuter.

Le suivant utilise un jeu de données contenant [ExperienceEvents](../creating-queries/experience-event-queries.md) et crée un histogramme du de page d’un site Web, en fonction de la hauteur d’écran du périphérique.

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

Une réponse positive renvoie les résultats du  :

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

Pour plus d&#39;informations sur la façon d&#39;écrire et d&#39;exécuter des  de, veuillez lire le [guide](../creating-queries/creating-queries.md)de  de en cours d&#39;exécution.