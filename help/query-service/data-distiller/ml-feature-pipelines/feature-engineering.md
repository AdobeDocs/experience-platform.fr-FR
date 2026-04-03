---
title: Fonctionnalités d’ingénierie pour le machine learning
description: Découvrez comment transformer les données de Adobe Experience Platform en fonctionnalités ou variables qui peuvent être utilisées par un modèle de machine learning. Utilisez Data Distiller pour calculer les fonctionnalités ML à grande échelle et partager ces fonctionnalités avec votre environnement de machine learning.
exl-id: 7fe017c9-ec46-42af-ac8f-734c4c6e24b5
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 13%

---

# Fonctionnalités d’ingénierie pour le machine learning

Ce document explique comment transformer les données de Adobe Experience Platform en **fonctionnalités** ou variables, qui peuvent être utilisées par un modèle de machine learning. Ce processus est appelé **ingénierie des fonctionnalités**. Utilisez Data Distiller pour calculer les fonctionnalités ML à grande échelle et partager ces fonctionnalités avec votre environnement de machine learning. Il s’agit des éléments suivants :

1. Créez un modèle de requête pour définir les libellés et les fonctions cibles à calculer pour votre modèle
2. Exécutez la requête et stockez les résultats dans un jeu de données d’entraînement

## Définir vos données d’identification {#define-training-data}

L’exemple suivant illustre une requête permettant d’extraire des données d’identification d’un jeu de données d’événements d’expérience pour un modèle afin de prédire la propension d’un utilisateur à s’abonner à une newsletter. Les événements d’abonnement sont représentés par le type d’événement `web.formFilledOut`. D’autres événements comportementaux du jeu de données sont utilisés pour dériver des fonctionnalités au niveau du profil afin de prédire les abonnements.

### Interroger les libellés positifs et négatifs {#query-positive-and-negative-labels}

Un jeu de données complet destiné à l’entraînement d’un modèle de machine learning (supervisé) comprend une variable cible ou un libellé qui représente le résultat à prédire, ainsi qu’un ensemble de fonctionnalités ou de variables explicatives utilisé pour décrire les exemples de profils utilisés pour entraîner le modèle.

Dans ce cas, le libellé est une variable appelée `subscriptionOccurred` qui est égale à 1 si le profil utilisateur comporte un événement de type `web.formFilledOut` , et à 0 dans les autres cas. La requête suivante renvoie un ensemble de 50 000 utilisateurs du jeu de données d’événements, y compris tous les utilisateurs avec des libellés positifs (`subscriptionOccurred = 1`) ainsi qu’un ensemble d’utilisateurs sélectionnés de manière aléatoire avec des libellés négatifs pour remplir la taille d’échantillon de 50 000 utilisateurs. Cela permet de s’assurer que les données de formation incluent des exemples positifs et négatifs pour que le modèle puisse en tirer des enseignements.

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)

query_labels = f"""
SELECT *
FROM (
    SELECT
        eventType,
        _{tenant_id}.user_id as userId,
        SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) 
            OVER (PARTITION BY _{tenant_id}.user_id) 
            AS "subscriptionOccurred",
        row_number() OVER (PARTITION BY _{tenant_id}.user_id ORDER BY randn()) AS random_row_number_for_user
    FROM {table_name}
)
WHERE (subscriptionOccurred = 1 AND eventType = 'web.formFilledOut') OR (subscriptionOccurred = 0 AND random_row_number_for_user = 1)
"""

df_labels = dd_cursor.query(query_labels, output="dataframe")
print(f"Number of classes: {len(df_labels)}")
df_labels.head()
```

**Exemple de sortie**

Nombre de classes : 50000

|   | eventType | userId | subscriptionOccurred | random_row_number_for_user |
| ---  |   ---  |   ---  |   ---  |   --- |
| 0 | directMarketing.emailClicked | 01027994177972439148069092698714414382 | 0 | 1 |
| 1 | directMarketing.emailOpened | 01054714817856066632264746967668888198 | 0 | 1 |
| 2 | web.formFilledOut | 01117296890525140996735553609305695042 | 1 | 15 |
| 3 | directMarketing.emailClicked | 01149554820363915324573708359099551093 | 0 | 1 |
| 4 | directMarketing.emailClicked | 01172121447143590196349410086995740317 | 0 | 1 |

{style="table-layout:auto"}

### Agréger les événements pour définir les fonctionnalités de ML {#define-features}

Avec une requête appropriée, vous pouvez rassembler les événements du jeu de données en fonctionnalités numériques significatives qui peuvent être utilisées pour entraîner un modèle de propension. Vous trouverez ci-dessous des exemples d’événements :

- **Nombre d’e-mails** envoyés à des fins marketing et reçus par l’utilisateur.
- Une partie de ces emails qui ont été **ouverts**.
- Partie de ces e-mails dans laquelle l’utilisateur **sélectionné** le lien.
- **Nombre de produits** consultés.
- Nombre de **propositions avec lesquelles il y a eu interaction**.
- Nombre de **propositions rejetées**.
- Nombre de **liens sélectionnés**.
- Nombre de minutes entre deux emails consécutifs reçus.
- Nombre de minutes entre deux ouvertures consécutives d’e-mails.
- Nombre de minutes entre deux e-mails consécutifs pendant lesquelles l’utilisateur a réellement sélectionné le lien.
- Nombre de minutes entre deux consultations consécutives du produit.
- Nombre de minutes entre deux propositions avec lesquelles il y a eu interaction.
- Nombre de minutes entre deux propositions qui ont été rejetées.
- Nombre de minutes entre deux liens sélectionnés.

La requête suivante agrège ces événements :

+++Sélectionner pour afficher un exemple de requête

```python
query_features = f"""
SELECT
    _{tenant_id}.user_id as userId,
    SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "emailsReceived",
    SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "emailsOpened",       
    SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "emailsClicked",       
    SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "productsViewed",       
    SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "propositionInteracts",       
    SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "propositionDismissed",
    SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "webLinkClicks" ,
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailSent', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_emailSent",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailOpened', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_emailOpened",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailClicked', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_emailClick",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'commerce.productViews', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_productView",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'decisioning.propositionInteract', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_propositionInteract",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'propositionDismiss', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_propositionDismiss",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'web.webinteraction.linkClicks', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_linkClick"
FROM {table_name}
"""

df_features = dd_cursor.query(query_features, output="dataframe")
df_features.head()
```

+++

**Exemple de sortie**

|   | userId | emailsReceived | emailsOpened | emailsClicked | productsViewed | propositionInteracts | propositionRejetée | webLinkClicks | minutes_Since_emailSent | minutes_Since_emailOpened | minutes_Since_emailClick | minutes_Since_productView | minutes_Since_propositionInteract | minutes_Since_propositionDismiss | minutes_Since_linkClick |
| --- |    --- |    ---   |  ---  |   ---  |   ---  |  ---  |  ---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---  |   --- |
| 0 | 01102546977582484968046916668339306826 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0,0 | NaN | NaN | NaN | NaN | Aucune | NaN |
| 1 | 01102546977582484968046916668339306826 | 2 | 0 | 0 | 0 | 0 | 0 | 0 | 0,0 | NaN | NaN | NaN | NaN | Aucune | NaN |
| 2 | 01102546977582484968046916668339306826 | 3 | 0 | 0 | 0 | 0 | 0 | 0 | 0,0 | NaN | NaN | NaN | NaN | Aucune | NaN |
| 3 | 01102546977582484968046916668339306826 | 3 | 1 | 0 | 0 | 0 | 0 | 0 | 540,0 | 0,0 | NaN | NaN | NaN | Aucune | NaN |
| 4 | 01102546977582484968046916668339306826 | 3 | 2 | 0 | 0 | 0 | 0 | 0 | 588,0 | 0,0 | NaN | NaN | NaN | Aucune | NaN |

{style="table-layout:auto"}

#### Combiner des requêtes de libellés et de fonctionnalités {#combine-queries}

Enfin, la requête de libellés et la requête de fonctionnalités peuvent être combinées en une seule requête qui renvoie un jeu de données d’entraînement de libellés et de fonctionnalités :

+++Sélectionner pour afficher un exemple de requête

```python
query_training_set = f"""
SELECT *
FROM (
    SELECT _{tenant_id}.user_id as userId, 
       eventType,
       timestamp,
       SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id) 
           AS "subscriptionOccurred",
       SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsReceived",
       SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsOpened",       
       SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsClicked",       
       SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "productsViewed",       
       SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionInteracts",       
       SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionDismissed",
       SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "webLinkClicks" ,
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailSent', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailSent",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailOpened', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailOpened",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailClicked', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailClick",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'commerce.productViews', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_productView",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'decisioning.propositionInteract', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionInteract",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'propositionDismiss', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionDismiss",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'web.webinteraction.linkClicks', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_linkClick",
        row_number() OVER (PARTITION BY _{tenant_id}.user_id ORDER BY randn()) AS random_row_number_for_user
    FROM {table_name} LIMIT 1000
)
WHERE (subscriptionOccurred = 1 AND eventType = 'web.formFilledOut') OR (subscriptionOccurred = 0 AND random_row_number_for_user = 1)
ORDER BY timestamp
"""

df_training_set = dd_cursor.query(query_training_set, output="dataframe")
df_training_set.head()
```

+++

**Exemple de sortie**

|  | userId | eventType | date et heure | subscriptionOccurred | emailsReceived | emailsOpened | emailsClicked | productsViewed | propositionInteracts | propositionRejetée | webLinkClicks | minutes_Since_emailSent | minutes_Since_emailOpened | minutes_Since_emailClick | minutes_Since_productView | minutes_Since_propositionInteract | minutes_Since_propositionDismiss | minutes_Since_linkClick | random_row_number_for_user |
| ---  |  --- |   ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---   | ---  |  ---  |  ---  |  --- |
| 0 | 02554909162592418347780983091131567290 | directMarketing.emailSent | 17/06/2023 13:44:59,086 | 0 | 2 | 0 | 0 | 0 | 0 | 0 | 0 | 0,0 | NaN | NaN | NaN | NaN | Aucune | NaN | 1 |
| 1 | 01130334080340815140184601481559659945 | directMarketing.emailOpened | 2023-06-19 06:01:55.366 | 0 | 1 | 3 | 0 | 1 | 0 | 0 | 0 | 1921,0 | 0,0 | NaN | 1703,0 | NaN | Aucune | NaN | 1 |
| 2 | 01708961660028351393477273586554010192 | web.formFilledOut | 19/06/2023 18:36:49,083 | 1 | 1 | 2 | 2 | 0 | 0 | 0 | 0 | 2365,0 | 26,0 | 1.0 | NaN | NaN | Aucune | NaN | 7 |
| 3 | 01809182902320674899156240602124740853 | directMarketing.emailSent | 21/06/2023 19:17:12,535 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0,0 | NaN | NaN | NaN | NaN | Aucune | NaN | 1 |
| 4 | 03441761949943678951106193028739001197 | directMarketing.emailSent | 21/06/2023 21:58:29.482 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0,0 | NaN | NaN | NaN | NaN | Aucune | NaN | 1 |

{style="table-layout:auto"}

## Créer un modèle de requête pour calculer de manière incrémentielle les données d’identification

Il est courant de recycler périodiquement un modèle avec des données d’apprentissage mises à jour pour maintenir la précision du modèle au fil du temps. Comme bonne pratique pour mettre à jour efficacement votre jeu de données d’entraînement, vous pouvez créer un modèle à partir de votre requête de jeu d’entraînement pour calculer de nouvelles données d’entraînement de manière incrémentielle. Cela vous permet de calculer les libellés et les fonctionnalités uniquement à partir des données qui ont été ajoutées au jeu de données d’événements d’expérience d’origine depuis la dernière mise à jour des données d’entraînement, et d’insérer les nouveaux libellés et fonctionnalités dans le jeu de données d’entraînement existant.

Pour ce faire, quelques modifications doivent être apportées à la requête du jeu de formation :

- Ajoutez une logique pour créer un jeu de données d’entraînement s’il n’existe pas, et insérez les nouveaux libellés et fonctionnalités dans le jeu de données d’entraînement existant dans le cas contraire. Cela nécessite une série de deux versions de la requête du jeu d’entraînement :
   - Tout d’abord, utilisez l’instruction `CREATE TABLE IF NOT EXISTS {table_name} AS` .
   - Ensuite, utilisez l’instruction `INSERT INTO {table_name}` dans le cas où le jeu de données d’entraînement existe déjà
- Ajoutez une instruction `SNAPSHOT BETWEEN $from_snapshot_id AND $to_snapshot_id` pour limiter la requête aux données d’événement ajoutées au cours d’un intervalle spécifié. Le préfixe `$` sur les ID d’instantané indique qu’il s’agit de variables qui seront transmises lors de l’exécution du modèle de requête.

L’application de ces modifications génère la requête suivante :

+++Sélectionner pour afficher un exemple de requête

```python
ctas_table_name = "propensity_training_set"

query_training_set_template = f"""
$$ BEGIN

SET @my_table_exists = SELECT table_exists('{ctas_table_name}');

CREATE TABLE IF NOT EXISTS {ctas_table_name} AS
SELECT *
FROM (
    SELECT _{tenant_id}.user_id as userId, 
       eventType,
       timestamp,
       SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id) 
           AS "subscriptionOccurred",
       SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsReceived",
       SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsOpened",       
       SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsClicked",       
       SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "productsViewed",       
       SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionInteracts",       
       SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionDismissed",
       SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "webLinkClicks" ,
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailSent', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailSent",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailOpened', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailOpened",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailClicked', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailClick",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'commerce.productViews', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_productView",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'decisioning.propositionInteract', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionInteract",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'propositionDismiss', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionDismiss",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'web.webinteraction.linkClicks', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_linkClick",
        row_number() OVER (PARTITION BY _{tenant_id}.user_id ORDER BY randn()) AS random_row_number_for_user
    FROM {table_name}
    SNAPSHOT BETWEEN $from_snapshot_id AND $to_snapshot_id
)
WHERE (subscriptionOccurred = 1 AND eventType = 'web.formFilledOut') OR (subscriptionOccurred = 0 AND random_row_number_for_user = 1)
ORDER BY timestamp;

INSERT INTO {ctas_table_name}
SELECT *
FROM (
    SELECT _{tenant_id}.user_id as userId, 
       eventType,
       timestamp,
       SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id) 
           AS "subscriptionOccurred",
       SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsReceived",
       SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsOpened",       
       SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsClicked",       
       SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "productsViewed",       
       SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionInteracts",       
       SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionDismissed",
       SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "webLinkClicks" ,
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailSent', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailSent",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailOpened', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailOpened",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailClicked', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailClick",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'commerce.productViews', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_productView",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'decisioning.propositionInteract', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionInteract",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'propositionDismiss', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionDismiss",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'web.webinteraction.linkClicks', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_linkClick",
        row_number() OVER (PARTITION BY _{tenant_id}.user_id ORDER BY randn()) AS random_row_number_for_user
    FROM {table_name}
    SNAPSHOT BETWEEN $from_snapshot_id AND $to_snapshot_id
)
WHERE 
    @my_table_exists = 't' AND
    ((subscriptionOccurred = 1 AND eventType = 'web.formFilledOut') OR (subscriptionOccurred = 0 AND random_row_number_for_user = 1))
ORDER BY timestamp;

EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';

END $$;
"""
```

+++

Enfin, le code suivant enregistre le modèle de requête dans la Distiller de données :

```python
template_res = dd.createQueryTemplate({
  "sql": query_training_set_template,
  "queryParameters": {},
  "name": "Template for propensity training data"
})
template_id = template_res["id"]

print(f"Template for propensity training data created as ID {template_id}")
```

**Exemple de sortie**

`Template for propensity training data created as ID f3d1ec6b-40c2-4d13-93b6-734c1b3c7235`

Une fois le modèle enregistré, vous pouvez exécuter la requête à tout moment en référençant l’ID du modèle et en spécifiant la plage d’ID d’instantané qui doit être incluse dans la requête. La requête suivante récupère les instantanés du jeu de données d’événements d’expérience d’origine :

```python
query_snapshots = f"""
SELECT snapshot_id 
FROM (
    SELECT history_meta('{table_name}')
) 
WHERE is_current = true OR snapshot_generation = 0 
ORDER BY snapshot_generation ASC
"""

df_snapshots = dd_cursor.query(query_snapshots, output="dataframe")
```

Le code suivant illustre l’exécution du modèle de requête, à l’aide des premier et dernier instantanés pour interroger l’ensemble du jeu de données :

```python
snapshot_start_id = str(df_snapshots["snapshot_id"].iloc[0])
snapshot_end_id = str(df_snapshots["snapshot_id"].iloc[1])

query_final_res = qs.postQueries(
    name=f"[CMLE][Week2] Query to generate training data created by {username}",
    templateId=template_id,
    queryParameters={
        "from_snapshot_id": snapshot_start_id,
        "to_snapshot_id": snapshot_end_id,
    },
    dbname=f"{cat_conn.sandbox}:all"
)
query_final_id = query_final_res["id"]
print(f"Query started successfully and got assigned ID {query_final_id} - it will take some time to execute")
```

**Exemple de sortie**

`Query started successfully and got assigned ID c6ea5009-1315-4839-b072-089ae01e74fd - it will take some time to execute`

Vous pouvez définir la fonction suivante pour vérifier régulièrement le statut de la requête :

```python
def wait_for_query_completion(query_id):
    while True:
        query_info = qs.getQuery(query_id)
        query_state = query_info["state"]
        if query_state in ["SUCCESS", "FAILED"]:
            break
        print("Query is still in progress, sleeping…")
        time.sleep(60)

    duration_secs = query_info["elapsedTime"] / 1000
    if query_state == "SUCCESS":
        print(f"Query completed successfully in {duration_secs} seconds")
    else:
        print(f"Query failed with the following errors:", file=sys.stderr)
        for error in query_info["errors"]:
            print(f"Error code {error['code']}: {error['message']}", file=sys.stderr)

wait_for_query_completion(query_final_id)
```

**Exemple de sortie**

```console
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query completed successfully in 473.8 seconds
```

## Étapes suivantes :

En lisant ce document, vous avez appris à transformer les données de Adobe Experience Platform en fonctionnalités, ou variables, qui peuvent être utilisées par un modèle de machine learning. L’étape suivante de la création de pipelines de fonctionnalités à partir d’Experience Platform pour alimenter des modèles personnalisés dans votre environnement de machine learning consiste à [exporter des jeux de données de fonctionnalités](./export-data.md).
