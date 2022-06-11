---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;Query Service;fonctions définies par adobe;sql;
solution: Experience Platform
title: Fonctions SQL définies par Adobe dans Query Service
topic-legacy: functions
description: Ce document fournit des informations sur les fonctions définies par Adobe disponibles dans Adobe Experience Platform Query Service.
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
source-git-commit: e0cdfc514a9e1277134d4c0d5396fc0bdf9d9958
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 19%

---

# Fonctions SQL définies par l’Adobe dans Query Service

Les fonctions définies par l’Adobe, ici appelées ADF, sont des fonctions prédéfinies de Adobe Experience Platform Query Service qui permettent d’effectuer des tâches commerciales courantes sur [!DNL Experience Event] data. Ces fonctions incluent des fonctions pour [Sessionization](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) et [Attribution](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=fr) comme dans Adobe Analytics.

Ce document fournit des informations sur les fonctions définies par Adobe disponibles dans [!DNL Query Service].

## Fonctions de fenêtre {#window-functions}

La majeure partie de la logique commerciale exige de rassembler les points de contact d’un client et de les classer par heure. Cette prise en charge est assurée par [!DNL Spark] SQL sous la forme de fonctions de fenêtre. Les fonctions de fenêtre font partie du langage SQL standard et sont prises en charge par de nombreux autres moteurs SQL.

Une fonction de fenêtre met à jour une agrégation et renvoie un élément unique pour chaque ligne de votre sous-ensemble classé. `SUM()` est la fonction d’agrégation la plus élémentaire. `SUM()` additionne vos lignes et fournit un total. Si vous appliquez plutôt `SUM()` à une fenêtre, la transformant ainsi en fonction de fenêtre, vous recevez une somme cumulée pour chaque ligne.

La majorité des [!DNL Spark] Les assistants SQL sont des fonctions de fenêtre qui mettent à jour chaque ligne de la fenêtre, l’état de cette ligne étant ajouté.

**Syntaxe de la requête**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description | Exemple |
| --------- | ----------- | ------- |
| `{PARTITION}` | Sous-groupe de lignes basé sur une colonne ou un champ disponible. | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | Une colonne ou un champ disponible utilisé pour classer le sous-ensemble ou les lignes. | `ORDER BY timestamp` |
| `{FRAME}` | Un sous-groupe des lignes d’une partition. | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessionisation

Lorsque vous utilisez [!DNL Experience Event] données provenant d’un site web, d’une application mobile, d’un système interactif de réponse vocale ou de tout autre canal d’interaction client, il est utile de regrouper les événements autour d’une période d’activité connexe. Généralement, une intention spécifique oriente votre activité, comme la recherche d’un produit, le paiement d’une facture, la vérification du solde d’un compte, le remplissage d’une demande, etc.

Ce regroupement, ou sessionisation des données, permet d’associer les événements pour découvrir plus de contexte sur l’expérience client.

Pour plus d’informations sur la mise en session dans Adobe Analytics, consultez la documentation sur [sessions contextuelles](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html).

**Syntaxe de la requête**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description |
| --------- | ----------- |
| `{TIMESTAMP}` | Champ d’horodatage trouvé dans le jeu de données. |
| `{EXPIRATION_IN_SECONDS}` | Nombre de secondes nécessaires entre les événements pour qualifier la fin de la session en cours et le début d’une nouvelle session. |

Une explication des paramètres de la variable `OVER()` se trouve dans la fonction [section fonctions de fenêtre](#window-functions).

**Exemple de requête**

```sql
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp,
  SESS_TIMEOUT(timestamp, 60 * 30)
    OVER (PARTITION BY endUserIds._experience.mcid.id
        ORDER BY timestamp
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS session
FROM experience_events
ORDER BY id, timestamp ASC
LIMIT 10
```

**Résultats**

```console
                id                |       timestamp       |      session       
----------------------------------+-----------------------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | (40,1,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | (55,1,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | (1361821,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | (54,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | (49,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | (33,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | (31,2,false,5)
(10 rows)
```

Pour l’exemple de requête donné, les résultats sont donnés dans la variable `session` colonne . Le `session` est composée des composants suivants :

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Paramètres | Description |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | La différence de temps, en secondes, entre l’enregistrement actif et l’enregistrement précédent. |
| `{NUM}` | Un numéro de session unique, commençant à 1, pour la clé définie dans la variable `PARTITION BY` de la fonction window. |
| `{IS_NEW}` | Une valeur booléenne utilisée pour déterminer si un enregistrement est le premier d’une session. |
| `{DEPTH}` | Profondeur de l’enregistrement actif dans la session. |

### SESS_START_IF

Cette requête renvoie l’état de la session pour la ligne actuelle, en fonction de l’horodatage actuel et de l’expression donnée et lance une nouvelle session avec la ligne actuelle.

**Syntaxe de la requête**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description |
| --------- | ----------- |
| `{TIMESTAMP}` | Champ d’horodatage trouvé dans le jeu de données. |
| `{TEST_EXPRESSION}` | Une expression par rapport à laquelle vous souhaitez vérifier les champs des données. Par exemple : `application.launches > 0`. |

Une explication des paramètres de la variable `OVER()` se trouve dans la fonction [section fonctions de fenêtre](#window-functions).

**Exemple de requête**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.launches.value > 0, true, false) AS isLaunch,
    SESS_START_IF(timestamp, application.launches.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**Résultats**

```console
                id                |       timestamp       | isLaunch |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | true     | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | false    | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | true     | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

Pour l’exemple de requête donné, les résultats sont donnés dans la variable `session` colonne . Le `session` est composée des composants suivants :

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Paramètres | Description |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | La différence de temps, en secondes, entre l’enregistrement actif et l’enregistrement précédent. |
| `{NUM}` | Un numéro de session unique, commençant à 1, pour la clé définie dans la variable `PARTITION BY` de la fonction window. |
| `{IS_NEW}` | Une valeur booléenne utilisée pour déterminer si un enregistrement est le premier d’une session. |
| `{DEPTH}` | Profondeur de l’enregistrement actif dans la session. |

### SESS_END_IF

Cette requête renvoie l’état de la session pour la ligne en cours, en fonction de l’horodatage actuel et de l’expression donnée, met fin à la session en cours et lance une nouvelle session sur la ligne suivante.

**Syntaxe de la requête**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description |
| --------- | ----------- |
| `{TIMESTAMP}` | Champ d’horodatage trouvé dans le jeu de données. |
| `{TEST_EXPRESSION}` | Une expression par rapport à laquelle vous souhaitez vérifier les champs des données. Par exemple : `application.launches > 0`. |

Une explication des paramètres de la variable `OVER()` se trouve dans la fonction [section fonctions de fenêtre](#window-functions).

**Exemple de requête**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.applicationCloses.value > 0 OR application.crashes.value > 0, true, false) AS isExit,
    SESS_END_IF(timestamp, application.applicationCloses.value > 0 OR application.crashes.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**Résultats**

```console
                id                |       timestamp       | isExit   |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | false    | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | true     | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | false    | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

Pour l’exemple de requête donné, les résultats sont donnés dans la variable `session` colonne . Le `session` est composée des composants suivants :

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Paramètres | Description |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | La différence de temps, en secondes, entre l’enregistrement actif et l’enregistrement précédent. |
| `{NUM}` | Un numéro de session unique, commençant à 1, pour la clé définie dans la variable `PARTITION BY` de la fonction window. |
| `{IS_NEW}` | Une valeur booléenne utilisée pour déterminer si un enregistrement est le premier d’une session. |
| `{DEPTH}` | Profondeur de l’enregistrement actif dans la session. |


## Cheminement

Le cheminement peut être utilisé pour comprendre la profondeur de l’engagement du client, confirmer que les étapes prévues d’une expérience fonctionnent comme prévu et identifier les éventuels problèmes affectant le client.

Les fonctions définies par Adobe suivantes prennent en charge l’établissement de vues de cheminement à partir de leurs relations précédentes et suivantes. Vous pourrez créer des pages précédentes et des pages suivantes ou parcourir plusieurs événements pour créer un cheminement.

### Page précédente

Détermine la valeur précédente d’un champ donné avec un nombre défini d’étapes restantes dans la fenêtre. Dans l’exemple, notez que la variable `WINDOW` est configurée avec un cadre de `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` paramétrer la fonction définie par Adobe pour qu’elle examine la ligne actuelle et toutes les lignes suivantes.

**Syntaxe de la requête**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description |
| --------- | ----------- |
| `{KEY}` | La colonne ou le champ de l’événement. |
| `{SHIFT}` | (Facultatif) Le nombre d’événements en dehors de l’événement en cours. Par défaut, la valeur est 1. |
| `{IGNORE_NULLS}` | (Facultatif) Une valeur booléenne qui indique si la valeur est nulle `{KEY}` doivent être ignorées. Par défaut, la valeur est `false`. |

Une explication des paramètres de la variable `OVER()` se trouve dans la fonction [section fonctions de fenêtre](#window-functions).

**Exemple de requête**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Résultats**

```console
                id                 |       timestamp       |                 name                |                    previous_page                    
-----------------------------------+-----------------------+-------------------------------------+-----------------------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Cart Details)
(10 rows)
```

Pour l’exemple de requête donné, les résultats sont donnés dans la variable `previous_page` colonne . La valeur de la variable `previous_page` repose sur la variable `{KEY}` utilisé dans la fonction définie par Adobe.

### Page suivante

Détermine la valeur suivante d’un champ donné avec un nombre défini d’étapes restantes dans la fenêtre. Dans l’exemple, notez que la variable `WINDOW` est configurée avec un cadre de `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` paramétrer la fonction définie par Adobe pour qu’elle examine la ligne actuelle et toutes les lignes suivantes.

**Syntaxe de la requête**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description |
| --------- | ----------- |
| `{KEY}` | La colonne ou le champ de l’événement. |
| `{SHIFT}` | (Facultatif) Le nombre d’événements en dehors de l’événement en cours. Par défaut, la valeur est 1. |
| `{IGNORE_NULLS}` | (Facultatif) Une valeur booléenne qui indique si la valeur est nulle `{KEY}` doivent être ignorées. Par défaut, la valeur est `false`. |

Une explication des paramètres de la variable `OVER()` se trouve dans la fonction [section fonctions de fenêtre](#window-functions).

**Exemple de requête**

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS next_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

**Résultats**

```console
                id                 |       timestamp       |                name                 |             previous_page             
-----------------------------------+-----------------------+-------------------------------------+---------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Shopping Cart: Cart Details)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Shopping Cart: Shipping Information)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Billing Information)
(10 rows)
```

Pour l’exemple de requête donné, les résultats sont donnés dans la variable `previous_page` colonne . La valeur de la variable `previous_page` repose sur la variable `{KEY}` utilisé dans la fonction définie par Adobe.

## Intervalle

L’intervalle vous permet d’explorer le comportement latent des clients sur une certaine période avant ou après un événement.

### Intervalle depuis la correspondance précédente

Cette requête renvoie un nombre représentant l’unité de temps depuis que l’événement correspondant précédent a été vu. Si aucun événement correspondant n’a été trouvé, la valeur null est renvoyée.

**Syntaxe de la requête**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description |
| --------- | ----------- |
| `{TIMESTAMP}` | Champ d’horodatage trouvé dans le jeu de données renseigné sur tous les événements. |
| `{EVENT_DEFINITION}` | L’expression permettant de qualifier l’événement précédent. |
| `{TIME_UNIT}` | Unité de sortie. La valeur possible inclut les jours, heures, minutes et secondes. Par défaut, la valeur est en secondes. |

Une explication des paramètres de la variable `OVER()` se trouve dans la fonction [section fonctions de fenêtre](#window-functions).

**Exemple de requête**

```sql
SELECT 
  page_name,
  SUM (time_between_previous_match) / COUNT(page_name) as average_minutes_since_registration
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_PREVIOUS_MATCH(timestamp, web.webPageDetails.name='Account Registration|Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS time_between_previous_match
FROM experience_events
)
WHERE time_between_previous_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_since_registration
LIMIT 10
```

**Résultats**

```console
             page_name             | average_minutes_since_registration 
-----------------------------------+------------------------------------
                                   |                                   
 Account Registration|Confirmation |                                0.0
 Seasonal                          |                   5.47029702970297
 Equipment                         |                  6.532110091743119
 Women                             |                  7.287081339712919
 Men                               |                  7.640918580375783
 Product List                      |                  9.387459807073954
 Unlimited Blog|February           |                  9.954545454545455
 Product Details|Buffalo           |                 13.304347826086957
 Unlimited Blog|June               |                  770.4285714285714
(10 rows)
```

Pour l’exemple de requête donné, les résultats sont donnés dans la variable `average_minutes_since_registration` colonne . La valeur de la variable `average_minutes_since_registration` correspond à la différence de temps entre les événements actuels et précédents. L’unité de temps a été définie précédemment dans la variable `{TIME_UNIT}`.

### Intervalle jusqu’à la correspondance suivante

Cette requête renvoie un nombre négatif représentant l’unité de temps derrière l’événement correspondant suivant. Si un événement correspondant est introuvable, la valeur null est renvoyée.

**Syntaxe de la requête**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description |
| --------- | ----------- |
| `{TIMESTAMP}` | Champ d’horodatage trouvé dans le jeu de données renseigné sur tous les événements. |
| `{EVENT_DEFINITION}` | L’expression permettant de qualifier l’événement suivant. |
| `{TIME_UNIT}` | (Facultatif) Unité de sortie. La valeur possible inclut les jours, heures, minutes et secondes. Par défaut, la valeur est en secondes. |

Une explication des paramètres de la variable `OVER()` se trouve dans la fonction [section fonctions de fenêtre](#window-functions).

**Exemple de requête**

```sql
SELECT 
  page_name,
  SUM (time_between_next_match) / COUNT(page_name) as average_minutes_until_order_confirmation
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_NEXT_MATCH(timestamp, web.webPageDetails.name='Shopping Cart|Order Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
    AS time_between_next_match
FROM experience_events
)
WHERE time_between_next_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_until_order_confirmation DESC
LIMIT 10
```

**Résultats**

```console
             page_name             | average_minutes_until_order_confirmation 
-----------------------------------+------------------------------------------
 Shopping Cart|Order Confirmation  |                                      0.0
 Men                               |                       -9.465295629820051
 Equipment                         |                       -9.682098765432098
 Product List                      |                       -9.690661478599221
 Women                             |                       -9.759459459459459
 Seasonal                          |                                  -10.295
 Shopping Cart|Order Review        |                      -366.33567364956144
 Unlimited Blog|February           |                       -615.0327868852459
 Shopping Cart|Billing Information |                       -775.6200495367711
 Product Details|Buffalo           |                      -1274.9571428571428
(10 rows)
```

Pour l’exemple de requête donné, les résultats sont donnés dans la variable `average_minutes_until_order_confirmation` colonne . La valeur de la variable `average_minutes_until_order_confirmation` est la différence de temps entre les événements en cours et les événements suivants. L’unité de temps a été définie précédemment dans la variable `{TIME_UNIT}`.

## Étapes suivantes

À l’aide des fonctions décrites ici, vous pouvez écrire des requêtes pour accéder aux vôtres. [!DNL Experience Event] jeux de données à l’aide de [!DNL Query Service]. Pour plus d’informations sur la création de requêtes dans [!DNL Query Service], reportez-vous à la documentation relative à [création de requêtes](../best-practices/writing-queries.md).

## Ressources supplémentaires

La vidéo suivante montre comment exécuter des requêtes dans l’interface Adobe Experience Platform et dans un client PSQL. En outre, la vidéo utilise également des exemples impliquant des propriétés individuelles dans un objet XDM, en utilisant des fonctions définies par Adobe et en utilisant CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)
