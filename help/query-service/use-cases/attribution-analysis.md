---
title: Analyse des attributs
description: Ce document explique comment utiliser Query Service pour créer une technique de mesure de l’efficacité marketing basée sur le modèle d’attribution marketing Première touche et Dernière touche.
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 10%

---

# Analyse de l’attribution

Attribution est un concept analytique qui permet de déterminer les tactiques marketing telles que les canaux, les offres et les messages, qui contribuent aux ventes commerciales ou aux conversions. Ce concept évalue le parcours client (le processus par lequel un client interagit avec une entreprise pour atteindre un objectif) qui entraîne un achat ou une acquisition en fonction des points de contact du client (chaque fois qu’un client interagit avec votre marque). Grâce à l’analyse d’attribution, les marketeurs peuvent évaluer le retour sur investissement des canaux qui les connectent à un client potentiel.

## Commencer

Les exemples SQL de ce document sont des requêtes couramment utilisées avec les données Adobe Analytics. Ce tutoriel nécessite une compréhension pratique des composants suivants :

* [Connecteur source Adobe Analytics pour la présentation des données de suite de rapports](../../sources/connectors/adobe-applications/mapping/analytics.md).
* [La documentation sur les mappages de champs Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) fournit des informations supplémentaires sur l’ingestion et le mappage de données d’analyse à utiliser avec Query Service.
* [Présentation Attribution IQ](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html)
* [Guide du panneau Attribution Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html).

Vous trouverez une explication des paramètres de la fonction `OVER()` dans la [section des fonctions de fenêtre](../sql/adobe-defined-functions.md#window-functions). Le [glossaire des termes Adobe Marketing et Commerce](https://business.adobe.com/glossary/index.html) peut également être utile.

Pour chacun des cas d’utilisation suivants, un exemple de requête SQL paramétré est fourni comme modèle que vous pouvez personnaliser. Spécifiez des paramètres partout où `{ }` apparaît dans les exemples SQL que vous souhaitez évaluer.

## Objectifs

Un cas d’utilisation d’attribution utilise les données Adobe Analytics pour aider à associer les actions des clients à un résultat réussi. Cette association est essentielle pour comprendre les facteurs qui influencent les expériences client. Les données d’analyse d’attribution peuvent être utilisées pour comprendre l’importance du point de contact d’un client au cours du parcours client.

Les exemples de requête contenus dans ce document prennent en charge divers cas d’utilisation pour l’attribution Première touche et Dernière touche avec différents paramètres d’expiration. Ce guide présente les concepts clés suivants :

* Attribution Première touche et Dernière touche.
* Attribution Première touche et Dernière touche avec délai d’expiration.
* Attribution Première touche et Dernière touche avec condition d’expiration.

## Paramètres de requête d’attribution {#attribution-query-parameters}

Le tableau ci-dessous fournit une ventilation des paramètres et de leurs descriptions utilisés dans les requêtes d’attribution Première touche et Dernière touche :

| Paramètre | Description |
|---|---|
| `{TIMESTAMP}` | Champ d’horodatage trouvé dans le jeu de données. |
| `{CHANNEL_NAME}` | Libellé de l’objet renvoyé. |
| `{CHANNEL_VALUE}` | La colonne ou le champ correspondant au canal cible de la requête. |
| `{EXP_TIMEOUT}` | La fenêtre de temps avant l’événement de canal, en secondes, pendant laquelle la requête recherche un événement Première touche. |
| `{EXP_CONDITION}` | La condition qui détermine le point d’expiration du canal. |
| `{EXP_BEFORE}` | Valeur booléenne qui indique si le canal expire avant ou après la condition spécifiée, `{EXP_CONDITION}`, est satisfait. Cette option est principalement activée pour les conditions d’expiration d’une session, afin de garantir que la Première touche n’est pas sélectionnée à partir d’une session précédente. Par défaut, cette valeur est définie sur `false`. |

## Composants de colonne de résultats de requête {#query-result-column-components}

Les résultats des requêtes d’attribution sont donnés dans la colonne `first_touch` ou `last_touch`. Ces colonnes sont constituées des composants suivants :

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Paramètres | Description |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`, saisi en tant que libellé dans la fabrique de données Azure (ADF). |
| `{VALUE}` | La valeur de `{CHANNEL_VALUE}` qui correspond à la Dernière touche dans l’intervalle `{EXP_TIMEOUT}` spécifié |
| `{TIMESTAMP}` | Horodatage de l’ [!DNL Experience Event] où la dernière touche s’est produite |
| `{FRACTION}` | L’attribution de la Dernière touche, exprimée en fraction décimale. |

### Attribution Première touche {#first-touch}

L’attribution Première touche attribue 100 % de la responsabilité d’un résultat réussi au canal initial rencontré par le client. Cet exemple SQL permet de mettre en évidence l’interaction qui a conduit à une série d’actions client ultérieure.

La requête ci-dessous renvoie la valeur d’attribution Première touche et les détails du canal dans le jeu de données [!DNL Experience Event] cible. Elle renvoie également un objet `struct` pour le canal sélectionné avec la valeur Première touche, l’horodatage et l’attribution pour chaque ligne.

>[!NOTE]
>
>L’identifiant Experience Cloud (ECID) est également connu sous le nom de MCID et continue à être utilisé dans les espaces de noms.

**Syntaxe de la requête**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

Pour obtenir une liste complète des paramètres potentiellement requis et leurs descriptions, consultez la [section Paramètres de requête d’attribution](#attribution-query-parameters).

**Exemple de requête**

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

**Résultats**

Dans les résultats ci-dessous, le code de suivi initial `em:946426` est extrait du jeu de données [!DNL Experience Event]. Ce code de suivi est attribué avec 100 % (`1.0`) de la responsabilité des actions du client, car il s’agissait de la première interaction.

```console
                 id                 |       timestamp       | trackingCode |                   first_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Pour une ventilation des résultats affichés dans la colonne `first_touch`, consultez la [section des composants de colonne](#query-result-column-components).

### Attribution Dernière touche {#second-touch}

L’attribution Dernière touche accorde 100 % de la responsabilité d’un résultat réussi au dernier canal rencontré par le client. Cet exemple SQL permet de mettre en évidence l’interaction finale dans une série d’actions du client.

La requête renvoie la valeur d’attribution Dernière touche et les détails du canal dans le jeu de données [!DNL Experience Event] cible. Elle renvoie également un objet `struct` pour le canal sélectionné avec la valeur Dernière touche, l’horodatage et l’attribution pour chaque ligne.

**Syntaxe de la requête**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

**Exemple de requête**

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

**Résultats**

Dans les résultats affichés ci-dessous, le code de suivi dans l’objet renvoyé est la dernière interaction dans chaque enregistrement [!DNL Experience Event]. Chaque code se voit attribuer 100 % (`1.0`) de la responsabilité des actions du client, car il s’agissait de la dernière interaction.

```console
                 id                |       timestamp       | trackingCode |                   last_touch                   
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

Pour une ventilation des résultats affichés dans la colonne `last_touch`, consultez la [section des composants de colonne](#query-result-column-components).

### Attribution Première touche avec condition d’expiration {#first-touch-attribution-with-expiration-condition}

Cette requête est utilisée pour déterminer quelle interaction a entraîné une série d’actions du client dans une partie du jeu de données [!DNL Experience Event] déterminée par une condition de votre choix.

La requête renvoie la valeur d’attribution Première touche et les détails d’un seul canal dans le jeu de données [!DNL Experience Event] cible, expirant après ou avant une condition. Elle renvoie également un objet `struct` avec la valeur Première touche, l’horodatage et l’attribution pour chaque ligne renvoyée pour le canal sélectionné.

**Syntaxe de la requête**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Pour obtenir une liste complète des paramètres potentiellement requis et leurs descriptions, consultez la [section Paramètres de requête d’attribution](#attribution-query-parameters).

**Exemple de requête**

Dans l’exemple ci-dessous, un achat est enregistré (`commerce.purchases.value IS NOT NULL`) sur chacun des quatre jours affichés dans les résultats (15, 21, 23 et 29 juillet), et le code de suivi initial de chaque jour se voit attribuer 100 % (`1.0`) de la responsabilité des actions du client.

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

**Résultats**

```console
                 id               |       timestamp       | trackingCode |                   first_touch                   
----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Pour une ventilation des résultats affichés dans la colonne `first_touch`, consultez la [section des composants de colonne](#query-result-column-components).

### Attribution Première touche avec délai d’expiration {#first-touch-attribution-with-expiration-timeout}

Cette requête est utilisée pour trouver l’interaction, au cours d’une période sélectionnée, qui a conduit à l’action client réussie.

La requête ci-dessous renvoie la valeur d’attribution Première touche et les détails d’un seul canal dans le jeu de données [!DNL Experience Event] cible pendant une période donnée. La requête renvoie un objet `struct` avec la valeur Première touche, la date et heure et l’attribution pour chaque ligne renvoyée pour le canal sélectionné.

**Syntaxe de la requête**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Pour obtenir une liste complète des paramètres potentiellement requis et leurs descriptions, consultez la [section Paramètres de requête d’attribution](#attribution-query-parameters).

**Exemple de requête**

Dans l’exemple ci-dessous, la Première touche renvoyée pour chaque action du client correspond à la première interaction au cours des sept jours précédents (expTimeout = 86 400 * 7).

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

**Résultats**

```console
                 id                 |       timestamp       | trackingCode |                   first_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

Pour une ventilation des résultats affichés dans la colonne `first_touch`, consultez la [section des composants de colonne](#query-result-column-components).

### Attribution Dernière touche avec condition d’expiration {#last-touch-attribution-with-expiration-condition}

Cette requête est utilisée pour trouver la dernière interaction dans une série d’actions du client dans une partie du jeu de données [!DNL Experience Event] déterminée par une condition de votre choix.

La requête ci-dessous renvoie la valeur d’attribution Dernière touche et les détails d’un seul canal dans le jeu de données [!DNL Experience Event] cible, expirant après ou avant une condition. La requête renvoie un objet `struct` avec la valeur Dernière touche, la date et heure et l’attribution pour chaque ligne renvoyée pour le canal sélectionné.

**Syntaxe de la requête**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Pour obtenir une liste complète des paramètres potentiellement requis et leurs descriptions, consultez la [section Paramètres de requête d’attribution](#attribution-query-parameters).

**Exemple de requête**

Dans l’exemple ci-dessous, un achat est enregistré (`commerce.purchases.value IS NOT NULL`) sur chacun des quatre jours affichés dans les résultats (15, 21, 23 et 29 juillet), et le dernier code de suivi de chaque jour se voit attribuer 100 % (`1.0`) de la responsabilité des actions du client.

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

**Exemple de résultats**

```console
                id                 |       timestamp       | trackingCode |                   last_touch                   
-----------------------------------+-----------------------+--------------+------------------------------------------------
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

Pour une ventilation des résultats affichés dans la colonne `last_touch`, consultez la [section des composants de colonne](#query-result-column-components).

### Attribution Dernière touche avec délai d’expiration {#last-touch-attribution-with-expiration-timeout}

Cette requête est utilisée pour trouver la dernière interaction dans un intervalle de temps sélectionné. La requête renvoie la valeur d’attribution Dernière touche et les détails d’un seul canal dans le jeu de données [!DNL Experience Event] cible pendant une période donnée. La requête renvoie un objet `struct` avec la valeur Dernière touche, la date et heure et l’attribution pour chaque ligne renvoyée pour le canal sélectionné.

**Syntaxe de la requête**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Pour obtenir une liste complète des paramètres potentiellement requis et leurs descriptions, consultez la [section Paramètres de requête d’attribution](#attribution-query-parameters).

**Exemple de requête**

Dans l’exemple ci-dessous, la Dernière touche renvoyée pour chaque action du client correspond à l’interaction finale qui a eu lieu au cours des sept jours suivants (`expTimeout = 86400 * 7`).

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

**Résultats**

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

Pour une ventilation des résultats affichés dans la colonne `last_touch`, consultez la [section des composants de colonne](#query-result-column-components).
