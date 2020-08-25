---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions définies par Adobe
topic: functions
translation-type: tm+mt
source-git-commit: 38cb8eeae3ac0a1852c59e433d1cacae82b1c6c0
workflow-type: tm+mt
source-wordcount: '2156'
ht-degree: 83%

---


# Fonctions définies par Adobe

Adobe-defined functions (ADFs) are prebuilt functions in [!DNL Query Service] that help perform common business related tasks on [!DNL ExperienceEvent] data. Il s’agit notamment de fonctions de sessionisation et d’attribution comme celles que l’on trouve dans Adobe Analytics. Consultez la [documentation d’Adobe Analytics](https://docs.adobe.com/content/help/fr-FR/analytics/landing/home.html) pour en savoir plus sur Adobe Analytics et sur les concepts sous-jacents aux fonctions définies par Adobe sur cette page. Ce document fournit des informations sur les fonctions définies par Adobe disponibles dans [!DNL Query Service].

## Fonctions de fenêtre

La majeure partie de la logique commerciale exige de rassembler les points de contact d’un client et de les classer par heure. This support is provided by [!DNL Spark] SQL in the form of window functions. Les fonctions de fenêtre font partie du langage SQL standard et sont prises en charge par de nombreux autres moteurs SQL.

Une fonction de fenêtre met à jour une agrégation et renvoie un élément unique pour chaque ligne de votre sous-ensemble classé. `SUM()` est la fonction d’agrégation la plus élémentaire. `SUM()` additionne vos lignes et fournit un total. Si vous appliquez plutôt `SUM()` à une fenêtre, la transformant ainsi en fonction de fenêtre, vous recevez une somme cumulée pour chaque ligne.

The majority of the [!DNL Spark] SQL helpers are window functions that update each row in your window, with the state of that row added.

### Spécification

Syntaxe : `OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| [partition] | Un sous-groupe de lignes basé sur une colonne ou un champ disponible. Exemple, `PARTITION BY endUserIds._experience.mcid.id` |
| [order] | Une colonne ou un champ disponible utilisé pour classer le sous-ensemble ou les lignes. Exemple, `ORDER BY timestamp` |
| [frame] | Un sous-groupe des lignes d’une partition. Exemple, `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessionisation

When you are working with [!DNL ExperienceEvent] data originating from a website, mobile application, interactive voice response system, or any other customer interaction channel it helps if events can be grouped around a related period of activity. Généralement, une intention spécifique oriente votre activité, comme la recherche d’un produit, le paiement d’une facture, la vérification du solde d’un compte, le remplissage d’une demande, etc. Ce regroupement permet d’associer les événements pour obtenir plus de contexte sur l’expérience client.

Pour plus d’informations sur la sessionisation dans Adobe Analytics, consultez la documentation sur [les sessions adaptées au contexte](https://docs.adobe.com/content/help/fr-FR/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html).

### Spécification

Syntaxe : `SESS_TIMEOUT(timestamp, expirationInSeconds) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ de date et heure trouvé dans le jeu de données |
| `expirationInSeconds` | Nombre de secondes nécessaires entre les événements pour qualifier la fin de la session en cours et le début d’une nouvelle session |

| Paramètres d’objet renvoyé | Description |
| ---------------------- | ------------- |
| `timestamp_diff` | Durée en secondes entre l’enregistrement actuel et l’enregistrement précédent |
| `num` | Un numéro de session unique, en partant de 1, pour la clé définie dans `PARTITION BY` de la fonction de fenêtre. |
| `is_new` | Une valeur booléenne utilisée pour déterminer si un enregistrement est le premier d’une session |
| `depth` | Profondeur de l’enregistrement en cours dans la session |

#### Exemple de requête

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

## Attribution

L’association entre les actions du client et le succès est un élément important pour comprendre les facteurs qui influencent l’expérience client. Les fonctions définies par Adobe suivantes prennent en charge la première et la dernière attribution avec des paramètres d’expiration différents.

Pour plus d’informations sur l’attribution dans Adobe , consultez la [présentation d’Attribution IQ](https://docs.adobe.com/content/help/fr-FR/analytics/analyze/analysis-workspace/panels/attribution.html) dans le guide d’analyse d’Analytics.[!DNL Analytics]

### Attribution Première touche

Returns the first touch attribution value and details for a single channel in the target [!DNL ExperienceEvent] dataset. La requête renvoie un objet `struct` avec la valeur Première touche, la date et heure et l’attribution pour chaque ligne renvoyée pour le canal sélectionné.

Cette requête est utile si vous voulez découvrir l’interaction qui a entraîné une série d’actions du client. Dans l’exemple ci-dessous, le code de suivi initial (`em:946426`[!DNL ExperienceEvent]) dans les données se voit attribuer 100 % (`1.0`) de la responsabilité des actions du client, car il s’agissait de la première interaction.

### Spécification

Syntaxe : `ATTRIBUTION_FIRST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ de date et heure trouvé dans le jeu de données |
| `channelName` | Un nom convivial à utiliser comme libellé dans l’objet renvoyé |
| `channelValue` | La colonne ou le champ correspondant au canal cible pour la requête |


| Paramètres d’objet renvoyé | Description |
| ---------------------- | ------------- |
| `name` | Le `channelName` saisi sous forme de libellé dans la fonction définie par Adobe |
| `value` | La valeur de `channelValue` qui correspond à la Première touche dans [!DNL ExperienceEvent] |
| `timestamp` | The timestamp of the [!DNL ExperienceEvent] where the first touch occured |
| `fraction` | L’attribution de la Première touche exprimée sous forme de crédit fractionnaire |

#### Exemple de requête

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

```console
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

Returns the last touch attribution value and details for a single channel in the target [!DNL ExperienceEvent] dataset. La requête renvoie un objet `struct` avec la valeur Dernière touche, la date et heure et l’attribution pour chaque ligne renvoyée pour le canal sélectionné.

Cette requête est utile si vous voulez découvrir l’interaction finale dans une série d’actions du client. In the example shown below, the tracking code in the returned object is the last interaction in each [!DNL ExperienceEvent] record. Chaque code se voit attribuer 100 % (`1.0`) de la responsabilité des actions du client, car il s’agissait de la dernière interaction.

### Spécification

Syntaxe : `ATTRIBUTION_LAST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ de date et heure trouvé dans le jeu de données |
| `channelName` | Un nom convivial à utiliser comme libellé dans l’objet renvoyé |
| `channelValue` | La colonne ou le champ correspondant au canal cible pour la requête |


| Paramètres d’objet renvoyé | Description |
| ---------------------- | ------------- |
| `name` | Le `channelName` saisi sous forme de libellé dans la fonction définie par Adobe |
| `value` | La valeur de `channelValue` qui correspond à la Dernière touche dans [!DNL ExperienceEvent] |
| `timestamp` | The timestamp of the [!DNL ExperienceEvent] where the `channelValue` was used |
| `fraction` | L’attribution de la Dernière touche exprimée sous forme de crédit fractionnaire |

#### Exemple de requête

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

```console
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

Returns the first touch attribution value and details for a single channel in the target [!DNL ExperienceEvent] dataset, expiring after or before a condition. La requête renvoie un objet `struct` avec la valeur Première touche, la date et heure et l’attribution pour chaque ligne renvoyée pour le canal sélectionné.

This query is useful if you want to see what interaction led to a series of customer actions within a portion of the [!DNL ExperienceEvent] dataset determined by a condition of your chosing. Dans l’exemple ci-dessous, un achat est enregistré (`commerce.purchases.value IS NOT NULL`) sur chacun des quatre jours affichés dans les résultats (15, 21, 23 et 29 juillet) et le code de suivi initial de chaque jour se voit attribuer 100 %(`1.0`) de la responsabilité des actions du client.

#### Spécification

Syntaxe : `ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ de date et heure trouvé dans le jeu de données |
| `channelName` | Un nom convivial à utiliser comme libellé dans l’objet renvoyé |
| `channelValue` | La colonne ou le champ correspondant au canal cible pour la requête |
| `expCondition` | La condition qui détermine le point d’expiration du canal |
| `expBefore` | La valeur par défaut est `false`. Valeur booléenne indiquant si le canal expire avant ou après que la condition spécifiée soit remplie. Activé principalement pour les conditions d’expiration d’une session (par exemple `sess.depth = 1, true`), afin de garantir que la Première touche n’est pas sélectionnée à partir d’une session précédente. |

| Paramètres d’objet renvoyé | Description |
| ---------------------- | ------------- |
| `name` | Le `channelName` saisi sous forme de libellé dans la fonction définie par Adobe |
| `value` | La valeur de `channelValue`[!DNL ExperienceEvent] qui correspond à la Première touche dans avant `expCondition` |
| `timestamp` | The timestamp of the [!DNL ExperienceEvent] where the first touch occured |
| `fraction` | L’attribution de la Première touche exprimée sous forme de crédit fractionnaire |

#### Exemple de requête

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

```console
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

Returns the first touch attribution value and details for a single channel in the target [!DNL ExperienceEvent] dataset for a specified time period. La requête renvoie un objet `struct` avec la valeur Première touche, la date et heure et l’attribution pour chaque ligne renvoyée pour le canal sélectionné. Cette requête est utile si vous voulez découvrir l’interaction, dans un intervalle de temps sélectionné, qui a entraîné une action du client. Dans l’exemple ci-dessous, la Première touche renvoyée pour chaque action du client correspond à la première interaction qui a eu lieu au cours des sept jours précédents (`expTimeout = 86400 * 7`).

#### Spécification

Syntaxe : `ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ de date et heure trouvé dans le jeu de données |
| `channelName` | Un nom convivial à utiliser comme libellé dans l’objet renvoyé |
| `channelValue` | La colonne ou le champ correspondant au canal cible pour la requête |
| `expTimeout` | La fenêtre de temps (en secondes) précédant l’événement du canal dans lequel la requête recherche un événement de Première touche |

| Paramètres d’objet renvoyé | Description |
| ---------------------- | ------------- |
| `name` | Le `channelName` saisi sous forme de libellé dans la fonction définie par Adobe |
| `value` | La valeur de `channelValue` qui correspond à la Première touche dans l’intervalle `expTimeout` spécifié |
| `timestamp` | The timestamp of the [!DNL ExperienceEvent] where the first touch occured |
| `fraction` | L’attribution de la Première touche exprimée sous forme de crédit fractionnaire |

#### Exemple de requête

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

```console
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

Returns the last touch attribution value and details for a single channel in the target [!DNL ExperienceEvent] dataset, expiring after or before a condition. La requête renvoie un objet `struct` avec la valeur Dernière touche, la date et heure et l’attribution pour chaque ligne renvoyée pour le canal sélectionné. This query is useful if you want to see the last interaction in a series of customer actions within a portion of the [!DNL ExperienceEvent] dataset determined by a condition of your chosing. Dans l’exemple ci-dessous, un achat est enregistré (`commerce.purchases.value IS NOT NULL`) sur chacun des quatre jours affichés dans les résultats (15, 21, 23 et 29 juillet) et le dernier code de suivi de chaque jour se voit attribuer 100 %(`1.0`) de la responsabilité des actions du client.

#### Spécification

Syntaxe : `ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ de date et heure trouvé dans le jeu de données |
| `channelName` | Un nom convivial à utiliser comme libellé dans l’objet renvoyé |
| `channelValue` | La colonne ou le champ correspondant au canal cible pour la requête |
| `expCondition` | La condition qui détermine le point d’expiration du canal |
| `expBefore` | La valeur par défaut est `false`. Valeur booléenne indiquant si le canal expire avant ou après que la condition spécifiée soit remplie. Activé principalement pour les conditions d’expiration d’une session (par exemple `sess.depth = 1, true`), afin de garantir que la Dernière touche n’est pas sélectionnée à partir d’une session précédente. |

| Paramètres d’objet renvoyé | Description |
| ---------------------- | ------------- |
| `name` | Le `channelName` saisi sous forme de libellé dans la fonction définie par Adobe |
| `value` | La valeur de `channelValue`[!DNL ExperienceEvent] qui correspond à la Dernière touche dans avant `expCondition` |
| `timestamp` | The timestamp of the [!DNL ExperienceEvent] where the last touch occured |
| `percentage` | L’attribution de la Dernière touche exprimée sous forme de crédit fractionnaire |

#### Exemple de requête

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

```console
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

Returns the last touch attribution value and details for a single channel in the target [!DNL ExperienceEvent] dataset for a specified time period. La requête renvoie un objet `struct` avec la valeur Dernière touche, la date et heure et l’attribution pour chaque ligne renvoyée pour le canal sélectionné. Cette requête est utile si vous voulez découvrir la dernière interaction dans un intervalle de temps sélectionné. Dans l’exemple ci-dessous, la Dernière touche renvoyée pour chaque action du client correspond à l’interaction finale qui a eu lieu au cours des sept jours suivants (`expTimeout = 86400 * 7`).

#### Spécification

Syntaxe : `ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ de date et heure trouvé dans le jeu de données |
| `channelName` | Un nom convivial à utiliser comme libellé dans l’objet renvoyé |
| `channelValue` | La colonne ou le champ correspondant au canal cible pour la requête |
| `expTimeout` | La fenêtre de temps (en secondes) suivant l’événement du canal dans lequel la requête recherche un événement de Dernière touche |

| Paramètres d’objet renvoyé | Description |
| ---------------------- | ------------- |
| `name` | Le `channelName` saisi sous forme de libellé dans la fonction définie par Adobe |
| `value` | La valeur de `channelValue` qui correspond à la Dernière touche dans l’intervalle `expTimeout` spécifié |
| `timestamp` | The timestamp of the [!DNL ExperienceEvent] where the last touch occured |
| `percentage` | L’attribution de la Dernière touche exprimée sous forme de crédit fractionnaire |

#### Exemple de requête

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

```console
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

Il est important de comprendre la façon dont les clients évoluent au sein d’une expérience. Elle peut servir à comprendre le degré d’engagement du client, à confirmer que les étapes visées d’une expérience fonctionnent comme prévu et à identifier les éventuels problèmes affectant le client. Les fonctions définies par Adobe suivantes prennent en charge les affichages de cheminement à partir des relations précédentes et suivantes. Vous pourrez créer la page précédente et la page suivante ou parcourir plusieurs événements pour créer le cheminement.

### Touche précédente

Détermine la valeur précédente d’un champ donné avec un nombre défini d’étapes restantes dans la fenêtre. Dans l’exemple, remarquez que la fonction `WINDOW` est configurée avec un cadre de `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` paramétrant la fonction définie par Adobe pour qu’elle examine la ligne actuelle et toutes celles qui la précèdent.

#### Spécification

Syntaxe : `PREVIOUS(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `key` | La colonne ou le champ de l’événement. |
| `shift` | (facultatif) Le nombre d’événements en dehors de l’événement actuel. La valeur par défaut est 1. |
| `ingnoreNulls` | Valeur booléenne indiquant si les valeurs `key` nulles doivent être ignorées. La valeur par défaut est `false`. |


| Paramètres d’objet renvoyé | Description |
| ---------------------- | ------------- |
| `value` | La valeur basée sur la `key` utilisée dans la fonction définie par Adobe |

#### Exemple de requête

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

### Touche suivante

Détermine la valeur suivante d’un champ donné avec un nombre défini d’étapes restantes dans la fenêtre. Dans l’exemple, remarquez que la fonction `WINDOW` est configurée avec un cadre de `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` paramétrant la fonction définie par Adobe pour qu’elle examine la ligne actuelle et toutes celles qui la suivent.

#### Spécification

Syntaxe : `NEXT(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `key` | La colonne ou le champ de l’événement |
| `shift` | (facultatif) Le nombre d’événements en dehors de l’événement actuel. La valeur par défaut est 1. |
| `ingnoreNulls` | Valeur booléenne indiquant si les valeurs `key` nulles doivent être ignorées. La valeur par défaut est `false`. |


| Paramètres d’objet renvoyé | Description |
| ---------------------- | ------------- |
| `value` | La valeur basée sur la `key` utilisée dans la fonction définie par Adobe |

#### Exemple de requête

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

## Intervalle

L’intervalle vous permet de découvrir le comportement latent des clients dans une période précédant ou suivant un événement. Examinez les événements qui ont lieu dans les 7 jours qui suivent une campagne ou un autre type d’événement chez tous vos clients.

### Intervalle depuis la correspondance précédente

Fournit une nouvelle dimension, qui mesure le temps écoulé depuis un incident particulier.

#### Spécification

Syntaxe : `TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ de date et heure trouvé dans le jeu de données renseigné sur tous les événements. |
| `eventDefintion` | Expression permettant de qualifier l’événement précédent. |
| `timeUnit` | Unité de sortie : jours, heures, minutes et secondes. Les secondes sont la valeur par défaut. |

Sortie : renvoie un nombre représentant l’unité de temps depuis l’affichage de l’événement correspondant précédent ou reste nulle si aucun événement correspondant n’a été trouvé.

#### Exemple de requête

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

### Intervalle jusqu’à la correspondance suivante

Fournit une nouvelle dimension, qui mesure le temps avant qu’un événement particulier ne se produise.

#### Spécification

Syntaxe : `TIME_BETWEEN_NEXT_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| Paramètre | Description |
| --- | --- |
| `timestamp` | Champ de date et heure trouvé dans le jeu de données renseigné sur tous les événements. |
| `eventDefintion` | Expression permettant de qualifier l’événement suivant. |
| `timeUnit` | Unité de sortie : jours, heures, minutes et secondes. Les secondes sont la valeur par défaut. |

Sortie : renvoie un nombre négatif représentant l’unité de temps avant l’événement correspondant suivant ou reste nulle si aucun événement correspondant n’est trouvé.

#### Exemple de requête

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

#### Résultats

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

## Étapes suivantes

Using the functions described here, you can write queries to access your own [!DNL ExperienceEvent] datasets using [!DNL Query Service]. For more information about authoring queries in [!DNL Query Service], see the documentation on [creating queries](../creating-queries/creating-queries.md).
