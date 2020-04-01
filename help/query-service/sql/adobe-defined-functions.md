---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions définies par Adobe
topic: functions
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Fonctions définies par Adobe

Les fonctions définies par Adobe (ADF) sont des fonctions prédéfinies dans le service de  de qui permettent d’exécuter des communs liés à l’activité sur les données ExperienceEvent. Il s’agit notamment des fonctions de segmentation et d’attribution, telles que celles d’Adobe Analytics. Voir la documentation [d’](https://docs.adobe.com/content/help/en/analytics/landing/home.html) Adobe Analytics pour en savoir plus sur Adobe Analytics et sur les concepts sous-jacents aux adaptateurs de données adaptatifs définis sur cette page. Ce fournit des informations sur les fonctions définies par Adobe disponibles dans le service .

## Fonctions de fenêtre

La majorité de la logique commerciale exige de rassembler les points de contact d’un client et de les commander à temps. Ce support est fourni par Spark SQL sous la forme de fonctions de fenêtre. Les fonctions de fenêtre font partie de SQL standard et sont prises en charge par de nombreux autres moteurs SQL.

Une fonction de fenêtre met à jour une agrégation et renvoie un élément unique pour chaque ligne de votre sous-ensemble ordonné. La fonction d’agrégation la plus élémentaire est `SUM()`. `SUM()` prend vos lignes et vous donne un total. Si vous appliquez plutôt `SUM()` à une fenêtre, en la transformant en fonction de fenêtre, vous recevez une somme cumulée avec chaque ligne.

La plupart des assistants Spark SQL sont des fonctions de fenêtre qui mettent à jour chaque ligne de la fenêtre, avec l’état de cette ligne ajouté.

### Spécification

Syntaxe : `OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| [partition] | Sous-groupe de lignes basé sur une colonne ou un champ disponible. Exemple, `PARTITION BY endUserIds._experience.mcid.id` |
| [ordre] | Colonne ou champ disponible utilisé pour classer le ou les sous-ensembles de lignes. Exemple, `ORDER BY timestamp` |
| [frame] | Sous-groupe des rangées dans une partition. Exemple, `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessionisation

Lorsque vous travaillez avec des données ExperienceEvent provenant d’un site Web, d’une application mobile, d’un système interactif de réponse vocale ou de tout autre d’interaction avec le client,  il est utile que les puissent être regroupés autour d’une période connexe d’un d’ de la . En règle générale, vous avez une intention spécifique de diriger votre   comme la recherche d’un produit, le paiement d’une facture, le contrôle du solde du compte, le remplissage d’une demande, etc. Ce regroupement permet d’associer le pour découvrir davantage le contexte de l’expérience client.

Pour plus d’informations sur la session dans Adobe Analytics, voir la documentation sur les sessions [adaptées au](https://docs.adobe.com/content/help/en/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html)contexte.

### Spécification

Syntaxe : `SESS_TIMEOUT(timestamp, expirationInSeconds) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ Horodatage trouvé dans le jeu de données |
| `expirationInSeconds` | Nombre de secondes nécessaires entre les  pour qualifier la fin de la session en cours et la  d&#39;une nouvelle session |

| Paramètres d’objet renvoyés | Description |
| ---------------------- | ------------- |
| `timestamp_diff` | Durée en secondes entre l’enregistrement actuel et l’enregistrement précédent |
| `num` | Numéro de session unique, commençant à 1, pour la clé définie dans la fonction `PARTITION BY` de la fenêtre. |
| `is_new` | Valeur booléenne utilisée pour déterminer si un enregistrement est le premier d’une session |
| `depth` | Profondeur de l’enregistrement actif dans la session |

#### Exemple de 

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

#### Résultats

```
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

## Attribution

L’association des actions des clients à la réussite est un élément important pour comprendre les facteurs qui influencent l’expérience des clients. Les fichiers ADF suivants prennent en charge l’attribution Première et Dernière avec des paramètres d’expiration différents.

Pour plus d’informations sur l’attribution dans Adobe Analytics, voir la présentation [de l’IQ](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/panels/attribution.html) d’attribution dans le Guide d’analyse d’Analytics.

### Attribution Première touche

Renvoie la valeur d’attribution Première touche et les détails d’un seul  de dans le jeu de données  ExperienceEvent. Le renvoie un `struct` objet avec la valeur Première touche, l’horodatage et l’attribution pour chaque ligne renvoyée pour le sélectionné.

Ce est utile si vous souhaitez savoir quelle interaction a conduit à une série d’actions du client. Dans l’exemple ci-dessous, le code de suivi initial (`em:946426`) dans les données ExperienceEvent est attribué à 100 % (`1.0`) de la responsabilité des actions du client, car il s’agissait de la première interaction.

### Spécification

Syntaxe : `ATTRIBUTION_FIRST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ Horodatage trouvé dans le jeu de données |
| `channelName` | Nom convivial à utiliser comme étiquette dans l’objet renvoyé |
| `channelValue` | Colonne ou champ correspondant au   pour le  de l’ |


| Paramètres d’objet renvoyés | Description |
| ---------------------- | ------------- |
| `name` | L’étiquette `channelName` saisie dans le fichier ADF |
| `value` | Valeur de `channelValue` qui est la première touche dans ExperienceEvent |
| `timestamp` | Horodatage de l’événement ExperienceEvent au cours duquel la première touche s’est produite |
| `fraction` | Attribution de la première touche exprimée sous forme de crédit fractionnel |

#### Exemple de 

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH(timestamp, 'Paid First', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
LIMIT 10
```

#### Résultats

```
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:06:12.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:02.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:55.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:08:44.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:10.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:43.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:53:02.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:12.0 | sms:70175    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:57.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2019-01-02 19:41:38.0 | em:526702    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
(10 rows)
```

### Attribution Dernière touche

Renvoie la valeur d’attribution Dernière touche et les détails d’un seul  de dans le jeu de données  ExperienceEvent. Le renvoie un `struct` objet avec la valeur Dernière touche, l’horodatage et l’attribution pour chaque ligne renvoyée pour le sélectionné.

Ce est utile si vous souhaitez voir l’interaction finale dans une série d’actions client. Dans l’exemple ci-dessous, le code de suivi dans l’objet renvoyé est la dernière interaction dans chaque enregistrement ExperienceEvent. Chaque code est attribué à 100 % (`1.0`) de la responsabilité des actions du client, car il s’agissait de la dernière interaction.

### Spécification

Syntaxe : `ATTRIBUTION_LAST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ Horodatage trouvé dans le jeu de données |
| `channelName` | Nom convivial à utiliser comme étiquette dans l’objet renvoyé |
| `channelValue` | Colonne ou champ correspondant au   pour le  de l’ |


| Paramètres d’objet renvoyés | Description |
| ---------------------- | ------------- |
| `name` | L’étiquette `channelName` saisie dans le fichier ADF |
| `value` | La valeur de `channelValue` ceci est la dernière touche dans ExperienceEvent |
| `timestamp` | Horodatage de l’événement ExperienceEvent dans lequel la `channelValue` variable |
| `fraction` | Attribution de la dernière touche exprimée sous forme de crédit fractionnel |

#### Exemple de 

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'trackingCode', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### Résultats

```
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:06:12.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:02.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:55.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:08:44.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:10.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:10.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:43.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:53:02.0 |              | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:12.0 | sms:70175    | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:57.0 |              | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-01-02 19:41:38.0 | em:526702    | (Paid Last,em:526702,2018-01-02 19:41:38.0,1.0)
(10 rows)
```

### Attribution Première touche avec condition d’expiration

Renvoie la valeur d’attribution Première touche et les détails d’un seul  d’dans le jeu de données  ExperienceEvent, expirant après ou avant une condition. Le renvoie un `struct` objet avec la valeur Première touche, l’horodatage et l’attribution pour chaque ligne renvoyée pour le sélectionné.

Ce est utile si vous souhaitez voir quelle interaction a conduit à une série d’actions du client dans une partie du jeu de données ExperienceEvent déterminée par une condition de votre choix. Dans l’exemple ci-dessous, un achat est enregistré (`commerce.purchases.value IS NOT NULL`) sur chacun des quatre jours affichés dans les résultats (15, 21, 23 et 29 juillet) et le code de suivi initial est attribué à 100 % (`1.0`) de la responsabilité des actions du client.

#### Spécification

Syntaxe : `ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ Horodatage trouvé dans le jeu de données |
| `channelName` | Nom convivial à utiliser comme étiquette dans l’objet renvoyé |
| `channelValue` | Colonne ou champ correspondant au   pour le  de l’ |
| `expCondition` | Condition qui détermine le point d’expiration du  |
| `expBefore` | La valeur par défaut est `false`. Valeur booléenne pour indiquer si le expire avant ou après que la condition spécifiée soit remplie. Activé principalement pour les conditions d’expiration d’une session (par exemple `sess.depth = 1, true`), afin de garantir que la première touche n’est pas sélectionnée à partir d’une session précédente. |

| Paramètres d’objet renvoyés | Description |
| ---------------------- | ------------- |
| `name` | L’étiquette `channelName` saisie dans le fichier ADF |
| `value` | Valeur de `channelValue` qui est la première touche dans l’événement ExperienceEvent avant la variable `expCondition` |
| `timestamp` | Horodatage de l’événement ExperienceEvent au cours duquel la première touche s’est produite |
| `fraction` | Attribution de la première touche exprimée sous forme de crédit fractionnel |

#### Exemple de 

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, 'Paid First', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### Résultats

```
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

### Attribution Première touche avec délai d’expiration

Renvoie la valeur d’attribution Première touche et les détails d’un seul  de dans le jeu de données  ExperienceEvent pendant une période spécifiée. Le renvoie un `struct` objet avec la valeur Première touche, l’horodatage et l’attribution pour chaque ligne renvoyée pour le sélectionné. Ce est utile si vous souhaitez voir quelle interaction, dans un intervalle de temps sélectionné, a conduit à une action du client. Dans l’exemple ci-dessous, la première touche renvoyée pour chaque action client est la première interaction au cours des sept jours précédents (`expTimeout = 86400 * 7`).

#### Spécification

Syntaxe : `ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ Horodatage trouvé dans le jeu de données |
| `channelName` | Nom convivial à utiliser comme étiquette dans l’objet renvoyé |
| `channelValue` | Colonne ou champ correspondant au   pour le  de l’ |
| `expTimeout` | La fenêtre de temps (en secondes) avant la  du  que le cherche un Première touche. |

| Paramètres d’objet renvoyés | Description |
| ---------------------- | ------------- |
| `name` | L’étiquette `channelName` saisie dans le fichier ADF |
| `value` | Valeur de `channelValue` qui correspond à la première touche dans l’intervalle `expTimeout` spécifié |
| `timestamp` | Horodatage de l’événement ExperienceEvent au cours duquel la première touche s’est produite |
| `fraction` | Attribution de la première touche exprimée sous forme de crédit fractionnel |

#### Exemple de 

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, 'Paid First', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### Résultats

```
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

### Attribution Dernière touche avec condition d’expiration

Renvoie la valeur d’attribution Dernière touche et les détails d’un seul  d’dans le jeu de données  ExperienceEvent, expirant après ou avant une condition. Le renvoie un `struct` objet avec la valeur Dernière touche, l’horodatage et l’attribution pour chaque ligne renvoyée pour le sélectionné. Ce est utile si vous souhaitez voir la dernière interaction dans une série d’actions du client dans une partie du jeu de données ExperienceEvent déterminée par une condition de votre choix. Dans l’exemple ci-dessous, un achat est enregistré (`commerce.purchases.value IS NOT NULL`) sur chacun des quatre jours affichés dans les résultats (15, 21, 23 et 29 juillet) et le dernier code de suivi sur chaque jour est attribué à 100 % (`1.0`) de la responsabilité des actions du client.

#### Spécification

Syntaxe : `ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ Horodatage trouvé dans le jeu de données |
| `channelName` | Nom convivial à utiliser comme étiquette dans l’objet renvoyé |
| `channelValue` | Colonne ou champ correspondant au   pour le  de l’ |
| `expCondition` | Condition qui détermine le point d’expiration du  |
| `expBefore` | La valeur par défaut est `false`. Valeur booléenne pour indiquer si le expire avant ou après que la condition spécifiée soit remplie. Activé principalement pour les conditions d’expiration de session (par exemple `sess.depth = 1, true`), afin de garantir que la dernière touche n’est pas sélectionnée à partir d’une session précédente. |

| Paramètres d’objet renvoyés | Description |
| ---------------------- | ------------- |
| `name` | L’étiquette `channelName` saisie dans le fichier ADF |
| `value` | Valeur de `channelValue` qui est la dernière touche dans l’événement ExperienceEvent avant la variable `expCondition` |
| `timestamp` | Horodatage de l’événement ExperienceEvent au cours duquel la dernière touche s’est produite |
| `percentage` | Attribution de la dernière touche exprimée sous forme de crédit fractionnel |

#### Exemple de 

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, 'trackingCode', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### Résultats

```
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 | em:550984    | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 | em:380097    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

### Attribution Dernière touche avec délai d’expiration

Renvoie la valeur d’attribution Dernière touche et les détails d’un seul  de dans le jeu de données  ExperienceEvent pendant une période spécifiée. Le renvoie un `struct` objet avec la valeur Dernière touche, l’horodatage et l’attribution pour chaque ligne renvoyée pour le sélectionné. Ce est utile si vous souhaitez voir la dernière interaction au cours d’un intervalle de temps sélectionné. Dans l’exemple ci-dessous, la dernière touche renvoyée pour chaque action du client est l’interaction finale au cours des sept jours suivants (`expTimeout = 86400 * 7`).

#### Spécification

Syntaxe : `ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ Horodatage trouvé dans le jeu de données |
| `channelName` | Nom convivial à utiliser comme étiquette dans l’objet renvoyé |
| `channelValue` | Colonne ou champ correspondant au   pour le  de l’ |
| `expTimeout` | La fenêtre de temps (en secondes) après au de  que le  cherche un Dernière touche |

| Paramètres d’objet renvoyés | Description |
| ---------------------- | ------------- |
| `name` | L’étiquette `channelName` saisie dans le fichier ADF |
| `value` | Valeur de `channelValue` qui est la dernière touche dans l’intervalle `expTimeout` spécifié |
| `timestamp` | Horodatage de l’événement ExperienceEvent au cours duquel la dernière touche s’est produite |
| `percentage` | Attribution de la dernière touche exprimée sous forme de crédit fractionnel |

#### Exemple de 

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, 'trackingCode', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### Résultats

```
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

## Touche précédente/suivante

Il est important de comprendre comment les clients naviguent dans une expérience. Il peut être utilisé pour comprendre l’intensité de l’engagement du client, confirmer les étapes prévues d’une expérience et identifier les points problématiques potentiels qui affectent le client. Les adaptateurs ADF suivants prennent en charge l’établissement de  de cheminement à partir de leurs relations Précédent et Suivant. Vous pourrez créer Page précédente et Page suivante, ou parcourir plusieurs pour créer le cheminement.

### Touche précédente

Détermine la valeur précédente d’un champ donné par un nombre défini d’étapes en dehors de la fenêtre. Remarquez dans l’exemple que la `WINDOW` Fonction est configurée avec un cadre de `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` configuration de l’outil ADF pour examiner la ligne active et tout ce qui la précède.

#### Spécification

Syntaxe : `PREVIOUS(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `key` | Colonne ou champ du . |
| `shift` | (Facultatif) Nombre d’ à l’écart de la  actuelle du. La valeur par défaut est 1. |
| `ingnoreNulls` | Valeur booléenne indiquant si `key` les valeurs nulles doivent être ignorées. La valeur par défaut est `false`. |


| Paramètres d’objet renvoyés | Description |
| ---------------------- | ------------- |
| `value` | Valeur basée sur la valeur `key` utilisée dans le fichier ADF |

#### Exemple de 

```sql
SELECT endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id, _experience.analytics.session.num
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp ASC
```

#### Résultats

```
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

### Touche suivante

Détermine la valeur suivante d’un champ particulier en fonction du nombre d’étapes à parcourir dans la fenêtre. Remarquez dans l’exemple que la `WINDOW` Fonction est configurée avec un cadre de `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` configuration de l’outil ADF pour examiner la ligne active et tout ce qui suit.

#### Spécification

Syntaxe : `NEXT(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `key` | Colonne ou champ du  |
| `shift` | (Facultatif) Nombre d’ à l’écart de la  actuelle du. La valeur par défaut est 1. |
| `ingnoreNulls` | Valeur booléenne indiquant si `key` les valeurs nulles doivent être ignorées. La valeur par défaut est `false`. |


| Paramètres d’objet renvoyés | Description |
| ---------------------- | ------------- |
| `value` | Valeur basée sur la valeur `key` utilisée dans le fichier ADF |

#### Exemple de 

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

#### Résultats

```
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

## Intervalle de temps

L’intervalle de temps vous permet d’explorer le comportement des clients latents dans une période antérieure ou postérieure à la survenue d’une . Examinez le  dans les 7 jours suivant une campagne ou un autre type de  pour tous vos clients.

### Intervalle entre la correspondance précédente

Fournit une nouvelle dimension, qui mesure le temps écoulé depuis un incident particulier.

#### Spécification

Syntaxe : `TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ d’horodatage situé dans le jeu de données renseigné sur tous les  de. |
| `eventDefintion` |   pour qualifier le précédent. |
| `timeUnit` | Unité de production : jours, heures, minutes et secondes. La valeur par défaut est secondes. |

Output : Renvoie un nombre représentant l’unité de temps depuis l’affichage de la  correspondante précédente ou reste nul si aucun  de correspondant n’a été trouvé.

#### Exemple de 

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

#### Résultats

```
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

### Intervalle entre la prochaine correspondance

Fournit une nouvelle dimension, qui mesure le temps avant qu’un  particulier ne se produise.

#### Spécification

Syntaxe : `TIME_BETWEEN_NEXT_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ d’horodatage situé dans le jeu de données renseigné sur tous les  de. |
| `eventDefintion` |   pour qualifier le prochain. |
| `timeUnit` | Unité de production : jours, heures, minutes et secondes. La valeur par défaut est secondes. |

Output : Renvoie un nombre négatif représentant l’unité de temps derrière le prochain correspondant ou reste nul si un correspondant est introuvable.

#### Exemple de 

```
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

#### Résultats

```
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

## Étapes suivantes

En utilisant les fonctions décrites ici, vous pouvez écrire des  pour accéder à vos propres jeux de données ExperienceEvent à l’aide de  Service. Pour plus d&#39;informations sur la création de  de dans le service , reportez-vous à la documentation sur la [création d&#39;un](../creating-queries/creating-queries.md)decréation.
