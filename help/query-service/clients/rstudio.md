---
keywords: Experience Platform;home;popular topics;Query service;query service;RStudio;rstudio;connect to query service;
solution: Experience Platform
title: Connexion à RStudio
topic: connect
description: Ce document décrit les étapes à suivre pour connecter RStudio à Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 70%

---


# Connexion à [!DNL RStudio]

Ce document décrit les étapes à suivre pour connecter RStudio à Adobe Experience Platform [!DNL Query Service].

Après avoir installé [!DNL RStudio], sur l&#39;écran *Console* qui s&#39;affiche, vous devez d&#39;abord préparer votre script R à utiliser [!DNL PostgreSQL].

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

Une fois que vous avez préparé votre script R à utiliser [!DNL PostgreSQL], vous pouvez désormais connecter [!DNL RStudio] à [!DNL Query Service] en chargeant le pilote [!DNL PostgreSQL].

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
| `{DATABASE_NAME}` | Le nom de la base de données qui sera utilisée. |
| `{HOST_NUMBER` et `{PORT_NUMBER}` | Le point de terminaison hôte et son port pour Query Service. |
| `{USERNAME}` et `{PASSWORD}` | Les identifiants de connexion qui seront utilisés. Le nom d’utilisateur prend la forme `ORG_ID@AdobeOrg`. |

>[!NOTE]
>
>Pour plus d’informations sur la manière dont trouver le nom, l’hôte et le port de la base de données ainsi que les informations d’identification de connexion, consultez la [page des informations d’identification sur Platform](https://platform.adobe.com/query/configuration). Pour trouver vos informations d’identification, connectez-vous à [!DNL Platform], cliquez sur **[!UICONTROL Requêtes]**, puis sur **[!UICONTROL Informations d’identification]**.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez écrire des requêtes pour exécuter et modifier des instructions SQL. Par exemple, vous pouvez utiliser `dbGetQuery(con, sql)` pour exécuter des requêtes, où `sql` est la requête SQL que vous souhaitez exécuter.

La requête suivante utilise un jeu de données contenant [ExperienceEvents](../best-practices/experience-event-queries.md) et crée un histogramme des pages vues d’un site web en fonction de la hauteur d’écran d’un appareil.

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

Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).