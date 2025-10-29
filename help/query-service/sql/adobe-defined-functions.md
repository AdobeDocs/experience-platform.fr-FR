---
keywords: Experience Platform;accueil;rubriques les plus consultées;query service;Query service;fonctions définies par adobe;sql;
solution: Experience Platform
title: Fonctions SQL définies par Adobe dans Query Service
description: Ce document fournit des informations sur les fonctions définies par Adobe disponibles dans Adobe Experience Platform Query Service.
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 13%

---

# Fonctions SQL définies par Adobe dans Query Service

Les fonctions définies par Adobe, appelées ADF, sont des fonctions préconfigurées dans Adobe Experience Platform Query Service qui permettent d’effectuer des tâches courantes liées à l’activité sur les données [!DNL Experience Event]. Il s’agit notamment de fonctions de [sessionisation](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) et [attribution](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html) comme celles d’Adobe Analytics.

Ce document fournit des informations sur les fonctions définies par Adobe disponibles dans [!DNL Query Service].

>[!NOTE]
>
>L’Experience Cloud ID (ECID) est également appelé MCID et continue à être utilisé dans les espaces de noms.

## Fonctions de fenêtre {#window-functions}

La majeure partie de la logique commerciale exige de rassembler les points de contact d’un client et de les classer par heure. Cette prise en charge est assurée par [!DNL Spark] SQL sous la forme de fonctions de fenêtre. Les fonctions de fenêtre font partie du langage SQL standard et sont prises en charge par de nombreux autres moteurs SQL.

Une fonction de fenêtre met à jour une agrégation et renvoie un élément unique pour chaque ligne de votre sous-ensemble classé. `SUM()` est la fonction d’agrégation la plus élémentaire. `SUM()` additionne vos lignes et fournit un total. Si vous appliquez plutôt `SUM()` à une fenêtre, la transformant ainsi en fonction de fenêtre, vous recevez une somme cumulée pour chaque ligne.

La plupart des assistants SQL [!DNL Spark] sont des fonctions de fenêtre qui mettent à jour chaque ligne dans votre fenêtre, en y ajoutant l’état de cette ligne.

**Syntaxe de la requête**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description | Exemple |
| --------- | ----------- | ------- |
| `{PARTITION}` | Sous-groupe de lignes basé sur une colonne ou un champ disponible. | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | Colonne ou champ disponible utilisé pour classer le sous-ensemble ou les lignes. | `ORDER BY timestamp` |
| `{FRAME}` | Sous-groupe des lignes d&#39;une partition. | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessionisation

Lorsque vous utilisez des données [!DNL Experience Event] provenant d’un site web, d’une application mobile, d’un système de réponse vocale interactive ou de tout autre canal d’interaction client, il est utile que les événements puissent être regroupés autour d’une période d’activité associée. En règle générale, votre activité est guidée par une intention spécifique, telle que la recherche d’un produit, le paiement d’une facture, la vérification du solde du compte, le remplissage d’une demande, etc.

Ce regroupement, ou sessionnalisation des données, permet d’associer les événements pour découvrir plus de contexte sur l’expérience client.

Pour plus d’informations sur la sessionnalisation dans Adobe Analytics, consultez la documentation sur les [sessions adaptées au contexte](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html).

**Syntaxe de la requête**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description |
| --------- | ----------- |
| `{TIMESTAMP}` | Champ d’horodatage trouvé dans le jeu de données. |
| `{EXPIRATION_IN_SECONDS}` | Le nombre de secondes nécessaires entre les événements pour qualifier la fin de la session en cours et le début d’une nouvelle session. |

Vous trouverez une explication des paramètres de la fonction `OVER()` dans la section [fonctions de fenêtre](#window-functions).

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
|----------------------------------+-----------------------+--------------------
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

Pour l’exemple de requête donné, les résultats sont donnés dans la colonne `session` . La colonne `session` est composée des composants suivants :

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Paramètres | Description |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Différence de temps, en secondes, entre l’enregistrement actif et l’enregistrement précédent. |
| `{NUM}` | Numéro de session unique, commençant à 1, pour la clé définie dans le `PARTITION BY` de la fonction de fenêtre. |
| `{IS_NEW}` | Valeur booléenne utilisée pour déterminer si un enregistrement est le premier d’une session. |
| `{DEPTH}` | Profondeur de l’enregistrement actif dans la session. |

### SESS_START_IF

Cette requête renvoie l’état de la session pour la ligne active, en fonction de la date et de l’heure actuelles et de l’expression données, et démarre une nouvelle session avec la ligne active.

**Syntaxe de la requête**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description |
| --------- | ----------- |
| `{TIMESTAMP}` | Champ d’horodatage trouvé dans le jeu de données. |
| `{TEST_EXPRESSION}` | Expression par rapport à laquelle vous souhaitez vérifier les champs des données. Par exemple : `application.launches > 0`. |

Vous trouverez une explication des paramètres de la fonction `OVER()` dans la section [fonctions de fenêtre](#window-functions).

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
|----------------------------------+-----------------------+----------+--------------------
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

Pour l’exemple de requête donné, les résultats sont donnés dans la colonne `session` . La colonne `session` est composée des composants suivants :

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Paramètres | Description |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Différence de temps, en secondes, entre l’enregistrement actif et l’enregistrement précédent. |
| `{NUM}` | Numéro de session unique, commençant à 1, pour la clé définie dans le `PARTITION BY` de la fonction de fenêtre. |
| `{IS_NEW}` | Valeur booléenne utilisée pour déterminer si un enregistrement est le premier d’une session. |
| `{DEPTH}` | Profondeur de l’enregistrement actif dans la session. |

### SESS_END_IF

Cette requête renvoie l’état de la session de la ligne active, en fonction de la date et de l’heure actuelles et de l’expression données, met fin à la session active et démarre une nouvelle session sur la ligne suivante.

**Syntaxe de la requête**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description |
| --------- | ----------- |
| `{TIMESTAMP}` | Champ d’horodatage trouvé dans le jeu de données. |
| `{TEST_EXPRESSION}` | Expression par rapport à laquelle vous souhaitez vérifier les champs des données. Par exemple : `application.launches > 0`. |

Vous trouverez une explication des paramètres de la fonction `OVER()` dans la section [fonctions de fenêtre](#window-functions).

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
|----------------------------------+-----------------------+----------+--------------------
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

Pour l’exemple de requête donné, les résultats sont donnés dans la colonne `session` . La colonne `session` est composée des composants suivants :

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Paramètres | Description |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Différence de temps, en secondes, entre l’enregistrement actif et l’enregistrement précédent. |
| `{NUM}` | Numéro de session unique, commençant à 1, pour la clé définie dans le `PARTITION BY` de la fonction de fenêtre. |
| `{IS_NEW}` | Valeur booléenne utilisée pour déterminer si un enregistrement est le premier d’une session. |
| `{DEPTH}` | Profondeur de l’enregistrement actif dans la session. |


## Cheminement

Le cheminement peut être utilisé pour comprendre la profondeur de l’engagement du client, confirmer que les étapes prévues d’une expérience fonctionnent comme prévu et identifier les problèmes potentiels ayant un impact sur le client.

Les fonctions ADF suivantes prennent en charge l’établissement de vues de cheminement à partir de leurs relations précédentes et suivantes. Vous pourrez créer des pages précédentes et suivantes, ou parcourir plusieurs événements pour créer un cheminement.

### Page précédente

Détermine la valeur précédente d’un champ donné avec un nombre défini d’étapes restantes dans la fenêtre. Notez dans l&#39;exemple que la fonction `WINDOW` est configurée avec une image de `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` définissant l&#39;ADF pour examiner la ligne actuelle et toutes les lignes suivantes.

**Syntaxe de la requête**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description |
| --------- | ----------- |
| `{KEY}` | La colonne ou le champ de l’événement. |
| `{SHIFT}` | (Facultatif) Nombre d’événements en dehors de l’événement actuel. Par défaut, la valeur est 1. |
| `{IGNORE_NULLS}` | (Facultatif) Valeur booléenne qui indique si les valeurs de `{KEY}` nulles doivent être ignorées. Par défaut, la valeur est `false`. |

Vous trouverez une explication des paramètres de la fonction `OVER()` dans la section [fonctions de fenêtre](#window-functions).

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
|-----------------------------------+-----------------------+-------------------------------------+-----------------------------------------------------
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

Pour l’exemple de requête donné, les résultats sont donnés dans la colonne `previous_page` . La valeur de la colonne `previous_page` est basée sur la `{KEY}` utilisée dans le fichier ADF.

### Page suivante

Détermine la valeur suivante d’un champ donné avec un nombre défini d’étapes restantes dans la fenêtre. Notez dans l&#39;exemple que la fonction `WINDOW` est configurée avec une image de `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` définissant l&#39;ADF pour examiner la ligne actuelle et toutes les lignes suivantes.

**Syntaxe de la requête**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description |
| --------- | ----------- |
| `{KEY}` | La colonne ou le champ de l’événement. |
| `{SHIFT}` | (Facultatif) Nombre d’événements en dehors de l’événement actuel. Par défaut, la valeur est 1. |
| `{IGNORE_NULLS}` | (Facultatif) Valeur booléenne qui indique si les valeurs de `{KEY}` nulles doivent être ignorées. Par défaut, la valeur est `false`. |

Vous trouverez une explication des paramètres de la fonction `OVER()` dans la section [fonctions de fenêtre](#window-functions).

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
|-----------------------------------+-----------------------+-------------------------------------+---------------------------------------
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

Pour l’exemple de requête donné, les résultats sont donnés dans la colonne `previous_page` . La valeur de la colonne `previous_page` est basée sur la `{KEY}` utilisée dans le fichier ADF.

## Intervalle

La période intermédiaire vous permet d’explorer le comportement latent des clients au cours d’une certaine période avant ou après un événement.

### Intervalle depuis la correspondance précédente

Cette requête renvoie un nombre représentant l’unité de temps depuis que l’événement correspondant précédent a été affiché. Si aucun événement correspondant n’a été trouvé, il renvoie la valeur null.

**Syntaxe de la requête**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description |
| --------- | ----------- |
| `{TIMESTAMP}` | Champ d’horodatage trouvé dans le jeu de données renseigné sur tous les événements. |
| `{EVENT_DEFINITION}` | Expression permettant de qualifier l’événement précédent. |
| `{TIME_UNIT}` | Unité de sortie. Les valeurs possibles sont les jours, heures, minutes et secondes. Par défaut, la valeur est secondes. |

Vous trouverez une explication des paramètres de la fonction `OVER()` dans la section [fonctions de fenêtre](#window-functions).

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
|-----------------------------------+------------------------------------
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

Pour l’exemple de requête donné, les résultats sont donnés dans la colonne `average_minutes_since_registration` . La valeur de la colonne `average_minutes_since_registration` correspond à la différence de temps entre les événements actuels et précédents. L’unité de temps a été définie précédemment dans le `{TIME_UNIT}`.

### Intervalle jusqu’à la correspondance suivante

Cette requête renvoie un nombre négatif représentant l’unité de temps derrière le prochain événement correspondant. Si aucun événement correspondant n’est trouvé, la valeur null est renvoyée.

**Syntaxe de la requête**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Paramètre | Description |
| --------- | ----------- |
| `{TIMESTAMP}` | Champ d’horodatage trouvé dans le jeu de données renseigné sur tous les événements. |
| `{EVENT_DEFINITION}` | Expression permettant de qualifier l’événement suivant. |
| `{TIME_UNIT}` | (Facultatif) Unité de sortie. Les valeurs possibles sont les jours, heures, minutes et secondes. Par défaut, la valeur est secondes. |

Vous trouverez une explication des paramètres de la fonction `OVER()` dans la section [fonctions de fenêtre](#window-functions).

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
|-----------------------------------+------------------------------------------
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

Pour l’exemple de requête donné, les résultats sont donnés dans la colonne `average_minutes_until_order_confirmation` . La valeur de la colonne `average_minutes_until_order_confirmation` correspond à la différence de temps entre les événements actuels et suivants. L’unité de temps a été définie précédemment dans le `{TIME_UNIT}`.

## Étapes suivantes

À l’aide des fonctions décrites ici, vous pouvez écrire des requêtes pour accéder à vos propres jeux de données [!DNL Experience Event] à l’aide de [!DNL Query Service]. Pour plus d’informations sur la création de requêtes dans [!DNL Query Service], consultez la documentation sur la [création de requêtes](../best-practices/writing-queries.md).

## Ressources supplémentaires

La vidéo suivante montre comment exécuter des requêtes dans l’interface Adobe Experience Platform et dans un client PSQL. En outre, la vidéo utilise également des exemples impliquant des propriétés individuelles dans un objet XDM, à l’aide de fonctions définies par Adobe et à l’aide de CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)
