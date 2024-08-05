---
keywords: Experience Platform;JupyterLab;notebooks;espace de travail de science des données;rubriques populaires;analyser les notebooks de données;aed;analyse exploratoire des données;science des données
solution: Experience Platform
title: Notebook d’analyse exploratoire des données (AED)
type: Tutorial
description: Ce guide porte sur l’utilisation du notebook d’analyse exploratoire des données (AED) pour découvrir des modèles dans les données web, agréger les événements avec un objectif de prédiction, nettoyer les données agrégées et comprendre la relation entre les prédicteurs et un objectif.
exl-id: 48209326-0a07-4b5c-8b49-a2082a78fa47
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '2789'
ht-degree: 99%

---

# Exploration des données web pour les modèles prédictifs à l’aide du notebook d’analyse exploratoire des données (AED)

>[!NOTE]
>
>Data Science Workspace ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs à Data Science Workspace.

Le notebook d’analyse exploratoire des données (AED) est conçu pour vous aider à découvrir des modèles au sein des données, à vérifier l’intégrité de ces dernières et à faire la synthèse des données pertinentes pour les modèles prédictifs.

L’exemple du notebook AED a été optimisé en tenant compte des données web et se compose de deux parties. La première partie commence par l’utilisation de Query Service pour afficher les tendances et les instantanés de données. Ensuite, les données sont agrégées au niveau du profil et du visiteur, en tenant compte de l’objectif d’analyse exploratoire des données.

La seconde partie commence par une analyse descriptive sur les données agrégées à l’aide des bibliothèques Python. Ce notebook présente des visualisations telles que des histogrammes, des graphiques de dispersion, des diagrammes à surface et une matrice de corrélation afin d’obtenir des informations exploitables utilisées pour déterminer les fonctionnalités les plus susceptibles de contribuer à la prédiction d’un objectif.

## Prise en main

Avant de lire ce guide, veuillez consulter le [[!DNL JupyterLab] guide de l’utilisateur](./overview.md) pour une présentation détaillée de [!DNL JupyterLab] et de son rôle dans l’espace de travail de science des données. En outre, si vous utilisez vos propres données, veuillez consulter la documentation relative à l’[accès aux données dans les notebooks  [!DNL Jupyterlab] ](./access-notebook-data.md). Ce guide contient des informations importantes sur les limites de données des notebooks.

Ce notebook utilise un jeu de données de valeurs moyennes sous la forme de données d’événements d’expérience Adobe Analytics trouvées dans Analytics Analysis Workspace. Pour utiliser le notebook AED, vous devez définir votre tableau de données avec les valeurs `target_table` et `target_table_id` suivantes. Tout jeu de données de valeurs moyennes peut être utilisé.

Pour rechercher ces valeurs, suivez les étapes décrites dans la section [Écriture dans un jeu de données en Python](./access-notebook-data.md#write-python) dans le guide d’accès aux données de JupyterLab. Le nom du jeu de données (`target_table`) se trouve dans le répertoire du jeu de données. Après un clic droit sur le jeu de données pour explorer ou écrire des données dans un notebook, un identifiant de jeu de données (`target_table_id`) est fourni dans l’entrée de code exécutable.

## Découverte des données

Cette section contient des étapes de configuration et des exemples de requêtes utilisées pour afficher des tendances telles que « dix premières villes par activité des utilisateurs » ou « dix premiers produits consultés ».

### Configuration des bibliothèques

JupyterLab prend en charge plusieurs bibliothèques. Le code suivant peut être collé et exécuté dans une cellule de code pour collecter et installer tous les packages obligatoires utilisés dans cet exemple. Vous pouvez utiliser des packages supplémentaires ou différents en dehors de cet exemple pour votre propre analyse de données. Pour obtenir la liste des packages pris en charge, copiez et collez `!pip list --format=columns` dans une nouvelle cellule.

```python
!pip install colorama
import chart_studio.plotly as py
import plotly.graph_objs as go
from plotly.offline import iplot
from scipy import stats
import numpy as np
import warnings
warnings.filterwarnings('ignore')
from scipy.stats import pearsonr
import matplotlib.pyplot as plt
from scipy.stats import pearsonr
import pandas as pd
import math
import re
import seaborn as sns
from datetime import datetime
import colorama
from colorama import Fore, Style
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)
pd.set_option('display.width', 1000)
pd.set_option('display.expand_frame_repr', False)
pd.set_option('display.max_colwidth', -1)
```

### Connectez-vous à Adobe Experience Platform [!DNL Query Service]

[!DNL JupyterLab] sur Platform vous permet d’utiliser SQL dans un notebook [!DNL Python] pour accéder aux données via [Query Service](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=fr). L’accès aux données par le biais de [!DNL Query Service] peut s’avérer utile pour la gestion de jeux de données volumineux grâce à ses temps d’exécution plus performants. Notez que l’interrogation de données à l’aide de [!DNL Query Service] est limitée à dix minutes de traitement.

Avant d’utiliser [!DNL Query Service] dans [!DNL JupyterLab], assurez-vous de bien comprendre le fonctionnement de la syntaxe SQL de [[!DNL Query Service] ](https://experienceleague.adobe.com/docs/experience-platform/query/sql/syntax.html?lang=fr).

Pour utiliser Query Service dans JupyterLab, vous devez d’abord créer une connexion entre votre notebook Python de travail et Query Service. Pour ce faire, exécutez la cellule suivante.

```python
qs_connect()
```

### Définir le jeu de données de valeurs moyennes à explorer

Pour commencer à interroger et à explorer les données, un tableau de jeu de données de valeurs moyennes doit être fourni. Copiez et remplacez les valeurs de `table_name` et `table_id` avec vos propres valeurs de tableau de données.

```python
target_table = "table_name"
target_table_id = "table_id"
```

Une fois l’opération terminée, cette cellule doit ressembler à l’exemple suivant :

```python
target_table = "cross_industry_demo_midvalues"
target_table_id = "5f7c40ef488de5194ba0157a"
```

### Parcourir le jeu de données pour trouver les dates disponibles

La cellule fournie ci-dessous vous permet d’afficher la période couverte dans le tableau. L’exploration du nombre de jours, de la première date et de la dernière date a pour but de faciliter la sélection d’une période pour une analyse plus approfondie.

```python
%%read_sql -c QS_CONNECTION
SELECT distinct Year(timestamp) as Year, Month(timestamp) as Month, count(distinct DAY(timestamp)) as Count_days, min(DAY(timestamp)) as First_date, max(DAY(timestamp)) as Last_date, count(timestamp) as Count_hits
from {target_table}
group by Month(timestamp), Year(timestamp)
order by Year, Month;
```

L’exécution de la cellule génère la sortie suivante :

![sortie de date de requête](../images/jupyterlab/eda/query-date-output.PNG)

### Configurer des dates pour la découverte de jeux de données

Après avoir déterminé les dates disponibles pour la découverte de jeux de données, les paramètres ci-dessous doivent être mis à jour. Les dates configurées dans cette cellule ne sont utilisées que pour la découverte de données sous la forme de requêtes. Les dates sont à nouveau mises à jour pour des plages appropriées pour l’analyse exploratoire des données abordée plus loin dans ce guide.

```python
target_year = "2020" ## The target year
target_month = "02" ## The target month
target_day = "(01,02,03)" ## The target days
```

### Découverte de jeux de données

Une fois que vous avez configuré tous vos paramètres, que vous avez démarré [!DNL Query Service], et que vous disposez d’une période, vous pouvez commencer la lecture de lignes de données. Vous devez limiter le nombre de lignes que vous lisez.

```python
from platform_sdk.dataset_reader import DatasetReader
from datetime import date
dataset_reader = DatasetReader(PLATFORM_SDK_CLIENT_CONTEXT, dataset_id=target_table_id)
# If you do not see any data or would like to expand the default date range, change the following query
Table = dataset_reader.limit(5).read()
```

Pour afficher le nombre de colonnes disponibles dans le jeu de données, utilisez la cellule suivante :

```python
print("\nNumber of columns:",len(Table.columns))
```

Pour afficher les lignes du jeu de données, utilisez la cellule suivante. Dans cet exemple, le nombre de lignes est limité à cinq.

```python
Table.head(5)
```

![sortie de ligne de tableau](../images/jupyterlab/eda/data-table-overview.PNG)

Une fois que vous avez une idée des données contenues dans le jeu de données, il peut s’avérer utile de ventiler davantage le jeu de données. Dans cet exemple, les noms des colonnes et les types de données de chacune des colonnes sont répertoriés, tandis que la sortie est utilisée pour vérifier si le type de données est correct ou non.

```python
ColumnNames_Types = pd.DataFrame(Table.dtypes)
ColumnNames_Types = ColumnNames_Types.reset_index()
ColumnNames_Types.columns = ["Column_Name", "Data_Type"]
ColumnNames_Types
```

![nom de colonne et liste des types de données](../images/jupyterlab/eda/data-columns.PNG)

### Exploration des tendances des jeux de données

La section suivante contient quatre exemples de requêtes utilisées pour explorer les tendances et les modèles dans les données. Les exemples présentés ci-dessous ne sont pas exhaustifs, mais ils présentent quelques-unes des fonctionnalités les plus courantes.

**Nombre d’activités par heure pour un jour spécifique**

Cette requête analyse le nombre d’actions et de clics tout au long de la journée. La sortie est représentée sous la forme d’un tableau contenant des mesures sur le nombre d’activités pour chaque heure de la journée.

```sql
%%read_sql query_2_df -c QS_CONNECTION

SELECT Substring(timestamp, 12, 2)                        AS Hour, 
       Count(enduserids._experience.aaid.id) AS Count 
FROM   {target_table}
WHERE  Year(timestamp) = {target_year} 
       AND Month(timestamp) = {target_month}  
       AND Day(timestamp) in {target_day}
GROUP  BY Hour
ORDER  BY Hour;
```

![sortie de la requête 1](../images/jupyterlab/eda/hour-count-raw.PNG)

Une fois la requête validée, les données peuvent être présentées sous la forme d’un histogramme graphique à une seule variable pour plus de clarté.

```python
trace = go.Bar(
    x = query_2_df['Hour'],
    y = query_2_df['Count'],
    name = "Activity Count"
)

layout = go.Layout(
    title = 'Activity Count by Hour of Day',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Hour of Day'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![sortie graphique à barres pour la requête 1](../images/jupyterlab/eda/activity-count-by-hour-of-day.png)

**Les 10 pages les plus consultées pour un jour donné**

Cette requête analyse les pages les plus consultées pour un jour donné. La sortie est représentée sous la forme d’un tableau contenant des mesures sur le nom des pages et le nombre de pages vues.

```sql
%%read_sql query_4_df -c QS_CONNECTION

SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  Year(timestamp) = {target_year}
       AND Month(timestamp) = {target_month}
       AND Day(timestamp) in {target_day}
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

Une fois la requête validée, les données peuvent être présentées sous la forme d’un histogramme graphique à une seule variable pour plus de clarté.

```python
trace = go.Bar(
    x = query_4_df['Page_Name'],
    y = query_4_df['Page_Views'],
    name = "Page Views"
)

layout = go.Layout(
    title = 'Top Ten Viewed Pages For a Given Day',
    width = 1000,
    height = 600,
    xaxis = dict(title = 'Page_Name'),
    yaxis = dict(title = 'Page_Views')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![Dix premières pages consultées](../images/jupyterlab/eda/top-ten-viewed-pages-for-a-given-day.png)

**Dix premières villes regroupées par activité utilisateur**

Cette requête analyse les villes d’où proviennent les données.

```sql
%%read_sql query_6_df -c QS_CONNECTION

SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE  Year(timestamp) = {target_year}
       AND Month(timestamp) = {target_month}
       AND Day(timestamp) in {target_day}
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

Une fois la requête validée, les données peuvent être présentées sous la forme d’un histogramme graphique à une seule variable pour plus de clarté.

```python
trace = go.Bar(
    x = query_6_df['state_city'],
    y = query_6_df['Count'],
    name = "Activity by City"
)

layout = go.Layout(
    title = 'Top Ten Cities by User Activity',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'City'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![Dix premières villes](../images/jupyterlab/eda/top-ten-cities-by-user-activity.png)

**Dix produits les plus consultés**

Cette requête fournit une liste des dix produits les plus consultés. Dans l’exemple ci-dessous, la fonction `Explode()` sert à renvoyer chaque produit dans l’objet `productlistitems` dans sa propre ligne. Vous pouvez ainsi effectuer une requête imbriquée pour agréger les produits vus pour différents SKU.

```sql
%%read_sql query_7_df -c QS_CONNECTION

SELECT Product_List_Items.sku AS Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems) AS Product_List_Items, 
              commerce.productviews.value   AS Product_Views 
       FROM   {target_table}
       WHERE  Year(timestamp) = {target_year}
              AND Month(timestamp) = {target_month}
              AND Day(timestamp) in {target_day}
              AND commerce.productviews.value IS NOT NULL) 
GROUP BY Product_SKU 
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

Une fois la requête validée, les données peuvent être présentées sous la forme d’un histogramme graphique à une seule variable pour plus de clarté.

```python
trace = go.Bar(
    x = "SKU-" + query_7_df['Product_SKU'],
    y = query_7_df['Total_Product_Views'],
    name = "Product View"
)

layout = go.Layout(
    title = 'Top Ten Viewed Products',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'SKU'),
    yaxis = dict(title = 'Product View Count')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![Dix premiers produits vus](../images/jupyterlab/eda/top-ten-viewed-products.png)

Après avoir exploré les tendances et les modèles des données, vous devriez avoir une idée assez précise des fonctionnalités que vous souhaitez créer pour la prédiction d’un objectif. Parcourir les tableaux peut rapidement mettre en évidence la forme de chaque attribut de données, les fausses représentations évidentes et les valeurs aberrantes importantes et commencer à suggérer les relations candidates à explorer entre les attributs.

## Analyse exploratoire des données

L’analyse exploratoire des données est utilisée pour améliorer votre compréhension des données et vous faire une idées des questions incontournables qui serviront de base à votre modélisation.

L’étape de découverte des données vous aura permis d’explorer les données au niveau de l’événement avec quelques agrégations au niveau de l’événement, de la ville ou de l’identifiant utilisateur pour afficher les tendances pour une journée. Bien que ces données soient importantes, elles n’offrent pas une vue d’ensemble. Vous ne comprenez toujours pas ce qui motive un achat sur votre site web.

Pour ce faire, vous devez agréger les données au niveau du profil/visiteur, définir un objectif d’achat et appliquer des concepts statistiques tels que des diagrammes de corrélation, des diagrammes à surface et des graphiques de dispersion. Ces méthodes sont utilisées pour comparer des modèles d’activités pour les acheteurs par rapport aux non-acheteurs dans la fenêtre de prédiction que vous définissez.

Dans cette section, les fonctionnalités suivantes sont créées et explorées :

- `COUNT_UNIQUE_PRODUCTS_PURCHASED` : nombre de produits uniques achetés.
- `COUNT_CHECK_OUTS` : nombre de passages en caisse.
- `COUNT_PURCHASES` : nombre d’achats.
- `COUNT_INSTANCE_PRODUCTADDS` : nombre d’instances d’ajout de produit.
- `NUMBER_VISITS` : nombre de visites.
- `COUNT_PAID_SEARCHES` : nombre de recherches payantes.
- `DAYS_SINCE_VISIT` : nombre de jours depuis la dernière visite.
- `TOTAL_ORDER_REVENUE` : montant total des commandes.
- `DAYS_SINCE_PURCHASE` : nombre de jours depuis le dernier achat.
- `AVG_GAP_BETWEEN_ORDERS_DAYS` : écart moyen entre les achats en jours.
- `STATE_CITY` : contient l’État et la ville.

Avant de poursuivre votre agrégation de données, vous devez définir les paramètres de la variable de prédiction utilisée dans l’analyse exploratoire des données. En d’autres termes, qu’attendez-vous de votre modèle de science des données ? Les paramètres courants incluent un objectif, une période de prédiction et une période d’analyse.

Si vous utilisez le notebook EDA, vous devez remplacer les valeurs ci-dessous avant de continuer.

```python
goal = "commerce.`order`.purchaseID" #### prediction variable
goal_column_type = "numerical" #### choose either "categorical" or "numerical"
prediction_window_day_start = "2020-01-01" #### YYYY-MM-DD
prediction_window_day_end = "2020-01-31" #### YYYY-MM-DD
analysis_period_day_start = "2020-02-01" #### YYYY-MM-DD
analysis_period_day_end = "2020-02-28" #### YYYY-MM-DD

### If the goal is a categorical goal then select threshold for the defining category and creating bins. 0 is no order placed, and 1 is at least one order placed:
threshold = 1
```

### Agrégation des données pour la création de fonctionnalités et d’objectifs

Pour commencer l’analyse exploratoire, vous devez créer un objectif au niveau du profil, puis agréger votre jeu de données. Dans cet exemple, deux requêtes sont fournies. La première requête contient la création d’un objectif. La seconde requête doit être mise à jour afin d’inclure d’autres variables que celles de la première requête. Vous pouvez mettre à jour la `limit` pour votre requête. Après avoir exécuté les requêtes suivantes, les données agrégées sont désormais disponibles pour exploration.

```sql
%%read_sql target_df -d -c QS_CONNECTION

SELECT DISTINCT endUserIDs._experience.aaid.id                  AS ID,
       Count({goal})                                            AS TARGET
FROM   {target_table}
WHERE DATE(TIMESTAMP) BETWEEN '{prediction_window_day_start}' AND '{prediction_window_day_end}'
GROUP BY endUserIDs._experience.aaid.id;
```

```sql
%%read_sql agg_data -d -c QS_CONNECTION

SELECT z.*, z1.state_city as STATE_CITY
from
((SELECT y.*,a2.AVG_GAP_BETWEEN_ORDERS_DAYS as AVG_GAP_BETWEEN_ORDERS_DAYS
from
(select a1.*, f.DAYS_SINCE_PURCHASE as DAYS_SINCE_PURCHASE
from
(SELECT DISTINCT a.ID  AS ID,
COUNT(DISTINCT Product_Items.SKU) as COUNT_UNIQUE_PRODUCTS_PURCHASED,
COUNT(a.check_out) as COUNT_CHECK_OUTS,
COUNT(a.purchases) as COUNT_PURCHASES, 
COUNT(a.product_list_adds) as COUNT_INSTANCE_PRODUCTADDS,
sum(CASE WHEN a.search_paid = 'TRUE' THEN 1 ELSE 0 END) as COUNT_PAID_SEARCHES,
DATEDIFF('{analysis_period_day_end}', MAX(a.date_a)) as DAYS_SINCE_VISIT,
ROUND(SUM(Product_Items.priceTotal * Product_Items.quantity), 2) AS TOTAL_ORDER_REVENUE
from 
(SELECT endUserIDs._experience.aaid.id as ID,
commerce.`checkouts`.value as check_out,
commerce.`order`.purchaseID as purchases, 
commerce.`productListAdds`.value as product_list_adds,
search.isPaid as search_paid,
DATE(TIMESTAMP) as date_a,
Explode(productlistitems) AS Product_Items
from {target_table}
Where DATE(TIMESTAMP) BETWEEN '{analysis_period_day_start}' AND '{analysis_period_day_end}') as a
group by a.ID) as a1
left join 
(SELECT DISTINCT endUserIDs._experience.aaid.id as ID,
DATEDIFF('{analysis_period_day_end}', max(DATE(TIMESTAMP))) as DAYS_SINCE_PURCHASE
from {target_table}
where DATE(TIMESTAMP) BETWEEN '{analysis_period_day_start}' AND '{analysis_period_day_end}'
and commerce.`order`.purchaseid is not null
GROUP BY endUserIDs._experience.aaid.id) as f
on f.ID = a1.ID
where a1.COUNT_PURCHASES>0) as y
left join
(select ab.ID, avg(DATEDIFF(ab.ORDER_DATES, ab.PriorDate)) as AVG_GAP_BETWEEN_ORDERS_DAYS
from
(SELECT distinct endUserIDs._experience.aaid.id as ID, TO_DATE(DATE(TIMESTAMP)) as ORDER_DATES, 
TO_DATE(LAG(DATE(TIMESTAMP),1) OVER (PARTITION BY endUserIDs._experience.aaid.id ORDER BY DATE(TIMESTAMP))) as PriorDate
FROM {target_table}
where DATE(TIMESTAMP) BETWEEN '{analysis_period_day_start}' AND '{analysis_period_day_end}'
AND commerce.`order`.purchaseid is not null) AS ab
where ab.PriorDate is not null
GROUP BY ab.ID) as a2
on a2.ID = y.ID) z    
left join
(select t.ID, t.state_city from
(
SELECT DISTINCT endUserIDs._experience.aaid.id as ID,
concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) as state_city, 
ROW_NUMBER() OVER(PARTITION BY endUserIDs._experience.aaid.id ORDER BY DATE(TIMESTAMP) DESC) AS ROWNUMBER
FROM   {target_table}
WHERE  DATE(TIMESTAMP) BETWEEN '{analysis_period_day_start}' AND '{analysis_period_day_end}') as t
where t.ROWNUMBER = 1) z1
on z.ID = z1.ID)
limit 500000;
```

### Fusionner les fonctionnalités du jeu de données agrégé avec un objectif

La cellule suivante est utilisée pour fusionner les fonctionnalités du jeu de données agrégé décrites dans l’exemple précédent avec votre objectif de prédiction.

```python
Data = pd.merge(agg_data,target_df, on='ID',how='left')
Data['TARGET'].fillna(0, inplace=True)
```

Les trois exemples de cellules suivants sont utilisés pour s’assurer que la fusion a réussi.

`Data.shape` renvoie le nombre de colonnes suivi du nombre de lignes, par exemple : (11913, 12).

```python
Data.shape
```

`Data.head(5)` renvoie un tableau contenant 5 lignes de données. Le tableau renvoyé contient les 12 colonnes de données agrégées mappées à un identifiant de profil.

```python
Data.head(5)
```

![exemple de tableau](../images/jupyterlab/eda/raw-aggregate-data.PNG)

Cette cellule imprime le nombre de profils uniques.

```python
print("Count of unique profiles:", (len(Data)))
```

### Détecter les valeurs manquantes et les valeurs aberrantes

Une fois l’agrégation des données terminée et fusionnée avec votre objectif, vous devez vérifier les données, ce qui est parfois appelé contrôle de l’intégrité des données.

Ce processus implique l’identification des valeurs manquantes et des valeurs aberrantes. Lorsque des problèmes sont identifiés, la tâche suivante consiste à élaborer des stratégies spécifiques pour les gérer.

>[!NOTE]
>
>Au cours de cette étape, vous pouvez détecter une corruption dans les valeurs qui peut signaler une erreur dans le processus de journalisation des données.

```python
Missing = pd.DataFrame(round(Data.isnull().sum()*100/len(Data),2))
Missing.columns =['Percentage_missing_values'] 
Missing['Features'] = Missing.index
```

La cellule suivante est utilisée pour visualiser les valeurs manquantes.

```python
trace = go.Bar(
    x = Missing['Features'],
    y = Missing['Percentage_missing_values'],
    name = "Percentage_missing_values")

layout = go.Layout(
    title = 'Missing values',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Features'),
    yaxis = dict(title = 'Percentage of missing values')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![Valeurs manquantes](../images/jupyterlab/eda/missing-values.png)

Après avoir détecté des valeurs manquantes, il est essentiel d’identifier les valeurs aberrantes. Les statistiques paramétriques telles que la moyenne, l’écart type et la corrélation sont très sensibles aux valeurs aberrantes. En outre, les hypothèses des procédures statistiques courantes telles que les régressions linéaires sont également fondées sur ces statistiques. Cela signifie que les valeurs aberrantes peuvent vraiment gâcher une analyse.

Pour identifier les valeurs aberrantes, cet exemple utilise un écart interquartile. L’écart interquartile (IQR) est l’écart entre le premier et le troisième quartile (25e et 75e percentiles). Cet exemple rassemble tous les points de données qui tombent sous 1,5 fois l’IQR en dessous du 25e percentile, ou 1,5 fois l’IQR au dessus du 75e percentile. Les valeurs qui se trouvent sous l’un de ces seuils sont définies comme une valeur aberrante dans la cellule suivante.

>[!TIP]
>
>Pour corriger les valeurs aberrantes, vous devez avoir une bonne compréhension de l’entreprise et de l’industrie dans lesquelles vous travaillez. Parfois, vous ne pouvez pas éliminer une observation juste parce que c’est une valeur aberrante. Les valeurs aberrantes peuvent être des observations légitimes et sont souvent les plus intéressantes. Pour en savoir plus sur l’élimination de valeurs aberrantes, consultez l’[étape facultative de nettoyage des données](#optional-data-clean).

```python
TARGET = Data.TARGET

Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
Data_numerical.drop(['TARGET'],axis = 1,inplace = True)
Data_numerical1 = Data_numerical

for i in range(0,len(Data_numerical1.columns)):
    Q1 = Data_numerical1.iloc[:,i].quantile(0.25)
    Q3 = Data_numerical1.iloc[:,i].quantile(0.75)
    IQR = Q3 - Q1
    Data_numerical1.iloc[:,i] = np.where(Data_numerical1.iloc[:,i]<(Q1 - 1.5 * IQR),np.nan, np.where(Data_numerical1.iloc[:,i]>(Q3 + 1.5 * IQR),
                                                                                                    np.nan,Data_numerical1.iloc[:,i]))
    
Outlier = pd.DataFrame(round(Data_numerical1.isnull().sum()*100/len(Data),2))
Outlier.columns =['Percentage_outliers'] 
Outlier['Features'] = Outlier.index   
```

Comme toujours, il est important de visualiser les résultats.

```python
trace = go.Bar(
    x = Outlier['Features'],
    y = Outlier['Percentage_outliers'],
    name = "Percentage_outlier")

layout = go.Layout(
    title = 'Outliers',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Features'),
    yaxis = dict(title = 'Percentage of outliers')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![graphe de valeurs aberrantes](../images/jupyterlab/eda/outliers.png)

### Analyse univariée

Une fois vos données corrigées concernant les valeurs manquantes et les valeurs aberrantes, vous pouvez commencer votre analyse. Il existe trois types d’analyses : l’analyse univariée, bivariée et multivariée. L’analyse univariée récupère les données, les synthétise, et détecte des modèles dans les données à l’aide de relations de variables uniques. L’analyse bivariée examine plus d’une variable à la fois, tandis que l’analyse multivariée examine trois variables ou plus à la fois.

L’exemple suivant génère un tableau pour visualiser la distribution des fonctionnalités.

```python
Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
distribution = pd.DataFrame([Data_numerical.count(),Data_numerical.mean(),Data_numerical.quantile(0), Data_numerical.quantile(0.01),
                             Data_numerical.quantile(0.05),Data_numerical.quantile(0.25), Data_numerical.quantile(0.5),
                        Data_numerical.quantile(0.75),  Data_numerical.quantile(0.95),Data_numerical.quantile(0.99), Data_numerical.max()])
distribution = distribution.T
distribution.columns = ['Count', 'Mean', 'Min', '1st_perc','5th_perc','25th_perc', '50th_perc','75th_perc','95th_perc','99th_perc','Max']
distribution
```

![distribution des fonctionnalités](../images/jupyterlab/eda/distribution-of-features.PNG)

Une fois que vous disposez d’une distribution des fonctionnalités, vous pouvez créer des graphiques de données visualisés à l’aide d’un tableau. Les cellules suivantes sont utilisées pour visualiser le tableau ci-dessus avec des données numériques.

```python
A = sns.palplot(sns.color_palette("Blues"))
```

```python
for column in Data_numerical.columns[0:]:
    plt.figure(figsize=(5, 4))
    plt.ticklabel_format(style='plain', axis='y')
    sns.distplot(Data_numerical[column], color = A, kde=False, bins=6, hist_kws={'alpha': 0.4});
```

![graphes de données numériques](../images/jupyterlab/eda/univaiate-graphs.png)

### Données catégorielles

Le regroupement de données catégorielles permet de comprendre les valeurs contenues dans chacune des colonnes de données agrégées et leurs distributions. Cet exemple utilise les 10 principales catégories afin d’élaborer un graphe pour les distributions. Il est important de noter qu’une colonne peut contenir des milliers de valeurs uniques. Vous ne devez pas encombrer un graphe, ce qui le rendrait illisible. En gardant à l’esprit votre objectif commercial, le regroupement de données donne des résultats plus significatifs.

```python
Data_categorical = Data.select_dtypes(include='object')
Data_categorical.drop(['ID'], axis = 1, inplace = True, errors = 'ignore')
```

```python
for column in Data_categorical.columns[0:]:
    if (len(Data_categorical[column].value_counts())>10):
        plt.figure(figsize=(12, 8))
        sns.countplot(x=column, data = Data_categorical, order = Data_categorical[column].value_counts().iloc[:10].index, palette="Set2");
    else:
        plt.figure(figsize=(12, 8))
        sns.countplot(x=column, data = Data_categorical, palette="Set2");
```

![colonnes catégorielles](../images/jupyterlab/eda/graph-category.PNG)

### Supprimer les colonnes avec une seule valeur distincte

Les colonnes qui n’ont qu’une seule valeur n’ajoutent aucune information à l’analyse et peuvent être supprimées.

```python
for col in Data.columns:
    if len(Data[col].unique()) == 1:
        if col == 'TARGET':
            print(Fore.RED + '\033[1m' + 'WARNING: TARGET HAS A SINGLE UNIQUE VALUE, ANY BIVARIATE ANALYSIS (NEXT STEP IN THIS NOTEBOOK) OR PREDICTION WILL BE MEANINGLESS' + Fore.RESET + '\x1b[21m')
        elif col == 'ID':
            print(Fore.RED + '\033[1m' + 'WARNING: THERE IS ONLY ONE PROFILE IN THE DATA, ANY BIVARIATE ANALYSIS (NEXT STEP IN THIS NOTEBOOK) OR PREDICTION WILL BE MEANINGLESS' + Fore.RESET + '\x1b[21m')
        else:
            print('Dropped column:',col)
            Data.drop(col,inplace=True,axis=1)
```

Une fois que vous avez supprimé les colonnes à une seule valeur, vérifiez si les autres colonnes contiennent des erreurs à l’aide de la commande `Data.columns` dans une nouvelle cellule.

### Corriger les valeurs manquantes

La section suivante contient des exemples d’approches pour corriger les valeurs manquantes. Même si dans les données ci-dessus, une seule colonne ne comportait pas de valeur, les exemples de cellules ci-dessous corrigent les valeurs pour tous les types de données. Ces cas comprennent notamment :

- Types de données numériques : entrée 0 ou max le cas échéant
- Types de données catégorielles : valeur modale d’entrée

```python
#### Select only numerical data
Data_numerical = Data.select_dtypes(include=['float64', 'int64'])

#### For columns that contain days we impute max days of history for null values, for rest all we impute 0

# Imputing days with max days of history
Days_cols = [col for col in Data_numerical.columns if 'DAYS_' in col]
d1 = datetime.strptime(analysis_period_day_start, "%Y-%m-%d")
d2 = datetime.strptime(analysis_period_day_end, "%Y-%m-%d")
A = abs((d2 - d1).days)

for column in Days_cols:
    Data[column].fillna(A, inplace=True)

# Imputing 0
Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
Missing_numerical = Data_numerical.columns[Data_numerical.isnull().any()].tolist()

for column in Missing_numerical:
    Data[column].fillna(0, inplace=True)
```

```python
#### Correct for missing values in categorical columns (Replace with mode)
Data_categorical = Data.select_dtypes(include='object')
Missing_cat = Data_categorical.columns[Data_categorical.isnull().any()].tolist() 
for column in Missing_cat:
    Data[column].fillna(Data[column].mode()[0], inplace=True)
```

Une fois l’opération terminée, les données nettoyées sont prêtes pour une analyse bivariée.

### Analyse bivariée

L’analyse bivariée est utilisée pour aider à comprendre la relation entre deux ensembles de valeurs, telles que vos fonctionnalités et une variable cible. Différents tracés s’adaptant aux types de données catégoriels et numériques, cette analyse doit être effectuée séparément pour chaque type de données. Les graphiques suivants sont recommandés pour l’analyse bivariée :

- **Corrélation** : un coefficient de corrélation est la mesure de la force d’une relation entre deux caractéristiques. La corrélation contient des valeurs comprises entre -1 et 1, où : 1 indique une forte relation positive, -1 indique une forte relation négative, et un résultat de zéro indique qu’aucune relation n’est établie.
- **Diagramme de dispersion** : les diagrammes de dispersion sont un moyen simple de visualiser les relations entre chaque variable. Il produit une matrice des relations entre chaque variable dans les données.
- **Carte thermique** : les cartes thermiques sont le coefficient de corrélation pour toutes les variables du jeu de données.
- **Boîte à moustache** : les boîtes à moustache sont une manière normalisée d’afficher la distribution des données en fonction d’un résumé à cinq chiffres (minimum, premier quartile (Q1), médian, troisième quartile (Q3) et maximum).
- **Graphique à nombres** : un graphique à nombres est comme un histogramme ou un graphique à barres pour certaines fonctionnalités catégorielles. Il indique le nombre d’occurrences d’un élément en fonction d’un certain type de catégorie.

Pour comprendre la relation entre la variable « objectif » et les prédicteurs/fonctionnalités, les graphiques sont utilisés en fonction des types de données. Pour les fonctionnalités numériques, vous devez utiliser une boîte à moustache si la variable « objectif » est catégorielle, ainsi qu’un diagramme de dispersion et une carte thermique si la variable « objectif » est numérique.

Pour les fonctionnalités catégorielles, vous devez utiliser un graphique à nombres si la variable « objectif » est catégorielle, ainsi qu’une boîte à moustache si la variable « objectif » est numérique. L’utilisation de ces méthodes permet de comprendre les relations. Ces relations peuvent prendre la forme de fonctionnalités ou de prédicteurs et d’un objectif.

**Prédicteurs numériques**

```python
if len(Data) == 1:
    print(Fore.RED + '\033[1m' + 'THERE IS ONLY ONE PROFILE IN THE DATA, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE AT LEAST ONE MORE PROFILE TO DO BIVARIATE ANALYSIS')
elif len(Data['TARGET'].unique()) == 1:
    print(Fore.RED + '\033[1m' + 'TARGET HAS A SINGLE UNIQUE VALUE, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE PROFILES WITH ATLEAST ONE DIFFERENT VALUE OF TARGET TO DO BIVARIATE ANALYSIS')
else:
    if (goal_column_type == "categorical"):
        TARGET_categorical = pd.DataFrame(np.where(TARGET>=threshold,"1","0"))
        TARGET_categorical.rename(columns={TARGET_categorical.columns[0]: "TARGET_categorical" }, inplace = True)
        Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
        Data_numerical.drop(['TARGET'],inplace=True,axis=1)
        Data_numerical = pd.concat([Data_numerical, TARGET_categorical.astype(int)], axis = 1)
        ncols_for_charts = len(Data_numerical.columns)-1
        nrows_for_charts = math.ceil(ncols_for_charts/4)
        fig, axes = plt.subplots(nrows=nrows_for_charts, ncols=4, figsize=(18, 15))
        for idx, feat in enumerate(Data_numerical.columns[:-1]):
            ax = axes[int(idx // 4), idx % 4]
            sns.boxplot(x='TARGET_categorical', y=feat, data=Data_numerical, ax=ax)
            ax.set_xlabel('')
            ax.set_ylabel(feat)
            fig.tight_layout();
    else:
        Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
        TARGET = pd.DataFrame(Data_numerical.TARGET)
        Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
        Data_numerical.drop(['TARGET'],inplace=True,axis=1)
        Data_numerical = pd.concat([Data_numerical, TARGET.astype(int)], axis = 1)
        for i in Data_numerical.columns[:-1]:
            sns.pairplot(x_vars=i, y_vars=['TARGET'], data=Data_numerical, height = 4)
        f, ax = plt.subplots(figsize = (10,8))
        corr = Data_numerical.corr()
```

L’exécution de la cellule génère les résultats suivants :

![graphes](../images/jupyterlab/eda/bivariant-graphs.png)

![carte thermique](../images/jupyterlab/eda/bi-graph10.PNG)

**Prédicteurs catégoriels**

L’exemple suivant permet de créer et d’afficher les graphiques de fréquence pour les 10 principales catégories de chaque variable catégorielle.

```python
if len(Data) == 1:
    print(Fore.RED + '\033[1m' + 'THERE IS ONLY ONE PROFILE IN THE DATA, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE AT LEAST ONE MORE PROFILE TO DO BIVARIATE ANALYSIS')
elif len(Data['TARGET'].unique()) == 1:
    print(Fore.RED + '\033[1m' + 'TARGET HAS A SINGLE UNIQUE VALUE, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE PROFILES WITH ATLEAST ONE DIFFERENT VALUE OF TARGET TO DO BIVARIATE ANALYSIS')
else:
    if (goal_column_type == "categorical"):
        TARGET_categorical = pd.DataFrame(np.where(TARGET>=threshold,"1","0"))
        TARGET_categorical.rename(columns={TARGET_categorical.columns[0]: "TARGET_categorical" }, inplace = True)
        Data_categorical = Data.select_dtypes(include='object')
        Data_categorical.drop(["ID"], axis =1, inplace = True)
        Cat_columns = Data_categorical
        Data_categorical = pd.concat([TARGET_categorical,Data_categorical], axis =1)
        for column in Cat_columns.columns:
            A = Data_categorical[column].value_counts().iloc[:10].index
            Data_categorical1 = Data_categorical[Data_categorical[column].isin(A)]
            plt.figure(figsize=(12, 8))
            sns.countplot(x="TARGET_categorical",hue=column, data = Data_categorical1, palette = 'Blues')
            plt.xlabel("GOAL")
            plt.ylabel("COUNT")
            plt.show();
    else:
        Data_categorical = Data.select_dtypes(include='object')
        Data_categorical.drop(["ID"], axis =1, inplace = True)
        Target = Data.TARGET
        Data_categorical = pd.concat([Data_categorical,Target], axis =1)
        for column in Data_categorical.columns[:-1]:
            A = Data_categorical[column].value_counts().iloc[:10].index
            Data_categorical1 = Data_categorical[Data_categorical[column].isin(A)]
            sns.catplot(x=column, y="TARGET", kind = "boxen", data =Data_categorical1, height=5, aspect=13/5);
```

L’exécution de la cellule génère la sortie suivante :

![relation de catégorie](../images/jupyterlab/eda/categorical-predictor.PNG)

### Fonctionnalités numériques importantes

L’analyse des corrélations permet de créer une liste des dix principales fonctionnalités numériques. Ces fonctionnalités peuvent toutes être utilisées pour prédire la fonctionnalité d’« objectif ». Cette liste peut être utilisée comme liste de fonctionnalités lorsque vous commencez à créer votre modèle.

```python
if len(Data) == 1:
    print(Fore.RED + '\033[1m' + 'THERE IS ONLY ONE PROFILE IN THE DATA, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE AT LEAST ONE MORE PROFILE TO FIND IMPORTANT VARIABLES')
elif len(Data['TARGET'].unique()) == 1:
    print(Fore.RED + '\033[1m' + 'TARGET HAS A SINGLE UNIQUE VALUE, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE PROFILES WITH ATLEAST ONE DIFFERENT VALUE OF TARGET TO FIND IMPORTANT VARIABLES')
else:
    Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
    Correlation = pd.DataFrame(Data_numerical.drop("TARGET", axis=1).apply(lambda x: x.corr(Data_numerical.TARGET)))
    Correlation['Corr_abs'] = abs(Correlation)
    Correlation = Correlation.sort_values(by = 'Corr_abs', ascending = False)
    Imp_features = pd.DataFrame(Correlation.index[0:10])
    Imp_features.rename(columns={0:'Important Feature'}, inplace=True)
    print(Imp_features)
```

![fonctionnalités importantes](../images/jupyterlab/eda/important-feature-model.PNG)

### Exemple d’information

Pendant que vous analysez vos données, il n’est pas rare de découvrir des informations. L’exemple suivant illustre une information qui mappe la récence et la valeur monétaire d’un événement cible.

```python
# Proxy for monetary value is TOTAL_ORDER_REVENUE and proxy for frequency is NUMBER_VISITS
if len(Data) == 1:
    print(Fore.RED + '\033[1m' + 'THERE IS ONLY ONE PROFILE IN THE DATA, INSIGHTS ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE AT LEAST ONE MORE PROFILE TO FIND IMPORTANT VARIABLES')
elif len(Data['TARGET'].unique()) == 1:
    print(Fore.RED + '\033[1m' + 'TARGET HAS A SINGLE UNIQUE VALUE, INSIGHTS ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE PROFILES WITH ATLEAST ONE DIFFERENT VALUE OF TARGET TO FIND IMPORTANT VARIABLES')
else:
    sns.lmplot("DAYS_SINCE_VISIT", "TOTAL_ORDER_REVENUE", Data, hue="TARGET", fit_reg=False);
```

![exemple d’information](../images/jupyterlab/eda/insight.PNG)

## Étape facultative de nettoyage des données {#optional-data-clean}

Pour corriger les valeurs aberrantes, vous devez avoir une bonne compréhension de l’entreprise et de l’industrie dans lesquelles vous travaillez. Parfois, vous ne pouvez pas éliminer une observation juste parce que c’est une valeur aberrante. Les valeurs aberrantes peuvent être des observations légitimes et sont souvent les plus intéressantes.

Pour plus d’informations sur les valeurs aberrantes et pour savoir s’il faut les supprimer ou pas, lisez cette entrée de la section [facteur d’analyse](https://www.theanalysisfactor.com/outliers-to-drop-or-not-to-drop/).

L’exemple suivant contient des limites de cellule et des points de données Floor qui sont des valeurs aberrantes en utilisant un [écart interquartile](https://www.thoughtco.com/what-is-the-interquartile-range-rule-3126244).

```python
TARGET = Data.TARGET

Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
Data_numerical.drop(['TARGET'],axis = 1,inplace = True)

for i in range(0,len(Data_numerical.columns)):
    Q1 = Data_numerical.iloc[:,i].quantile(0.25)
    Q3 = Data_numerical.iloc[:,i].quantile(0.75)
    IQR = Q3 - Q1
    Data_numerical.iloc[:,i] = np.where(Data_numerical.iloc[:,i]<(Q1 - 1.5 * IQR), (Q1 - 1.5 * IQR), np.where(Data_numerical.iloc[:,i]>(Q3 + 1.5 * IQR),
                                                                                                     (Q3 + 1.5 * IQR),Data_numerical.iloc[:,i]))
Data_categorical = Data.select_dtypes(include='object')
Data = pd.concat([Data_categorical, Data_numerical, TARGET], axis = 1)
```

## Étapes suivantes

Une fois votre analyse de données exploratoires terminée, vous pouvez commencer à créer un modèle. Vous pouvez également utiliser les données et les informations que vous avez dérivées pour créer un tableau de bord avec des outils tels que Power BI.

Adobe Experience Platform sépare le processus de création de modèle en deux étapes distinctes : recettes (une instance de modèle) et modèles. Pour lancer le processus de création de recette, consultez la documentation de [création d’une recette dans les notebooks JupyerLab](./create-a-model.md). Ce document contient des informations et des exemples pour la création, la formation et la notation d’une recette dans les notebooks [!DNL JupyterLab].
