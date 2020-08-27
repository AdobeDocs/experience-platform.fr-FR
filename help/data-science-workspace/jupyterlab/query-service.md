---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;query service
solution: Experience Platform
title: Query Service dans les notebooks Jupyter
topic: Tutorial
description: Adobe Experience Platform vous permet d’utiliser le langage de requête structuré (SQL) dans Data Science Workspace en intégrant Query Service à JupyterLab en tant que fonctionnalité standard. Ce didacticiel présente des exemples de requêtes SQL pour des cas d'utilisation courants afin d'explorer, de transformer et d'analyser les données Adobe Analytics.
translation-type: tm+mt
source-git-commit: 43d568a401732a753553847dee1b4a924fcc24fd
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 68%

---


# Query Service dans les notebooks Jupyter

[!DNL Adobe Experience Platform] vous permet d&#39;utiliser le langage SQL (Structured Requête Language) dans [!DNL Data Science Workspace] en intégrant [!DNL Query Service] en tant que fonction [!DNL JupyterLab] standard.

This tutorial demonstrates sample SQL queries for common use cases to explore, transform, and analyze [!DNL Adobe Analytics] data.

## Prise en main

Avant de commencer ce tutoriel, vous devez disposer des éléments suivants :

- Accès à [!DNL Adobe Experience Platform]. If you do not have access to an IMS Organization in [!DNL Experience Platform], please speak to your system administrator before proceeding

- Un [!DNL Adobe Analytics] jeu de données

- Une connaissance concrète des concepts clés suivants employés dans ce tutoriel :
   - [[ ! Modèle de données d’expérience DNL (XDM) et système XDM]](../../xdm/home.md)
   - [[ !Service de Requête DNL]](../../query-service/home.md)
   - [[ !Syntaxe SQL du service de Requête DNL]](../../query-service/sql/overview.md)
   - [Adobe Analytics]

## Accès [!DNL JupyterLab] et [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. In [[!DNL Experience Platform]](https://platform.adobe.com), navigate to **[!UICONTROL Notebooks]** from the left navigation column. Laissez charger JupyterLab.

   ![](../images/jupyterlab/query/jupyterlab_launcher.png)

   >[!NOTE]
   >
   >If a new Launcher tab did not automatically appear, open a new Launcher tab by clicking **[!UICONTROL File]** then select **[!UICONTROL New Launcher]**.

2. Dans l’onglet de lanceur, cliquez sur l’icône **[!UICONTROL Vierge]** dans un environnement Python 3 pour ouvrir un notebook vierge.

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3 est actuellement le seul environnement pris en charge pour Query Service dans les notebooks.

3. Dans le rail de sélection de gauche, cliquez sur l’icône **[!UICONTROL Données]** et double-cliquez sur le répertoire **[!UICONTROL Jeux de données]** pour afficher sous forme de liste tous les jeux de données.

   ![](../images/jupyterlab/query/dataset.png)

4. Find an [!DNL Adobe Analytics] dataset to explore and right-click on the listing, click **[!UICONTROL Query Data in Notebook]** to generate SQL queries in the empty notebook.

5. Cliquez sur la première cellule générée contenant la fonction `qs_connect()` et exécutez-la en cliquant sur le bouton de lecture. Cette fonction crée une connexion entre votre instance de notebook et [!DNL Query Service].

   ![](../images/jupyterlab/query/execute.png)

6. Copy down the [!DNL Adobe Analytics] dataset name from the second generated SQL query, it will be the value after `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. Insérez une nouvelle cellule de notebook en cliquant sur le bouton **+**.

   ![](../images/jupyterlab/query/insert_cell.gif)

8. Copiez, collez et exécutez les instructions d’importation suivantes dans une nouvelle cellule. Ces instructions seront utilisées pour visualiser vos données :

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. Ensuite, copiez et collez les variables suivantes dans une nouvelle cellule. Modifiez leur valeur en fonction de vos besoins, puis exécutez-les.

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table` : Nom de votre [!DNL Adobe Analytics] jeu de données.
   - `target_year` : année spécifique de laquelle proviennent les données cibles.
   - `target_month` : mois spécifique duquel provient la cible.
   - `target_day` : jour spécifique d’où proviennent les données cibles.

   >[!NOTE]
   >
   >Vous pouvez modifier ces valeurs à tout moment. Dans ce cas, veillez à exécuter la cellule de variables afin que les modifications soient appliquées.

## Interrogation de vos données {#query-your-data}

Entrez les requêtes SQL suivantes dans des cellules de notebook distinctes. Exécutez une requête en cliquant sur sa cellule, puis sur le bouton de **[!UICONTROL lecture]**. Les résultats des requêtes réussies ou les journaux d’erreurs sont affichés sous la cellule exécutée.

When a notebook is inactive for an extended period of time, the connection between the notebook and [!DNL Query Service] may break. In such cases, restart [!DNL JupyterLab] by clicking the **[!UICONTROL Power]** button located at the top right corner.

![](../images/jupyterlab/query/restart_button.png)

Le noyau du notebook sera réinitialisé, mais les cellules seront conservées. Exécutez de nouveau **[!UICONTROL toutes]** les cellules pour reprendre là où vous vous étiez arrêté.

### Décompte horaire de visiteurs {#hourly-visitor-count}

La requête suivante renvoie le décompte horaire de visiteurs pour une date spécifique :

#### Requête

```sql
%%read_sql hourly_visitor -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                               AS Day,
       Substring(timestamp, 12, 2)                               AS Hour, 
       Count(DISTINCT concat(enduserids._experience.aaid.id, 
                             _experience.analytics.session.num)) AS Visit_Count 
FROM   {target_table}
WHERE _acp_year = {target_year} 
      AND _acp_month = {target_month}  
      AND _acp_day = {target_day}
GROUP  BY Day, Hour
ORDER  BY Hour;
```

Dans la requête ci-dessus, le `_acp_year` cible dans la clause `WHERE` est défini comme la valeur `target_year`. Incluez des variables dans les requêtes SQL en les insérant entre parenthèses (`{}`).

La première ligne de la requête contient la variable facultative `hourly_visitor`. Les résultats des requêtes seront stockés dans cette variable sous la forme d’un cadre de données pandas. Storing results in a dataframe allows you to later visualize the query results using a desired [!DNL Python] package. Execute the following [!DNL Python] code in a new cell to generate a bar graph:

```python
trace = go.Bar(
    x = hourly_visitor['Hour'],
    y = hourly_visitor['Visit_Count'],
    name = "Visitor Count"
)
layout = go.Layout(
    title = 'Visit Count by Hour of Day',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Hour of Day'),
    yaxis = dict(title = 'Count')
)
fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

### Décompte horaire de l’activité {#hourly-activity-count}

La requête suivante renvoie le décompte horaire d’actions pour une date spécifique :

#### Requête <!-- omit in toc -->

```sql
%%read_sql hourly_actions -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE  _acp_year = {target_year} 
       AND _acp_month = {target_month}  
       AND _acp_day = {target_day}
GROUP  BY Day, Hour
ORDER  BY Hour;
```

L’exécution de la requête ci-dessus stockera les résultats dans `hourly_actions` en tant que cadre de données. Exécutez la fonction suivante dans une nouvelle cellule pour prévisualiser les résultats :

```python
hourly_actions.head()
```

La requête ci-dessus peut être modifiée pour renvoyer le décompte horaire d’actions pour une période spécifique à l’aide d’opérateurs logiques dans la clause **WHERE** :

#### Requête <!-- omit in toc -->

```sql
%%read_sql hourly_actions_date_range -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE  timestamp >= TO_TIMESTAMP('2019-06-01 00', 'YYYY-MM-DD HH')
       AND timestamp <= TO_TIMESTAMP('2019-06-02 23', 'YYYY-MM-DD HH')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

L’exécution de la requête modifiée stockera les résultats dans `hourly_actions_date_range` en tant que cadre de données. Exécutez la fonction suivante dans une nouvelle cellule pour prévisualiser les résultats :

```python
hourly_actions_date_rage.head()
```

### Décompte d’événements par visite {#number-of-events-per-visitor-session}

La requête suivante renvoie le décompte d’événements par visite pour une date spécifique :

#### Requête <!-- omit in toc -->

```sql
%%read_sql events_per_session -c QS_CONNECTION
SELECT concat(enduserids._experience.aaid.id, 
              '-#', 
              _experience.analytics.session.num) AS aaid_sess_key, 
       Count(timestamp)                          AS Count 
FROM   {target_table}
WHERE  _acp_year = {target_year} 
       AND _acp_month = {target_month}  
       AND _acp_day = {target_day}
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

Execute the following [!DNL Python] code to generate a histogram for the number of events per visit session:

```python
data = [go.Histogram(x = events_per_session['Count'])]

layout = go.Layout(
    title = 'Histogram of Number of Events per Visit Session',
    xaxis = dict(title = 'Number of Events'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = data, layout = layout)
iplot(fig)
```

### Pages les plus consultées pour un jour spécifique {#popular-pages-for-a-given-day}

La requête suivante renvoie les dix pages les plus consultées pour une date spécifique :

#### Requête <!-- omit in toc -->

```sql
%%read_sql popular_pages -c QS_CONNECTION
SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

### Utilisateurs actifs pour un jour spécifique {#active-users-for-a-given-day}

La requête suivante renvoie les dix utilisateurs les plus actifs pour une date spécifique :

#### Requête <!-- omit in toc -->

```sql
%%read_sql active_users -c QS_CONNECTION
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp)               AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY aaid
ORDER  BY Count DESC
LIMIT  10;
```

### Villes actives par activité d’utilisateur {#active-cities-by-user-activity}

La requête suivante renvoie les dix villes qui génèrent la majorité des activités d’utilisateur pour une date spécifique :

#### Requête <!-- omit in toc -->

```sql
%%read_sql active_cities -c QS_CONNECTION
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## Étapes suivantes <!-- omit in toc -->

This tutorial demonstrated some sample uses cases for utilizing [!DNL Query Service] in [!DNL Jupyter] notebooks. Suivez le tutoriel [Analyser vos données à l’aide des notebooks Jupyter](./analyze-your-data.md) pour découvrir la manière dont des opérations similaires sont exécutées à l’aide du SDK d’accès aux données.