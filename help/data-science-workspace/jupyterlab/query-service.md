---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;rubriques les plus consultées;service de requête
solution: Experience Platform
title: Query Service dans Jupyter Notebook
type: Tutorial
description: Adobe Experience Platform vous permet d’utiliser le langage de requête structuré (SQL) dans l’espace de travail de science des données en intégrant Query Service à JupyterLab en tant que fonctionnalité standard. Ce tutoriel présente des exemples de requêtes SQL pour des cas d’utilisation courants afin d’explorer, de transformer et d’analyser les données Adobe Analytics.
exl-id: c5ac7d11-a3bd-4ef8-a650-9f496a8bbaa7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 60%

---

# Query Service dans Jupyter Notebook

[!DNL Adobe Experience Platform] vous permet d’utiliser le langage de requête structuré (SQL) dans [!DNL Data Science Workspace] par intégration [!DNL Query Service] into [!DNL JupyterLab] en tant que fonctionnalité standard.

Ce tutoriel présente des exemples de requêtes SQL pour des cas d’utilisation courants afin d’explorer, de transformer et d’analyser [!DNL Adobe Analytics] data.

## Prise en main

Avant de commencer ce tutoriel, vous devez disposer des éléments suivants :

- Accès à [!DNL Adobe Experience Platform]. Si vous n’avez pas accès à une organisation dans [!DNL Experience Platform], contactez votre administrateur système avant de poursuivre

- Un [!DNL Adobe Analytics] dataset

- Une connaissance concrète des concepts clés suivants employés dans ce tutoriel :
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## Accès [!DNL JupyterLab] et [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. Dans [[!DNL Experience Platform]](https://platform.adobe.com), accédez à **[!UICONTROL Notebooks]** dans la colonne de navigation de gauche. Laissez charger JupyterLab.

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >Si un nouvel onglet de lanceur n’apparaît pas automatiquement, ouvrez un nouvel onglet de lanceur en cliquant sur **[!UICONTROL Fichier]** puis sélectionnez **[!UICONTROL Nouveau lanceur]**.

2. Dans l’onglet de lanceur, cliquez sur l’icône **[!UICONTROL Vierge]** dans un environnement Python 3 pour ouvrir un notebook vierge.

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3 est actuellement le seul environnement pris en charge pour Query Service dans les notebooks.

3. Dans le rail de sélection de gauche, cliquez sur l’icône **[!UICONTROL Données]** et double-cliquez sur le répertoire **[!UICONTROL Jeux de données]** pour afficher sous forme de liste tous les jeux de données.

   ![](../images/jupyterlab/query/dataset.png)

4. Rechercher une [!DNL Adobe Analytics] jeu de données à explorer et cliquez avec le bouton droit sur la liste, cliquez sur **[!UICONTROL Données de requête dans Notebook]** pour générer des requêtes SQL dans le notebook vide.

5. Cliquez sur la première cellule générée contenant la fonction `qs_connect()` et exécutez-la en cliquant sur le bouton de lecture. Cette fonction crée une connexion entre votre instance de notebook et [!DNL Query Service].

   ![](../images/jupyterlab/query/execute.png)

6. Copiez le [!DNL Adobe Analytics] nom du jeu de données de la seconde requête SQL générée, il s’agira de la valeur suivant `FROM`.

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

   - `target_table`: Nom de votre [!DNL Adobe Analytics] jeu de données.
   - `target_year` : année spécifique de laquelle proviennent les données cibles.
   - `target_month` : mois spécifique duquel provient la cible.
   - `target_day` : jour spécifique d’où proviennent les données cibles.

   >[!NOTE]
   >
   >Vous pouvez modifier ces valeurs à tout moment. Dans ce cas, veillez à exécuter la cellule de variables afin que les modifications soient appliquées.

## Interrogation de vos données {#query-your-data}

Entrez les requêtes SQL suivantes dans des cellules de notebook distinctes. Exécutez une requête en la sélectionnant dans sa cellule, puis en sélectionnant le champ **[!UICONTROL play]** bouton . Les résultats des requêtes réussies ou les journaux d’erreurs sont affichés sous la cellule exécutée.

Lorsqu’un notebook est inactif pendant une longue période, la connexion entre le notebook et [!DNL Query Service] peut rompre. Dans ce cas, redémarrez. [!DNL JupyterLab] en sélectionnant l’option **Redémarrer** button ![bouton de redémarrage](../images/jupyterlab/user-guide/restart_button.png) situé dans le coin supérieur droit à côté du bouton d’alimentation.

Le noyau du notebook se réinitialise, mais les cellules restent, exécutez à nouveau toutes les cellules pour continuer là où vous vous êtes arrêté.

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
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

Dans la requête ci-dessus, l’horodatage de la variable `WHERE` est définie sur comme étant la valeur de `target_year`. Incluez des variables dans les requêtes SQL en les insérant entre parenthèses (`{}`).

La première ligne de la requête contient la variable facultative `hourly_visitor`. Les résultats des requêtes seront stockés dans cette variable sous la forme d’un cadre de données pandas. Le stockage des résultats dans un cadre de données vous permet de visualiser ultérieurement les résultats de la requête à l’aide d’une [!DNL Python] module. Exécutez les opérations suivantes [!DNL Python] code dans une nouvelle cellule pour générer un graphique à barres :

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
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
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

L&#39;exécution de la requête modifiée stocke les résultats dans `hourly_actions_date_range` comme cadre de données. Exécutez la fonction suivante dans une nouvelle cellule pour prévisualiser les résultats :

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
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

Exécutez les opérations suivantes [!DNL Python] afin de générer un histogramme pour le nombre d’événements par session de visite :

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
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
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
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
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
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## Étapes suivantes

Ce tutoriel a présenté quelques exemples d’utilisation de [!DNL Query Service] in [!DNL Jupyter] notebooks. Suivez le tutoriel [Analyser vos données à l’aide des notebooks Jupyter](./analyze-your-data.md) pour découvrir la manière dont des opérations similaires sont exécutées à l’aide du SDK d’accès aux données.
